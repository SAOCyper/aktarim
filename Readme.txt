import { injectable, postConstruct, inject } from '@theia/core/shared/inversify';
import { ArtemisService } from './artemis.service';
import { SatelliteClientManager } from '../rpc/satellite-client-manager';
import { SatelliteApplicationService } from './satellite-application.service';
import { CustomLogger as Cl } from '../logging/custom-logger';
import { correlationGet } from './gsc-correlation-cache';

// GSC Kuyruk Sabitleri
const GSC_DB_QUEUE = 'gsc.server.database_request_queue_';
const GSC_DB_RESPONSE = `${GSC_DB_QUEUE}/response`;
const GSC_ODSRUNNER_QUEUE = 'gsc.server.odsrunner_request_queue_';
const GSC_ODSRUNNER_RESPONSE = `${GSC_ODSRUNNER_QUEUE}/response`;
const GSC_PASSCALC_QUEUE = 'gsc.server.passcalculations_request_queue_';
const GSC_PASSCALC_RESPONSE = `${GSC_PASSCALC_QUEUE}/response`;
const GSC_PASSOPERATIONS_QUEUE = 'gsc.server.passoperations_request_queue_';
const GSC_PASSOPERATIONS_RESPONSE = `${GSC_PASSOPERATIONS_QUEUE}/response`;
const GSC_ADMIN_QUEUE = 'gsc.server.administration_request_queue_';
const GSC_ADMIN_RESPONSE = `${GSC_ADMIN_QUEUE}/response`;


@injectable()
export class OdsListenerService {
  private readonly logger = new Cl(OdsListenerService.name);

  // Expose an internal Map for the cache
  private cache = new Map<string, { value: any, expires: number }>();
  private async cacheSet(key: string, value: any, ttlMs: number) {
      this.cache.set(key, { value, expires: Date.now() + ttlMs });
  }
  private async cacheGet<T>(key: string): Promise<T | null> {
      const item = this.cache.get(key);
      if (!item) return null;
      if (Date.now() > item.expires) {
          this.cache.delete(key);
          return null;
      }
      return item.value as T;
  }
  private async cacheDel(key: string) {
      this.cache.delete(key);
  }

  constructor(
    @inject(ArtemisService) private readonly artemis: ArtemisService,
    @inject(SatelliteClientManager) private readonly gateway: SatelliteClientManager,
    @inject(SatelliteApplicationService) private readonly satelliteAppService: SatelliteApplicationService,
  ) { }

  /**
   * Returns cached ODS trajectory points for a satellite ID.
   * Used by the Theia Express REST route to serve /satellite/trajectory/:id
   */
  async getTrajectory(satId: string): Promise<any[]> {
    return (await this.cacheGet<any[]>(`ODS_TRAJECTORY:${satId}`)) || [];
  }

  @postConstruct()
  init() {
    this.logger.log('Subscribing to GSC response queues...');

    // 1. GSC Database Request - Uydu Listesi / İstasyon Listesi cevapları
    this.artemis.subscribe(GSC_DB_RESPONSE, async (payload: any, headers?: any) => {
      this.logger.debug(`[GSC-DB-RESPONSE] @class: ${payload?.['@class']} | Keys: ${payload ? Object.keys(payload): null}`);
      await this.handleDatabaseResponse(payload, headers);
    });

    // 2. GSC OdsRunner Request - ODS'e uydu ekleme/çıkarma, efemeris, geçiş listesi, TLE cevapları
    this.artemis.subscribe(GSC_ODSRUNNER_RESPONSE, async (payload: any, headers?: any) => {
      this.logger.debug(`[GSC-ODSRUNNER-RESPONSE] @class: ${payload['@class']} | Keys: ${Object.keys(payload)}`);
      await this.handleOdsRunnerResponse(payload, headers);
    });

    // 3. GSC Pass Calculations Request - Gelecek Zamanlı Geçiş Listesi
    this.artemis.subscribe(GSC_PASSCALC_RESPONSE, async (payload: any, headers?: any) => {
      this.logger.debug(`[GSC-PASSCALC-RESPONSE] @class: ${payload['@class']} | Keys: ${Object.keys(payload)}`);
      await this.handlePassCalcResponse(payload, headers);
    });

    // 4. GSC Pass Operations Request - Anlık Geçiş Bilgisi ve Konfigürasyon Değişimleri
    this.artemis.subscribe(GSC_PASSOPERATIONS_RESPONSE, async (payload: any, headers?: any) => {
      this.logger.debug(`[GSC-PASSOPERATIONS-RESPONSE] @class: ${payload['@class']} | Keys: ${Object.keys(payload)}`);
      await this.handlePassOperationsResponse(payload, headers);
    });

    // 5. GSC Administration Request - Sistem Çalışma Modu / feedback cevapları
    this.artemis.subscribe(GSC_ADMIN_RESPONSE, async (payload: any, headers?: any) => {
      this.logger.debug(`[GSC-ADMIN-RESPONSE] @class: ${payload['@class']} | Keys: ${Object.keys(payload)}`);
      await this.handleAdminResponse(payload, headers);
    });

    this.logger.log(`Subscribed to:\n  - ${GSC_DB_RESPONSE}\n  - ${GSC_ODSRUNNER_RESPONSE}\n  - ${GSC_PASSCALC_RESPONSE}\n  - ${GSC_PASSOPERATIONS_RESPONSE}\n  - ${GSC_ADMIN_RESPONSE}`);
  }

  // ─────────────────────────────────────────────────────────────────
  // GSC DATABASE RESPONSE HANDLER
  // ─────────────────────────────────────────────────────────────────

