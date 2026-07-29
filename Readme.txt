import React from 'react';
import {
    Viewer,
    Cartesian3,
    Color,
    CallbackProperty,
    Quaternion,
    Matrix3,
    SampledPositionProperty,
    ExtrapolationType,
    HermitePolynomialApproximation,
    JulianDate,
    CallbackPositionProperty,
    VelocityOrientationProperty,
    LabelStyle,
    Math as CesiumMath,
    DistanceDisplayCondition,
    PolygonHierarchy,
    Cartesian2,
    VerticalOrigin,
    Entity,
    ArcType
} from 'cesium';

import { toCartesian3, toJulianDate, SatellitePosition, GroundStation, TrajectoryPoint } from '../utils/cesium-helpers';

export interface EntityManagerDeps {
    drawingMode: 'none' | 'polygon' | 'circle' | 'pick-gs';
    isDrawing: boolean;
    polygonPoints: Cartesian3[];
    circleCenter: Cartesian3 | null;
    circleRadius: number;

    // Infrastructure & Core
    satellites: SatellitePosition[];
    groundStations: GroundStation[];
    trajectories: Record<string, TrajectoryPoint[]>;
    fullTrajectories: Record<string, TrajectoryPoint[]>;
    celestialBody: 'earth' | 'moon';
    showSatellites: boolean;
    showOrbits: boolean;
    showCoverage: boolean;
    show3DTerrain: boolean;
    selectedModel: string;
    hiddenOrbitIds: Set<string>;
    selectedSatelliteId: string | null;
    earthCenter: Cartesian3;
    moonCenter: Cartesian3;

    // Mutable Refs
    refs: {
        satellitesRef: React.MutableRefObject<SatellitePosition[]>;
        trajectoryAddedRef: React.MutableRefObject<Record<string, number>>;
        lastAddedTimeRef: React.MutableRefObject<Record<string, JulianDate>>;
        orbitChunksRef: React.MutableRefObject<Record<string, {
            fullPositions: Cartesian3[];
            fullTimes: number[];
            startIdx?: string | number;
            fullLength?: number;
            drawnStartIndex?: number;
            drawnEndIndex?: number;
            positions?: Cartesian3[];
            times?: number[]
        }>>;
        pingSizeRef: React.MutableRefObject<Record<string, number>>;
    };
}

export class CesiumEntityManager {
    private materialRegistry: Record<string, any> = {};
    private framePositionCache: Record<string, { time: string, pos: Cartesian3 }> = {};
    private lastLinkCalcTime: number = 0;
    private gsWinnersCache: Record<string, { satId: string, priority: number }> = {};

    // [Opt-1] Coverage frame-level cache: recompute footprints and cone geometries exactly once per simulation frame
    private coverageFrameCache: Record<string, {
        dayNumber: number;
        secondsOfDay: number;
        cp: Cartesian3;
        sp: Cartesian3;
        alt: number;
        coverageRadius: number;
        swathRadius: number;
        coneLength: number;
        coneRadius: number;
    }> = {};

    private orbitColorListener: ((e: Event) => void) | null = null;

    constructor(private viewer: Viewer | null) {
        this.orbitColorListener = (e: Event) => {
            try {
                const { satId, color } = (e as CustomEvent).detail;
                if (!satId || !color) return;
                // Find all track entities for this sat and update their material
                const trackId = `${satId}-predicted-track`;
                const trackEntity = this.safeGetById(trackId);
                if (trackEntity?.polyline) {
                    trackEntity.polyline.material = Color.fromCssColorString(color).withAlpha(0.8) as any;
                }
            } catch (_) { }
        };
        if (typeof window !== 'undefined') {
            window.addEventListener('soc-orbit-colors-changed', this.orbitColorListener);
        }
    }

    public destroy() {
        console.log('[CesiumEntityManager] Destroying and clearing all entities...');

        if (this.orbitColorListener && typeof window !== 'undefined') {
            window.removeEventListener('soc-orbit-colors-changed', this.orbitColorListener);
            this.orbitColorListener = null;
        }

        if (!this.viewer || this.viewer.isDestroyed()) {
            this.viewer = null;
            return;
        }

        // Comprehensive entity removal
        try {
            this.viewer.entities.removeAll();
            this.viewer.scene.primitives.removeAll();
            this.viewer.scene.groundPrimitives.removeAll();
        } catch (e) {
            console.warn('[CesiumEntityManager] Error clearing primitives during destroy:', e);
        }

        this.viewer = null;
        this.framePositionCache = {};
        this.materialRegistry = {};
        this.gsWinnersCache = {};
        this.coverageFrameCache = {};
    }

    private get entities() {
        if (!this.viewer || this.viewer.isDestroyed()) return undefined;
        try {
            return this.viewer.entities;
        } catch (e) {
            return undefined;
        }
    }

    private safeGetById(id: string): Entity | undefined {
        if (!id || !this.entities) return undefined;
        try {
            return this.entities.getById(id) as any;
        } catch (e) {
            console.warn(`[CesiumEntityManager] Error in getById for ${id}:`, e);
            return undefined;
        }
    }

    private getMaterial(type: 'glow' | 'dash', color: Color, _options: any = {}) {
        // [Opt-2] PolylineGlowMaterialProperty and PolylineDashMaterialProperty are multi-pass GPU shaders.
        // On Software WebGL they are extremely expensive. Plain Color is a single-pass draw call.
        // We keep the type signature for compatibility but always return a flat Color.
        return color;
    }

