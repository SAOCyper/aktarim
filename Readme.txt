 @uzay/gsc-core-extension: npm info ok
46.94 
46.94 > @uzay/gsc-earth-extension:build
46.94 
47.15 @uzay/gsc-earth-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
47.15 @uzay/gsc-earth-extension: npm info using npm@10.9.2
47.15 @uzay/gsc-earth-extension: npm info using node@v22.14.0
47.15 @uzay/gsc-earth-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
47.15 @uzay/gsc-earth-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
47.15 @uzay/gsc-earth-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
47.15 @uzay/gsc-earth-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
47.15 @uzay/gsc-earth-extension: npm warn config `--include=optional` to include them.
47.15 @uzay/gsc-earth-extension: npm warn config
47.15 @uzay/gsc-earth-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
47.15 @uzay/gsc-earth-extension: npm info config found workspace root at /home/theia
47.15 @uzay/gsc-earth-extension: npm verbose title npm run build
47.15 @uzay/gsc-earth-extension: npm verbose argv "run" "build"
47.15 @uzay/gsc-earth-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_09_52_819Z-
47.15 @uzay/gsc-earth-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_09_52_819Z-debug-0.log
47.16 @uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
47.16 @uzay/gsc-earth-extension: > tsc
48.41 @uzay/gsc-earth-extension: src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
48.41 @uzay/gsc-earth-extension: src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
48.41 @uzay/gsc-earth-extension: src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
48.41 @uzay/gsc-earth-extension: src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
48.41 @uzay/gsc-earth-extension: src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
48.43 @uzay/gsc-earth-extension: npm verbose stack Error: command failed
48.43 @uzay/gsc-earth-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
48.43 @uzay/gsc-earth-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
48.43 @uzay/gsc-earth-extension: npm verbose pkgid @uzay/gsc-earth-extension@1.0.0
48.43 @uzay/gsc-earth-extension: npm error Lifecycle script `build` failed with error:
48.43 @uzay/gsc-earth-extension: npm error code 2
48.43 @uzay/gsc-earth-extension: npm error path /home/theia/extensions/gsc-earth-extension
48.43 @uzay/gsc-earth-extension: npm error workspace @uzay/gsc-earth-extension@1.0.0
48.43 @uzay/gsc-earth-extension: npm error location /home/theia/extensions/gsc-earth-extension
48.43 @uzay/gsc-earth-extension: npm error command failed
48.43 @uzay/gsc-earth-extension: npm error command sh -c tsc
48.43 @uzay/gsc-earth-extension: npm verbose cwd /home/theia/extensions/gsc-earth-extension
48.43 @uzay/gsc-earth-extension: npm verbose os Linux 6.12.69+deb13-amd64
48.43 @uzay/gsc-earth-extension: npm verbose node v22.14.0
48.43 @uzay/gsc-earth-extension: npm verbose npm  v10.9.2
48.43 @uzay/gsc-earth-extension: npm verbose exit 2
48.43 @uzay/gsc-earth-extension: npm verbose code 2
48.44 
48.44 
48.44 
48.44  Lerna (powered by Nx)   Running target build for 8 projects failed
48.44 
48.44 Tasks not run because their dependencies failed or --nx-bail=true:
48.44 
48.44 - @uzay/gsc-files-extension:build
48.44 - @uzay/gsc-mission-extension:build
48.44 - @uzay/gsc-moon-extension:build
48.44 - @uzay/gsc-pass-control-extension:build
48.44 - @uzay/gsc-pass-prediction-extension:build
48.44 - @uzay/gsc-settings-extension:build
48.44 
48.44 Failed tasks:
48.44 
48.44 - @uzay/gsc-earth-extension:build
48.44 
48.48 
48.48 npm verb unsafe-perm in lifecycle true
48.48 npm info gsc.scheduling.theia@ Failed to exec compile script
48.48 npm verb stack Error: gsc.scheduling.theia@ compile: `lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile`
48.48 npm verb stack Exit status 130
48.48 npm verb stack     at EventEmitter.<anonymous> (/home/theia/node_modules/npm/lib/utils/lifecycle.js:217:16)
48.48 npm verb stack     at EventEmitter.emit (node:events:518:28)
48.48 npm verb stack     at ChildProcess.<anonymous> (/home/theia/node_modules/npm/lib/utils/spawn.js:24:14)
48.48 npm verb stack     at ChildProcess.emit (node:events:518:28)
48.48 npm verb stack     at maybeClose (node:internal/child_process:1101:16)
48.48 npm verb stack     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
48.48 npm verb pkgid gsc.scheduling.theia@
48.48 npm verb cwd /home/theia
48.48 npm ERR! Linux 6.12.69+deb13-amd64
48.48 npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "compile"
48.48 npm ERR! node v22.14.0
48.48 npm ERR! npm  v2.15.12
48.48 npm ERR! code ELIFECYCLE
48.48 npm ERR! gsc.scheduling.theia@ compile: `lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile`
48.48 npm ERR! Exit status 130
48.48 npm ERR! 
48.48 npm ERR! Failed at the gsc.scheduling.theia@ compile script 'lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile'.
48.48 npm ERR! This is most likely a problem with the gsc.scheduling.theia package,
48.48 npm ERR! not with npm itself.
48.48 npm ERR! Tell the author that this fails on your system:
48.48 npm ERR!     lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile
48.48 npm ERR! You can get information on how to open an issue for this project with:
48.48 npm ERR!     npm bugs gsc.scheduling.theia
48.48 npm ERR! Or if that isn't available, you can get their info via:
48.48 npm ERR! 
48.48 npm ERR!     npm owner ls gsc.scheduling.theia
48.48 npm ERR! There is likely additional logging output above.
48.48 npm verb exit [ 1, true ]
48.48 
48.48 npm ERR! Please include the following file with any support request:
48.48 npm ERR!     /home/theia/npm-debug.log
48.49 npm verbose cwd /home/theia
48.49 npm verbose os Linux 6.12.69+deb13-amd64
48.49 npm verbose node v22.14.0
48.49 npm verbose npm  v10.9.2
48.49 npm verbose exit 1
48.49 npm verbose code 1
------
Dockerfile:33
--------------------
  32 |     # Download plugins and build application production mode
  33 | >>> RUN npm install --verbose && \
  34 | >>>     npx lerna run build --scope="@uzay/*" --concurrency=1 --skip-nx-cache && \
  35 | >>>     #npm run build:extensions --concurrency=1 --skip-nx-cache --verbose && \
  36 | >>>     npm run download:plugins --verbose && \
  37 | >>>     npm run build:browser:prod --verbose && \
  38 | >>>     find . -name \*.ts -o -name \*.ts.map -o -name \*.spec.* -type f -delete && \
  39 | >>>     rm -rf .git gsc-core-extension
  40 |     
--------------------
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npx lerna run build --scope=\"@uzay/*\" --concurrency=1 --skip-nx-cache &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.map -o -name \\*.spec.* -type f -delete &&     rm -rf .git gsc-core-extension" did not complete successfully: exit code: 1
