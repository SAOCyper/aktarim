/**
 * theia-entry.ts
 *
 * Library entry point for Eclipse Theia consumption.
 * Exports all hooks, services, models, RPCs, contexts, and helper utilities.
 */
// Hooks & Context
export * from './features/satellite/hooks/useSatelliteSystem';
export * from './features/satellite/hooks/useSocData';
export * from './features/satellite/hooks/useSimulationClock';
export * from './features/satellite/context/AppSettingsContext';

// Services & Models
export * from './features/satellite/services/SocDataService';
export * from './features/satellite/services/CesiumEntityManager';
export * from './features/satellite/models/GlobalConfig';

// RPC
export * from './rpc/satellite-rpc';

// Configuration & Core
export * from './core/config';

// Shared Utilities & Types
export * from './features/satellite/utils/cesium-helpers';

/**
 * Call this function before mounting ReactWidgets to instruct Cesium
 * and other static-asset loading logic to point to the Vite server.
 */
export function setupTheiaEnvironment(viteBaseUrl: string) {
    const base = viteBaseUrl.replace(/\/+$/, '');
    (window as any).CESIUM_BASE_URL = `${base}/cesium/`;
    (window as any).SOC_STATIC_BASE_URL = base;
    (window as any).IS_THEIA = true;
}