    public updateEntities(deps: EntityManagerDeps) {
        if (!this.viewer || this.viewer.isDestroyed()) return;

        // Final guard for scene access which can throw if context is lost
        try {
            if (!this.viewer.scene) return;
        } catch (e) {
            return;
        }

        const {
            satellites, groundStations, celestialBody,
            showSatellites, showOrbits, showCoverage, selectedModel,
            hiddenOrbitIds, earthCenter, moonCenter, refs
        } = deps;

        const isEarth = celestialBody === 'earth';

        // Resource Disposal / Cache Pruning
        const incomingSatIds = new Set(satellites.map((s: SatellitePosition) => s.id));

        // 1. Prune material cache (if needed)
        // (Previously satrecCache pruning removed)

        // 2. Prune orbit chunks & refs
        [refs.orbitChunksRef.current, refs.trajectoryAddedRef.current, refs.lastAddedTimeRef.current, refs.pingSizeRef.current].forEach(cache => {
            Object.keys(cache).forEach(id => {
                if (!incomingSatIds.has(id)) delete (cache as any)[id];
            });
        });

        // 2. Pre-calculate winning links by priority for each GS (Throttled for Performance)
        const now = performance.now();
        let gsWinners = this.gsWinnersCache;
        if (now - this.lastLinkCalcTime > 1000) { // Limit to 1Hz for heavy O(S*G) link logic
            gsWinners = this.calculateGsWinners(deps);
            this.gsWinnersCache = gsWinners;
            this.lastLinkCalcTime = now;
        }

        // 3. Process Satellites
        satellites.forEach((sat: SatellitePosition) => {
            let entity = this.safeGetById(sat.id);
            const center = sat.referenceBody === 'moon' ? moonCenter : earthCenter;
            const isOnMoon = sat.referenceBody === 'moon';

            if (!entity) {
                const isLinked = sat.linkStatus === 'connected';
                const isVisible = isOnMoon ? celestialBody === 'moon' : celestialBody === 'earth';

                // YENİ: Tamamen Cesium saatine bağlı pürüzsüz anlık yörünge CallbackProperty'si
                const positionProperty = this.createUnifiedPositionProperty(sat, refs, center);

                entity = this.entities?.add({
                    id: sat.id,
                    position: positionProperty,
                    orientation: (isOnMoon || sat.referenceBody !== celestialBody) ? undefined : this.createSafeOrientationProperty(positionProperty, center) as any,
                    model: {
                        uri: (() => { const p = (sat as any).modelPath || selectedModel; return (p && p.startsWith('/')) ? (window.location.origin + p) : p; })(),
                        scale: ((sat as any).modelScale ?? 1.0) * 300, // RAW SCALE MULTIPLIER to make the actual mesh HUGE
                        minimumPixelSize: 150,
                        maximumScale: ((sat as any).modelScale ?? 1.0) * 3000,
                        show: showSatellites && isVisible
                    },
                    point: {
                        pixelSize: 10,
                        color: (isLinked ? Color.LIME : Color.ORANGERED) as any,
                        outlineColor: (isLinked ? Color.GREEN : Color.DARKRED) as any,
                        outlineWidth: 3,
                        show: (showSatellites && isVisible) as any
                    },
                    label: {
                        text: sat.id,
                        font: 'bold 16px Inter, sans-serif',
                        verticalOrigin: 1,
                        pixelOffset: new Cartesian3(60, 20, 0),
                        fillColor: isLinked ? Color.LIME : Color.ORANGE,
                        show: showSatellites && isVisible,
                        distanceDisplayCondition: new DistanceDisplayCondition(0.0, 10000000.0) // Hide labels when camera is very far
                    },
                });

                // Ground Trace
                this.ensureGroundTrace(sat, entity, showOrbits, isVisible, isOnMoon, hiddenOrbitIds);

                const satTraj = deps.trajectories[sat.id];
                if (satTraj && satTraj.length > 0) {
                    refs.trajectoryAddedRef.current[sat.id] = new Date(satTraj[0].time).getTime();
                }

                if (isEarth) {
                    this.createEarthSpecificEntities(sat, entity, showSatellites, showCoverage, isOnMoon);
                }
            } else {
                // Update existing
                this.updateExistingSatellite(sat, entity, { ...deps, gsWinners });
                this.ensureGroundTrace(sat, entity, showOrbits, (isOnMoon ? celestialBody === 'moon' : celestialBody === 'earth'), isOnMoon, hiddenOrbitIds);
            }
        });

        // 3. Process Ground Stations
        this.processGroundStations(deps);

        // 4. Process Orbits / Trajectories
        this.processOrbitTracks(deps);

        // 5. Process Heatmap for Service Requests
        this.processHeatmaps(deps);

        // 7. Process Active Drawing
        this.processActiveDrawing(deps);

        // 8. Cleanup rogue entities
        this.cleanupRogueEntities(deps);
    }

    // (Removed duplicate destroy)

    private createEarthSpecificEntities(sat: SatellitePosition, entity: any, showSatellites: boolean, showCoverage: boolean, isOnMoon: boolean) {
        const viewer = this.viewer;
        if (!viewer || viewer.isDestroyed()) return;

        // maxOffNadir is usually in degrees
        const maxOffNadir = (sat as any).maxOffNadir ?? 35.0;
        const maxOffNadirRad = CesiumMath.toRadians(maxOffNadir);

        const swathWidthKm = (sat as any).swathWidth ?? 10.0;
        const halfSwathAngle = Math.atan((swathWidthKm / 2) / 600);

        // Frame-level caching helper to prevent redundant calculations in the same frame
        const getCoverageData = (time: JulianDate) => {
            const defaultRes = {
                cp: new Cartesian3(),
                sp: new Cartesian3(),
                alt: 550000,
                coverageRadius: 1000,
                swathRadius: 10,
                coneLength: 500000,
                coneRadius: 1000
            };

            if (!time || !viewer || viewer.isDestroyed()) {
                return defaultRes;
            }

            const cached = this.coverageFrameCache[sat.id];
            if (cached && cached.dayNumber === time.dayNumber && cached.secondsOfDay === time.secondsOfDay) {
                return cached;
            }

            // Not cached for this frame, compute it!
            const cp = entity?.position?.getValue(time);
            if (!cp) {
                return defaultRes;
            }

            const ellipsoid = viewer.scene.globe.ellipsoid;
            const sp = ellipsoid.scaleToGeodeticSurface(cp, new Cartesian3()) || new Cartesian3();
            const alt = Cartesian3.distance(cp, sp);

            const coverageRadius = Math.max(10, alt * Math.tan(maxOffNadirRad));
            const swathRadius = Math.max(10, alt * Math.tan(halfSwathAngle));
            const coneLength = Math.max(10, alt);
            const coneRadius = Math.max(10, alt * Math.tan(maxOffNadirRad));

            const result = {
                dayNumber: time.dayNumber,
                secondsOfDay: time.secondsOfDay,
                cp: Cartesian3.clone(cp),
                sp,
                alt,
                coverageRadius,
                swathRadius,
                coneLength,
                coneRadius
            };

            this.coverageFrameCache[sat.id] = result;
            return result;
        };

        // Ground-projected position (for footprint ellipses/point)
        const groundPos = new CallbackPositionProperty((time, result?: Cartesian3) => {
            if (!viewer || viewer.isDestroyed()) return undefined;
            const data = getCoverageData(time || viewer.clock.currentTime);
            return Cartesian3.clone(data.sp, result);
        }, false);

        this.entities?.add({
            id: `${sat.id}-coverage-footprint`,
            position: groundPos,
            ellipse: {
                semiMajorAxis: new CallbackProperty((time) => getCoverageData(time || viewer.clock.currentTime).coverageRadius, false) as any,
                semiMinorAxis: new CallbackProperty((time) => getCoverageData(time || viewer.clock.currentTime).coverageRadius, false) as any,
                height: 0, material: Color.CYAN.withAlpha(0.05), outline: true, outlineColor: Color.CYAN.withAlpha(0.4), show: showSatellites && showCoverage && !isOnMoon
            }
        });

        this.entities?.add({
            id: `${sat.id}-swath-footprint`,
            position: groundPos,
            ellipse: {
                semiMajorAxis: new CallbackProperty((time) => getCoverageData(time || viewer.clock.currentTime).swathRadius, false) as any,
                semiMinorAxis: new CallbackProperty((time) => getCoverageData(time || viewer.clock.currentTime).swathRadius, false) as any,
                height: 0, material: Color.MAGENTA.withAlpha(0.6), outline: true, outlineColor: Color.MAGENTA.withAlpha(0.6), show: showSatellites && showCoverage && !isOnMoon
            }
        });

        this.entities?.add({
            id: `${sat.id}-footprint-center`,
            position: groundPos,
            point: { pixelSize: 5, color: Color.CYAN.withAlpha(0.4), show: showSatellites && showCoverage && !isOnMoon }
        });

        this.entities?.add({
            id: `${sat.id}-fov-cone`,
            position: new CallbackPositionProperty((time, result?: Cartesian3) => {
                if (!viewer || viewer.isDestroyed()) return undefined;
                const data = getCoverageData(time || viewer.clock.currentTime);
                // Center of cylinder is midpoint of cp (satellite) and sp (ground projection)
                return Cartesian3.lerp(data.cp, data.sp, 0.5, result || new Cartesian3());
            }, false),
            cylinder: {
                length: new CallbackProperty((time) => getCoverageData(time || viewer.clock.currentTime).coneLength, false) as any,
                topRadius: 0,
                bottomRadius: new CallbackProperty((time) => getCoverageData(time || viewer.clock.currentTime).coneRadius, false) as any,
                material: Color.CYAN.withAlpha(0.03), outline: true, outlineColor: Color.CYAN.withAlpha(0.25), show: showSatellites && showCoverage && !isOnMoon
            } as any
        });
    }

