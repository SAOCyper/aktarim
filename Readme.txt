import * as React from 'react';
import { useState, useMemo, useEffect, useRef, useCallback } from 'react';
import { useSocData, useAppSettings, useSimulationClock } from '@uzay/gsc-common';

interface Pass {
    aos: string;
    los: string;
    duration: number;
    maxElevation: number;
    direction: string;
}

interface LinkedPass extends Pass {
    passId: string;
    satId: string;
    satName?: string;
    gsId?: string;
    passConfig?: string;
    endingConfig?: string;
    satelliteNo?: any;
    startAzimuthDegrees?: number;
    averageAltitude?: number;
    schedule?: string;
}

// Glow indicators matching workspace styling rules
const accentBlue = '#00c6ff';
const accentRed = '#ff4b72';
const accentGreen = '#05ffc0';
const accentAmber = '#fbbf24';

function progressColor(pct: number, maxEl: number): string {
    if (maxEl > 45) return `hsl(${140 - pct * 0.4}, 85%, 50%)`; // vibrant green → teal
    if (maxEl > 20) return `hsl(${50 - pct * 0.3}, 95%, 50%)`;  // vibrant yellow → amber
    return `hsl(${355}, 90%, ${60 - pct * 0.15}%)`;              // premium red dimming
}

function renderScheduleBadge(schedule: string | undefined, isDark: boolean): React.ReactNode {
    const val = schedule || '';
    let label = 'PLANLANMAMIŞ';
    let bg = isDark ? 'rgba(255, 255, 255, 0.03)' : 'rgba(0, 0, 0, 0.03)';
    let color = isDark ? '#94a3b8' : '#64748b';
    let border = isDark ? '1px solid rgba(255, 255, 255, 0.05)' : '1px solid rgba(0, 0, 0, 0.05)';

    switch (val) {
        case 'SCHEDULED':
            label = 'PLANLANDI';
            bg = 'rgba(16, 185, 129, 0.12)';
            color = '#05ffc0';
            border = '1px solid rgba(16, 185, 129, 0.2)';
            break;
        case 'CANCELLED':
            label = 'İPTAL EDİLDİ';
            bg = 'rgba(239, 68, 68, 0.12)';
            color = '#fa0808';
            border = '1px solid rgba(239, 68, 68, 0.2)';
            break;
        case 'AUTO_SCHEDULED':
            label = 'OTO-PLANLANDI';
            bg = 'rgba(59, 130, 246, 0.12)';
            color = '#05ffc0';
            border = '1px solid rgba(59, 130, 246, 0.2)';
            break;
        case 'AUTO_UNSCHEDULED':
            label = 'OTO-PLANDIŞI';
            bg = 'rgba(245, 158, 11, 0.12)';
            color = '#e23b3b';
            border = '1px solid rgba(245, 158, 11, 0.2)';
            break;
        case 'PARTIALLY_SCHEDULED':
            label = 'KISMİ PLANLANDI';
            bg = 'rgba(217, 70, 239, 0.12)';
            color = '#e879f9';
            border = '1px solid rgba(217, 70, 239, 0.2)';
            break;
    }

    return (
        <span style={{
            fontSize: '0.68rem',
            fontWeight: 800,
            padding: '3px 8px',
            borderRadius: '6px',
            backgroundColor: bg,
            color: color,
            border: border,
            textTransform: 'uppercase',
            letterSpacing: '0.04em',
            display: 'inline-block',
            textAlign: 'center',
            minWidth: '95px'
        }}>
            {label}
        </span>
    );
}

// Custom hook to receive simulation time from standard clock channel
function useDecoupledSimulationClock() {
    const [clockState, setClockState] = useState({
        simulationTime: new Date().toISOString(),
        simulationMultiplier: 1,
        currentTime: new Date().toISOString()
    });

    useEffect(() => {
        const chTime = new BroadcastChannel('soc-state-time');
        chTime.onmessage = (ev) => {
            setClockState(prev => ({
                simulationTime: ev.data.simulationTime || prev.simulationTime,
                simulationMultiplier: ev.data.simulationMultiplier !== undefined ? ev.data.simulationMultiplier : prev.simulationMultiplier,
                currentTime: ev.data.currentTime || prev.currentTime,
            }));
        };
        return () => chTime.close();
    }, []);

    const simNow = useSimulationClock(clockState.simulationTime, clockState.simulationMultiplier, clockState.currentTime);
    return simNow;
}

