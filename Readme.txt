100 vulnerabilities (6 low, 55 moderate, 31 high, 8 critical)
To address issues that do not require attention, run:
  npm audit fix
To address all issues possible (including breaking changes), run:
  npm audit fix --force
Some issues need review, and may require choosing
a different dependency.
Run `npm audit` for details.
npm verbose cwd /builds/gss/gsc/gsc.scheduling.theia
npm verbose os Linux 6.12.101+deb13-amd64
npm verbose node v22.14.0
npm verbose npm  v10.9.2
npm verbose exit 0
npm info ok
$ npm run compile
> compile
> lerna run compile
lerna notice cli v9.0.7
lerna info ci enabled
 Lerna (powered by Nx)   Running target compile for 2 projects:
- gsc-browser-app
- gsc-browser-app-cesium
> gsc-browser-app:compile
> gsc-browser-app-cesium:compile
gsc-browser-app: > gsc-browser-app@1.0.0 compile
gsc-browser-app: > tsc -b
gsc-browser-app-cesium: > gsc-browser-app-cesium@1.0.0 compile
gsc-browser-app-cesium: > tsc -b
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/browser/common-index.ts(1,15): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/features/satellite/hooks/useSatelliteSystem.ts(3,40): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/utils/cesium-helpers.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via '../utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSatelliteSystem.ts'
gsc-browser-app-cesium:     Imported via '../utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/SocDataService.ts'
gsc-browser-app-cesium:     Imported via '../features/satellite/utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/rpc/satellite-rpc.ts'
gsc-browser-app-cesium:     Imported via '../utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSocData.ts'
gsc-browser-app-cesium:     Imported via '../utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/CesiumEntityManager.ts'
gsc-browser-app-cesium:     Imported via './features/satellite/utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium:     Imported via './features/satellite/utils/cesium-helpers' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/features/satellite/hooks/useSatelliteSystem.ts(4,24): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/core/config.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via '../../../core/config' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSatelliteSystem.ts'
gsc-browser-app-cesium:     Imported via '../../../core/config' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/SocDataService.ts'
gsc-browser-app-cesium:     Imported via './core/config' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium:     Imported via './core/config' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/features/satellite/hooks/useSocData.ts(12,32): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/SocDataService.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via '../services/SocDataService' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSocData.ts'
gsc-browser-app-cesium:     Imported via './features/satellite/services/SocDataService' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/features/satellite/services/SocDataService.ts(15,38): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/rpc/satellite-rpc.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via '../../../rpc/satellite-rpc' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/SocDataService.ts'
gsc-browser-app-cesium:     Imported via '../../../rpc/satellite-rpc' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/SocDataService.ts'
gsc-browser-app-cesium:     Imported via './rpc/satellite-rpc' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium:     Imported via './rpc/satellite-rpc' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(13,1): error TS6200: Definitions of the following identifiers conflict with those in another file: Config, setupTheiaEnvironment, FrameworkMode, useSatelliteSystem, WidgetTitleSync, AppSettingsProvider, widgetTitleSync, appSettingsProvider
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(13,36): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSatelliteSystem.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(14,28): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSocData.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via './features/satellite/hooks/useSocData' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium:     Imported via './features/satellite/hooks/useSocData' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(16,36): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/hooks/useSimulationClock.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(17,108): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/context/AppSettingsContext.tsx' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(21,37): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/services/CesiumEntityManager.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium: ../extensions/gsc-core-extension/src/common/theia-entry.ts(22,28): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/features/satellite/models/GlobalConfig.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via './features/satellite/models/GlobalConfig' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium:     Imported via './features/satellite/models/GlobalConfig' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/common/theia-entry.ts'
gsc-browser-app-cesium: ../extensions/gsc-earth-extension/src/browser/satellite-client-impl.ts(2,49): error TS6059: File '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-core-extension/src/browser/common-index.ts' is not under 'rootDir' '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src'. 'rootDir' is expected to contain all source files.
gsc-browser-app-cesium:   The file is in the program because:
gsc-browser-app-cesium:     Imported via '@uzay/gsc-core-extension' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src/browser/satellite-client-impl.ts'
gsc-browser-app-cesium:     Imported via '@uzay/gsc-core-extension' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src/browser/cesium-view-widget.tsx'
gsc-browser-app-cesium:     Imported via '@uzay/gsc-core-extension' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src/browser/components/EarthViewer.tsx'
gsc-browser-app-cesium:     Imported via '@uzay/gsc-core-extension' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src/browser/soc-frontend-contribution.ts'
gsc-browser-app-cesium:     Imported via '@uzay/gsc-core-extension' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src/browser/soc-frontend-module.ts'
gsc-browser-app-cesium:     Imported via '@uzay/gsc-core-extension' from file '/builds/gss/gsc/gsc.scheduling.theia/extensions/gsc-earth-extension/src/browser/soc-widgets.d.ts'
gsc-browser-app-cesium: ../extensions/gsc-earth-extension/tsconfig.json(48,9): error TS5023: Unknown compiler option 'references'.
gsc-browser-app-cesium: npm error Lifecycle script `compile` failed with error:
gsc-browser-app-cesium: npm error code 1
gsc-browser-app-cesium: npm error path /builds/gss/gsc/gsc.scheduling.theia/browser-app-cesium
gsc-browser-app-cesium: npm error workspace gsc-browser-app-cesium@1.0.0
gsc-browser-app-cesium: npm error location /builds/gss/gsc/gsc.scheduling.theia/browser-app-cesium
gsc-browser-app-cesium: npm error command failed
gsc-browser-app-cesium: npm error command sh -c tsc -b
 Lerna (powered by Nx)   Running target compile for 2 projects failed
Failed tasks:
- gsc-browser-app-cesium:compile
Cleaning up project directory and file based variables 00:01
ERROR: Job failed: exit code 1