    /**
     * UYDU KONUMUNA ODS SABİTLEMESİ (SGP4 Kaldırıldı)
     * Uydunun görseldeki (dot) konumu artık sadece ODS yörünge hattından interpole edilir.
     * Bu sayede uydu her zaman yörünge hattının üzerinde kalır ve tahmin yürütülmez.
     */
    private createUnifiedPositionProperty(sat: SatellitePosition, refs: EntityManagerDeps['refs'], _center: Cartesian3) {
        return new CallbackPositionProperty((clockTime, result?: Cartesian3) => {
            if (!this.viewer || this.viewer.isDestroyed()) return undefined;
            const clockTimeValue = clockTime || this.viewer.clock.currentTime;
            if (!clockTimeValue) return undefined;

            const targetTime = JulianDate.toDate(clockTimeValue).getTime();

            // Frame-level Caching
            const timeKey = `${clockTimeValue.dayNumber}_${clockTimeValue.secondsOfDay.toFixed(3)}`;
            const cacheKey = `${sat.id}_${timeKey}`;
            if (this.framePositionCache[cacheKey]) {
                return Cartesian3.clone(this.framePositionCache[cacheKey].pos, result);
            }

            // ODS Buffer Check
            const cachedTrack = refs.orbitChunksRef.current[sat.id];
            if (!cachedTrack || !cachedTrack.fullTimes || cachedTrack.fullTimes.length < 2) {
                // Return undefined so Cesium hides the entity.
                // Returning ZERO (moonCenter) caused Cesium to try normalize(0,0,0) → crash.
                return undefined;
            }

            const times = cachedTrack.fullTimes;
            const positions = cachedTrack.fullPositions;

            // Zaman penceresi dışındaysak en yakın sınır noktasını dön
            if (targetTime < times[0]) {
                return Cartesian3.clone(positions[0], result);
            }
            if (targetTime > times[times.length - 1]) {
                return Cartesian3.clone(positions[positions.length - 1], result);
            }

            // Binary Search for surrounding points
            let low = 0, high = times.length - 2;
            while (low <= high) {
                const mid = (low + high) >>> 1;
                if (times[mid] <= targetTime) low = mid + 1;
                else high = mid - 1;
            }

            const idx = Math.max(0, high);
            const t0 = times[idx];
            const t1 = times[idx + 1];
            const p0 = positions[idx];
            const p1 = positions[idx + 1];

            // Linear Interpolation (p0 -> p1)
            const factor = (targetTime - t0) / (t1 - t0);
            const finalPos = Cartesian3.lerp(p0, p1, factor, result || new Cartesian3());

            // Cache for this frame
            if (Object.keys(this.framePositionCache).length > 30) this.framePositionCache = {};
            this.framePositionCache[cacheKey] = { time: timeKey, pos: Cartesian3.clone(finalPos) };

            return finalPos;
        }, false);
    }

    private createSafeOrientationProperty(positionProperty: any, center: Cartesian3) {
        let lastResult = Quaternion.IDENTITY.clone();
        return new CallbackProperty((time, result) => {
            if (!this.viewer || this.viewer.isDestroyed()) return undefined;
            const t = time || this.viewer.clock.currentTime;
            if (!t) return undefined;

            const p = positionProperty.getValue(t);
            if (!p) return undefined;

            // Get position 1 second later to compute direction/velocity
            const tNext = JulianDate.addSeconds(t, 1, new JulianDate());
            const pNext = positionProperty.getValue(tNext);
            if (!pNext) return lastResult;

            const velocity = Cartesian3.subtract(pNext, p, new Cartesian3());
            const mag = Cartesian3.magnitude(velocity);
            if (!Number.isFinite(mag) || mag < 0.01) {
                return lastResult;
            }

            const dir = Cartesian3.normalize(velocity, new Cartesian3());

            // "Up" vector is relative to the celestial body center (zenith)
            const upVec = Cartesian3.subtract(p, center, new Cartesian3());
            const upMag = Cartesian3.magnitude(upVec);
            if (!Number.isFinite(upMag) || upMag < 0.01) {
                return lastResult;
            }
            const up = Cartesian3.normalize(upVec, new Cartesian3());

            let right = Cartesian3.cross(up, dir, new Cartesian3());
            const rightMag = Cartesian3.magnitude(right);
            if (!Number.isFinite(rightMag) || rightMag < 0.001) {
                right = Cartesian3.cross(Cartesian3.UNIT_Z, up, new Cartesian3());
                const altRightMag = Cartesian3.magnitude(right);
                if (!Number.isFinite(altRightMag) || altRightMag < 0.001) {
                    right = Cartesian3.UNIT_X;
                } else {
                    Cartesian3.normalize(right, right);
                }
            } else {
                Cartesian3.normalize(right, right);
            }

            const forward = Cartesian3.cross(up, right, new Cartesian3());
            const mat3 = new Matrix3(
                right.x, forward.x, up.x,
                right.y, forward.y, up.y,
                right.z, forward.z, up.z
            );

            const q = Quaternion.fromRotationMatrix(mat3, result || new Quaternion());
            Quaternion.clone(q, lastResult);
            return q;
        }, false);
    }