export function PassPredictionSummary(): any {
    const socState = useSocData();
    const { t, theme } = useAppSettings();
    const [hoveredCardIndex, setHoveredCardIndex] = useState<number | null>(null);

    const fmtSecs = (secs: number): string => {
        if (secs < 0) secs = 0;
        const h = Math.floor(secs / 3600);
        const m = Math.floor((secs % 3600) / 60);
        const s = Math.floor(secs % 60);
        return h > 0 ? `${h}${t('hoursShort')} ${m}${t('minutesShort')} ${s}${t('secondsShort')}` : `${m}${t('minutesShort')} ${s}${t('secondsShort')}`;
    };

    const isDark = theme === 'dark';
    
    // Core design system tokens
    const fontStyle = '"Outfit", "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif';
    const panelBg = isDark ? 'radial-gradient(circle at 50% 0%, #101726 0%, #0a0f1d 100%)' : 'radial-gradient(circle at 50% 0%, #f8fafc 0%, #e2e8f0 100%)';
    const panelText = isDark ? '#f8fafc' : '#1e293b';
    const textMuted = isDark ? '#94a3b8' : '#64748b';
    const borderColor = isDark ? 'rgba(255, 255, 255, 0.08)' : 'rgba(0, 0, 0, 0.08)';
    const cardBg = isDark ? 'rgba(255, 255, 255, 0.02)' : 'rgba(0, 0, 0, 0.015)';

    const simNow = useDecoupledSimulationClock();

    const findSatellite = useCallback((idOrNo: any) => {
        if (!idOrNo) return null;
        const targetStr = String(idOrNo);
        return socState.satellites?.find((s: any) =>
            s.id === targetStr ||
            s.noradId === targetStr ||
            s.id === `SAT-${targetStr}` ||
            String(s.noradId) === targetStr
        );
    }, [socState.satellites]);

    const getPassStatus = (p: any, now: Date) => {
        if (!p) return null;
        const aosStr = p.realStartTime || p.passageStart || p.aos || p.startAos || p.realAos || p.accessTime;
        const losStr = p.realEndTime || p.passageStop || p.los || p.endLos || p.realLos || p.losTime;
        if (!aosStr || !losStr) return null;
        const aos = new Date(aosStr);
        const los = new Date(losStr);
        const nowMs = now.getTime();
        if (isNaN(aos.getTime()) || isNaN(los.getTime())) return null;
        const isStarted = nowMs >= aos.getTime();
        const isEnded = nowMs >= los.getTime();
        let label = '';
        let diffMs = 0;
        let color = '';
        if (isEnded) { label = 'COMPLETED'; diffMs = 0; color = '#94a3b8'; }
        else if (isStarted) { label = 'LOS IN'; diffMs = los.getTime() - nowMs; color = accentGreen; }
        else { label = 'AOS IN'; diffMs = aos.getTime() - nowMs; color = accentAmber; }
        return { label, diffMs, color, isStarted, isEnded, aos, los };
    };

    const approachingPasses = socState.approachingPasses || [];
    const currentPass = socState.currentPass;

    const countdownInfo = useMemo(() => {
        const status = getPassStatus(currentPass, simNow);
        if (status) return {
            pass: currentPass,
            label: status.label,
            diffSecs: status.diffMs / 1000,
            color: status.color,
            isActive: status.isStarted && !status.isEnded
        };
        return null;
    }, [currentPass, simNow]);

    return (
        <div style={{ 
            padding: '16px 20px', 
            background: panelBg, 
            color: panelText, 
            height: '100%', 
            overflowY: 'auto', 
            boxSizing: 'border-box',
            fontFamily: fontStyle,
            display: 'flex',
            flexDirection: 'column',
            gap: '14px',
            borderBottom: `1.5px solid ${borderColor}`
        }}>
            {/* Horizontal Grid of Upcoming Passes */}
            <div style={{ display: 'grid', gridTemplateColumns: 'repeat(4, 1fr)', gap: '10px' }}>
                {approachingPasses.length > 0 ? approachingPasses.slice(0, 4).map((p: any, i: number) => {
                    const status = getPassStatus(p, simNow);
                    if (!status) return null;
                    const isHovered = hoveredCardIndex === i;

                    return (
                        <div 
                            key={i} 
                            onMouseEnter={() => setHoveredCardIndex(i)}
                            onMouseLeave={() => setHoveredCardIndex(null)}
                            style={{
                                background: i === 0 
                                    ? (isDark ? 'linear-gradient(135deg, rgba(0, 198, 255, 0.08), rgba(0, 0, 0, 0.2))' : 'linear-gradient(135deg, rgba(0, 198, 255, 0.05), rgba(255, 255, 255, 0.8))') 
                                    : cardBg,
                                border: `1.5px solid ${i === 0 ? accentBlue : (isHovered ? (isDark ? 'rgba(255, 255, 255, 0.15)' : 'rgba(0, 0, 0, 0.15)') : borderColor)}`,
                                borderRadius: '12px', 
                                padding: '10px 12px',
                                display: 'flex', 
                                flexDirection: 'column', 
                                gap: '3px',
                                transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)',
                                transform: isHovered ? 'translateY(-2px)' : 'none',
                                boxShadow: i === 0 
                                    ? `0 4px 12px rgba(0, 198, 255, ${isHovered ? 0.2 : 0.1})` 
                                    : (isHovered ? '0 4px 10px rgba(0, 0, 0, 0.1)' : 'none'),
                                cursor: 'default'
                            }}
                        >
                            <div style={{ 
                                fontSize: '0.62rem', 
                                color: status.isStarted && !status.isEnded ? status.color : textMuted, 
                                textTransform: 'uppercase', 
                                fontWeight: 800,
                                letterSpacing: '0.08em',
                                display: 'flex',
                                alignItems: 'center',
                                gap: '4px'
                            }}>
                                <span style={{ width: '5px', height: '5px', borderRadius: '50%', backgroundColor: status.color, display: 'inline-block' }} />
                                {status.label}
                            </div>
                            <div style={{ 
                                fontSize: '0.84rem', 
                                fontWeight: 800, 
                                color: i === 0 ? accentBlue : panelText, 
                                whiteSpace: 'nowrap', 
                                overflow: 'hidden', 
                                textOverflow: 'ellipsis' 
                            }}>
                                {findSatellite(p.satelliteNo || p.satId || p.satNo)?.name || p.satelliteNo || p.satId || p.satNo}
                            </div>
                            <div style={{ 
                                fontSize: '0.94rem', 
                                fontWeight: 900, 
                                fontFamily: 'monospace', 
                                color: status.color,
                                letterSpacing: '-0.02em',
                                marginTop: '2px'
                            }}>
                                {fmtSecs(status.diffMs / 1000)}
                            </div>
                        </div>
                    );
                }) : (
                    <div style={{ 
                        gridColumn: 'span 4', 
                        textAlign: 'center', 
                        padding: '16px', 
                        fontSize: '0.8rem', 
                        color: textMuted, 
                        background: cardBg, 
                        borderRadius: '12px',
                        border: `1.5px dashed ${borderColor}`
                    }}>
                        <span className="fa fa-clock" style={{ marginRight: '6px', color: accentBlue }} />
                        GSC'den geçiş bekleniyor...
                    </div>
                )}
            </div>

            {/* Glowing Active Target Card */}
            {currentPass && (
                <div style={{
                    padding: '14px 20px',
                    background: isDark 
                        ? 'linear-gradient(135deg, rgba(16, 23, 38, 0.8), rgba(0, 0, 0, 0.4))' 
                        : 'linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(241, 245, 249, 0.95))',
                    border: `1.5px solid ${accentBlue}`,
                    borderRadius: '14px',
                    boxShadow: isDark ? '0 8px 24px rgba(0, 198, 255, 0.12)' : '0 8px 20px rgba(0, 0, 0, 0.06)',
                    display: 'flex',
                    justifyContent: 'space-between',
                    alignItems: 'center',
                    position: 'relative',
                    overflow: 'hidden'
                }}>
                    {/* Background accent glow */}
                    <div style={{
                        position: 'absolute',
                        top: '-30px',
                        right: '-30px',
                        width: '100px',
                        height: '100px',
                        background: `radial-gradient(circle, rgba(0, 198, 255, 0.2) 0%, transparent 70%)`,
                        pointerEvents: 'none'
                    }} />

                    <div style={{ display: 'flex', alignItems: 'center', gap: '14px' }}>
                        <div style={{
                            width: '42px',
                            height: '42px',
                            borderRadius: '10px',
                            backgroundColor: isDark ? 'rgba(0, 198, 255, 0.1)' : 'rgba(0, 198, 255, 0.06)',
                            display: 'flex',
                            alignItems: 'center',
                            justifyContent: 'center',
                            border: `1px solid rgba(0, 198, 255, 0.2)`,
                        }}>
                            <span className="fa fa-satellite-dish" style={{ color: accentBlue, fontSize: '1.2rem', animation: 'spin-pulse 3s linear infinite' }} />
                        </div>
                        <div>
                            <div style={{ 
                                fontSize: '0.65rem', 
                                color: accentBlue, 
                                fontWeight: 900, 
                                textTransform: 'uppercase',
                                letterSpacing: '0.1em'
                            }}>
                                {t('activePassSum')}
                            </div>
                            <div style={{ fontSize: '1.15rem', fontWeight: 900, color: panelText, marginTop: '2px' }}>
                                {findSatellite(currentPass.satelliteNo || currentPass.satId || currentPass.satNo)?.name || currentPass.satelliteNo || currentPass.satId || currentPass.satNo}
                            </div>
                        </div>
                    </div>

                    <div>
                        {countdownInfo && (
                            <div style={{ display: 'flex', alignItems: 'center', gap: '15px' }}>
                                <div style={{ textAlign: 'right' }}>
                                    <div style={{ 
                                        fontSize: '0.62rem', 
                                        color: countdownInfo.color === '#94a3b8' ? countdownInfo.color : textMuted, 
                                        fontWeight: 800,
                                        letterSpacing: '0.08em',
                                        textTransform: 'uppercase'
                                    }}>
                                        {countdownInfo.label}
                                    </div>
                                    <div style={{ 
                                        fontSize: '1.8rem', 
                                        fontWeight: 900, 
                                        fontFamily: 'monospace', 
                                        color: countdownInfo.color,
                                        textShadow: countdownInfo.color !== '#94a3b8' ? `0 0 10px ${countdownInfo.color}44` : 'none',
                                        letterSpacing: '-0.03em',
                                        marginTop: '1px'
                                    }}>
                                        {fmtSecs(countdownInfo.diffSecs)}
                                    </div>
                                </div>
                            </div>
                        )}
                    </div>
                </div>
            )}
            <style>{`
                @keyframes spin-pulse {
                    0% { transform: scale(1); }
                    50% { transform: scale(1.08); }
                    100% { transform: scale(1); }
                }
            `}</style>
        </div>
    );
}


interface PastPassRowProps {
    pass: LinkedPass;
    isDark: boolean;
    borderColor: string;
    tableBorder: string;
    textMuted: string;
    panelText: string;
    selectedSatelliteId: string | null;
    findSatellite: (id: any) => any;
    socState: any;
    selectedPassId?: string | null;
    onRowClick?: (passId: string) => void;
}

