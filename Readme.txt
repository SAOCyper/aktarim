38.47 npm info run nx@22.7.8 postinstall node_modules/nx node -e "try{require('./dist/bin/post-install')}catch(e){}"
38.47 npm info run esbuild@0.28.2 postinstall browser-app-cesium/node_modules/@theia/application-manager/node_modules/esbuild node install.js
38.47 npm info run esbuild@0.28.2 postinstall browser-app/node_modules/@theia/application-manager/node_modules/esbuild node install.js
38.49 npm info run core-js@2.6.12 postinstall { code: 0, signal: null }
38.49 npm info run node-pty@1.2.0-beta.12 postinstall { code: 0, signal: null }
38.51 npm info run esbuild@0.25.12 postinstall { code: 0, signal: null }
38.53 npm info run esbuild@0.28.2 postinstall { code: 0, signal: null }
38.53 npm info run esbuild@0.28.2 postinstall { code: 0, signal: null }
38.55 npm info run puppeteer@25.1.0 postinstall { code: 0, signal: null }
38.55 npm info run puppeteer@25.1.0 postinstall { code: 0, signal: null }
38.63 npm info run nx@22.7.8 postinstall { code: 0, signal: null }
39.05 
39.05 > postinstall
39.05 > theia check:theia-version
39.05 
39.17 Found 3 missing packages:
39.17 
39.17 * perf_hooks
39.17 * reflect-metadata
39.17 * module
39.17 
39.17 
39.19 
39.19 added 2199 packages in 39s
39.19 
39.19 314 packages are looking for funding
39.19   run `npm fund` for details
39.19 npm verbose cwd /home/theia
39.19 npm verbose os Linux 6.12.69+deb13-amd64
39.19 npm verbose node v22.14.0
39.19 npm verbose npm  v10.9.2
39.19 npm verbose exit 0
39.19 npm info ok
39.29 npm verbose cli /usr/local/bin/node /usr/local/bin/npm
39.29 npm info using npm@10.9.2
39.29 npm info using node@v22.14.0
39.30 npm verbose title npm run build:extensions
39.30 npm verbose argv "run" "build:extensions" "--loglevel" "verbose"
39.30 npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_47_33_582Z-
39.30 npm verbose logfile /root/.npm/_logs/2026-08-21T11_47_33_582Z-debug-0.log
39.31 
39.31 > build:extensions
39.31 > lerna run --scope="@uzay/*" build
39.31 
39.78 lerna notice cli v9.0.7
39.86 lerna notice filter including "@uzay/*"
39.86 lerna info filter [ '@uzay/*' ]
39.89 
39.89  Lerna (powered by Nx)   Running target build for 8 projects:
39.89 
39.89 - @uzay/gsc-core-extension
39.89 - @uzay/gsc-earth-extension
39.89 - @uzay/gsc-files-extension
39.89 - @uzay/gsc-mission-extension
39.89 - @uzay/gsc-moon-extension
39.89 - @uzay/gsc-pass-control-extension
39.89 - @uzay/gsc-pass-prediction-extension
39.89 - @uzay/gsc-settings-extension
39.89 
39.89 
39.89 
39.89 > @uzay/gsc-core-extension:build
39.89 
40.10 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
40.10 @uzay/gsc-core-extension: npm info using npm@10.9.2
40.10 @uzay/gsc-core-extension: npm info using node@v22.14.0
40.10 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
40.10 @uzay/gsc-core-extension: npm verbose title npm run build
40.10 @uzay/gsc-core-extension: npm verbose argv "run" "build"
40.10 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_47_34_369Z-
40.10 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-21T11_47_34_369Z-debug-0.log
40.12 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
40.12 @uzay/gsc-core-extension: > tsc
41.66 @uzay/gsc-core-extension: src/node/rpc/satellite-client-manager.ts(2,33): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
41.69 @uzay/gsc-core-extension: npm verbose stack Error: command failed
41.69 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
41.69 @uzay/gsc-core-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
41.69 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
41.69 @uzay/gsc-core-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
41.69 @uzay/gsc-core-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
41.69 @uzay/gsc-core-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
41.69 @uzay/gsc-core-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
41.69 @uzay/gsc-core-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
41.69 @uzay/gsc-core-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
41.69 @uzay/gsc-core-extension: npm verbose pkgid @uzay/gsc-core-extension@1.0.0
41.69 @uzay/gsc-core-extension: npm error Lifecycle script `build` failed with error:
41.69 @uzay/gsc-core-extension: npm error code 2
41.69 @uzay/gsc-core-extension: npm error path /home/theia/extensions/gsc-core-extension
41.69 @uzay/gsc-core-extension: npm error workspace @uzay/gsc-core-extension@1.0.0
41.69 @uzay/gsc-core-extension: npm error location /home/theia/extensions/gsc-core-extension
41.69 @uzay/gsc-core-extension: npm error command failed
41.69 @uzay/gsc-core-extension: npm error command sh -c tsc
41.69 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
41.69 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
41.69 @uzay/gsc-core-extension: npm verbose node v22.14.0
41.69 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
41.69 @uzay/gsc-core-extension: npm verbose exit 2
41.69 @uzay/gsc-core-extension: npm verbose code 2
41.70 
41.70  Lerna (powered by Nx)   Running target build for 8 projects failed
41.70 
41.70 Tasks not run because their dependencies failed or --nx-bail=true:
41.70 
41.70 - @uzay/gsc-earth-extension:build
41.70 - @uzay/gsc-files-extension:build
41.70 - @uzay/gsc-mission-extension:build
41.70 - @uzay/gsc-moon-extension:build
41.70 - @uzay/gsc-pass-control-extension:build
41.70 
41.70 
41.70 - @uzay/gsc-pass-prediction-extension:build
41.70 - @uzay/gsc-settings-extension:build
41.70 
41.70 Failed tasks:
41.70 
41.70 - @uzay/gsc-core-extension:build
41.70 
41.72 npm verbose cwd /home/theia
41.72 npm verbose os Linux 6.12.69+deb13-amd64
41.72 npm verbose node v22.14.0
41.72 npm verbose npm  v10.9.2
41.72 npm verbose exit 130
41.72 npm verbose code 130
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