  /**
   * Gelen GSC veritabanı cevabına göre SatListResponse veya StationListResponse işler.
   */
  private async handleDatabaseResponse(payload: any, headers?: any) {
    try {
      const javaClass: string = payload['@class'] || '';
      const headerCorrId = headers?.['correlation-id'] || headers?.['JMSCorrelationID'] || headers?.['correlationId'] || '';
      const payloadCorrId = payload.correlationId || payload.corrId || '';
      const corrId = headerCorrId || payloadCorrId;

      this.logger.log(`[GSC-DB-INCOMING] Class: ${javaClass} | CorrId: ${corrId} | Keys: ${Object.keys(payload).join(',')}`);

      // Uydu Listesi Cevabı (SatListResponse)
      if (javaClass.includes('SatListResponse') || payload.satelliteList) {
        const list: any[] = payload.satelliteList || [];
        this.logger.log(`### GSC SAT LIST RECEIVED (${list.length} ITEMS) ###`);

        await this.satelliteAppService.syncSatellites(list);
        await this.cacheDel('ALL_SATELLITES');

        list.forEach(sat => {
          this.logger.log(
            `[SAT] No: ${sat.satelliteNo} | Name: ${sat.satelliteName} | Priority: ${sat.priorityNum} | TLE Auto: ${sat.tleAutoUpdate} | Disabled: ${sat.disabled}`
          );
        });
        this.gateway.broadcast('satellite_updated', { count: list.length, type: 'gsc_sat_list' });
        return;
      }

      // Tekil Uydu Cevabı (SatResponse)
      const isSatResponse = javaClass.includes('SatResponse') || 
                            payload.satellite !== undefined || 
                            (payload.satelliteNo !== undefined && payload.satelliteName !== undefined);

      if (isSatResponse) {
        const satNo = payload.satellite?.satelliteNo || payload.satelliteNo;
        this.logger.log(`[GSC-DB] Detected SatResponse for No: ${satNo}. Syncing...`);
        await this.satelliteAppService.syncSingleSatellite(payload);
        return;
      }

      // Yer İstasyonu Listesi Cevabı (StationListResponse)
      if (javaClass.includes('StationListResponse') || payload.stationList || payload.groundStationList || payload.stationlist) {
        const list: any[] = payload.stationList || payload.groundStationList || payload.stationlist || [];
        this.logger.log(`### GSC STATION LIST RECEIVED (${list.length} ITEMS) ###`);

        await this.satelliteAppService.syncGroundStations(list);

        list.forEach(gs => {
          this.logger.log(
            `[GS] Name: ${gs.name || gs.stationName} | Lat: ${gs.latitude || gs.lat} | Lon: ${gs.longitude || gs.lon} | Alt: ${gs.altitude || gs.alt} | ElevMask: ${gs.elevMask || gs.minElevation}`
          );
        });
        this.gateway.broadcast('ground_station_updated', { count: list.length, type: 'gsc_station_list' });
        return;
      }

      // Aktif İstasyon Cevabı (ActiveStationResponse)
      if (javaClass.includes('ActiveStationResponse') || payload.activeStationId !== undefined || payload.stationId !== undefined) {
        const activeId = payload.activeStationId || payload.stationId;
        if (activeId) {
            this.logger.log(`[GSC-DB] Received authoritative ActiveStation: ${activeId}`);
            await this.satelliteAppService.setActiveStation(activeId);
            // No broadcast here because setActiveStation already broadcasts
        }
        return;
      }

      this.logger.log(`[GSC-DB-DEBUG] javaClass: ${javaClass}, keys: ${Object.keys(payload)}`);

      let detectedSatNo: number | undefined = payload.satelliteNo !== undefined ? Number(payload.satelliteNo) : undefined;

      // Extract satNo from corrId if possible (e.g. "sat-config-names:123:timestamp")
      if (detectedSatNo === undefined && corrId.startsWith('sat-config-')) {
        const parts = corrId.split(':');
        if (parts.length >= 2) {
          detectedSatNo = Number(parts[1]);
        }
      }

      // --- SATELLITE CONFIG HANDLERS (Check these first) ---

      // Sat Config Names Response
      if (javaClass.includes('SatConfigNamesResponse') || (payload.configNames && detectedSatNo !== undefined) || corrId.startsWith('sat-config-names:')) {
        this.logger.log(`[GSC-DB] Received Sat Config Names for Sat ${detectedSatNo}: ${payload.configNames?.length || 0} items`);
        this.gateway.broadcast('sat_config_names', {
          satelliteNo: detectedSatNo,
          configNames: payload.configNames || []
        });
        return;
      }

      // Sat Config Response
      if (javaClass.includes('SatConfigResponse') || payload.satConfiguration || corrId.startsWith('sat-config-details:')) {
        this.logger.log(`[GSC-DB] Received Sat Config details for Sat ${detectedSatNo}, Config: ${payload.satConfiguration?.configName}`);
        this.gateway.broadcast('sat_config_details', {
          satelliteNo: detectedSatNo,
          satConfiguration: payload.satConfiguration
        });
        return;
      }

      // --- GLOBAL CONFIG HANDLERS ---

      // Global Config Names Response (Strict: must NOT have satelliteNo)
      if (javaClass.includes('GlobalConfigNamesResponse') || (payload.configNames && payload.satelliteNo === undefined)) {
        this.logger.log(`[GSC-DB] Received Global Config Names: ${payload.configNames?.length || 0} items`);
        this.gateway.broadcast('global_config_names', { configNames: payload.configNames || [] });
        return;
      }

      // Global Config Response (Strict: must NOT have satelliteNo)
      if (javaClass.includes('GlobalConfigResponse') || (payload.configuration && payload.satelliteNo === undefined)) {
        this.logger.log(`[GSC-DB] Received Global Config details for: ${payload.configuration?.configName}`);
        this.gateway.broadcast('global_config_details', { configuration: payload.configuration });
        return;
      }

      const hasPassPrefs = javaClass.includes('PassPreferences') || javaClass.includes('PassSettings') || payload.passPreferences !== undefined || payload.passSettings !== undefined || payload.passPreferencesResponse !== undefined || (payload.passMinusDay !== undefined && payload.passPlusDay !== undefined);
      if ( hasPassPrefs) {
        const prefs = payload.passPreferences || payload.passSettings || payload.passPreferencesResponse || payload ;
        this.logger.log(`[GSC-DB] Received PassPreferences: MinusDay=${prefs.passMinusDay}, PlusDay=${prefs.passPlusDay}, SendMin = ${prefs.configSendMinBeforePass}, Overlap=${prefs.overlapMinDiff}`);
        this.gateway.broadcast('pass_preferences', prefs);
        return;
      }
      // PassPreferences Response
      if (javaClass.includes('PassSettingsResponse') || (payload.passMinusDay !== undefined && payload.passPlusDay !== undefined)) {
        this.logger.log(`[GSC-DB] Received PassSettingsResponse: MinusDay=${payload.passMinusDay}, PlusDay=${payload.passPlusDay}, SendMin=${payload.configSendMinBeforePass}, Overlap=${payload.overlapMinDiff}`);
        this.gateway.broadcast('pass_preferences', payload);
        return;
      }

      // --- Feedback Handling ---
      // GSC bazen veriyi 'feedback' objesi içinde gönderir
      const fb = payload.feedback || payload;
      const isFeedback = javaClass.includes('Feedback') || payload.feedback !== undefined || fb.feedbackContent !== undefined;

      if (isFeedback) {
        const feedbackSuccessful = fb.successful === true || fb.successful === 'true';
        const feedbackContent = fb.feedbackContent || '';
        const feedbackMessage = fb.message || '';
        const finalCorrId = corrId || fb.correlationId || fb.corrId || '';

        this.logger.log(`[GSC-DB] Received Feedback: ${feedbackSuccessful ? 'SUCCESS' : 'FAIL'} | Content: ${feedbackContent} | Message: ${feedbackMessage} | CorrId: ${finalCorrId}`);

        // --- Handle Pass Settings Feedback ---
        if (finalCorrId.startsWith('PASS_SETTINGS_')) {
          this.gateway.broadcast('pass_settings_feedback', {
            successful: feedbackSuccessful || feedbackContent === 'SUCCESS' || feedbackContent === 'REQUEST_IS_RECEIVED',
            message: feedbackMessage || feedbackContent
          });
        }

        // --- Handle Priority Update Feedback ---
        if (finalCorrId.startsWith('PRIORITY_UPDATE_')) {
          const isActuallySuccess = feedbackSuccessful || feedbackContent === 'SUCCESS' || feedbackContent === 'REQUEST_IS_RECEIVED';
          
          if (isActuallySuccess) {
            const parts = finalCorrId.split('_');
            const satNo = Number(parts[2]);
            const newPriority = Number(parts[3]);
            const oldPriority = Number(parts[4]);

            this.logger.log(`[GSC-DB] Priority update success for Sat ${satNo} (moved to ${newPriority}). Checking for displacement...`);

            // Find if another satellite occupies the new priority
            let displacedSatNo: number | null = null;
            let morePriorForDisplaced = false;

            if (!isNaN(newPriority) && !isNaN(oldPriority)) {
                const sats = await this.satelliteAppService.getAllSatellites();
                for (const otherSat of sats) {
                    if (otherSat.id !== String(satNo) && otherSat.priority === newPriority) {
                        displacedSatNo = Number(otherSat.noradId || otherSat.id);
                        // If target sat went UP (e.g. 2 -> 1, priority number decreased), 
                        // the displaced sat must go DOWN (1 -> 2, morePrior=false).
                        // If target sat went DOWN (e.g. 1 -> 2, priority number increased),
                        // the displaced sat must go UP (2 -> 1, morePrior=true).
                        morePriorForDisplaced = (oldPriority < newPriority); 
                        break;
                    }
                }
            }

            if (displacedSatNo !== null) {
                this.logger.log(`[GSC-DB] Displacing Sat ${displacedSatNo} to priority ${oldPriority}`);
                const displacedCorrId = `DISPLACED_PRIORITY_${displacedSatNo}_${Date.now()}`;
                const payload = {
                    satelliteNo: displacedSatNo,
                    morePrior: morePriorForDisplaced,
                    '@class': 'tr.gov.uzay.gsc.server.database.api.messaging.requests.PriorityUpdateRequest'
                };
                this.artemis.publish(GSC_DB_QUEUE, payload['@class'], payload, `${GSC_DB_QUEUE}/response`, displacedCorrId)
                    .catch(err => this.logger.error(`[GSC-DB] Displaced priority update failed: ${err.message}`));
            }

            // DB'nin güncellenmesi için kısa bir süre bekle (Race condition önlemi)
            setTimeout(() => {
              this.satelliteAppService.requestGscSatellite(satNo).catch(() => { });
              if (displacedSatNo) {
                  this.satelliteAppService.requestGscSatellite(displacedSatNo).catch(() => { });
              }
            }, 2000);
          } else {
            this.logger.error(`[GSC-DB] Priority update FAILED for Sat ${finalCorrId}: ${feedbackMessage} (Content: ${feedbackContent})`);
          }
        }

        // Broadcast results
        this.gateway.broadcast('global_config_operation_result', {
          successful: feedbackSuccessful,
          message: feedbackMessage,
          feedbackContent: feedbackContent
        });

        this.gateway.broadcast('sat_config_operation_result', {
          successful: feedbackSuccessful,
          message: feedbackMessage,
          feedbackContent: feedbackContent
        });

        if (feedbackSuccessful) {
          this.artemis.sendGlobalConfigNamesRequest();
        }
        return;
      }

      this.logger.warn(`[GSC-DB-RESPONSE] Unknown: ${javaClass}. Keys: ${Object.keys(payload)}`);
    } catch (error: any) {
      this.logger.error(`[GSC-DB-RESPONSE] Processing error: ${error.message}`);
    }
  }