const PastPassRow = React.memo(({
    pass,
    isDark,
    borderColor,
    tableBorder,
    textMuted,
    panelText,
    selectedSatelliteId,
    findSatellite,
    socState,
    selectedPassId,
    onRowClick
}: PastPassRowProps): any => {
    const [isHovered, setIsHovered] = useState(false);
    
    const handlePassClick = (p: LinkedPass) => {
        const cmdChannel = new BroadcastChannel('soc-cmd');
        cmdChannel.postMessage({ type: 'jumpToTime', value: p.aos });
        const srSyncChannel = new BroadcastChannel('soc-sr-sync');
        srSyncChannel.postMessage({ startTime: p.aos.slice(0, 16), endTime: p.los.slice(0, 16) });
        cmdChannel.close();
        srSyncChannel.close();
    };

    const isSelected = pass.passId === selectedPassId;
    const isSatSelected = pass.satId === selectedSatelliteId;
    const rowBg = isSelected
        ? (isDark ? 'rgba(0, 198, 255, 0.08)' : 'rgba(0, 198, 255, 0.06)')
        : (isHovered 
            ? (isDark ? 'rgba(255, 255, 255, 0.015)' : 'rgba(0, 0, 0, 0.015)') 
            : (isDark ? 'rgba(255,255,255,0.005)' : 'rgba(0,0,0,0.005)'));

    const aosDate = new Date(pass.aos);
    const losDate = new Date(pass.los);

    return (
        <tr 
            onClick={() => {
                handlePassClick(pass);
                onRowClick?.(pass.passId);
            }}
            onMouseEnter={() => setIsHovered(true)}
            onMouseLeave={() => setIsHovered(false)}
            style={{ 
                borderBottom: `1px solid ${tableBorder}`, 
                cursor: 'pointer', 
                transition: 'background-color 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)', 
                backgroundColor: rowBg, 
                color: isSelected ? '#00c6ff' : (isSatSelected ? '#a78bfa' : panelText), 
                opacity: 0.55 
            }}
        >
            <td style={{ padding: '12px 14px', fontWeight: 800, display: 'flex', alignItems: 'center', gap: '8px' }}>
                {pass.satName || pass.satId}
            </td>
            <td style={{ padding: '12px 14px', fontFamily: 'monospace', fontSize: '0.78rem', fontWeight: 700 }}>
                <span style={{ textDecoration: 'line-through' }}>{aosDate.toLocaleString()}</span>
            </td>
            <td style={{ padding: '12px 14px', fontFamily: 'monospace', fontSize: '0.78rem', fontWeight: 700, color: textMuted }}>
                <span style={{ textDecoration: 'line-through' }}>{losDate.toLocaleString()}</span>
            </td>
            <td style={{ padding: '12px 14px' }}>
                <span style={{ fontFamily: 'monospace', fontWeight: 700, fontSize: '0.75rem', background: 'rgba(255,255,255,0.04)', padding: '2px 6px', borderRadius: '4px' }}>
                    {pass.passConfig || (findSatellite(pass.satelliteNo || pass.satId)?.defaultPassConfig) || '(Varsayılan)'}
                </span>
            </td>
            <td style={{ padding: '12px 14px' }}>
                <span style={{ fontFamily: 'monospace', fontWeight: 700, fontSize: '0.75rem', background: 'rgba(255,255,255,0.04)', padding: '2px 6px', borderRadius: '4px' }}>
                    {pass.endingConfig || (findSatellite(pass.satelliteNo || pass.satId)?.defaultEndingConfig) || '(Varsayılan)'}
                </span>
            </td>
            <td style={{ padding: '12px 14px', textAlign: 'center', fontWeight: 800 }}>
                {(pass.duration / 60).toFixed(1)}m
            </td>
            <td style={{ 
                padding: '12px 14px', 
                textAlign: 'center', 
                color: pass.maxElevation > 45 ? '#05ffc0' : (pass.maxElevation > 20 ? '#fbbf24' : '#ff4b72'), 
                fontWeight: 800 
            }}>
                {pass.maxElevation.toFixed(1)}°
            </td>
            <td style={{ padding: '12px 14px', textAlign: 'center', color: '#a78bfa', fontWeight: 700, fontFamily: 'monospace' }}>
                {pass.startAzimuthDegrees != null ? `${pass.startAzimuthDegrees.toFixed(1)}°` : <span style={{ color: textMuted }}>—</span>}
            </td>
            <td style={{ padding: '12px 14px', textAlign: 'center', color: '#60a5fa', fontWeight: 700, fontFamily: 'monospace' }}>
                {pass.averageAltitude != null ? `${(pass.averageAltitude / 1000).toFixed(0)} km` : <span style={{ color: textMuted }}>—</span>}
            </td>
            <td style={{ padding: '12px 14px', textAlign: 'center' }}>
                {renderScheduleBadge(pass.schedule, isDark)}
            </td>
            <td style={{ padding: '12px 14px', textAlign: 'center' }}>
                <span style={{ 
                    fontSize: '0.68rem', 
                    color: textMuted, 
                    fontWeight: 800,
                    background: 'rgba(0,0,0,0.05)',
                    padding: '3px 8px',
                    borderRadius: '4px'
                }}>
                    GEÇTİ
                </span>
            </td>
        </tr>
    );
});
PastPassRow.displayName = 'PastPassRow';

interface ActivePassRowProps {
    pass: LinkedPass;
    isDark: boolean;
    borderColor: string;
    tableBorder: string;
    textMuted: string;
    panelText: string;
    selectedSatelliteId: string | null;
    findSatellite: (id: any) => any;
    socState: any;
    t: any;
    selectedPassId?: string | null;
    onRowClick?: (passId: string) => void;
}

