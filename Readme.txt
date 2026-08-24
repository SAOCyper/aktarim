gsc-browser-app-cesium: > gsc-browser-app-cesium@1.0.0 compile
gsc-browser-app-cesium: > tsc -b
gsc-browser-app: > gsc-browser-app@1.0.0 compile
gsc-browser-app: > tsc -b
gsc-browser-app: error TS18003: No inputs were found in config file '/builds/gss/gsc/gsc.scheduling.theia/browser-app/tsconfig.json'. Specified 'include' paths were '[]' and 'exclude' paths were '[]'.
gsc-browser-app: npm error Lifecycle script `compile` failed with error:
gsc-browser-app: npm error code 1
gsc-browser-app: npm error path /builds/gss/gsc/gsc.scheduling.theia/browser-app
gsc-browser-app: npm error workspace gsc-browser-app@1.0.0
gsc-browser-app: npm error location /builds/gss/gsc/gsc.scheduling.theia/browser-app
gsc-browser-app: npm error command failed
gsc-browser-app: npm error command sh -c tsc -b
 Lerna (powered by Nx)   Running target compile for 3 projects failed
Failed tasks:
- gsc-browser-app:compile
Cleaning up project directory and file based variables 00:01
ERROR: Job failed: exit code 1
