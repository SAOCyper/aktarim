Lerna (powered by Nx)   Running target compile for 2 projects:
- gsc-browser-app
- gsc-browser-app-cesium
> gsc-browser-app:compile
> gsc-browser-app-cesium:compile
gsc-browser-app: > gsc-browser-app@1.0.0 compile
gsc-browser-app: > tsc -b
gsc-browser-app-cesium: > gsc-browser-app-cesium@1.0.0 compile
gsc-browser-app-cesium: > tsc -b
gsc-browser-app: ../extensions/gsc-earth-extension/src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
gsc-browser-app: ../extensions/gsc-earth-extension/src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
gsc-browser-app: ../extensions/gsc-earth-extension/src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
gsc-browser-app: ../extensions/gsc-earth-extension/src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
gsc-browser-app: ../extensions/gsc-earth-extension/src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
gsc-browser-app: npm error Lifecycle script `compile` failed with error:
gsc-browser-app: npm error code 1
gsc-browser-app: npm error path /builds/gss/gsc/gsc.scheduling.theia/browser-app
gsc-browser-app: npm error workspace gsc-browser-app@1.0.0
gsc-browser-app: npm error location /builds/gss/gsc/gsc.scheduling.theia/browser-app
gsc-browser-app: npm error command failed
gsc-browser-app: npm error command sh -c tsc -b
 Lerna (powered by Nx)   Running target compile for 2 projects failed
Failed tasks:
- gsc-browser-app:compile
Cleaning up project directory and file based variables 00:01
ERROR: Job failed: exit code 1
