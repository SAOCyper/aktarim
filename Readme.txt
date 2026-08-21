root@2a85f57da0c0:/home/theia# npm run build:extensions

> build:extensions
> lerna run --scope="@uzay/*" build

lerna notice cli v9.0.7
lerna notice filter including "@uzay/*"
lerna info filter [ '@uzay/*' ]

 Lerna (powered by Nx)   Running target build for 8 projects:

- @uzay/gsc-core-extension
- @uzay/gsc-earth-extension
- @uzay/gsc-files-extension
- @uzay/gsc-mission-extension
- @uzay/gsc-moon-extension
- @uzay/gsc-pass-control-extension
- @uzay/gsc-pass-prediction-extension
- @uzay/gsc-settings-extension

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

> @uzay/gsc-core-extension:build

@uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
@uzay/gsc-core-extension: > tsc

> @uzay/gsc-earth-extension:build


> @uzay/gsc-files-extension:build


> @uzay/gsc-pass-prediction-extension:build


> @uzay/gsc-moon-extension:build


> @uzay/gsc-mission-extension:build


> @uzay/gsc-pass-control-extension:build


> @uzay/gsc-settings-extension:build

@uzay/gsc-pass-prediction-extension: > @uzay/gsc-pass-prediction-extension@1.0.0 build
@uzay/gsc-pass-prediction-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-mission-extension: > @uzay/gsc-mission-extension@1.0.0 build
@uzay/gsc-mission-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-files-extension: > @uzay/gsc-files-extension@1.0.0 build
@uzay/gsc-files-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-settings-extension: > @uzay/gsc-settings-extension@1.0.0 build
@uzay/gsc-settings-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-pass-control-extension: > @uzay/gsc-pass-control-extension@1.0.0 build
@uzay/gsc-pass-control-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-moon-extension: npm warn config ignoring workspace config at /home/theia/extensions/gsc-moon-extension/.npmrc
@uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
@uzay/gsc-earth-extension: > tsc
@uzay/gsc-moon-extension: > @uzay/gsc-moon-extension@1.0.0 build
@uzay/gsc-moon-extension: > tsc -p tsconfig.json && cpx "src/**/*.css" lib/
@uzay/gsc-settings-extension: src/browser/components/SettingsWidget.tsx(2,32): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-settings-extension: src/browser/soc-settings-widget.tsx(5,54): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-settings-extension: npm error Lifecycle script `build` failed with error:
@uzay/gsc-settings-extension: npm error code 2
@uzay/gsc-settings-extension: npm error path /home/theia/extensions/gsc-settings-extension
@uzay/gsc-settings-extension: npm error workspace @uzay/gsc-settings-extension@1.0.0
@uzay/gsc-settings-extension: npm error location /home/theia/extensions/gsc-settings-extension
@uzay/gsc-settings-extension: npm error command failed
@uzay/gsc-settings-extension: npm error command sh -c tsc && cpx "src/**/*.css" lib/

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Running target build for 8 projects failed

Failed tasks:

- @uzay/gsc-settings-extension:build

root@2a85f57da0c0:/home/theia# npm run build:extensions

> build:extensions
> lerna run --scope="@uzay/*" build --concurrency=1

lerna notice cli v9.0.7
lerna notice filter including "@uzay/*"
lerna info filter [ '@uzay/*' ]

 Lerna (powered by Nx)   Running target build for 8 projects:

- @uzay/gsc-core-extension
- @uzay/gsc-earth-extension
- @uzay/gsc-files-extension
- @uzay/gsc-mission-extension
- @uzay/gsc-moon-extension
- @uzay/gsc-pass-control-extension
- @uzay/gsc-pass-prediction-extension
- @uzay/gsc-settings-extension

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

> @uzay/gsc-core-extension:build

@uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
@uzay/gsc-core-extension: > tsc

> @uzay/gsc-earth-extension:build

@uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
@uzay/gsc-earth-extension: > tsc
@uzay/gsc-earth-extension: src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-earth-extension: src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-earth-extension: src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-earth-extension: src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-earth-extension: src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
@uzay/gsc-earth-extension: npm error Lifecycle script `build` failed with error:
@uzay/gsc-earth-extension: npm error code 2
@uzay/gsc-earth-extension: npm error path /home/theia/extensions/gsc-earth-extension
@uzay/gsc-earth-extension: npm error workspace @uzay/gsc-earth-extension@1.0.0
@uzay/gsc-earth-extension: npm error location /home/theia/extensions/gsc-earth-extension
@uzay/gsc-earth-extension: npm error command failed
@uzay/gsc-earth-extension: npm error command sh -c tsc

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Running target build for 8 projects failed