  // ─────────────────────────────────────────────────────────────────
  // GSC ODSRUNNER RESPONSE HANDLER
  // ─────────────────────────────────────────────────────────────────

  /**
   * GSC OdsRunner cevabını türüne göre yönlendirir.
   */
  private async handleOdsRunnerResponse(payload: any, headers?: any) {
    try {
      const javaClass: string = payload['@class'] || '';

      // Korelasyon ID'den gönderen satellite ID'yi çöz
      let correlationMeta: string | null = null;
      if (headers) {
        const corrId = headers['correlation-id'] || headers['JMSCorrelationID'];
        if (corrId) {
          correlationMeta = correlationGet(corrId) ?? null;
          if (correlationMeta) {
            this.logger.log(`[GSC-CORR] Resolved meta "${correlationMeta}" from correlation ${corrId}`);
          }
        }
      }

      // ODS'e uydu ekleme cevabı (Catalog No veya TLE ile)
      if (javaClass.includes('OdsSatAdditionWithCatalogNoResponse') || javaClass.includes('OdsSatAdditionWithTleResponse')) {
        await this.handleSatAdditionResponse(payload, correlationMeta);
        return;
      }

      // ODS'ten uydu çıkarma cevabı
      if (javaClass.includes('OdsSatelliteRemovalResponse')) {
        await this.handleSatRemovalResponse(payload, correlationMeta);
        return;
      }

      // Efemeris / Konum Haritası cevabı (SatPositionsMapResponse)
      if (javaClass.includes('SatPositionsMapResponse') || payload.positionsMap) {
        await this.handlePositionsMapResponse(payload, correlationMeta);
        return;
      }

      // Geçiş Yörüngesi cevabı (PassTrajectoryResponse)
      if (javaClass.includes('PassTrajectoryResponse') || payload.trajectoryPointList || payload.trajectory) {
        await this.handlePassTrajectoryResponse(payload, correlationMeta);
        return;
      }


      // TLE cevabı (LatestTleResponse)
      if (javaClass.includes('LatestTleResponse') || payload.tleLine1 || payload.tleLine2 || payload.tle) {
        await this.handleLatestTleResponse(payload, correlationMeta);
        return;
      }

      this.logger.warn(`[GSC-ODSRUNNER-RESPONSE] Unknown response @class: "${javaClass}". Keys: ${Object.keys(payload)}`);
    } catch (error: any) {
      this.logger.error(`[GSC-ODSRUNNER-RESPONSE] Processing error: ${error.message}`);
    }
  }

