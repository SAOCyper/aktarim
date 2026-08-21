 @uzay/gsc-core-extension:build

@uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
@uzay/gsc-core-extension: > tsc
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/browser/common-index.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/core/config.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/context/AppSettingsContext.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSatelliteSystem.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSimulationClock.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSocData.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/models/GlobalConfig.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/CesiumEntityManager.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/SocDataService.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/utils/cesium-helpers.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/rpc/satellite-rpc.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/theia-entry.d.ts' because it would overwrite input file.
@uzay/gsc-core-extension: npm error Lifecycle script `build` failed with error:
@uzay/gsc-core-extension: npm error code 1
@uzay/gsc-core-extension: npm error path /home/theia/extensions/gsc-core-extension
@uzay/gsc-core-extension: npm error workspace @uzay/gsc-core-extension@1.0.0
@uzay/gsc-core-extension: npm error location /home/theia/extensions/gsc-core-extension
@uzay/gsc-core-extension: npm error command failed
@uzay/gsc-core-extension: npm error command sh -c tsc

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Running target build for 8 projects failed

Tasks not run because their dependencies failed or --nx-bail=true:

- @uzay/gsc-earth-extension:build
- @uzay/gsc-files-extension:build
- @uzay/gsc-mission-extension:build
- @uzay/gsc-moon-extension:build
- @uzay/gsc-pass-control-extension:build
- @uzay/gsc-pass-prediction-extension:build
- @uzay/gsc-settings-extension:build

Failed tasks:

- @uzay/gsc-core-extension:build

root@2a85f57da0c0:/home/theia# ^C