    private updateExistingSatellite(sat: SatellitePosition, entity: any, deps: EntityManagerDeps & { gsWinners?: Record<string, any> }) {
        const { celestialBody, showSatellites, showCoverage, earthCenter, groundStations, refs, gsWinners, selectedModel, selectedSatelliteId } = deps;
        const isOnMoon = sat.referenceBody === 'moon';
        const isEarth = celestialBody === 'earth';
        const isVisible = isOnMoon ? celestialBody === 'moon' : celestialBody === 'earth';
        const center = sat.referenceBody === 'moon' ? deps.moonCenter : earthCenter;

        // EĞER ESKİ MANTIKLA YARATILMIŞ BİR POZİSYON VARSA (Scrubbing sırasında titreyen), YENİSİYLE DEĞİŞTİR!
        if (!(entity as any)._soc_position_initialized) {
            const newProp = this.createUnifiedPositionProperty(sat, refs, center);
            entity.position = newProp;
            (entity as any)._soc_position_initialized = true;
        }

        const shouldHaveOrientation = !(isOnMoon || sat.referenceBody !== celestialBody);
        if (!shouldHaveOrientation) {
            if (entity.orientation !== undefined) {
                entity.orientation = undefined;
            }
        } else {
            if (entity.orientation === undefined) {
                entity.orientation = this.createSafeOrientationProperty(entity.position, center) as any;
            }
        }

        const connectedGsIds = groundStations
            .filter(gs => gsWinners?.[gs.id]?.satId === sat.id)
            .map(gs => gs.id);

        const isLinked = connectedGsIds.length > 0;

        if (entity.point) {
            entity.point.color = (isLinked ? Color.LIME : Color.ORANGERED) as any;
            entity.point.outlineColor = (isLinked ? Color.GREEN : Color.DARKRED) as any;
            entity.point.show = (showSatellites && isVisible) as any;
        }
        if (entity.model) {
            entity.model.color = (isLinked ? Color.WHITE : Color.ORANGE.withAlpha(0.8)) as any;
            entity.model.show = (showSatellites && isVisible) as any;
            const rawUri = (sat as any).modelPath || selectedModel;
            entity.model.uri = ((rawUri && rawUri.startsWith('/')) ? (window.location.origin + rawUri) : rawUri) as any;
            const rawScale = (sat as any).modelScale ?? 1.0;
            const safeScale = (Number.isFinite(rawScale) && rawScale > 0.001) ? rawScale : 1.0;
            entity.model.scale = (safeScale * 500) as any;
            entity.model.minimumPixelSize = 150 as any;
            entity.model.maximumScale = (safeScale * 5000) as any;
        }
        if (entity.label) {
            entity.label.show = (showSatellites && isVisible) as any;
            entity.label.fillColor = (isLinked ? Color.LIME : Color.ORANGE) as any;
        }
        if (entity.path) entity.path.show = false as any;

        ['coverage-footprint', 'swath-footprint', 'footprint-center', 'fov-cone'].forEach(suffix => {
            const e = this.safeGetById(`${sat.id}-${suffix}`);
            if (e) e.show = (showSatellites && showCoverage && isEarth) as any;
        });

        const existingHud = this.safeGetById(`${sat.id}-hud`);
        if (existingHud && existingHud.label) {
            existingHud.label.show = (showSatellites && isVisible) as any;
        }

        if (sat.id === selectedSatelliteId) {
            const satEntity = this.safeGetById(sat.id);
            if (satEntity && isVisible && this.viewer && !this.viewer.isDestroyed()) {
                this.viewer.trackedEntity = satEntity;
            }
        }

        // Comm Lines (Multi-GS)
        groundStations.forEach(gs => {
            const commLineId = `${sat.id}-comm-line-${gs.id}`;
            const existingCommLine = this.safeGetById(commLineId);
            const isThisGsLinked = connectedGsIds.includes(gs.id);

            if (isThisGsLinked && isEarth) {
                if (!existingCommLine) {
                    this.entities?.add({
                        id: commLineId,
                        show: true,
                        polyline: {
                            positions: new CallbackProperty((time) => {
                                const satEntity = this.safeGetById(sat.id);
                                const gsPos = Cartesian3.fromDegrees(gs.lon, gs.lat, 10);
                                if (!this.viewer || this.viewer.isDestroyed()) return [];
                                const satPos = satEntity?.position?.getValue(time || this.viewer.clock.currentTime);
                                return (satPos && gsPos) ? [satPos, gsPos] : [];
                            }, false) as any,
                            width: 6,
                            // [Opt-2] Replaced PolylineGlowMaterialProperty with plain color
                            material: Color.LIME.withAlpha(0.8) as any,
                            show: true
                        }
                    });
                } else {
                    existingCommLine.show = true;
                }
            } else {
                if (existingCommLine) existingCommLine.show = false;
            }
        });
    }