function ActivePassRow({
    pass,
    isDark,
    borderColor,
    tableBorder,
    textMuted,
    panelText,
    selectedSatelliteId,
    findSatellite,
    socState,
    t,
    selectedPassId,
    onRowClick
}: ActivePassRowProps): any {
    const [isHovered, setIsHovered] = useState(false);
    const simNow = useDecoupledSimulationClock();

    const handlePassClick = (p: LinkedPass) => {
        const cmdChannel = new BroadcastChannel('soc-cmd');
        cmdChannel.postMessage({ type: 'jumpToTime', value: p.aos });
        const srSyncChannel = new BroadcastChannel('soc-sr-sync');
        srSyncChannel.postMessage({ startTime: p.aos.slice(0, 16), endTime: p.los.slice(0, 16) });
        cmdChannel.close();
        srSyncChannel.close();
    };

    const getPassStatus = (p: any, now: Date) => {
        if (!p) return null;
        const aosStr = p.realStartTime || p.passageStart || p.aos || p.startAos || p.realAos || p.accessTime;
        const losStr = p.realEndTime || p.passageStop || p.los || p.endLos || p.realLos || p.losTime;
        if (!aosStr || !losStr) return null;
        const aos = new Date(aosStr);
        const los = new Date(losStr);
        const nowMs = now.getTime();
        if (isNaN(aos.getTime()) || isNaN(los.getTime())) return null;
        const isStarted = nowMs >= aos.getTime();
        const isEnded = nowMs >= los.getTime();
        let label = '';
        let diffMs = 0;
        let color = '';
        if (isEnded) { label = 'COMPLETED'; diffMs = 0; color = '#94a3b8'; }
        else if (isStarted) { label = 'LOS IN'; diffMs = los.getTime() - nowMs; color = '#05ffc0'; }
        else { label = 'AOS IN'; diffMs = aos.getTime() - nowMs; color = '#fbbf24'; }
        return { label, diffMs, color, isStarted, isEnded, aos, los };
    };

    const fmtSecs = (secs: number): string => {
        if (secs < 0) secs = 0;
        const h = Math.floor(secs / 3600);
        const m = Math.floor((secs % 3600) / 60);
        const s = Math.floor(secs % 60);
        return h > 0 ? `${h}${t('hoursShort') || 'sa'} ${m}${t('minutesShort') || 'dk'} ${s}${t('secondsShort') || 'sn'}` : `${m}${t('minutesShort') || 'dk'} ${s}${t('secondsShort') || 'sn'}`;
    };

    const fontStyle = '"Outfit", "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif';
    const status = getPassStatus(pass, simNow);
    if (!status) return null;

    const isActive = socState.currentPass && pass.passId === socState.currentPass.passId;
    const isPast = status.isEnded;
    const isSelected = pass.passId === selectedPassId;
    const isSatSelected = pass.satId === selectedSatelliteId;

    const pct = status.isStarted && !status.isEnded ? ((simNow.getTime() - status.aos.getTime()) / (status.los.getTime() - status.aos.getTime())) * 100 : 0;

    const rowBg = isSelected
        ? (isDark ? 'rgba(0, 198, 255, 0.08)' : 'rgba(0, 198, 255, 0.06)')
        : (isActive 
            ? (isDark ? 'rgba(5, 255, 192, 0.05)' : 'rgba(5, 255, 192, 0.04)') 
            : (isHovered 
                ? (isDark ? 'rgba(255, 255, 255, 0.015)' : 'rgba(0, 0, 0, 0.015)') 
                : (isPast ? (isDark ? 'rgba(255,255,255,0.005)' : 'rgba(0,0,0,0.005)') : 'transparent')));

    return (
        <React.Fragment>
            <tr 
                onClick={() => {
                    handlePassClick(pass);
                    onRowClick?.(pass.passId);
                }}
                onMouseEnter={() => setIsHovered(true)}
                onMouseLeave={() => setIsHovered(false)}
                style={{ 
                    borderBottom: isActive ? 'none' : `1px solid ${tableBorder}`, 
                    cursor: 'pointer', 
                    transition: 'background-color 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)', 
                    backgroundColor: rowBg, 
                    color: isPast ? textMuted : (isSelected ? '#00c6ff' : (isSatSelected ? '#a78bfa' : panelText)), 
                    opacity: isPast ? 0.55 : 1 
                }}
            >
                <td style={{ padding: '12px 14px', fontWeight: 800, display: 'flex', alignItems: 'center', gap: '8px' }}>
                    {isActive && (
                        <span style={{ 
                            width: '8px', 
                            height: '8px', 
                            borderRadius: '50%', 
                            backgroundColor: '#05ffc0', 
                            display: 'inline-block',
                            boxShadow: '0 0 8px #05ffc0', 
                            animation: 'pulse-glow 1.5s infinite' 
                        }} />
                    )}
                    {pass.satName || pass.satId}
                </td>
                <td style={{ padding: '12px 14px', fontFamily: 'monospace', fontSize: '0.78rem', fontWeight: 700 }}>
                    {isPast ? <span style={{ textDecoration: 'line-through' }}>{status.aos.toLocaleString()}</span> : status.aos.toLocaleString()}
                </td>
                <td style={{ padding: '12px 14px', fontFamily: 'monospace', fontSize: '0.78rem', fontWeight: 700, color: isPast ? textMuted : '#fbbf24' }}>
                    {isPast ? <span style={{ textDecoration: 'line-through' }}>{status.los.toLocaleString()}</span> : status.los.toLocaleString()}
                </td>
                <td style={{ padding: '12px 14px' }}>
                    {isPast ? (
                        <span style={{ fontFamily: 'monospace', fontWeight: 700, fontSize: '0.75rem', background: 'rgba(255,255,255,0.04)', padding: '2px 6px', borderRadius: '4px' }}>
                            {pass.passConfig || (findSatellite(pass.satelliteNo || pass.satId)?.defaultPassConfig) || '(Varsayılan)'}
                        </span>
                    ) : (
                        <select 
                            value={pass.passConfig || ''} 
                            onChange={(e) => { e.stopPropagation(); socState.changePassConfigs?.(pass.passId, e.target.value, pass.endingConfig || ''); }} 
                            onClick={(e) => e.stopPropagation()} 
                            style={{ 
                                background: isDark ? 'rgba(0,0,0,0.3)' : 'rgba(255,255,255,0.8)', 
                                color: panelText, 
                                border: `1px solid ${borderColor}`, 
                                borderRadius: '6px', 
                                fontSize: '0.74rem', 
                                fontWeight: 700,
                                padding: '4px 8px',
                                width: '130px', 
                                outline: 'none',
                                fontFamily: fontStyle
                            }}
                        >
                            <option value="">
                                {(() => {
                                    const sat = findSatellite(pass.satelliteNo || pass.satId);
                                    return sat?.defaultPassConfig ? `${sat.defaultPassConfig} (Varsayılan)` : 'Varsayılan Yok';
                                })()}
                            </option>
                            {(socState.satConfigNames?.[pass.satelliteNo] || 
                              socState.satConfigNames?.[pass.satId] || 
                              socState.satConfigNames?.[String(pass.satelliteNo)] || 
                              []).map((c: string) => (
                                <option key={c} value={c.trim()}>{c.trim()}</option>
                            ))}
                        </select>
                    )}
                </td>
                <td style={{ padding: '12px 14px' }}>
                    {isPast ? (
                        <span style={{ fontFamily: 'monospace', fontWeight: 700, fontSize: '0.75rem', background: 'rgba(255,255,255,0.04)', padding: '2px 6px', borderRadius: '4px' }}>
                            {pass.endingConfig || (findSatellite(pass.satelliteNo || pass.satId)?.defaultEndingConfig) || '(Varsayılan)'}
                        </span>
                    ) : (
                        <select 
                            value={pass.endingConfig || ''} 
                            onChange={(e) => { e.stopPropagation(); socState.changePassConfigs?.(pass.passId, pass.passConfig || '', e.target.value); }} 
                            onClick={(e) => e.stopPropagation()} 
                            style={{ 
                                background: isDark ? 'rgba(0,0,0,0.3)' : 'rgba(255,255,255,0.8)', 
                                color: panelText, 
                                border: `1px solid ${borderColor}`, 
                                borderRadius: '6px', 
                                fontSize: '0.74rem', 
                                fontWeight: 700,
                                padding: '4px 8px',
                                width: '130px', 
                                outline: 'none',
                                fontFamily: fontStyle
                            }}
                        >
                            <option value="">
                                {(() => {
                                    const sat = findSatellite(pass.satelliteNo || pass.satId);
                                    return sat?.defaultEndingConfig ? `${sat.defaultEndingConfig} (Varsayılan)` : 'Varsayılan Yok';
                                })()}
                            </option>
                            {(socState.satConfigNames?.[pass.satelliteNo] || 
                              socState.satConfigNames?.[pass.satId] || 
                              socState.satConfigNames?.[String(pass.satelliteNo)] || 
                              []).map((c: string) => (
                                <option key={c} value={c.trim()}>{c.trim()}</option>
                            ))}
                        </select>
                    )}
                </td>
                <td style={{ padding: '12px 14px', textAlign: 'center', fontWeight: 800 }}>
                    {(pass.duration / 60).toFixed(1)}m
                </td>
                <td style={{ 
                    padding: '12px 14px', 
                    textAlign: 'center', 
                    color: pass.maxElevation > 45 ? '#05ffc0' : (pass.maxElevation > 20 ? '#fbbf24' : '#ff4b72'), 
                    fontWeight: 800 
                }}>
                    {pass.maxElevation.toFixed(1)}°
                </td>
                <td style={{ padding: '12px 14px', textAlign: 'center', color: '#a78bfa', fontWeight: 700, fontFamily: 'monospace' }}>
                    {pass.startAzimuthDegrees != null ? `${pass.startAzimuthDegrees.toFixed(1)}°` : <span style={{ color: textMuted }}>—</span>}
                </td>
                <td style={{ padding: '12px 14px', textAlign: 'center', color: '#60a5fa', fontWeight: 700, fontFamily: 'monospace' }}>
                    {pass.averageAltitude != null ? `${(pass.averageAltitude / 1000).toFixed(0)} km` : <span style={{ color: textMuted }}>—</span>}
                </td>
                <td style={{ padding: '12px 14px', textAlign: 'center' }}>
                    {renderScheduleBadge(pass.schedule, isDark)}
                </td>
                <td style={{ padding: '12px 14px', textAlign: 'center' }}>
                    {isPast ? (
                        <span style={{ 
                            fontSize: '0.68rem', 
                            color: textMuted, 
                            fontWeight: 800,
                            background: 'rgba(0,0,0,0.05)',
                            padding: '3px 8px',
                            borderRadius: '4px'
                        }}>
                            {(t('past') || 'GEÇTİ').toUpperCase()}
                        </span>
                    ) : (
                        <div style={{ display: 'flex', flexDirection: 'column', alignItems: 'center', gap: '1px' }}>
                            <span style={{ fontSize: '0.66rem', color: status.isStarted ? '#05ffc0' : textMuted, fontWeight: 900, letterSpacing: '0.05em' }}>
                                {status.label}
                            </span>
                            <span style={{ color: status.color, fontFamily: 'monospace', fontWeight: 800, fontSize: '0.85rem' }}>
                                {fmtSecs(status.diffMs / 1000)}
                            </span>
                        </div>
                    )}
                </td>
            </tr>
            {isActive && (
                <tr style={{ backgroundColor: rowBg, borderBottom: `1px solid ${tableBorder}` }}>
                    <td colSpan={11} style={{ padding: '0 14px 12px 14px' }}>
                        {/* Glassmorphic glowing progress bar */}
                        <div style={{ height: '5px', borderRadius: '4px', background: isDark ? 'rgba(255,255,255,0.05)' : 'rgba(0,0,0,0.05)', overflow: 'hidden' }}>
                            <div style={{ 
                                height: '100%', 
                                width: `${pct}%`, 
                                background: `linear-gradient(90deg, ${progressColor(pct, pass.maxElevation)}, ${progressColor(Math.min(pct + 25, 100), pass.maxElevation)})`, 
                                borderRadius: '4px', 
                                boxShadow: `0 0 8px ${progressColor(pct, pass.maxElevation)}88`, 
                                transition: 'width 0.4s ease' 
                            }} />
                        </div>
                    </td>
                </tr>
            )}
        </React.Fragment>
    );
}

