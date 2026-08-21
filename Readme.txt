9 npm info run keytar@7.9.0 install { code: 0, signal: null }
37.02 npm info run sqlite3@5.1.7 install { code: 0, signal: null }
38.15 npm info run @theia/ffmpeg@1.74.1 install { code: 0, signal: null }
38.17 npm info run @theia/ffmpeg@1.74.1 install { code: 0, signal: null }
40.50 npm info run drivelist@12.0.2 install { code: 0, signal: null }
40.50 npm info run puppeteer@25.1.0 postinstall browser-app-cesium/node_modules/puppeteer node install.mjs
40.51 npm info run puppeteer@25.1.0 postinstall browser-app/node_modules/puppeteer node install.mjs
40.51 npm info run core-js@2.6.12 postinstall node_modules/core-js node -e "try{require('./postinstall')}catch(e){}"
40.52 npm info run esbuild@0.25.12 postinstall node_modules/esbuild node install.js
40.52 npm info run node-pty@1.2.0-beta.12 postinstall node_modules/node-pty node scripts/post-install.js
40.52 npm info run nx@22.7.8 postinstall node_modules/nx node -e "try{require('./dist/bin/post-install')}catch(e){}"
40.53 npm info run esbuild@0.28.2 postinstall browser-app-cesium/node_modules/@theia/application-manager/node_modules/esbuild node install.js
40.53 npm info run esbuild@0.28.2 postinstall browser-app/node_modules/@theia/application-manager/node_modules/esbuild node install.js
40.55 npm info run core-js@2.6.12 postinstall { code: 0, signal: null }
40.56 npm info run esbuild@0.25.12 postinstall { code: 0, signal: null }
40.56 npm info run node-pty@1.2.0-beta.12 postinstall { code: 0, signal: null }
40.59 npm info run esbuild@0.28.2 postinstall { code: 0, signal: null }
40.59 npm info run esbuild@0.28.2 postinstall { code: 0, signal: null }
40.61 npm info run puppeteer@25.1.0 postinstall { code: 0, signal: null }
40.62 npm info run puppeteer@25.1.0 postinstall { code: 0, signal: null }
40.69 npm info run nx@22.7.8 postinstall { code: 0, signal: null }
41.10 
41.10 > postinstall
41.10 > theia check:theia-version
41.10 
41.27 Found 5 missing packages:
41.27 
41.27 * perf_hooks
41.27 * reflect-metadata
41.27 * module
41.27 * busboy
41.27 * sqlite3
41.27 
41.27 
41.29 
41.29 added 2194 packages in 41s
41.29 
41.29 314 packages are looking for funding
41.29   run `npm fund` for details
41.29 npm verbose cwd /home/theia
41.29 npm verbose os Linux 6.12.69+deb13-amd64
41.29 npm verbose node v22.14.0
41.29 npm verbose npm  v10.9.2
41.29 npm verbose exit 0
41.29 npm info ok
41.39 npm verbose cli /usr/local/bin/node /usr/local/bin/npm
41.39 npm info using npm@10.9.2
41.39 npm info using node@v22.14.0
41.39 npm verbose title npm run build:extensions
41.39 npm verbose argv "run" "build:extensions" "--loglevel" "verbose"
41.39 npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_33_59_248Z-
41.39 npm verbose logfile /root/.npm/_logs/2026-08-21T11_33_59_248Z-debug-0.log
41.40 
41.40 > build:extensions
41.40 > lerna run --scope="@uzay/*" build
41.40 
41.87 lerna notice cli v9.0.7
41.97 lerna notice filter including "@uzay/*"
41.97 lerna info filter [ '@uzay/*' ]
42.00 
42.00  Lerna (powered by Nx)   Running target build for 8 projects:
42.00 
42.00 - @uzay/gsc-core-extension
42.00 - @uzay/gsc-earth-extension
42.00 - @uzay/gsc-files-extension
42.00 - @uzay/gsc-mission-extension
42.00 - @uzay/gsc-moon-extension
42.00 - @uzay/gsc-pass-control-extension
42.00 - @uzay/gsc-pass-prediction-extension
42.00 - @uzay/gsc-settings-extension
42.00 
42.00 
42.01 
42.01 > @uzay/gsc-core-extension:build
42.01 
42.23 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
42.23 @uzay/gsc-core-extension: npm info using npm@10.9.2
42.23 @uzay/gsc-core-extension: npm info using node@v22.14.0
42.23 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
42.23 @uzay/gsc-core-extension: npm verbose title npm run build
42.23 @uzay/gsc-core-extension: npm verbose argv "run" "build"
42.23 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_34_00_062Z-
42.23 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-21T11_34_00_062Z-debug-0.log
42.24 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
42.24 @uzay/gsc-core-extension: > tsc
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/browser/common-index.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/core/config.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/context/AppSettingsContext.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSatelliteSystem.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSimulationClock.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSocData.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/models/GlobalConfig.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/CesiumEntityManager.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/SocDataService.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/utils/cesium-helpers.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/rpc/satellite-rpc.d.ts' because it would overwrite input file.
43.79 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/theia-entry.d.ts' because it would overwrite input file.
43.81 @uzay/gsc-core-extension: npm verbose stack Error: command failed
43.81 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
43.81 @uzay/gsc-core-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
43.81 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
43.81 @uzay/gsc-core-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
43.81 @uzay/gsc-core-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
43.81 @uzay/gsc-core-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
43.81 @uzay/gsc-core-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
43.81 @uzay/gsc-core-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
43.81 @uzay/gsc-core-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
43.81 @uzay/gsc-core-extension: npm verbose pkgid @uzay/gsc-core-extension@1.0.0
43.81 @uzay/gsc-core-extension: npm error Lifecycle script `build` failed with error:
43.81 @uzay/gsc-core-extension: npm error code 1
43.81 @uzay/gsc-core-extension: npm error path /home/theia/extensions/gsc-core-extension
43.81 @uzay/gsc-core-extension: npm error workspace @uzay/gsc-core-extension@1.0.0
43.81 @uzay/gsc-core-extension: npm error location /home/theia/extensions/gsc-core-extension
43.81 @uzay/gsc-core-extension: npm error command failed
43.81 @uzay/gsc-core-extension: npm error command sh -c tsc
43.81 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
43.81 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
43.81 @uzay/gsc-core-extension: npm verbose node v22.14.0
43.81 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
43.81 @uzay/gsc-core-extension: npm verbose exit 1
43.81 @uzay/gsc-core-extension: npm verbose code 1
43.83 
43.83 
43.83 
43.83  Lerna (powered by Nx)   Running target build for 8 projects failed
43.83 
43.83 Tasks not run because their dependencies failed or --nx-bail=true:
43.83 
43.83 - @uzay/gsc-earth-extension:build
43.83 - @uzay/gsc-files-extension:build
43.83 - @uzay/gsc-mission-extension:build
43.83 - @uzay/gsc-moon-extension:build
43.83 - @uzay/gsc-pass-control-extension:build
43.83 - @uzay/gsc-pass-prediction-extension:build
43.83 - @uzay/gsc-settings-extension:build
43.83 
43.83 Failed tasks:
43.83 
43.83 - @uzay/gsc-core-extension:build
43.83 
43.85 npm verbose cwd /home/theia
43.85 npm verbose os Linux 6.12.69+deb13-amd64
43.85 npm verbose node v22.14.0
43.85 npm verbose npm  v10.9.2
43.85 npm verbose exit 130
43.85 npm verbose code 130
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
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npm run build:extensions --verbose &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.m
