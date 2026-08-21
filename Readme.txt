35.58 npm info run nx@22.7.8 postinstall { code: 0, signal: null }
36.01 
36.01 > postinstall
36.01 > theia check:theia-version
36.01 
36.18 Found 5 missing packages:
36.18 
36.18 * perf_hooks
36.18 * reflect-metadata
36.18 * module
36.18 * busboy
36.18 * sqlite3
36.18 
36.18 
36.21 
36.21 added 2194 packages in 36s
36.21 
36.21 314 packages are looking for funding
36.21   run `npm fund` for details
36.21 npm verbose cwd /home/theia
36.21 npm verbose os Linux 6.12.69+deb13-amd64
36.21 npm verbose node v22.14.0
36.21 npm verbose npm  v10.9.2
36.21 npm verbose exit 0
36.21 npm info ok
36.30 npm verbose cli /usr/local/bin/node /usr/local/bin/npm
36.30 npm info using npm@10.9.2
36.30 npm info using node@v22.14.0
36.30 npm verbose title npm run build:extensions
36.30 npm verbose argv "run" "build:extensions" "--loglevel" "verbose"
36.30 npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_43_16_027Z-
36.31 npm verbose logfile /root/.npm/_logs/2026-08-21T11_43_16_027Z-debug-0.log
36.32 
36.32 > build:extensions
36.32 > lerna run --scope="@uzay/*" build
36.32 
36.79 lerna notice cli v9.0.7
36.86 lerna notice filter including "@uzay/*"
36.86 lerna info filter [ '@uzay/*' ]
36.89 
36.89  Lerna (powered by Nx)   Running target build for 8 projects:
36.89 
36.89 - @uzay/gsc-core-extension
36.89 - @uzay/gsc-earth-extension
36.89 - @uzay/gsc-files-extension
36.89 - @uzay/gsc-mission-extension
36.89 - @uzay/gsc-moon-extension
36.89 - @uzay/gsc-pass-control-extension
36.89 - @uzay/gsc-pass-prediction-extension
36.89 - @uzay/gsc-settings-extension
36.89 
36.89 
36.89 
36.89 > @uzay/gsc-core-extension:build
36.89 
37.11 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
37.11 @uzay/gsc-core-extension: npm info using npm@10.9.2
37.11 @uzay/gsc-core-extension: npm info using node@v22.14.0
37.11 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
37.11 @uzay/gsc-core-extension: npm verbose title npm run build
37.11 @uzay/gsc-core-extension: npm verbose argv "run" "build"
37.11 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T11_43_16_814Z-
37.11 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-21T11_43_16_814Z-debug-0.log
37.12 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
37.12 @uzay/gsc-core-extension: > tsc
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/browser/common-index.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/core/config.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/context/AppSettingsContext.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSatelliteSystem.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSimulationClock.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/hooks/useSocData.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/models/GlobalConfig.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/CesiumEntityManager.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/services/SocDataService.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/features/satellite/utils/cesium-helpers.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/rpc/satellite-rpc.d.ts' because it would overwrite input file.
38.72 @uzay/gsc-core-extension: error TS5055: Cannot write file '/home/theia/extensions/gsc-core-extension/lib/common/theia-entry.d.ts' because it would overwrite input file.
38.74 @uzay/gsc-core-extension: npm verbose stack Error: command failed
38.74 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
38.74 @uzay/gsc-core-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
38.74 @uzay/gsc-core-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
38.74 @uzay/gsc-core-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
38.74 @uzay/gsc-core-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
38.74 @uzay/gsc-core-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
38.74 @uzay/gsc-core-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
38.74 @uzay/gsc-core-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
38.74 @uzay/gsc-core-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
38.74 @uzay/gsc-core-extension: npm verbose pkgid @uzay/gsc-core-extension@1.0.0
38.74 @uzay/gsc-core-extension: npm error Lifecycle script `build` failed with error:
38.74 @uzay/gsc-core-extension: npm error code 1
38.74 @uzay/gsc-core-extension: npm error path /home/theia/extensions/gsc-core-extension
38.74 @uzay/gsc-core-extension: npm error workspace @uzay/gsc-core-extension@1.0.0
38.74 @uzay/gsc-core-extension: npm error location /home/theia/extensions/gsc-core-extension
38.74 @uzay/gsc-core-extension: npm error command failed
38.74 @uzay/gsc-core-extension: npm error command sh -c tsc
38.74 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
38.74 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
38.74 @uzay/gsc-core-extension: npm verbose node v22.14.0
38.74 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
38.74 @uzay/gsc-core-extension: npm verbose exit 1
38.74 @uzay/gsc-core-extension: npm verbose code 1
38.75 
38.75 
38.75 
38.75  Lerna (powered by Nx)   Running target build for 8 projects failed
38.75 
38.75 Tasks not run because their dependencies failed or --nx-bail=true:
38.75 
38.75 - @uzay/gsc-earth-extension:build
38.75 - @uzay/gsc-files-extension:build
38.75 - @uzay/gsc-mission-extension:build
38.75 - @uzay/gsc-moon-extension:build
38.75 - @uzay/gsc-pass-control-extension:build
38.75 - @uzay/gsc-pass-prediction-extension:build
38.75 - @uzay/gsc-settings-extension:build
38.75 
38.75 Failed tasks:
38.75 
38.75 - @uzay/gsc-core-extension:build
38.75 
38.76 npm verbose cwd /home/theia
38.76 npm verbose os Linux 6.12.69+deb13-amd64
38.76 npm verbose node v22.14.0
38.76 npm verbose npm  v10.9.2
38.76 npm verbose exit 130
38.76 npm verbose code 130
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