  // ─────────────────────────────────────────────────────────────────
  // GSC PASSCALC RESPONSE HANDLER
  // ─────────────────────────────────────────────────────────────────

  private async handlePassCalcResponse(payload: any, headers?: any) {
    try {
      // BÜTÜN IDENTIFIER'LARI DENE (GSC bazen farklı header isimleri kullanabiliyor)
      const rawCorrId: string = headers?.['correlation-id'] || headers?.['JMSCorrelationID'] || headers?.['correlationId'] || headers?.['id'] || '';
      const correlationMeta = rawCorrId ? (correlationGet(rawCorrId) ?? null): null;
      // Check if it is a Feedback response
      const javaClass: string = payload['@class'] || '';
      const fb = payload.feedback || payload;
      const isFeedback = javaClass.includes('Feedback') || payload.feedback !== undefined || fb.feedbackContent !== undefined;

      if (isFeedback) {
        const feedbackSuccessful = fb.successful === true || fb.successful === 'true';
        const feedbackContent = fb.feedbackContent || '';
        const feedbackMessage = fb.message || '';

        this.logger.log(`[GSC-PASSCALC-FEEDBACK] Received Feedback: ${feedbackSuccessful ? 'SUCCESS' : 'FAIL'} | Content: ${feedbackContent} | Message: ${feedbackMessage} | CorrId: ${rawCorrId}`);

        if (rawCorrId.startsWith('TLE_RENEWAL:') || javaClass.includes('TleRenewal')) {
        // Broadcast to socket clients
          this.gateway.broadcast('tle_renewal_result', {
            successful: feedbackSuccessful,
            message: feedbackMessage,
            feedbackContent: feedbackContent,
            correlationId: rawCorrId
          });

          const parts = rawCorrId.split(':');
          if (parts.length >= 2) {
            const satelliteNo = Number(parts[1]);
            this.logger.log(`[TLE-RENEWAL] TLE renewal successful for Sat ${satelliteNo}. Triggering automatic requestLatestTle...`);
            await this.satelliteAppService.requestLatestTle(satelliteNo);
          }
        }
        else if(rawCorrId.startsWith('PASS_SCHED_SETTING_:')){
          this.logger.log(`[PASS_SCHED_SETTING_] Broadcast result for CorrId: ${rawCorrId}, Success: ${feedbackSuccessful}`);
          this.gateway.broadcast('pass_schedule_setting_result', { successful: feedbackSuccessful, message: feedbackMessage || feedbackContent, correlationId: rawCorrId});
        }
        else {
          this.gateway.broadcast('pass_calc_feedback', {successful: feedbackSuccessful, message: feedbackContent || feedbackMessage, correlationId: rawCorrId});
        }
        return;
      }

      // Case-insensitive pass list extraction
      const passList: any[] = payload.passList || payload.passlist || payload.futurePassList || payload.passageList || payload.satellitePassList || [];

      this.logger.log(`[GSC-PASSCALC] Received Message | ID: ${rawCorrId} | Items: ${passList.length} | Keys: ${Object.keys(payload)}`);

      // 1. GLOBAL REFRESH (PAST/FUTURE/GLOBAL)
      const isGlobal = rawCorrId.includes('GLOBAL') || rawCorrId.includes('FUTURE') || rawCorrId.includes('PAST');
      let gsIdFromCorr = 'ALL';
      if (isGlobal) {
        if (passList.length === 0) {
          this.logger.warn(`[GSC-PASSCALC] Received GLOBAL message but passList is EMPTY. ID: ${rawCorrId}`);
        } else {
          
          this.logger.log(`[GSC-PASSCALC] Raw Correlation ID:${rawCorrId}`);
          if(rawCorrId.startsWith('FILTEREDPASS:')) {
            const parts = rawCorrId.substring('FILTEREDPASS:'.length).split('_');
            if(parts.length > 0 && parts[0]){
              gsIdFromCorr = parts[0];
              this.logger.log(`[GSC-PASSCALC] GSID Correlation ID:${gsIdFromCorr}`);
            }
          }
          this.logger.log(`[GSC-PASSCALC] ${rawCorrId} ID'li tüm geçişleri yakala. Yer İstasyonu ID: ${gsIdFromCorr} Items: ${passList.length}`);
          
          if(rawCorrId.includes('PAST_REFRESH_') || rawCorrId.includes('FUTURE_REFRESH_')){
            const parts = rawCorrId.split('_');
            if (parts.length >=3){
              gsIdFromCorr = parts[2];
            }
          }
          if(gsIdFromCorr === 'ALL' && correlationMeta && correlationMeta.startsWith('GLOBAL_REFRESH|')){
            gsIdFromCorr = correlationMeta.substring('GLOBAL_REFRESH|'.length);
          }

          const normalizedPasses = passList.map(p => this.normalizePass(p, gsIdFromCorr));
          // Save in backend memory
          await this.satelliteAppService.saveInMemoryPrecalculatedPasses(normalizedPasses);

          this.gateway.broadcast('pass_prediction', { count: normalizedPasses.length, gsId: 'ALL', passes: normalizedPasses });
        }
        return;
      }

      // 2. DASHBOARD NEXT: Eğer ID kartlara aitse
      if (rawCorrId.includes('DASHBOARD_NEXT')) {
        const gsId = rawCorrId.split('_')[2] || 'ALL';
        const normalizedPasses = passList.map(p => this.normalizePass(p, gsId));
        this.logger.log(`[GSC-PASSCALC] Received Dashboard Approaching (GS: ${gsId}) | Items: ${passList.length}`);
        this.satelliteAppService.setApproachingPasses(normalizedPasses, gsId);
        this.gateway.broadcast('approaching_passes', { passes: normalizedPasses, gsId });
        return;
      }

      // 3. FALLBACK: Liste varsa tabloya
      if (passList.length > 0) {
        this.logger.log(`[GSC-PASSCALC] Catch-all routing for ID: ${rawCorrId} | Items: ${passList.length}`);
        const normalizedPasses = passList.map(p => this.normalizePass(p, gsIdFromCorr));
        
        // Save in backend memory
        await this.satelliteAppService.saveInMemoryPrecalculatedPasses(normalizedPasses);

        this.gateway.broadcast('pass_prediction', { count: normalizedPasses.length, gsId: gsIdFromCorr, passes: normalizedPasses });
      } else {
        this.logger.debug(`[GSC-PASSCALC] Discarded message (Empty or Non-relevant) | ID: ${rawCorrId}`);
      }
    } catch (error: any) {
      this.logger.error(`[GSC-PASSCALC-RESPONSE] Error: ${error.message}`);
    }
  }

