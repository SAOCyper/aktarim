root@2a85f57da0c0:/home/theia# find extensions/gsc-core-extension/ -maxdepth 3
extensions/gsc-core-extension/
extensions/gsc-core-extension/public
extensions/gsc-core-extension/public/earth
extensions/gsc-core-extension/public/moon
extensions/gsc-core-extension/.gitignore
extensions/gsc-core-extension/src
extensions/gsc-core-extension/src/browser
extensions/gsc-core-extension/src/browser/common-index.ts
extensions/gsc-core-extension/src/browser/satellite-client-impl.ts
extensions/gsc-core-extension/src/browser/soc-core-frontend-contribution.ts
extensions/gsc-core-extension/src/browser/soc-core-frontend-module.ts
extensions/gsc-core-extension/src/common
extensions/gsc-core-extension/src/common/features
extensions/gsc-core-extension/src/common/rpc
extensions/gsc-core-extension/src/common/main.tsx
extensions/gsc-core-extension/src/common/theia-entry.ts
extensions/gsc-core-extension/src/common/assets
extensions/gsc-core-extension/src/common/App.css
extensions/gsc-core-extension/src/common/core
extensions/gsc-core-extension/src/common/App.tsx
extensions/gsc-core-extension/src/common/index.css
extensions/gsc-core-extension/src/node
extensions/gsc-core-extension/src/node/rpc
extensions/gsc-core-extension/src/node/soc-backend-contribution.ts
extensions/gsc-core-extension/src/node/static-assets-server-contribution.ts
extensions/gsc-core-extension/src/node/services
extensions/gsc-core-extension/src/node/logging
extensions/gsc-core-extension/src/node/soc-core-backend-module.ts
extensions/gsc-core-extension/tsconfig.tsbuildinfo
extensions/gsc-core-extension/tsconfig.json
extensions/gsc-core-extension/package.jsonnpm http fetch GET 200 https://registry.npmjs.org/@typescript-eslint%2ftypescript-estree 341ms (cache updated)
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
npm verbose code 1