    private processGroundStations(deps: EntityManagerDeps) {
        const { groundStations, satellites, celestialBody, earthCenter, showCoverage, refs } = deps;
        const isEarth = celestialBody === 'earth';

        groundStations.forEach(gs => {
            let entity = this.safeGetById(gs.id);
            if (!entity) {
                this.entities?.add({
                    id: gs.id, position: Cartesian3.fromDegrees(gs.lon, gs.lat, 10),
                    point: { pixelSize: 12, color: Color.YELLOW, outlineColor: Color.BLACK, outlineWidth: 2, show: isEarth },
                    label: { text: gs.name, font: '14px Inter, sans-serif', verticalOrigin: 1, pixelOffset: new Cartesian3(0, -18, 0), show: isEarth },
                });
            } else {
                entity.show = isEarth;
                if (entity.point) entity.point.pixelSize = 12 as any;
                if (entity.label) entity.label.pixelOffset = new Cartesian3(0, -18, 0) as any;
            }

            // Dish
            const dishId = `${gs.id}-dish`;
            let dishEntity = this.safeGetById(dishId);

            if (!dishEntity) {
                this.entities?.add({
                    id: dishId,
                    position: new CallbackPositionProperty((time, result) => {
                        if (!this.viewer || this.viewer.isDestroyed()) return Cartesian3.fromDegrees(gs.lon, gs.lat, 25, undefined, result);
                        try {
                            const camHeight = this.viewer.camera.positionCartographic.height;
                            const scale = Math.max(1, camHeight / 250000);
                            const h = 25 * scale;
                            return Cartesian3.fromDegrees(gs.lon, gs.lat, h, undefined, result);
                        } catch (e) {
                            return Cartesian3.fromDegrees(gs.lon, gs.lat, 25, undefined, result);
                        }
                    }, false),
                    orientation: new CallbackProperty((_time, result) => {
                        const basePos = Cartesian3.fromDegrees(gs.lon, gs.lat, 0);
                        const baseMag = Cartesian3.magnitude(basePos);
                        const isBaseValid = Number.isFinite(baseMag) && baseMag >= 0.001;
                        let dir;
                        const connectedSat = satellites.find(s => s.linkStatus === 'connected' && s.referenceBody === 'earth');

                        if (connectedSat) {
                            const satPos = toCartesian3(connectedSat, earthCenter);
                            const diff = Cartesian3.subtract(satPos, basePos, new Cartesian3());
                            const diffMag = Cartesian3.magnitude(diff);
                            if (!Number.isFinite(diffMag) || diffMag < 0.001) {
                                dir = isBaseValid ? Cartesian3.normalize(basePos, new Cartesian3()) : Cartesian3.UNIT_Z;
                            } else {
                                dir = Cartesian3.normalize(diff, new Cartesian3());
                            }
                        } else {
                            dir = isBaseValid ? Cartesian3.normalize(basePos, new Cartesian3()) : Cartesian3.UNIT_Z;
                        }

                        const up = dir;
                        let right = Cartesian3.cross(Cartesian3.UNIT_Z, up, new Cartesian3());
                        const rightMag = Cartesian3.magnitude(right);
                        if (!Number.isFinite(rightMag) || rightMag < 0.001) right = Cartesian3.UNIT_X;
                        else Cartesian3.normalize(right, right);

                        const forward = Cartesian3.cross(up, right, new Cartesian3());
                        const mat3 = new Matrix3(right.x, forward.x, up.x, right.y, forward.y, up.y, right.z, forward.z, up.z);
                        return Quaternion.fromRotationMatrix(mat3, result);
                    }, false) as any,
                    cylinder: {
                        length: new CallbackProperty(() => {
                            if (!this.viewer || this.viewer.isDestroyed()) return 200;
                            try {
                                const camHeight = this.viewer.camera.positionCartographic?.height ?? 0;
                                const scale = Number.isFinite(camHeight) ? Math.max(1, camHeight / 250000) : 1;
                                return 200 * scale;
                            } catch (e) { return 200; }
                        }, false) as any,
                        topRadius: new CallbackProperty(() => {
                            if (!this.viewer || this.viewer.isDestroyed()) return 400;
                            try {
                                const camHeight = this.viewer.camera.positionCartographic?.height ?? 0;
                                const scale = Number.isFinite(camHeight) ? Math.max(1, camHeight / 250000) : 1;
                                return 400 * scale;
                            } catch (e) { return 400; }
                        }, false) as any,
                        bottomRadius: 0,
                        material: Color.SLATEGRAY.withAlpha(0.95), outline: true, outlineColor: Color.DARKSLATEGRAY, show: isEarth
                    } as any
                });
            } else {
                dishEntity.show = isEarth;
            }

            // Ping Ring
            const anyLinked = satellites.some(s => s.linkStatus === 'connected' && s.referenceBody === 'earth');
            const pingId = `${gs.id}-ping-ring`;
            const existingPing = this.safeGetById(pingId);

            if (anyLinked && isEarth) {
                const currentPing = refs.pingSizeRef.current[gs.id] || 0;
                const nextPing = currentPing >= 600000 ? 50000 : currentPing + 15000;
                refs.pingSizeRef.current[gs.id] = nextPing;
                const alpha = Math.max(0.05, 0.4 * (1 - nextPing / 600000));

                if (!existingPing) {
                    this.entities?.add({
                        id: pingId,
                        position: Cartesian3.fromDegrees(gs.lon, gs.lat, 0),
                        ellipse: { semiMajorAxis: nextPing, semiMinorAxis: nextPing, height: 0, material: Color.LIME.withAlpha(alpha), outline: true, outlineColor: Color.LIME.withAlpha(alpha + 0.1), show: true }
                    });
                } else if (existingPing.ellipse) {
                    existingPing.ellipse.semiMajorAxis = nextPing as any;
                    existingPing.ellipse.semiMinorAxis = nextPing as any;
                    existingPing.ellipse.material = Color.LIME.withAlpha(alpha) as any;
                    existingPing.ellipse.outlineColor = Color.LIME.withAlpha(alpha + 0.1) as any;
                    existingPing.show = true;
                }
            } else {
                refs.pingSizeRef.current[gs.id] = 0;
                if (existingPing) existingPing.show = false;
            }

            // Static Coverage
            const coverageId = `${gs.id}-static-coverage`;
            let coverageEntity = this.safeGetById(coverageId);
            if (!coverageEntity) {
                this.entities?.add({
                    id: coverageId,
                    position: Cartesian3.fromDegrees(gs.lon, gs.lat, 0),
                    ellipse: { semiMajorAxis: 2000000, semiMinorAxis: 2000000, material: Color.YELLOW.withAlpha(0.04), outline: true, outlineColor: Color.YELLOW.withAlpha(0.35), outlineWidth: 3, show: (showCoverage && isEarth) as any, height: 0 }
                });
            } else {
                coverageEntity.show = (showCoverage && isEarth) as any;
            }
        });
    }