  // ─────────────────────────────────────────────────────────────────
  // GSC PASS OPERATIONS RESPONSE HANDLER
  // ─────────────────────────────────────────────────────────────────

  private async handlePassOperationsResponse(payload: any, headers?: any) {
    try {
      const javaClass: string = payload['@class'] || '';

      let correlationMeta: string | null = null;
      let rawCorrId = '';
      if (headers) {
        rawCorrId = headers['correlation-id'] || headers['JMSCorrelationID'] || '';
        if (rawCorrId) {
          correlationMeta = correlationGet(rawCorrId) ?? null;
        }
      }

      // Check for PassStarting / PassStopping feedback
      const fb = payload.feedback || payload;
      const isFeedback = javaClass.includes('Feedback') || payload.feedback !== undefined || fb.feedbackContent !== undefined;

      if (isFeedback && (rawCorrId.startsWith('PASS_START_') || rawCorrId.startsWith('PASS_STOP_') || javaClass.includes('PassStartingResponse') || javaClass.includes('PassStoppingResponse'))) {
        const successful = fb.successful === true || fb.successful === 'true';
        const message = fb.message || '';
        const feedbackContent = fb.feedbackContent || '';
        this.logger.log(`[GSC-OPERATIONS] Pass operation feedback received. CorrId: ${rawCorrId}, Success: ${successful}, Message: ${message}`);
        this.gateway.broadcast('pass_operation_result', {
          successful,
          message,
          feedbackContent,
          operation: (rawCorrId.startsWith('PASS_START_') || javaClass.includes('PassStarting')) ? 'START' : 'STOP'
        });
        return;
      }

      // Current Satellite Pass Response handler
      const isDashboardCurrent = correlationMeta?.startsWith('DASHBOARD_CURRENT|');
      if (javaClass.includes('CurrentSatellitePassResponse') || payload.satellitePass || isDashboardCurrent) {
        const rawPass = payload.satellitePass || payload;

        let gsId = 'DEFAULT';
        // If we have gsId in metadata, use it
        if (isDashboardCurrent && correlationMeta) gsId = correlationMeta.split('|')[1];
        else if (correlationMeta?.startsWith('FILTEREDPASS|')) gsId = correlationMeta.split('|')[1];

        const pass = this.normalizePass(rawPass, gsId);

        let shouldClear = false;
        if (pass && pass.los) {
          const los = new Date(pass.los);
          // If the pass ended more than 1 minute ago, it's definitely stale for the "current" slot.
          if (Date.now() - los.getTime() > 60000) {
            this.logger.warn(`[GSC-FILTER] Ignoring stale current pass for ${pass.satelliteNo} (LOS was at ${los.toISOString()})`);
            shouldClear = true;
          }
        } else if (!pass || Object.keys(pass).length === 0) {
          shouldClear = true;
        }

        const passToSet = shouldClear ? null : pass;
        this.satelliteAppService.setCurrentPass(passToSet, gsId);
        this.gateway.broadcast('current_pass', { pass: passToSet, gsId });
        return;
      }

      // PassConfigsChangeResponse - Konfigürasyon Değişikliği Onayı
      if (javaClass.includes('PassConfigsChangeResponse') || javaClass.includes('Feedback')) {
        this.logger.log(`[GSC-OPERATIONS] Received Config Change Feedback: ${JSON.stringify(payload.feedback || payload)}`);
        this.gateway.broadcast('config_change_result', { success: true, payload });
        return;
      }

      this.logger.warn(`[GSC-PASSOPERATIONS-RESPONSE] Unknown: ${javaClass}. Keys: ${Object.keys(payload)}`);
    } catch (error: any) {
      this.logger.error(`[GSC-PASSOPERATIONS-RESPONSE] Processing error: ${error.message}`);
    }
  }