export function PassPredictionList(): any {
    const socState = useSocData();
    const { t, theme, selectedSatelliteId } = useAppSettings();

    const fmtSecs = (secs: number): string => {
        if (secs < 0) secs = 0;
        const h = Math.floor(secs / 3600);
        const m = Math.floor((secs % 3600) / 60);
        const s = Math.floor(secs % 60);
        return h > 0 ? `${h}${t('hoursShort')} ${m}${t('minutesShort')} ${s}${t('secondsShort')}` : `${m}${t('minutesShort')} ${s}${t('secondsShort')}`;
    };

    const isDark = theme === 'dark';
    
    // Core design system tokens
    const fontStyle = '"Outfit", "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif';
    const panelBg = isDark ? 'radial-gradient(circle at 50% 0%, #101726 0%, #0a0f1d 100%)' : 'radial-gradient(circle at 50% 0%, #f8fafc 0%, #e2e8f0 100%)';
    const panelText = isDark ? '#f8fafc' : '#1e293b';
    const textMuted = isDark ? '#94a3b8' : '#64748b';
    const borderColor = isDark ? 'rgba(255, 255, 255, 0.08)' : 'rgba(0, 0, 0, 0.08)';
    const tableBorder = isDark ? 'rgba(255, 255, 255, 0.04)' : 'rgba(0, 0, 0, 0.04)';
    const cardBg = isDark ? 'rgba(255, 255, 255, 0.02)' : 'rgba(0, 0, 0, 0.015)';
    
    const inputStyle: React.CSSProperties = {
        padding: '10px 14px',
        backgroundColor: isDark ? 'rgba(0, 0, 0, 0.25)' : 'rgba(255, 255, 255, 0.95)',
        color: panelText,
        border: `1.5px solid ${borderColor}`,
        borderRadius: '10px', 
        fontSize: '0.82rem', 
        fontWeight: 600,
        outline: 'none',
        fontFamily: fontStyle,
        transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)'
    };

    const [coarseTime, setCoarseTime] = useState(new Date());

    useEffect(() => {
        const interval = setInterval(() => {
            setCoarseTime(new Date());
        }, 10000); // coarse update every 10 seconds to avoid unnecessary re-renders
        return () => clearInterval(interval);
    }, []);

    const [allPasses, setAllPasses] = useState<LinkedPass[]>([]);
    const [filterSatId, setFilterSatId] = useState<string>('all');
    const [filterDateFrom, setFilterDateFrom] = useState<string>('');
    const [filterDateTo, setFilterDateTo] = useState<string>('');
    const [hidePast, setHidePast] = useState(true);
    const [showFilters, setShowFilters] = useState(false);
    const [activeHoverBtn, setActiveHoverBtn] = useState<string | null>(null);
    const [selectedPassId, setSelectedPassId] = useState<string | null>(null);
    const [actionLoading, setActionLoading] = useState<string | null>(null);
    const [localNotification, setLocalNotification] = useState<{ message: string, type: 'success' | 'error' } | null>(null);

    const groundStations = socState.groundStations || [];

    useEffect(() => {
        if (socState.onPassScheduleSettingResult) {
            const unsub = socState.onPassScheduleSettingResult((res: any) => {
                setActionLoading(null);
                if (res.successful) {
                    setLocalNotification({ message: "Geçiş planlama ayarı başarıyla güncellendi.", type: 'success' });
                    socState.fetchPasses?.(true).catch(console.error);
                } else {
                    setLocalNotification({ message: res.message || "İşlem gerçekleştirilemedi.", type: 'error' });
                }
                setTimeout(() => setLocalNotification(null), 4000);
            });
            return () => unsub();
        }
    }, [socState]);

    const handleRowClick = useCallback((passId: string) => {
        setSelectedPassId(prev => prev === passId ? null : passId);
    }, []);

    const handleActionClick = useCallback(async (passId: string, schedule: string) => {
        setActionLoading(passId);
        try {
            if (socState.updatePassSchedule) {
                setLocalNotification( { message: "Pass Schedule talep gönderme deneniyor", type: 'success'});
                await socState.updatePassSchedule(passId, schedule);
                setLocalNotification({ message: "İşlem talebi gönderildi...", type: 'success' });
            } else {
                throw new Error("RPC updatePassSchedule not defined");
            }
        } catch (e) {
            console.error(e);
            setActionLoading(null);
            setLocalNotification({ message: "Talep gönderilemedi.", type: 'error' });
            setTimeout(() => setLocalNotification(null), 4000);
        }
    }, [socState]);

    const findSatellite = useCallback((idOrNo: any) => {
        if (!idOrNo) return null;
        const targetStr = String(idOrNo);
        return socState.satellites?.find((s: any) =>
            s.id === targetStr ||
            s.noradId === targetStr ||
            s.id === `SAT-${targetStr}` ||
            String(s.noradId) === targetStr
        );
    }, [socState.satellites]);

    const updatePasses = useCallback(() => {
        if (!socState.passPredictions) return;
        const combined: LinkedPass[] = [];
        Object.entries(socState.passPredictions || {}).forEach(([satId, passes]) => {
            const satObj = findSatellite(satId);
            const satName = satObj?.name || (satId.startsWith('SAT-') ? satId.substring(4) : satId);
            const satNoNumeric = satObj?.noradId ? parseInt(satObj.noradId, 10) : (satId.startsWith('SAT-') ? parseInt(satId.substring(4), 10) : parseInt(satId, 10));
            const filtered = (passes as any[] || []);
            filtered.forEach(p => {
                combined.push({
                    passId: p.passId || '',
                    satId,
                    satName,
                    gsId: p.gsId || p.groundStationId,
                    aos: p.aos || p.accessTime,
                    los: p.los || p.lossTime,
                    duration: p.duration,
                    maxElevation: p.maxElevation || p.maxEl,
                    direction: p.direction || 'Unknown',
                    passConfig: p.passConfig,
                    endingConfig: p.endingConfig,
                    satelliteNo: p.satelliteNo || satNoNumeric,
                    startAzimuthDegrees: p.startAzimuthDegrees,
                    averageAltitude: p.averageAltitude,
                    schedule: p.schedule || p.passSchedule
                });
            });
        });
        combined.sort((a, b) => new Date(a.aos).getTime() - new Date(b.aos).getTime());
        setAllPasses(combined);
    }, [socState.passPredictions, findSatellite]);

    useEffect(() => {
        updatePasses();
    }, [updatePasses, socState.satellites]);

    // Automatically fetch configuration names for all satellites in the fleet
    useEffect(() => {
        if (socState.satellites && socState.satellites.length > 0) {
            socState.satellites.forEach((sat: any) => {
                const satNo = sat.noradId ? parseInt(sat.noradId, 10) : parseInt(sat.id, 10);
                if (satNo && socState.fetchSatConfigNames) {
                    socState.fetchSatConfigNames(satNo);
                }
            });
        }
    }, [socState.satellites]);

    const uniqueSatIds = useMemo(() => {
        const map = new Map<string, string>();
        allPasses.forEach((p: LinkedPass) => {
            map.set(p.satId, p.satName || p.satId);
        });
        return Array.from(map.entries()).sort((a, b) => a[1].localeCompare(b[1]));
    }, [allPasses]);

    const filteredPasses = useMemo(() => {
        const coarseTimeMs = coarseTime.getTime();
        return allPasses.filter((p: LinkedPass) => {
            if (filterSatId !== 'all' && p.satId !== filterSatId) return false;
            if (!p.aos || !p.los) return false;
            const aosTime = new Date(p.aos).getTime();
            const losTime = new Date(p.los).getTime();
            if (isNaN(aosTime) || isNaN(losTime)) return false;
            if (hidePast) {
                if (losTime < coarseTimeMs - 300000) return false;
            }
            const fromTime = filterDateFrom ? new Date(filterDateFrom).getTime() : 0;
            const toTime = filterDateTo ? new Date(filterDateTo + 'T23:59:59').getTime() : Infinity;
            if (fromTime > 0 && aosTime < fromTime) return false;
            if (toTime < Infinity && aosTime > toTime) return false;
            return true;
        });
    }, [allPasses, filterSatId, filterDateFrom, filterDateTo, coarseTime, hidePast]);

    const clearFilters = () => {
        setFilterSatId('all');
        setFilterDateFrom('');
        setFilterDateTo('');
    };
    const hasActiveFilters = filterSatId !== 'all' || filterDateFrom || filterDateTo;

    const exportPassesCSV = () => {
        let csv = 'Satellite,AOS (UTC),LOS (UTC),Duration (min),Max Elevation (°),Start Azimuth (°),Avg Altitude (km),Ground Station\n';
        filteredPasses.forEach((p: LinkedPass) => {
            const gsName = groundStations.find(gs => gs.id === p.gsId)?.name || p.gsId || 'Unknown';
            const startAz = p.startAzimuthDegrees != null ? p.startAzimuthDegrees.toFixed(1) : '-';
            const avgAlt = p.averageAltitude != null ? (p.averageAltitude / 1000).toFixed(1) : '-';
            csv += `${p.satName || p.satId},${new Date(p.aos).toISOString()},${new Date(p.los).toISOString()},${Math.round(p.duration / 60)},${p.maxElevation.toFixed(1)},${startAz},${avgAlt},${gsName}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `pass-predictions-${new Date().toISOString().split('T')[0]}.csv`;
        a.click();
        URL.revokeObjectURL(url);
    };

    const exportPassesPDF = () => {
        const printWindow = window.open('', '_blank');
        if (!printWindow) return;
        let html = `
            <html>
            <head>
                <title>Pass Predictions - ${new Date().toLocaleDateString()}</title>
                <style>
                    body { font-family: 'Outfit', 'Inter', system-ui, sans-serif; padding: 40px; color: #1e293b; background-color: #f8fafc; }
                    h1 { color: #0f172a; margin-top: 0; font-weight: 800; letter-spacing: -0.025em; }
                    table { width: 100%; border-collapse: separate; border-spacing: 0; margin-top: 30px; border: 1.5px solid #e2e8f0; border-radius: 12px; overflow: hidden; background: white; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05); }
                    th, td { padding: 14px 18px; text-align: left; border-bottom: 1px solid #e2e8f0; }
                    th { background-color: #f1f5f9; font-weight: 800; text-transform: uppercase; font-size: 0.72rem; letter-spacing: 0.08em; color: #64748b; }
                    tr:last-child td { border-bottom: none; }
                    .header { display: flex; justify-content: space-between; align-items: flex-end; border-bottom: 3px solid #00c6ff; padding-bottom: 20px; margin-bottom: 20px; }
                    .sat-name { color: #00c6ff; font-weight: 800; }
                    .footer { margin-top: 50px; font-size: 0.8rem; color: #94a3b8; text-align: center; }
                </style>
            </head>
            <body>
                <div class="header">
                    <div>
                        <h1>Pass Predictions Report</h1>
                        <div style="color: #64748b; font-weight: 600; font-size: 0.85rem; text-transform: uppercase; letter-spacing: 0.08em;">Orbital Tracking System :: Analysis Division</div>
                    </div>
                    <div style="text-align: right; color: #64748b; font-size: 0.9rem;">
                        <div>Generated: <strong>${new Date().toLocaleString()}</strong></div>
                        <div>Total Predictions: <strong>${filteredPasses.length}</strong></div>
                    </div>
                </div>
                <table>
                    <thead>
                        <tr>
                            <th>Satellite</th>
                            <th>AOS (UTC)</th>
                            <th>LOS (UTC)</th>
                            <th>Duration</th>
                            <th>Max Elevation</th>
                            <th>Start Azimuth (°)</th>
                            <th>Avg Altitude (km)</th>
                            <th>Ground Station</th>
                        </tr>
                    </thead>
                    <tbody>
        `;
        filteredPasses.forEach((p: LinkedPass) => {
            const gsName = groundStations.find(gs => gs.id === p.gsId)?.name || p.gsId || 'Unknown';
            const startAzPdf = p.startAzimuthDegrees != null ? `${p.startAzimuthDegrees.toFixed(1)}°` : '-';
            const avgAltPdf = p.averageAltitude != null ? `${(p.averageAltitude / 1000).toFixed(1)} km` : '-';
            html += `
                <tr>
                    <td class="sat-name">${p.satName || p.satId}</td>
                    <td style="font-family: monospace;">${new Date(p.aos).toLocaleString()}</td>
                    <td style="font-family: monospace;">${new Date(p.los).toLocaleString()}</td>
                    <td style="font-weight: 700;">${Math.round(p.duration / 60)} min</td>
                    <td style="color: #fbbf24; font-weight: 800;">${p.maxElevation.toFixed(1)}°</td>
                    <td style="color: #a78bfa; font-weight: 700;">${startAzPdf}</td>
                    <td style="color: #60a5fa; font-weight: 700;">${avgAltPdf}</td>
                    <td>${gsName}</td>
                </tr>
            `;
        });
        html += `</tbody></table>
                <div class="footer">
                    &copy; ${new Date().getFullYear()} Orbital Tracking System. All rights reserved. This document is property of OTS Command.
                </div>
            </body></html>`;
        printWindow.document.write(html);
        printWindow.document.close();
        setTimeout(() => { printWindow.print(); }, 500);
    };

    const isHovered = (id: string) => activeHoverBtn === id;

    return (
        <div style={{ 
            padding: '12px', 
            background: panelBg, 
            color: panelText, 
            height: '100%', 
            overflowY: 'auto', 
            boxSizing: 'border-box',
            fontFamily: fontStyle,
            display: 'flex',
            flexDirection: 'column',
            gap: '8px'
        }}>
            {/* Table Action Header */}
            <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
                <h2 style={{ 
                    fontSize: '1.05rem', 
                    display: 'flex', 
                    alignItems: 'center', 
                    gap: '10px', 
                    margin: 0,
                    fontWeight: 900,
                    textTransform: 'uppercase',
                    letterSpacing: '0.06em'
                }}>
                    <span className="fa fa-satellite" style={{ color: '#8b5cf6', filter: 'drop-shadow(0 0 6px rgba(139, 92, 246, 0.4))' }}></span>
                    {t('allFleetPasses')}
                </h2>
                
                {/* Clean Button Group with premium hover animations */}
                <div style={{ display: 'flex', gap: '8px' }}>
                    <button 
                        onMouseEnter={() => setActiveHoverBtn('csv')}
                        onMouseLeave={() => setActiveHoverBtn(null)}
                        onClick={exportPassesCSV} 
                        style={{ 
                            background: 'rgba(255,255,255,0.03)', 
                            border: `1.5px solid ${isHovered('csv') ? accentBlue : borderColor}`, 
                            color: isHovered('csv') ? panelText : textMuted, 
                            borderRadius: '8px', 
                            padding: '6px 12px', 
                            fontSize: '0.78rem', 
                            fontWeight: 700,
                            cursor: 'pointer', 
                            display: 'flex', 
                            alignItems: 'center', 
                            gap: '6px',
                            transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)',
                            transform: isHovered('csv') ? 'translateY(-1px)' : 'none'
                        }}
                    >
                        <span className="fa fa-file-csv" style={{ color: isHovered('csv') ? accentBlue : textMuted }}></span> CSV
                    </button>
                    <button 
                        onMouseEnter={() => setActiveHoverBtn('pdf')}
                        onMouseLeave={() => setActiveHoverBtn(null)}
                        onClick={exportPassesPDF} 
                        style={{ 
                            background: 'rgba(255,255,255,0.03)', 
                            border: `1.5px solid ${isHovered('pdf') ? accentBlue : borderColor}`, 
                            color: isHovered('pdf') ? panelText : textMuted, 
                            borderRadius: '8px', 
                            padding: '6px 12px', 
                            fontSize: '0.78rem', 
                            fontWeight: 700,
                            cursor: 'pointer', 
                            display: 'flex', 
                            alignItems: 'center', 
                            gap: '6px',
                            transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)',
                            transform: isHovered('pdf') ? 'translateY(-1px)' : 'none'
                        }}
                    >
                        <span className="fa fa-file-pdf" style={{ color: isHovered('pdf') ? accentBlue : textMuted }}></span> PDF
                    </button>
                    <button 
                        onMouseEnter={() => setActiveHoverBtn('filter')}
                        onMouseLeave={() => setActiveHoverBtn(null)}
                        onClick={() => setShowFilters(v => !v)} 
                        style={{ 
                            background: hasActiveFilters ? 'rgba(251,191,36,0.12)' : 'rgba(255,255,255,0.03)', 
                            border: `1.5px solid ${hasActiveFilters ? accentAmber : (isHovered('filter') ? accentBlue : borderColor)}`, 
                            color: hasActiveFilters ? accentAmber : (isHovered('filter') ? panelText : textMuted), 
                            borderRadius: '8px', 
                            padding: '6px 12px', 
                            fontSize: '0.78rem', 
                            fontWeight: 700,
                            cursor: 'pointer', 
                            display: 'flex', 
                            alignItems: 'center', 
                            gap: '6px',
                            transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)',
                            transform: isHovered('filter') ? 'translateY(-1px)' : 'none',
                            boxShadow: hasActiveFilters ? '0 0 10px rgba(251,191,36,0.15)' : 'none'
                        }}
                    >
                        <span className="fa fa-filter"></span>
                        {hasActiveFilters ? t('filtered') : t('filter')}
                    </button>
                    <button 
                        onMouseEnter={() => setActiveHoverBtn('refresh')}
                        onMouseLeave={() => setActiveHoverBtn(null)}
                        onClick={() => {
                            const satId = selectedSatelliteId || (socState.satellites?.[0]?.id);
                            if (satId) {
                                const ch = new BroadcastChannel('soc-cmd');
                                ch.postMessage({ type: 'refreshPasses', satId });
                                ch.close();
                            }
                        }} 
                        style={{ 
                            background: 'rgba(139, 92, 246, 0.12)', 
                            border: `1.5px solid ${isHovered('refresh') ? '#a78bfa' : 'rgba(139, 92, 246, 0.25)'}`, 
                            color: '#a78bfa', 
                            borderRadius: '8px', 
                            padding: '6px 12px', 
                            fontSize: '0.78rem', 
                            fontWeight: 700,
                            cursor: 'pointer', 
                            display: 'flex', 
                            alignItems: 'center', 
                            gap: '6px',
                            transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)',
                            transform: isHovered('refresh') ? 'translateY(-1px)' : 'none',
                            boxShadow: '0 0 10px rgba(139, 92, 246, 0.15)'
                        }}
                    >
                        <span className="fa fa-sync-alt"></span> {t('refreshPasses')}
                    </button>
                </div>
            </div>

            {/* Premium Sliding Glassmorphic Filter Box */}
            {showFilters && (
                <div style={{ 
                    background: cardBg, 
                    border: `1.5px solid ${borderColor}`, 
                    borderRadius: '12px', 
                    padding: '16px 18px', 
                    display: 'flex', 
                    flexDirection: 'column', 
                    gap: '12px',
                    boxShadow: '0 4px 15px rgba(0, 0, 0, 0.04)'
                }}>
                    <div style={{ 
                        fontSize: '0.72rem', 
                        fontWeight: 900, 
                        color: accentAmber, 
                        textTransform: 'uppercase', 
                        letterSpacing: '0.08em', 
                        display: 'flex', 
                        justifyContent: 'space-between', 
                        alignItems: 'center' 
                    }}>
                        <span>🔍 {t('filter')}</span>
                        {hasActiveFilters && (
                            <button 
                                onClick={clearFilters} 
                                style={{ 
                                    background: 'none', 
                                    border: 'none', 
                                    color: accentRed, 
                                    cursor: 'pointer', 
                                    fontSize: '0.72rem', 
                                    fontWeight: 800,
                                    padding: 0,
                                    fontFamily: fontStyle
                                }}
                            >
                                ✕ {t('clearAll')}
                            </button>
                        )}
                    </div>

                    <div style={{ display: 'grid', gridTemplateColumns: '2fr 3fr', gap: '12px', alignItems: 'end' }}>
                        <div style={{ display: 'flex', flexDirection: 'column', gap: '5px' }}>
                            <label style={{ fontSize: '0.75rem', color: textMuted, fontWeight: 700 }}>{t('sat')}</label>
                            <select value={filterSatId} onChange={e => setFilterSatId(e.target.value)} style={{ ...inputStyle, width: '100%' }}>
                                <option value="all">{t('allSatellites')}</option>
                                {uniqueSatIds.map(([id, name]) => <option key={id} value={id}>{name}</option>)}
                            </select>
                        </div>
                        <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: '10px' }}>
                            <div style={{ display: 'flex', flexDirection: 'column', gap: '5px' }}>
                                <label style={{ fontSize: '0.75rem', color: textMuted, fontWeight: 700 }}>{t('from')}</label>
                                <input type="date" value={filterDateFrom} onChange={e => setFilterDateFrom(e.target.value)} style={{ ...inputStyle, width: '100%', colorScheme: isDark ? 'dark' : 'light' }} />
                            </div>
                            <div style={{ display: 'flex', flexDirection: 'column', gap: '5px' }}>
                                <label style={{ fontSize: '0.75rem', color: textMuted, fontWeight: 700 }}>{t('to')}</label>
                                <input type="date" value={filterDateTo} onChange={e => setFilterDateTo(e.target.value)} style={{ ...inputStyle, width: '100%', colorScheme: isDark ? 'dark' : 'light' }} />
                            </div>
                        </div>
                    </div>

                    <div 
                        style={{ 
                            display: 'flex', 
                            alignItems: 'center', 
                            gap: '10px', 
                            cursor: 'pointer', 
                            userSelect: 'none',
                            width: 'fit-content'
                        }} 
                        onClick={() => setHidePast(!hidePast)}
                    >
                        <div style={{ 
                            width: '16px', 
                            height: '16px', 
                            border: `1.5px solid ${hidePast ? accentAmber : borderColor}`, 
                            borderRadius: '4px', 
                            display: 'flex', 
                            alignItems: 'center', 
                            justifyContent: 'center', 
                            backgroundColor: hidePast ? 'rgba(251,191,36,0.1)' : 'transparent',
                            transition: 'all 0.2s cubic-bezier(0.25, 0.8, 0.25, 1)'
                        }}>
                            {hidePast && <span className="fa fa-check" style={{ fontSize: '9px', color: accentAmber }}></span>}
                        </div>
                        <span style={{ fontSize: '0.8rem', color: hidePast ? accentAmber : textMuted, fontWeight: 700 }}>{t('hidePastPasses')}</span>
                    </div>
                </div>
            )}

            {/* Local Toast Banner */}
            {localNotification && (
                <div style={{
                    padding: '10px 14px',
                    borderRadius: '8px',
                    background: localNotification.type === 'success' ? 'rgba(16, 185, 129, 0.12)' : 'rgba(239, 68, 68, 0.12)',
                    border: `1.5px solid ${localNotification.type === 'success' ? '#34d399' : '#f87171'}`,
                    color: localNotification.type === 'success' ? '#34d399' : '#f87171',
                    fontSize: '0.8rem',
                    fontWeight: 700,
                    display: 'flex',
                    alignItems: 'center',
                    gap: '10px',
                    marginBottom: '12px'
                }}>
                    <span className={`fa ${localNotification.type === 'success' ? 'fa-check-circle' : 'fa-exclamation-circle'}`}></span>
                    {localNotification.message}
                </div>
            )}

            {/* Results Count */}
            <div style={{ fontSize: '0.78rem', color: textMuted, fontWeight: 700, marginBottom: '4px' }}>
                {filteredPasses.length} {t('found')}
            </div>

            {/* Premium Table Rendering */}
            {filteredPasses.length > 0 ? (
                <div style={{ overflowX: 'auto', borderRadius: '12px', border: `1.5px solid ${borderColor}`, boxShadow: '0 4px 15px rgba(0, 0, 0, 0.02)' }}>
                    <table style={{ width: '100%', borderCollapse: 'collapse', fontSize: '0.82rem', textAlign: 'left' }}>
                        <thead>
                            <tr style={{ borderBottom: `1.5px solid ${borderColor}`, backgroundColor: isDark ? 'rgba(255,255,255,0.015)' : 'rgba(0,0,0,0.01)' }}>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted }}>{t('sat')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted }}>{t('startAOS')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted }}>{t('endAOS')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted }}>{t('stConfig')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted }}>{t('endConfig')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted, textAlign: 'center' }}>{t('duration')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted, textAlign: 'center' }}>{t('maxEl')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: '#a78bfa', textAlign: 'center' }}>{t('startAzimuth')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: '#60a5fa', textAlign: 'center' }}>{t('averageAlt')}</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted, textAlign: 'center' }}>PLAN</th>
                                <th style={{ padding: '12px 14px', textTransform: 'uppercase', letterSpacing: '0.08em', fontSize: '0.72rem', fontWeight: 800, color: textMuted, textAlign: 'center' }}>{t('status')}</th>
                            </tr>
                        </thead>
                        <tbody>
                            {filteredPasses.map((p: LinkedPass) => {
                                const isPast = new Date(p.los).getTime() < coarseTime.getTime();
                                const isSelected = p.passId === selectedPassId;
                                return (
                                    <React.Fragment key={p.passId}>
                                        {isPast ? (
                                            <PastPassRow 
                                                pass={p} 
                                                isDark={isDark} 
                                                borderColor={borderColor} 
                                                tableBorder={tableBorder} 
                                                textMuted={textMuted} 
                                                panelText={panelText} 
                                                selectedSatelliteId={selectedSatelliteId} 
                                                findSatellite={findSatellite} 
                                                socState={socState} 
                                                selectedPassId={selectedPassId}
                                                onRowClick={handleRowClick}
                                            />
                                        ) : (
                                            <ActivePassRow 
                                                pass={p} 
                                                isDark={isDark} 
                                                borderColor={borderColor} 
                                                tableBorder={tableBorder} 
                                                textMuted={textMuted} 
                                                panelText={panelText} 
                                                selectedSatelliteId={selectedSatelliteId} 
                                                findSatellite={findSatellite} 
                                                socState={socState} 
                                                t={t} 
                                                selectedPassId={selectedPassId}
                                                onRowClick={handleRowClick}
                                            />
                                        )}
                                        {isSelected && (
                                            <tr style={{ 
                                                backgroundColor: isDark ? 'rgba(0, 198, 255, 0.03)' : 'rgba(0, 198, 255, 0.02)', 
                                                borderBottom: `1px solid ${tableBorder}` 
                                            }}>
                                                <td colSpan={11} style={{ padding: '10px 14px' }}>
                                                    <div style={{ display: 'flex', gap: '10px', alignItems: 'center', justifyContent: 'flex-end' }}>
                                                        <span style={{ fontSize: '0.8rem', color: textMuted, marginRight: 'auto', fontWeight: 700, textTransform: 'uppercase', letterSpacing: '0.04em' }}>
                                                            ⚙️ {p.satName || p.satId} - GEÇİŞ İŞLEMLERİ (AOS: {new Date(p.aos).toLocaleTimeString()}):
                                                        </span>
                                                        
                                                        <button
                                                            onClick={(e) => {
                                                                e.stopPropagation();
                                                                handleActionClick(p.passId, 'SCHEDULED');
                                                            }}
                                                            disabled={actionLoading === p.passId}
                                                            style={{
                                                                background: 'rgba(16, 185, 129, 0.12)',
                                                                border: '1px solid rgba(16, 185, 129, 0.3)',
                                                                color: '#34d399',
                                                                borderRadius: '6px',
                                                                padding: '6px 12px',
                                                                fontSize: '0.74rem',
                                                                fontWeight: 700,
                                                                cursor: 'pointer',
                                                                transition: 'all 0.15s ease',
                                                                display: 'flex',
                                                                alignItems: 'center',
                                                                gap: '6px',
                                                                opacity: actionLoading === p.passId ? 0.5 : 1
                                                            }}
                                                            onMouseEnter={e => { if (actionLoading !== p.passId) e.currentTarget.style.background = 'rgba(16, 185, 129, 0.22)'; }}
                                                            onMouseLeave={e => { if (actionLoading !== p.passId) e.currentTarget.style.background = 'rgba(16, 185, 129, 0.12)'; }}
                                                        >
                                                            <span className="fa fa-calendar-plus"></span> Plana Ekle
                                                        </button>

                                                        <button
                                                            onClick={(e) => {
                                                                e.stopPropagation();
                                                                handleActionClick(p.passId, 'CANCELLED');
                                                            }}
                                                            disabled={actionLoading === p.passId}
                                                            style={{
                                                                background: 'rgba(239, 68, 68, 0.12)',
                                                                border: '1px solid rgba(239, 68, 68, 0.3)',
                                                                color: '#f87171',
                                                                borderRadius: '6px',
                                                                padding: '6px 12px',
                                                                fontSize: '0.74rem',
                                                                fontWeight: 700,
                                                                cursor: 'pointer',
                                                                transition: 'all 0.15s ease',
                                                                display: 'flex',
                                                                alignItems: 'center',
                                                                gap: '6px',
                                                                opacity: actionLoading === p.passId ? 0.5 : 1
                                                            }}
                                                            onMouseEnter={e => { if (actionLoading !== p.passId) e.currentTarget.style.background = 'rgba(239, 68, 68, 0.22)'; }}
                                                            onMouseLeave={e => { if (actionLoading !== p.passId) e.currentTarget.style.background = 'rgba(239, 68, 68, 0.12)'; }}
                                                        >
                                                            <span className="fa fa-calendar-times"></span> Plandan Çıkar
                                                        </button>

                                                        <button
                                                            onClick={(e) => {
                                                                e.stopPropagation();
                                                                handleActionClick(p.passId, 'AUTO_SCHEDULED');
                                                            }}
                                                            disabled={actionLoading === p.passId}
                                                            style={{
                                                                background: 'rgba(59, 130, 246, 0.12)',
                                                                border: '1px solid rgba(59, 130, 246, 0.3)',
                                                                color: '#60a5fa',
                                                                borderRadius: '6px',
                                                                padding: '6px 12px',
                                                                fontSize: '0.74rem',
                                                                fontWeight: 700,
                                                                cursor: 'pointer',
                                                                transition: 'all 0.15s ease',
                                                                display: 'flex',
                                                                alignItems: 'center',
                                                                gap: '6px',
                                                                opacity: actionLoading === p.passId ? 0.5 : 1
                                                            }}
                                                            onMouseEnter={e => { if (actionLoading !== p.passId) e.currentTarget.style.background = 'rgba(59, 130, 246, 0.22)'; }}
                                                            onMouseLeave={e => { if (actionLoading !== p.passId) e.currentTarget.style.background = 'rgba(59, 130, 246, 0.12)'; }}
                                                        >
                                                            <span className="fa fa-magic"></span> Otomatik Planlama Yap
                                                        </button>
                                                    </div>
                                                </td>
                                            </tr>
                                        )}
                                    </React.Fragment>
                                );
                            })}
                        </tbody>
                    </table>
                </div>
            ) : (
                <div style={{ 
                    padding: '40px', 
                    textAlign: 'center', 
                    color: textMuted, 
                    fontSize: '0.86rem', 
                    background: cardBg, 
                    borderRadius: '12px', 
                    border: `1.5px dashed ${borderColor}` 
                }}>
                    <span className="fa fa-info-circle" style={{ marginBottom: '10px', fontSize: '1.4rem', display: 'block', color: accentBlue }}></span>
                    {hasActiveFilters ? t('noPassesMatch') : t('noPassesFound')}
                </div>
            )}
            <style>{`
                @keyframes pulse-glow { 
                    0%, 100% { opacity: 1; transform: scale(1); } 
                    50% { opacity: 0.3; transform: scale(0.9); } 
                }
            `}</style>
        </div>
    );
}

export function PassPredictionPanel(): any {
    const { theme } = useAppSettings();
    const isDark = theme === 'dark';
    const borderColor = isDark ? 'rgba(255, 255, 255, 0.08)' : 'rgba(0, 0, 0, 0.08)';

    return (
        <div style={{ height: '100%', display: 'flex', flexDirection: 'column', overflow: 'hidden' }}>
            <div style={{ height: '240px', flexShrink: 0 }}>
                <PassPredictionSummary />
            </div>
            <div style={{ flex: 1, overflow: 'hidden', borderTop: `1.5px solid ${borderColor}` }}>
                <PassPredictionList />
            </div>
        </div>
    );
}
