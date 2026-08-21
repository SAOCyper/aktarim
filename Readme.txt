npm http fetch GET 200 https://registry.npmjs.org/@typescript-eslint%2ftypescript-estree 341ms (cache updated)
npm info run puppeteer@25.1.0 postinstall { code: 1, signal: null }
npm info run puppeteer@25.1.0 postinstall { code: 1, signal: null }
npm verbose stack Error: command failed
npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
npm verbose stack     at /usr/local/lib/node_modules/npm/node_modules/@npmcli/arborist/lib/arborist/rebuild.js:329:17
npm verbose stack     at run (/usr/local/lib/node_modules/npm/node_modules/promise-call-limit/dist/commonjs/index.js:67:22)
npm verbose stack     at /usr/local/lib/node_modules/npm/node_modules/promise-call-limit/dist/commonjs/index.js:84:9
npm verbose stack     at new Promise (<anonymous>)
npm verbose stack     at callLimit (/usr/local/lib/node_modules/npm/node_modules/promise-call-limit/dist/commonjs/index.js:35:69)
npm verbose pkgid puppeteer@25.1.0
npm error code 1
npm error path /home/theia/browser-app/node_modules/puppeteer
npm error command failed
npm error command sh -c node install.mjs
npm error **INFO** Skipping Firefox download as instructed.
npm error Error: ERROR: Failed to set up chrome v149.0.7827.22! Set "PUPPETEER_SKIP_DOWNLOAD" env variable to skip download.
npm error     at downloadBrowser (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:26:15)
npm error     at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
npm error     at async Promise.allSettled (index 0)
npm error     at async downloadBrowsers (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:83:21) {
npm error   [cause]: Error: All providers failed for chrome 149.0.7827.22:
npm error     - DefaultProvider: 
npm error       at installWithProviders (file:///home/theia/browser-app/node_modules/@puppeteer/browsers/lib/install.js:108:11)
npm error       at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
npm error       at async install (file:///home/theia/browser-app/node_modules/@puppeteer/browsers/lib/install.js:118:12)
npm error       at async downloadBrowser (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:14:24)
npm error       at async Promise.allSettled (index 0)
npm error       at async downloadBrowsers (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:83:21)
npm error }
npm error Error: ERROR: Failed to set up chrome-headless-shell v149.0.7827.22! Set "PUPPETEER_SKIP_DOWNLOAD" env variable to skip download.
npm error     at downloadBrowser (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:26:15)
npm error     at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
npm error     at async Promise.allSettled (index 1)
npm error     at async downloadBrowsers (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:83:21) {
npm error   [cause]: Error: All providers failed for chrome-headless-shell 149.0.7827.22:
npm error     - DefaultProvider: 
npm error       at installWithProviders (file:///home/theia/browser-app/node_modules/@puppeteer/browsers/lib/install.js:108:11)
npm error       at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
npm error       at async install (file:///home/theia/browser-app/node_modules/@puppeteer/browsers/lib/install.js:118:12)
npm error       at async downloadBrowser (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:14:24)
npm error       at async Promise.allSettled (index 1)
npm error       at async downloadBrowsers (file:///home/theia/browser-app/node_modules/puppeteer/lib/puppeteer/node/install.js:83:21)
npm error }
npm verbose cwd /home/theia
npm verbose os Linux 6.12.69+deb13-amd64
npm verbose node v22.14.0
npm verbose npm  v10.9.2
npm verbose exit 1
npm verbose code 1root@2a85f57da0c0:/home/theia# npm run build:extensions

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

Tasks not run because their dependencies failed or --nx-bail=true:

- @uzay/gsc-files-extension:build
- @uzay/gsc-mission-extension:build
- @uzay/gsc-moon-extension:build
- @uzay/gsc-pass-control-extension:build
- @uzay/gsc-pass-prediction-extension:build
- @uzay/gsc-settings-extension:build

Failed tasks:

- @uzay/gsc-earth-extension:build