    private processOrbitTracks(deps: EntityManagerDeps) {
        const { trajectories, fullTrajectories, satellites, celestialBody, showOrbits, hiddenOrbitIds, refs, earthCenter, moonCenter } = deps;
        const orbitSource = fullTrajectories || trajectories; // Fallback to sliced if full is missing

        Object.entries(orbitSource).forEach(([rawSatId, points]) => {
            if (!points || points.length < 2) return;

            // Robust lookup: Match by either ID or NORAD ID
            const sat = satellites.find(s => s && (String(s.id) === String(rawSatId) || (s.noradId && String(s.noradId) === String(rawSatId))));

            // USE THE RESOLVED PRIMARY SAT ID FOR THE CACHE KEY
            // This ensures movement logic (createUnifiedPositionProperty) can find it.
            const satId = sat ? sat.id : rawSatId;

            const trackId = `${satId}-predicted-track`;
            const trackEntity = this.safeGetById(trackId);

            const isLinked = sat?.linkStatus === 'connected';
            const isVisible = sat
                ? (String(sat.referenceBody || 'earth').toLowerCase() === String(celestialBody).toLowerCase())
                : true;

            // Read custom color from localStorage; fall back to default cyan/yellow
            let orbitColor: Color;
            try {
                const stored = typeof localStorage !== 'undefined' ? localStorage.getItem('soc-orbit-colors') : null;
                if (stored) {
                    const colors = JSON.parse(stored);
                    const hex = colors[String(satId)];
                    orbitColor = hex ? Color.fromCssColorString(hex).withAlpha(0.8) : (isLinked ? Color.CYAN.withAlpha(0.7) : Color.YELLOW.withAlpha(0.5));
                } else {
                    orbitColor = isLinked ? Color.CYAN.withAlpha(0.7) : Color.YELLOW.withAlpha(0.5);
                }
            } catch (_) {
                orbitColor = isLinked ? Color.CYAN.withAlpha(0.7) : Color.YELLOW.withAlpha(0.5);
            }

            const orbitMaterial = this.getMaterial('glow', orbitColor);
            const shouldShowOrbit = showOrbits && isVisible && !hiddenOrbitIds.has(satId);

            const firstTime = points[0]?.time;
            let targetTime = Date.now();
            if (this.viewer && !this.viewer.isDestroyed()) {
                try {
                    targetTime = JulianDate.toDate(this.viewer.clock.currentTime).getTime();
                } catch (e) { }
            }
            const center = (sat?.referenceBody === 'moon' || (celestialBody === 'moon' && !sat)) ? moonCenter : earthCenter;

            let cachedTrack = refs.orbitChunksRef.current[satId];

            // 1. Incremental Cartesian Caching
            // IMPROVED: If the hook already populated the high-performance buffer, reuse it.
            // We only recalculate if the start time has jumped significantly or buffer is empty.
            const needsFullReset = !cachedTrack || cachedTrack.startIdx !== firstTime || !cachedTrack.fullPositions || cachedTrack.fullPositions.length === 0;

            if (needsFullReset) {
                const fullPos = points.map(p => toCartesian3(p, center));
                const fullTimes = points.map(p => new Date(p.time).getTime());

                let low = 0, high = fullTimes.length - 1;
                while (low <= high) {
                    const mid = (low + high) >>> 1;
                    if (fullTimes[mid] <= targetTime) low = mid + 1;
                    else high = mid - 1;
                }
                const startIdx = Math.max(0, high);
                const endIdx = Math.min(fullTimes.length - 1, startIdx + 200);

                cachedTrack = refs.orbitChunksRef.current[satId] = {
                    startIdx: firstTime as any,
                    fullLength: points.length,
                    fullPositions: fullPos,
                    fullTimes: fullTimes,
                    drawnStartIndex: startIdx,
                    drawnEndIndex: endIdx,
                    positions: fullPos.slice(startIdx, endIdx + 1),
                    times: fullTimes.slice(startIdx, endIdx + 1)
                };
                if (trackEntity?.polyline) trackEntity.polyline.positions = cachedTrack.positions as any;
            } else if (cachedTrack.fullLength !== points.length && points.length > (cachedTrack.fullLength || 0)) {
                // Incremental update for new points
                const lastLen = cachedTrack.fullLength!;
                const newPoints = points.slice(lastLen);
                cachedTrack.fullPositions.push(...newPoints.map(p => toCartesian3(p, center)));
                cachedTrack.fullTimes.push(...newPoints.map(p => new Date(p.time).getTime()));
                cachedTrack.fullLength = points.length;

                // Hardening: Limit trajectory history to prevent OOM over long sessions
                if (cachedTrack.fullPositions.length > 10000) {
                    const toRemove = cachedTrack.fullPositions.length - 8000;
                    cachedTrack.fullPositions.splice(0, toRemove);
                    cachedTrack.fullTimes.splice(0, toRemove);
                    cachedTrack.drawnStartIndex = Math.max(0, (cachedTrack.drawnStartIndex ?? 0) - toRemove);
                    cachedTrack.drawnEndIndex = Math.max(0, (cachedTrack.drawnEndIndex ?? 0) - toRemove);
                }
            }

            // 2. Always start from current time to prevent past trails
            const fullTimes = cachedTrack.fullTimes;
            let low = 0, high = fullTimes.length - 1;
            while (low <= high) {
                const mid = (low + high) >>> 1;
                if (fullTimes[mid] <= targetTime) low = mid + 1;
                else high = mid - 1;
            }

            const newStart = Math.max(0, high);
            const newEnd = Math.min(fullTimes.length - 1, newStart + 200);

            if (newStart !== cachedTrack.drawnStartIndex) {
                cachedTrack.drawnStartIndex = newStart;
                cachedTrack.drawnEndIndex = newEnd;
                cachedTrack.positions = cachedTrack.fullPositions.slice(newStart, newEnd + 1);
                cachedTrack.times = fullTimes.slice(newStart, newEnd + 1);

                if (trackEntity?.polyline) {
                    trackEntity.polyline.positions = cachedTrack.positions as any;
                }
            }

            if (!trackEntity) {
                const newEntity = this.entities?.add({
                    id: trackId,
                    show: shouldShowOrbit as any,
                    polyline: {
                        positions: cachedTrack.positions,
                        width: isLinked ? 3 : 1.5,
                        material: orbitMaterial as any,
                        clampToGround: true,
                        arcType: ArcType.GEODESIC
                    } as any
                });
                (newEntity as any)._soc_track_linked = isLinked;
            } else if (trackEntity.polyline) {
                if (trackEntity.polyline.positions instanceof CallbackProperty) {
                    trackEntity.polyline.positions = cachedTrack.positions as any;
                }
                if ((trackEntity as any)._soc_track_linked !== isLinked) {
                    trackEntity.polyline.material = orbitMaterial as any;
                    trackEntity.polyline.width = (isLinked ? 3 : 1.5) as any;
                    (trackEntity as any)._soc_track_linked = isLinked;
                }
                trackEntity.show = shouldShowOrbit as any;
            }
        });
    }

