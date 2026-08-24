/**
 * theia-entry.ts
 *
 * Library entry point for Eclipse Theia consumption.
 * When Vite builds with --mode theia, this file becomes the root
 * and all exported components are available to the Theia extension's
 * ReactWidget factories.
 *
 * Usage in Theia widget:
 *   import { CesiumViewer, PanelPage } from 'soc-widgets';
 */
// Hooks & Context
export { useSatelliteSystem } from './features/satellite/hooks/useSatelliteSystem';
export { useSocData } from './features/satellite/hooks/useSocData';
export type { SocDataHookResult } from './features/satellite/hooks/useSocData';
export { useSimulationClock } from './features/satellite/hooks/useSimulationClock';
export { AppSettingsProvider, appSettingsProvider, WidgetTitleSync, widgetTitleSync, useAppSettings } from './features/satellite/context/AppSettingsContext';

// Services & Models
export { SocDataService } from './features/satellite/services/SocDataService';
export { CesiumEntityManager } from './features/satellite/services/CesiumEntityManager';
export { ConfigType } from './features/satellite/models/GlobalConfig';
export type { GlobalConfiguration, SatConfiguration } from './features/satellite/models/GlobalConfig';

export { satelliteServerPath, SatelliteServerSymbol } from './rpc/satellite-rpc';
export type { SatelliteClient, SatelliteServer } from './rpc/satellite-rpc';

// Configuration
export { Config } from './core/config';
export type { FrameworkMode } from './core/config';

// Shared types & Helpers
export { toJulianDate, toCartesian3 } from './features/satellite/utils/cesium-helpers';
export type { SatellitePosition, GroundStation } from './features/satellite/utils/cesium-helpers';

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