  // ─────────────────────────────────────────────────────────────────
  // GSC ADMINISTRATION RESPONSE HANDLER
  // ─────────────────────────────────────────────────────────────────

  private async handleAdminResponse(payload: any, headers?: any) {
    try {
      const javaClass: string = payload['@class'] || '';
      const corrId = headers?.['correlation-id'] || headers?.['JMSCorrelationID'] || headers?.['correlationId'] || '';
      this.logger.log(`[GSC-ADMIN-INCOMING] Class: ${javaClass} | CorrId: ${corrId} | Keys: ${Object.keys(payload).join(',')}`);

      // Check SystemModeResponse
      if (javaClass.includes('SystemModeResponse') || payload.systemMode !== undefined || payload.mode !== undefined) {
        let systemMode = payload.systemMode || payload.mode;
        this.logger.log(`[GSC-ADMIN] Received System Mode response: ${systemMode}`);
        
        // Normalize NONE to MANUAL
        if (systemMode === 'NONE') {
          systemMode = 'MANUAL';
        }

        this.gateway.broadcast('system_mode_update', { systemMode });
        return;
      }

      // Check FeedBack
      const fb = payload.feedback || payload;
      const isFeedback = javaClass.includes('Feedback') || payload.feedback !== undefined || fb.successful !== undefined || fb.feedbackContent !== undefined;

      if (isFeedback) {
        const feedbackSuccessful = fb.successful === true || fb.successful === 'true';
        const feedbackContent = fb.feedbackContent || '';
        const feedbackMessage = fb.message || '';

        this.logger.log(`[GSC-ADMIN] Received Feedback: ${feedbackSuccessful ? 'SUCCESS' : 'FAIL'} | Content: ${feedbackContent} | Message: ${feedbackMessage}`);

        // Try to extract systemMode from feedback fields or text content
        let systemMode = fb.systemMode || fb.mode;
        if (!systemMode) {
          const lowerText = `${feedbackContent} ${feedbackMessage}`.toLowerCase();
          if (lowerText.includes('manual') || lowerText.includes('none') || lowerText.includes('manüel')) {
            systemMode = 'MANUAL';
          } else if (lowerText.includes('automatic') || lowerText.includes('otomatik')) {
            systemMode = 'AUTOMATIC';
          }
        }

        // Normalize NONE to MANUAL
        if (systemMode === 'NONE') {
          systemMode = 'MANUAL';
        }

        // If system mode is successfully resolved, broadcast global state update
        if (systemMode === 'AUTOMATIC' || systemMode === 'MANUAL') {
          this.logger.log(`[GSC-ADMIN] Extracted and broadcasting system mode: ${systemMode}`);
          this.gateway.broadcast('system_mode_update', { systemMode });
        }

        this.gateway.broadcast('system_mode_setting_result', {
          successful: feedbackSuccessful,
          message: feedbackMessage,
          feedbackContent: feedbackContent,
          systemMode: systemMode
        });
        return;
      }

      this.logger.warn(`[GSC-ADMIN-RESPONSE] Unknown response: ${javaClass}`);
    } catch (error: any) {
      this.logger.error(`[GSC-ADMIN-RESPONSE] Processing error: ${error.message}`);
    }
  }