    private processHeatmaps(deps: EntityManagerDeps) {
        const { celestialBody } = deps;
        if (celestialBody !== 'earth') {
            // Hide heatmaps if on moon
            this.entities?.values.forEach(entity => {
                if (entity.id.startsWith('heatmap-sr-')) entity.show = false;
            });
            return;
        }

        const currentHeatmapIds = new Set<string>();
        const oneDayAgo = Date.now() - 24 * 60 * 60 * 1000;

        // Cleanup old heatmaps
        this.entities?.values.forEach(entity => {
            if (entity.id.startsWith('heatmap-sr-') && !currentHeatmapIds.has(entity.id)) {
                this.entities?.remove(entity);
            }
        });
    }

    private processActiveDrawing(deps: EntityManagerDeps) {
        const { drawingMode, isDrawing, polygonPoints, circleCenter, circleRadius } = deps;

        if (drawingMode === 'polygon' && polygonPoints.length > 0) {
            let polyline = this.safeGetById('aoi-drawing-polyline');
            if (!polyline && this.entities) {
                this.entities?.add({
                    id: 'aoi-drawing-polyline',
                    polyline: {
                        positions: new CallbackProperty(() => polygonPoints, false),
                        width: 3, material: Color.fromCssColorString('#facc15'), clampToGround: true
                    } as any
                });
            }
            let polygon = this.safeGetById('aoi-drawing-polygon');
            if (!polygon && this.entities) {
                this.entities?.add({
                    id: 'aoi-drawing-polygon',
                    polygon: {
                        hierarchy: new CallbackProperty(() => {
                            if (polygonPoints.length < 3) return new PolygonHierarchy([]);
                            return new PolygonHierarchy(polygonPoints);
                        }, false) as any,
                        material: Color.fromCssColorString('#facc15').withAlpha(0.3),
                        outline: true,
                        outlineColor: Color.fromCssColorString('#facc15')
                    } as any
                });
            }
        } else if (drawingMode === 'circle' && circleCenter) {
            let circle = this.safeGetById('aoi-drawing-circle');
            if (!circle && this.entities) {
                this.entities?.add({
                    id: 'aoi-drawing-circle',
                    position: circleCenter,
                    ellipse: {
                        semiMajorAxis: new CallbackProperty(() => Math.max(1, circleRadius), false) as any,
                        semiMinorAxis: new CallbackProperty(() => Math.max(1, circleRadius), false) as any,
                        material: Color.fromCssColorString('#facc15').withAlpha(0.3),
                        height: 0
                    } as any
                });
            } else if (circle) {
                circle.position = circleCenter as any;
            }
        }

        if (drawingMode === 'none') {
            ['aoi-drawing-polygon', 'aoi-drawing-polyline', 'aoi-drawing-circle'].forEach(id => {
                const ent = this.safeGetById(id);
                if (ent) this.entities?.remove(ent);
            });
        }
    }

    private cleanupRogueEntities(deps: EntityManagerDeps) {
        const { satellites, groundStations, trajectories, drawingMode } = deps;
        const currentSatIds = new Set(satellites.map(s => s.id));
        const currentGsIds = new Set(groundStations.map(gs => gs.id));

        const toRemove: any[] = [];

        this.entities?.values.forEach(entity => {
            const id = entity.id;

            // 1. Satellite & Ground Station related
            if (id.endsWith('-sgp4-traj') || id.endsWith('-comm-line') || id.endsWith('-fov-cone') || id.endsWith('-hud') || id.endsWith('-coverage-footprint') || id.endsWith('-swath-footprint') || id.endsWith('-footprint-center') || id.endsWith('-ground-trace')) {
                const baseId = id.split('-').slice(0, -2).join('-') || id.split('-')[0];
                if (baseId && !currentSatIds.has(baseId) && !currentGsIds.has(baseId)) {
                    toRemove.push(entity);
                }
            } else if (id.endsWith('-dish') || id.endsWith('-static-coverage') || id.endsWith('-ping-ring')) {
                const baseId = id.replace(/-dish|-static-coverage|-ping-ring/, '');
                if (!currentGsIds.has(baseId)) toRemove.push(entity);
            } else if (id.endsWith('-predicted-track')) {
                const baseId = id.replace('-predicted-track', '');
                if (!trajectories[baseId]) toRemove.push(entity);
            }

            // 6. Base satellites/GS (only if they aren't in incoming and aren't special bodies)
            if (!['earth-body', 'moon-body'].includes(id) && !currentSatIds.has(id) && !currentGsIds.has(id)) {
                // If it's a "clean" ID (no prefix/suffix recognized above)
                if (!id.includes('-') && !id.startsWith('aoi-') && !id.startsWith('sr-') && !id.startsWith('heatmap-')) {
                    toRemove.push(entity);
                }
            }
        });

        // Perform removal outside iteration loop
        toRemove.forEach(e => {
            try {
                this.entities?.remove(e);
            } catch (err) {
                // Silent catch for double-removals during race conditions
            }
        });
    }

    private ensureGroundTrace(sat: any, entity: any, showOrbits: boolean, isVisible: boolean, isOnMoon: boolean, hiddenOrbitIds: Set<string>) {
        const gtId = `${sat.id}-ground-trace`;
        let gt = this.safeGetById(gtId);
        const shouldShow = showOrbits && isVisible && !hiddenOrbitIds.has(sat.id);

        if (!gt) {
            gt = this.entities?.add({
                id: gtId,
                position: new CallbackPositionProperty((clockTime, result?: Cartesian3) => {
                    if (!this.viewer || this.viewer.isDestroyed()) return undefined;
                    const satPos = entity?.position?.getValue(clockTime || this.viewer.clock.currentTime);
                    if (!satPos) return undefined;
                    const scene = this.viewer.scene;
                    const carto = scene.globe.ellipsoid.cartesianToCartographic(satPos);
                    if (!carto) return undefined;
                    return Cartesian3.fromRadians(carto.longitude, carto.latitude, 0, undefined, result);
                }, false),
                path: {
                    show: shouldShow as any,
                    width: 2,
                    material: this.getMaterial('dash', Color.YELLOW.withAlpha(0.6), { gapColor: Color.TRANSPARENT }),
                    leadTime: 7200, trailTime: 0, resolution: 120
                }
            });
        } else {
            if (gt.path) {
                gt.path.show = shouldShow as any;
            }
        }
    }

