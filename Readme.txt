28.27   run `npm fund` for details
28.27 npm verbose cwd /home/theia
28.27 npm verbose os Linux 6.12.69+deb13-amd64
28.27 npm verbose node v22.14.0
28.27 npm verbose npm  v10.9.2
28.27 npm verbose exit 0
28.27 npm info ok
28.99 lerna notice cli v9.0.7
29.07 lerna notice filter including "@uzay/gsc-core-extension"
29.07 lerna info filter [ '@uzay/gsc-core-extension' ]
29.09 
29.09 > @uzay/gsc-core-extension:build
29.09 
29.32 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
29.32 @uzay/gsc-core-extension: > tsc
30.41 
30.41 
30.41 
30.41  Lerna (powered by Nx)   Successfully ran target build for project @uzay/gsc-core-extension
30.41 
30.41 
30.53 npm verbose cli /usr/local/bin/node /usr/local/bin/npm
30.53 npm info using npm@10.9.2
30.53 npm info using node@v22.14.0
30.53 npm verbose title npm run build:extensions
30.53 npm verbose argv "run" "build:extensions" "--concurrency" "1" "--skip-nx-cache" "--loglevel" "verbose"
30.53 npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T12_42_51_406Z-
30.53 npm verbose logfile /root/.npm/_logs/2026-08-21T12_42_51_406Z-debug-0.log
30.55 
30.55 > build:extensions
30.55 > lerna run --scope="@uzay/*" build --concurrency=1
30.55 
31.00 lerna notice cli v9.0.7
31.07 lerna notice filter including "@uzay/*"
31.07 lerna info filter [ '@uzay/*' ]
31.09 
31.09  Lerna (powered by Nx)   Running target build for 8 projects:
31.09 
31.09 - @uzay/gsc-core-extension
31.09 - @uzay/gsc-earth-extension
31.09 - @uzay/gsc-files-extension
31.09 - @uzay/gsc-mission-extension
31.09 - @uzay/gsc-moon-extension
31.09 - @uzay/gsc-pass-control-extension
31.09 - @uzay/gsc-pass-prediction-extension
31.09 - @uzay/gsc-settings-extension
31.09 
31.09 
31.09 
31.09 > @uzay/gsc-core-extension:build
31.09 
31.30 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
31.30 @uzay/gsc-core-extension: npm info using npm@10.9.2
31.30 @uzay/gsc-core-extension: npm info using node@v22.14.0
31.30 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
31.30 @uzay/gsc-core-extension: npm verbose title npm run build
31.30 @uzay/gsc-core-extension: npm verbose argv "run" "build"
31.30 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T12_42_52_158Z-
31.31 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-21T12_42_52_158Z-debug-0.log
31.32 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
31.32 @uzay/gsc-core-extension: > tsc
32.30 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
32.30 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
32.30 @uzay/gsc-core-extension: npm verbose node v22.14.0
32.30 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
32.30 @uzay/gsc-core-extension: npm verbose exit 0
32.30 @uzay/gsc-core-extension: npm info ok
32.31 
32.31 > @uzay/gsc-earth-extension:build
32.31 
32.53 @uzay/gsc-earth-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
32.53 @uzay/gsc-earth-extension: npm info using npm@10.9.2
32.53 @uzay/gsc-earth-extension: npm info using node@v22.14.0
32.53 @uzay/gsc-earth-extension: npm info config found workspace root at /home/theia
32.53 @uzay/gsc-earth-extension: npm verbose title npm run build
32.53 @uzay/gsc-earth-extension: npm verbose argv "run" "build"
32.53 @uzay/gsc-earth-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-21T12_42_53_385Z-
32.53 @uzay/gsc-earth-extension: npm verbose logfile /root/.npm/_logs/2026-08-21T12_42_53_385Z-debug-0.log
32.54 @uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
32.54 @uzay/gsc-earth-extension: > tsc
33.81 @uzay/gsc-earth-extension: src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
33.81 @uzay/gsc-earth-extension: src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
33.81 @uzay/gsc-earth-extension: src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
33.81 @uzay/gsc-earth-extension: src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
33.81 @uzay/gsc-earth-extension: src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
33.82 @uzay/gsc-earth-extension: npm verbose stack Error: command failed
33.82 @uzay/gsc-earth-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
33.82 @uzay/gsc-earth-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
33.82 @uzay/gsc-earth-extension: npm verbose pkgid @uzay/gsc-earth-extension@1.0.0
33.82 @uzay/gsc-earth-extension: npm error Lifecycle script `build` failed with error:
33.82 @uzay/gsc-earth-extension: npm error code 2
33.82 @uzay/gsc-earth-extension: npm error path /home/theia/extensions/gsc-earth-extension
33.82 @uzay/gsc-earth-extension: npm error workspace @uzay/gsc-earth-extension@1.0.0
33.82 @uzay/gsc-earth-extension: npm error location /home/theia/extensions/gsc-earth-extension
33.82 @uzay/gsc-earth-extension: npm error command failed
33.82 @uzay/gsc-earth-extension: npm error command sh -c tsc
33.82 @uzay/gsc-earth-extension: npm verbose cwd /home/theia/extensions/gsc-earth-extension
33.82 @uzay/gsc-earth-extension: npm verbose os Linux 6.12.69+deb13-amd64
33.82 @uzay/gsc-earth-extension: npm verbose node v22.14.0
33.82 @uzay/gsc-earth-extension: npm verbose npm  v10.9.2
33.82 @uzay/gsc-earth-extension: npm verbose exit 2
33.82 @uzay/gsc-earth-extension: npm verbose code 2
33.83 
33.83 
33.83 
33.83  Lerna (powered by Nx)   Running target build for 8 projects failed
33.83 
33.83 Tasks not run because their dependencies failed or --nx-bail=true:
33.83 
33.83 - @uzay/gsc-files-extension:build
33.83 - @uzay/gsc-mission-extension:build
33.83 - @uzay/gsc-moon-extension:build
33.83 - @uzay/gsc-pass-control-extension:build
33.83 - @uzay/gsc-pass-prediction-extension:build
33.83 - @uzay/gsc-settings-extension:build
33.83 
33.83 Failed tasks:
33.83 
33.83 - @uzay/gsc-earth-extension:build
33.83 
33.84 npm verbose cwd /home/theia
33.84 npm verbose os Linux 6.12.69+deb13-amd64
33.84 npm verbose node v22.14.0
33.84 npm verbose npm  v10.9.2
33.84 npm verbose exit 130
33.84 npm verbose code 130
------
Dockerfile:33
--------------------
  32 |     # Download plugins and build application production mode
  33 | >>> RUN npm install --verbose && \
  34 | >>>     npx lerna run build --scope="@uzay/gsc-core-extension" --skip-nx-cache && \
  35 | >>>     npm run build:extensions --concurrency=1 --skip-nx-cache --verbose && \
  36 | >>>     npm run download:plugins --verbose && \
  37 | >>>     npm run build:browser:prod --verbose && \
  38 | >>>     find . -name \*.ts -o -name \*.ts.map -o -name \*.spec.* -type f -delete && \
  39 | >>>     rm -rf .git gsc-core-extension
  40 |     
--------------------
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npx lerna run build --scope=\"@uzay/gsc-core-extension\" --skip-nx-cache &&     npm run build:extensions --concurrency=1 --skip-nx-cache --verbose &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.map -o -name \\*.spec.* -type f -delete &&     rm -rf .git gsc-core-extension" did not complete successfully: exit code: 130