  // ─────────────────────────────────────────────────────────────────
  // SUB-HANDLERS
  // ─────────────────────────────────────────────────────────────────

  /**
   * ODS'e uydu ekleme (Catalog No veya TLE) cevabını işler.
   */
  private async handleSatAdditionResponse(payload: any, meta: string | null) {
    const feedback = payload.feedback;
    const success: boolean = feedback?.successful ?? false;
    const message: string = feedback?.message || (success ? 'Başarılı' : 'Bilinmeyen hata');

    this.logger.log(`[GSC-SAT-ADDITION] Result: ${success ? 'SUCCESS' : 'FAIL'} | Message: ${message} | Meta: ${meta}`);
    this.gateway.broadcast('gsc_sat_addition_result', { success, message, meta });

    if (success) {
      this.logger.log('[GSC-SAT-ADDITION] Operation successful. Refreshing Sat List from GSC DB...');
      const requestPayload = {
        requestType: 'GET_ALL_SATELLITES',
        '@class': 'tr.gov.uzay.gsc.server.datamodels.api.messaging.requests.SatListRequest'
      };
      await this.artemis.publish(GSC_DB_QUEUE, requestPayload['@class'], requestPayload, GSC_DB_RESPONSE).catch(err => {
        this.logger.error(`[GSC-SAT-ADDITION] Failed to refresh Sat List: ${err.message}`);
      });
    }
  }

  /**
   * ODS'ten uydu çıkarma cevabını işler.
   */
  private async handleSatRemovalResponse(payload: any, meta: string | null) {
    const feedback = payload.feedback;
    const success: boolean = feedback?.successful ?? false;
    const message: string = feedback?.message || (success ? 'Başarılı' : 'Bilinmeyen hata');

    this.logger.log(`[GSC-SAT-REMOVAL] Result: ${success ? 'SUCCESS' : 'FAIL'} | Message: ${message} | Meta: ${meta}`);
    this.gateway.broadcast('gsc_sat_removal_result', { success, message, meta });

    if (success) {
      this.logger.log('[GSC-SAT-REMOVAL] Operation successful. Refreshing Sat List from GSC DB...');
      const requestPayload = {
        requestType: 'GET_ALL_SATELLITES',
        '@class': 'tr.gov.uzay.gsc.server.datamodels.api.messaging.requests.SatListRequest'
      };
      await this.artemis.publish(GSC_DB_QUEUE, requestPayload['@class'], requestPayload, GSC_DB_RESPONSE).catch(err => {
        this.logger.error(`[GSC-SAT-REMOVAL] Failed to refresh Sat List: ${err.message}`);
      });
    }
  }

  /**
   * Uydu konum haritası (SatPositionsMapResponse) cevabını işler ve cache'e yazar.
   */
  private async handlePositionsMapResponse(payload: any, meta: string | null) {
    const noradId = meta?.startsWith('POSITIONS:') ? meta.split(':')[1] : meta;
    const positionsMap = payload.positionsMap;

    if (!positionsMap) {
      this.logger.warn(`[GSC-POSITIONS] positionsMap missing! Keys: ${Object.keys(payload)}`);
      return;
    }

    // İlk key formatını logla — debug için
    const sampleKey = Object.keys(positionsMap)[0];
    this.logger.debug(`[GSC-POSITIONS] Timestamp sample: "${sampleKey}"`);

    // Satellite'yi bellekte bul
    const allSats = await this.satelliteAppService.getAllSatellites();
    const satellite = allSats.find(s => s.noradId === (noradId ? noradId.toString() : undefined));

    if (!satellite) {
      this.logger.warn(`[GSC-POSITIONS] No satellite found for noradId: ${noradId}`);
      return;
    }

    const trajectoryArray: any[] = [];
    for (const [timestamp, coords] of Object.entries(positionsMap) as [string, any][]) {
      try {
        const time = this.parseJavaTimestamp(timestamp).toISOString();

        const lat = coords[0];
        const lon = coords[1];
        const altKm = coords[2] / 1000;

        const cesiumRadius = (6371 + altKm) * 1000;
        const latRad = lat * (Math.PI / 180);
        const lonRad = lon * (Math.PI / 180);
        const x = cesiumRadius * Math.cos(latRad) * Math.cos(lonRad);
        const y = cesiumRadius * Math.cos(latRad) * Math.sin(lonRad);
        const z = cesiumRadius * Math.sin(latRad);

        trajectoryArray.push({ id: satellite.id, time, lat, lon, alt: altKm, x, y, z, referenceBody: 'earth' });
      } catch (e: any) {
        this.logger.warn(`[GSC-POSITIONS] Skipping entry: ${e.message}`);
      }
    }

    this.logger.log(`[GSC-POSITIONS] Processed ${trajectoryArray.length} points for ${satellite.id}`);

    // Cache'e yaz (mevcut veriyle birleştir)
    const cacheKey = `ODS_TRAJECTORY:${satellite.id}`;
    const existing = await this.cacheGet<any[]>(cacheKey) || [];
    const mergeMap = new Map<string, any>();
    existing.forEach(p => mergeMap.set(p.time, p));
    trajectoryArray.forEach(p => mergeMap.set(p.time, p));

    let merged = Array.from(mergeMap.values()).sort(
      (a, b) => new Date(a.time).getTime() - new Date(b.time).getTime()
    );
    if (merged.length > 10000) merged = merged.slice(-10000);

    await this.cacheSet(cacheKey, merged, 24 * 60 * 60 * 1000);

    // Skipping DB update per user request
    this.logger.debug(`[GSC-POSITIONS] Updated cache for ${satellite.id}. No DB save.`);

    this.gateway.broadcast('satellite_updated', {
      id: satellite.id,
      type: 'gsc_positions_update',
      points: trajectoryArray.slice(-200),
      latest: trajectoryArray[0] // Pass the latest position for the Satellite List update
    });
  }