    private calculateGsWinners(deps: EntityManagerDeps): Record<string, { satId: string, priority: number }> {
        const { satellites, groundStations, celestialBody } = deps;
        const gsWinners: Record<string, { satId: string, priority: number }> = {};
        const isEarth = celestialBody === 'earth';
        if (!this.viewer || this.viewer.isDestroyed()) return gsWinners;
        const clockTimeValue = this.viewer.clock.currentTime;

        if (!clockTimeValue || !isEarth) return gsWinners;

        satellites.forEach(sat => {
            if (sat.referenceBody !== 'earth') return;

            // Reuse the interpolated position for this frame
            const timeKey = `${clockTimeValue.dayNumber}_${clockTimeValue.secondsOfDay.toFixed(3)}`;
            const cacheKey = `${sat.id}_${timeKey}`;

            let satPos = this.framePositionCache[cacheKey]?.pos;

            // If not in cache (e.g. dot hidden or first run), we can try to find it in orbitChunks
            if (!satPos) {
                const cachedTrack = deps.refs.orbitChunksRef.current[sat.id];
                if (cachedTrack && cachedTrack.fullTimes && cachedTrack.fullTimes.length >= 2) {
                    // Quick one-off interpolation for link budget
                    const targetTime = JulianDate.toDate(clockTimeValue).getTime();
                    const times = cachedTrack.fullTimes;
                    if (targetTime >= times[0] && targetTime <= times[times.length - 1]) {
                        let low = 0, high = times.length - 2;
                        while (low <= high) {
                            const mid = (low + high) >>> 1;
                            if (times[mid] <= targetTime) low = mid + 1;
                            else high = mid - 1;
                        }
                        const idx = Math.max(0, high);
                        const factor = (targetTime - times[idx]) / (times[idx + 1] - times[idx]);
                        satPos = Cartesian3.lerp(cachedTrack.fullPositions[idx], cachedTrack.fullPositions[idx + 1], factor, new Cartesian3());
                    }
                }
            }

            if (!satPos) return;

            groundStations.forEach(gs => {
                const gsPos = Cartesian3.fromDegrees(gs.lon, gs.lat, (gs as any).alt || 0);

                // Vector from GS to Sat
                const vector = Cartesian3.subtract(satPos!, gsPos, new Cartesian3());
                const distance = Cartesian3.magnitude(vector);
                if (distance < 0.001) return;

                // Surface normal at GS
                if (!this.viewer || this.viewer.isDestroyed()) return;
                const normal = this.viewer.scene.globe.ellipsoid.geodeticSurfaceNormal(gsPos, new Cartesian3());
                if (!normal) return;

                // Elevation = angle between (Sat-GS) vector and surface normal
                const normVec = Cartesian3.normalize(vector, new Cartesian3());
                const cosAngle = Cartesian3.dot(normVec, normal);
                const elevAngle = CesiumMath.toDegrees(Math.asin(Math.max(-1, Math.min(1, cosAngle))));

                // Min Elevation Limit (Default 5.0)
                const threshold = (gs as any).minElevation ?? 5.0;

                if (elevAngle >= threshold) {
                    const satPriority = (sat as any).priority ?? 0;
                    if (!gsWinners[gs.id] || satPriority > gsWinners[gs.id].priority) {
                        gsWinners[gs.id] = { satId: sat.id, priority: satPriority };
                    }
                }
            });
        });
        return gsWinners;
    }
    /**
     * Real-time sync for high-frequency link and telemetry updates (10Hz).
     */
    public update(currentTime: Date, satellites: SatellitePosition[], groundStations: GroundStation[]) {
        if (!this.viewer || this.viewer.isDestroyed()) return;

        // 1. Recalculate GS winners for the current time (Throttled to 1Hz)
        const now = performance.now();
        let gsWinners = this.gsWinnersCache;
        if (now - this.lastLinkCalcTime > 1000) {
            gsWinners = this.calculateGsWinners({
                satellites,
                groundStations,
                celestialBody: 'earth',
                trajectories: {},
                fullTrajectories: {},
                showSatellites: true,
                showOrbits: true,
                showCoverage: true,
                show3DTerrain: true,
                selectedModel: '',
                hiddenOrbitIds: new Set(),
                selectedSatelliteId: null,
                earthCenter: Cartesian3.ZERO,
                moonCenter: Cartesian3.ZERO,
                refs: {
                    satellitesRef: { current: satellites } as any,
                    trajectoryAddedRef: { current: {} } as any,
                    lastAddedTimeRef: { current: {} } as any,
                    orbitChunksRef: { current: {} } as any,
                    pingSizeRef: { current: {} } as any
                },
                drawingMode: 'none',
                isDrawing: false,
                polygonPoints: [],
                circleCenter: null,
                circleRadius: 0
            });
            this.gsWinnersCache = gsWinners;
            this.lastLinkCalcTime = now;
        }

        const winSet = new Set(Object.values(gsWinners).map(w => w.satId));

        // 2. Update visuals for each satellite (O(S) instead of O(S*G))
        satellites.forEach(sat => {
            try {
                const entity = this.safeGetById(sat.id);
                if (!entity) return;

                const isLinked = winSet.has(sat.id);

                if (entity.point) {
                    entity.point.color = (isLinked ? Color.LIME : Color.ORANGERED) as any;
                    entity.point.outlineColor = (isLinked ? Color.GREEN : Color.DARKRED) as any;
                }
                if (entity.model) {
                    entity.model.color = (isLinked ? Color.WHITE : Color.ORANGE.withAlpha(0.8)) as any;
                }
                if (entity.label) {
                    entity.label.fillColor = (isLinked ? Color.LIME : Color.ORANGE) as any;
                }

                // Update comm lines
                groundStations.forEach(gs => {
                    const commLineId = `${sat.id}-comm-line-${gs.id}`;
                    const commLine = this.safeGetById(commLineId);
                    const isThisGsLinked = gsWinners[gs.id]?.satId === sat.id;

                    if (commLine) {
                        commLine.show = isThisGsLinked as any;
                    } else if (isThisGsLinked && this.entities) {
                        try {
                            const gsPos = Cartesian3.fromDegrees(gs.lon, gs.lat, 100);
                            this.entities?.add({
                                id: commLineId,
                                polyline: {
                                    positions: new CallbackProperty((time) => {
                                        const p = entity?.position?.getValue(time);
                                        return p ? [p, gsPos] : [];
                                    }, false),
                                    width: 6,
                                    // [Opt-2] Plain color replaces PolylineGlowMaterialProperty
                                    material: Color.LIME.withAlpha(0.8) as any,
                                    show: true
                                }
                            });
                        } catch (e) {
                            console.warn(`[CesiumEntityManager] Failed to create comm line: ${commLineId}`, e);
                        }
                    }
                });
            } catch (err) {
                console.error(`[CesiumEntityManager] Error updating satellite: ${sat.id}`, err);
            }
        });
    }
}
