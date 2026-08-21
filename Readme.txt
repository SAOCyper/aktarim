38.20 npm info run puppeteer@25.1.0 postinstall browser-app-cesium/node_modules/puppeteer node install.mjs
38.20 npm info run puppeteer@25.1.0 postinstall browser-app/node_modules/puppeteer node install.mjs
38.21 npm info run core-js@2.6.12 postinstall node_modules/core-js node -e "try{require('./postinstall')}catch(e){}"
38.21 npm info run esbuild@0.25.12 postinstall node_modules/esbuild node install.js
38.21 npm info run node-pty@1.2.0-beta.12 postinstall node_modules/node-pty node scripts/post-install.js
38.22 npm info run nx@22.7.8 postinstall node_modules/nx node -e "try{require('./dist/bin/post-install')}catch(e){}"
38.22 npm info run esbuild@0.28.2 postinstall browser-app-cesium/node_modules/@theia/application-manager/node_modules/esbuild node install.js
38.22 npm info run esbuild@0.28.2 postinstall browser-app/node_modules/@theia/application-manager/node_modules/esbuild node install.js
38.24 npm info run core-js@2.6.12 postinstall { code: 0, signal: null }
38.24 npm info run node-pty@1.2.0-beta.12 postinstall { code: 0, signal: null }
38.27 npm info run esbuild@0.25.12 postinstall { code: 0, signal: null }
38.27 npm info run esbuild@0.28.2 postinstall { code: 0, signal: null }
38.27 npm info run esbuild@0.28.2 postinstall { code: 0, signal: null }
38.30 npm info run puppeteer@25.1.0 postinstall { code: 0, signal: null }
38.30 npm info run puppeteer@25.1.0 postinstall { code: 0, signal: null }
38.38 npm info run nx@22.7.8 postinstall { code: 0, signal: null }
38.79 
38.79 > postinstall
38.79 > theia check:theia-version
38.79 
38.97 Found 5 missing packages:
38.97 
38.97 * perf_hooks
38.97 * reflect-metadata
38.97 * module
38.97 * busboy
38.97 * sqlite3
38.97 
38.97 
38.99 
38.99 added 2194 packages in 39s
38.99 
38.99 314 packages are looking for funding
38.99   run `npm fund` for details
38.99 npm verbose cwd /home/theia
38.99 npm verbose os Linux 6.12.69+deb13-amd64
38.99 npm verbose node v22.14.0
38.99 npm verbose npm  v10.9.2
38.99 npm verbose exit 0
38.99 npm info ok
39.10 npm verbose cli /usr/local/bin/node /usr/local/bin/npm
39.10 npm info using npm@10.9.2
39.10 npm info using node@v22.14.0
39.10 npm verbose title npm run build:extensions
39.10 npm verbose argv "run" "build:extensions" "--loglevel" "verbose"
39.10 npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_39_20_152Z-
39.10 npm verbose logfile /root/.npm/_logs/2026-08-21T11_39_20_152Z-debug-0.log
39.11 
39.11 > build:extensions
39.11 > lerna run --scope="@uzay/*" build
39.11 
39.58 lerna notice cli v9.0.7
39.69 lerna notice filter including "@uzay/*"
39.69 lerna info filter [ '@uzay/*' ]
39.72 
39.72  Lerna (powered by Nx)   Running target build for 8 projects:
39.72 
39.72 - @uzay/gsc-core-extension
39.72 - @uzay/gsc-earth-extension
39.72 - @uzay/gsc-files-extension
39.72 - @uzay/gsc-mission-extension
39.72 - @uzay/gsc-moon-extension
39.72 - @uzay/gsc-pass-control-extension
39.72 - @uzay/gsc-pass-prediction-extension
39.72 - @uzay/gsc-settings-extension
39.72 
39.72 
39.72 
39.72 > @uzay/gsc-core-extension:build
39.72 
39.93 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
39.93 @uzay/gsc-core-extension: npm info using npm@10.9.2
39.93 @uzay/gsc-core-extension: npm info using node@v22.14.0
39.93 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
39.93 @uzay/gsc-core-extension: npm verbose title npm run build
39.93 @uzay/gsc-core-extension: npm verbose argv "run" "build"
39.93 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_39_20_961Z-
39.93 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-21T11_39_20_961Z-debug-0.log
39.94 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
39.94 @uzay/gsc-core-extension: > tsc
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/browser/common-index.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/core/config.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/context/AppSettingsContext.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSatelliteSystem.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSimulationClock.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSocData.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/models/GlobalConfig.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/CesiumEntityManager.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/SocDataService.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/utils/cesium-helpers.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/rpc/satellite-rpc.d.ts' because it would overwrite input file.
41.49 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/theia-entry.d.ts' because it would overwrite input file.
41.51 @uzay/gsc-core-extension: npm verbose stack Error: command failed
41.51 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
41.51 @uzay/gsc-core-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
41.51 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
41.51 @uzay/gsc-core-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
41.51 @uzay/gsc-core-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
41.51 @uzay/gsc-core-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
41.51 @uzay/gsc-core-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
41.51 @uzay/gsc-core-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
41.51 @uzay/gsc-core-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
41.51 @uzay/gsc-core-extension: npm verbose pkgid @uzay/gsc-core-extension@1.0.0
41.51 @uzay/gsc-core-extension: npm error Lifecycle script `build` failed with error:
41.51 @uzay/gsc-core-extension: npm error code 1
41.51 @uzay/gsc-core-extension: npm error path /home/theia/extensions/gsc-core-extension
41.51 @uzay/gsc-core-extension: npm error workspace @uzay/gsc-core-extension@1.0.0
41.51 @uzay/gsc-core-extension: npm error location /home/theia/extensions/gsc-core-extension
41.51 @uzay/gsc-core-extension: npm error command failed
41.51 @uzay/gsc-core-extension: npm error command sh -c tsc
41.51 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
41.51 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
41.51 @uzay/gsc-core-extension: npm verbose node v22.14.0
41.51 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
41.51 @uzay/gsc-core-extension: npm verbose exit 1
41.51 @uzay/gsc-core-extension: npm verbose code 1
41.52 
41.52 
41.52 
41.52  Lerna (powered by Nx)   Running target build for 8 projects failed
41.52 
41.52 Tasks not run because their dependencies failed or --nx-bail=true:
41.52 
41.52 - @uzay/gsc-earth-extension:build
41.52 - @uzay/gsc-files-extension:build
41.52 - @uzay/gsc-mission-extension:build
41.52 - @uzay/gsc-moon-extension:build
41.52 - @uzay/gsc-pass-control-extension:build
41.52 - @uzay/gsc-pass-prediction-extension:build
41.52 - @uzay/gsc-settings-extension:build
41.52 
41.52 Failed tasks:
41.52 
41.52 - @uzay/gsc-core-extension:build
41.52 
41.53 npm verbose cwd /home/theia
41.53 npm verbose os Linux 6.12.69+deb13-amd64
41.53 npm verbose node v22.14.0
41.53 npm verbose npm  v10.9.2
41.53 npm verbose exit 130
41.53 npm verbose code 130
------
Dockerfile:33
--------------------
  32 |     # Download plugins and build application production mode
  33 | >>> RUN npm install --verbose && \
  34 | >>>     npm run build:extensions --verbose && \
  35 | >>>     npm run download:plugins --verbose && \
  36 | >>>     npm run build:browser:prod --verbose && \
  37 | >>>     find . -name \*.ts -o -name \*.ts.map -o -name \*.spec.* -type f -delete && \
  38 | >>>     rm -rf .git gsc-core-extension
  39 |     
--------------------
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npm run build:extensions --verbose &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.map -o -name \\*.spec.* -type f -delete &&     rm -rf .git gsc-core-extension" did not complete successfully: exit code: 130
mert@mertunubol:~/Development/gsc.scheduling.theia$ 