  /**
   * Geçiş yörüngesi (PassTrajectoryResponse) cevabını işler.
   * Payload içinde `trajectoryPointList` (Trajectory nesnesi) beklenir.
   */
  private async handlePassTrajectoryResponse(payload: any, meta: string | null) {
    let noradId: string | null = null;
    let gsName: string | null = null;
    let satelliteNo: string | null = null;
    let timeType: string | null = null;

    if (meta?.startsWith('PASSTRAJECTORY:')) {
      const parts = meta.split(':');
      if (parts.length >= 3) {
        noradId = parts[1] || null;
        gsName = parts[2] || null;
      } else if (parts.length === 2) {
        // format: PASSTRAJECTORY:<satelliteNo>
        satelliteNo = parts[1].split('_')[0] || null;
      }
      
      // Check if it's our new format PASSTRAJECTORY:${satelliteNo}:${timeType}
      if (parts.length >= 2 && !gsName) {
        satelliteNo = parts[1] || null;
        if (parts[2]) {
          timeType = parts[2].split('_')[0] || null;
        }
      }
    }

    const trajectory = payload.trajectory || payload;
    const points: any[] = trajectory?.trajectoryPointList || [];
    const startingTime = trajectory?.startingTime || '';

    this.logger.log(`[GSC-PASS-TRAJECTORY] Received ${points.length} trajectory points. SatelliteNo/Norad: ${satelliteNo || noradId}, GS: ${gsName || 'N/A'}`);

    this.gateway.broadcast('satellite_updated', {
      type: 'gsc_pass_trajectory',
      noradId: noradId || satelliteNo,
      gsName,
      pointCount: points.length,
      points,
      startingTime
    });

    // Dedicated broadcast for our new Pass Control Extension
    this.gateway.broadcast('pass_trajectory_update', {
      satelliteNo: satelliteNo || noradId,
      timeType,
      points,
      startingTime
    });
  }

  /**
   * Robust date parser for GSC timestamps
   */
  private parseJavaTimestamp(val: any): Date {
    if (!val) return new Date();
    if (val instanceof Date) return val;
    if (typeof val === 'number') return new Date(val);

    const valStr = String(val);

    // Clean high-precision nanos if present (e.g. 2026-04-20T05:44:27.814319324Z -> 2026-04-20T05:44:27.814Z)
    const cleaned = valStr.replace(/(\.[0-9]{3})[0-9]+/, '$1');

    const date = new Date(cleaned);
    if (!isNaN(date.getTime())) return date;

    // Handle "YYYY-MM-DD_HH-mm-ss" format often found in GSC logs
    const logFormat = valStr.replace(/_/g, 'T').replace(/-/g, (m, offset) => (offset > 10 ? ':' : '-'));
    const logDate = new Date(logFormat);
    if (!isNaN(logDate.getTime())) return logDate;

    return new Date(valStr);
  }

  /**
   * Normalizes a GSC pass object to a format suitable for the frontend
   */
  private normalizePass(pass: any, gsIdOverride?: string): any {
    if (!pass || typeof pass !== 'object') return null;

    const aos = pass.aos || pass.realStartTime || pass.schedStartTime || pass.startTime || pass.start_time;
    const los = pass.los || pass.realEndTime || pass.schedEndTime || pass.endTime || pass.end_time;
    const gsId = (gsIdOverride && gsIdOverride !== 'ALL') ? gsIdOverride : (pass.gsId || pass.groundStationId || 'DEFAULT');
    const normalizedAos = this.parseJavaTimestamp(aos);
    const normalizedLos = this.parseJavaTimestamp(los);
    let duration = pass.duration;

    if (!duration || duration <= 0) {
      duration = Math.max(0, Math.round((normalizedLos.getTime() - normalizedAos.getTime()) / 1000));
    }

    return {
      ...pass,
      passId: pass.passId || `P-${Date.now()}-${Math.random().toString(36).substr(2, 5)}`,
      aos: normalizedAos.toISOString(),
      los: normalizedLos.toISOString(),
      duration: duration,
      maxElevation: pass.maxElevation || pass.maxElevationDegrees || pass.max_elevation || 0,
      gsId: gsId,
      groundStationId: gsId,
      satelliteNo: pass.satelliteNo || pass.satId || 'UNKNOWN'
    };
  }

  /**
   * En son TLE bilgisini (LatestTleResponse) işler ve frontend'e yayınlar.
   */
  private async handleLatestTleResponse(payload: any, meta: string | null) {
    const satNo = meta?.startsWith('LATEST_TLE:') ? meta.split(':')[1] : (payload.satelliteNo || payload.noradId || payload.tle?.satelliteNo || payload.tle?.noradId);
    
    this.logger.log(`[GSC-ODSRUNNER] Received Latest TLE for Sat: ${satNo}`);
    
    let t1 = payload.tleLine1 || payload.tle?.tleLine1;
    let t2 = payload.tleLine2 || payload.tle?.tleLine2;

    if ( Array.isArray(payload.tle) && payload.tle.length >= 2) {
      t1 = payload.tle[0];
      t2 = payload.tle[1];
    }
    // Frontend'e TLE ve tazelik bilgisini gönder
    this.gateway.broadcast('latest_tle_update', {
      satelliteNo: satNo,
      tleLine1: t1,
      tleLine2: t2,
      timestamp: new Date().toISOString()
    });
  }
}
