44.22 > build:browser:prod
44.22 > npm run compile && npm run build:extensions && cd browser-app && npm run build:prod
44.22 
44.28 npm info it worked if it ends with ok
44.28 npm verb cli [
44.28 npm verb cli   '/usr/local/bin/node',
44.28 npm verb cli   '/home/theia/node_modules/.bin/npm',
44.28 npm verb cli   'run',
44.28 npm verb cli   'compile'
44.28 npm verb cli ]
44.28 npm info using npm@2.15.12
44.28 npm info using node@v22.14.0
44.34 npm verb run-script [ 'precompile', 'compile', 'postcompile' ]
44.34 npm info precompile gsc.scheduling.theia@
44.34 
44.34 > gsc.scheduling.theia@ precompile /home/theia
44.34 > lerna run clean
44.34 
44.79 lerna notice cli v9.0.7
44.87 
44.87  Lerna (powered by Nx)   Running target clean for 10 projects:
44.87 
44.87 - gsc-browser-app
44.87 - gsc-browser-app-cesium
44.87 - @uzay/gsc-core-extension
44.87 - @uzay/gsc-earth-extension
44.87 - @uzay/gsc-files-extension
44.87 - @uzay/gsc-mission-extension
44.87 - @uzay/gsc-moon-extension
44.87 - @uzay/gsc-pass-control-extension
44.87 - @uzay/gsc-pass-prediction-extension
44.87 - @uzay/gsc-settings-extension
44.87 
44.87 
44.87 
44.87 > @uzay/gsc-core-extension:clean
44.87 
45.11 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.11 @uzay/gsc-core-extension: npm info using npm@10.9.2
45.11 @uzay/gsc-core-extension: npm info using node@v22.14.0
45.11 @uzay/gsc-core-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.11 @uzay/gsc-core-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.11 @uzay/gsc-core-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.11 @uzay/gsc-core-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.11 @uzay/gsc-core-extension: npm warn config `--include=optional` to include them.
45.11 @uzay/gsc-core-extension: npm warn config
45.11 @uzay/gsc-core-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.11 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
45.11 @uzay/gsc-core-extension: npm verbose title npm run clean
45.11 @uzay/gsc-core-extension: npm verbose argv "run" "clean"
45.11 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_537Z-
45.11 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_537Z-debug-0.log
45.12 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 clean
45.12 @uzay/gsc-core-extension: > rimraf lib
45.18 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
45.18 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.18 @uzay/gsc-core-extension: npm verbose node v22.14.0
45.18 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
45.18 @uzay/gsc-core-extension: npm verbose exit 0
45.18 @uzay/gsc-core-extension: npm info ok
45.19 
45.19 > @uzay/gsc-earth-extension:clean
45.19 
45.20 
45.20 > @uzay/gsc-files-extension:clean
45.20 
45.20 
45.20 > @uzay/gsc-mission-extension:clean
45.20 
45.21 
45.21 > @uzay/gsc-moon-extension:clean
45.21 
45.21 
45.21 > @uzay/gsc-pass-control-extension:clean
45.21 
45.21 
45.21 > @uzay/gsc-pass-prediction-extension:clean
45.21 
45.22 
45.22 > @uzay/gsc-settings-extension:clean
45.22 
45.41 @uzay/gsc-files-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.41 @uzay/gsc-files-extension: npm info using npm@10.9.2
45.41 @uzay/gsc-files-extension: npm info using node@v22.14.0
45.41 @uzay/gsc-files-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.41 @uzay/gsc-files-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.41 @uzay/gsc-files-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.41 @uzay/gsc-files-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.41 @uzay/gsc-files-extension: npm warn config `--include=optional` to include them.
45.41 @uzay/gsc-files-extension: npm warn config
45.41 @uzay/gsc-files-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.41 @uzay/gsc-files-extension: npm info config found workspace root at /home/theia
45.41 @uzay/gsc-files-extension: npm verbose title npm run clean
45.41 @uzay/gsc-files-extension: npm verbose argv "run" "clean"
45.41 @uzay/gsc-files-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_846Z-
45.41 @uzay/gsc-files-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_846Z-debug-0.log
45.42 @uzay/gsc-mission-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.42 @uzay/gsc-mission-extension: npm info using npm@10.9.2
45.42 @uzay/gsc-mission-extension: npm info using node@v22.14.0
45.42 @uzay/gsc-mission-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.42 @uzay/gsc-mission-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.42 @uzay/gsc-mission-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.42 @uzay/gsc-mission-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.42 @uzay/gsc-mission-extension: npm warn config `--include=optional` to include them.
45.42 @uzay/gsc-mission-extension: npm warn config
45.42 @uzay/gsc-mission-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.42 @uzay/gsc-mission-extension: npm info config found workspace root at /home/theia
45.42 @uzay/gsc-mission-extension: npm verbose title npm run clean
45.42 @uzay/gsc-mission-extension: npm verbose argv "run" "clean"
45.42 @uzay/gsc-mission-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_858Z-
45.43 @uzay/gsc-mission-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_858Z-debug-0.log
45.43 @uzay/gsc-pass-control-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.43 @uzay/gsc-pass-control-extension: npm info using npm@10.9.2
45.43 @uzay/gsc-pass-control-extension: npm info using node@v22.14.0
45.43 @uzay/gsc-pass-control-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.43 @uzay/gsc-pass-control-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.43 @uzay/gsc-pass-control-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.43 @uzay/gsc-pass-control-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.43 @uzay/gsc-pass-control-extension: npm warn config `--include=optional` to include them.
45.43 @uzay/gsc-pass-control-extension: npm warn config
45.43 @uzay/gsc-pass-control-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.43 @uzay/gsc-pass-control-extension: npm info config found workspace root at /home/theia
45.43 @uzay/gsc-files-extension: > @uzay/gsc-files-extension@1.0.0 clean
45.43 @uzay/gsc-files-extension: > rimraf lib
45.43 @uzay/gsc-pass-control-extension: npm verbose title npm run clean
45.43 @uzay/gsc-pass-control-extension: npm verbose argv "run" "clean"
45.43 @uzay/gsc-pass-control-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_862Z-
45.43 @uzay/gsc-pass-control-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_862Z-debug-0.log
45.43 @uzay/gsc-moon-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.43 @uzay/gsc-moon-extension: npm info using npm@10.9.2
45.43 @uzay/gsc-moon-extension: npm info using node@v22.14.0
45.43 @uzay/gsc-moon-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.43 @uzay/gsc-moon-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.43 @uzay/gsc-moon-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.43 @uzay/gsc-moon-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.43 @uzay/gsc-moon-extension: npm warn config `--include=optional` to include them.
45.43 @uzay/gsc-moon-extension: npm warn config
45.43 @uzay/gsc-moon-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.43 @uzay/gsc-moon-extension: npm warn config ignoring workspace config at /home/theia/extensions/gsc-moon-extension/.npmrc
45.43 @uzay/gsc-moon-extension: npm info config found workspace root at /home/theia
45.43 @uzay/gsc-moon-extension: npm verbose title npm run clean
45.43 @uzay/gsc-moon-extension: npm verbose argv "run" "clean"
45.43 @uzay/gsc-moon-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_867Z-
45.43 @uzay/gsc-moon-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_867Z-debug-0.log
45.44 @uzay/gsc-mission-extension: > @uzay/gsc-mission-extension@1.0.0 clean
45.44 @uzay/gsc-mission-extension: > rimraf lib
45.44 @uzay/gsc-earth-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.44 @uzay/gsc-pass-control-extension: > @uzay/gsc-pass-control-extension@1.0.0 clean
45.44 @uzay/gsc-pass-control-extension: > rimraf lib
45.44 @uzay/gsc-earth-extension: npm info using npm@10.9.2
45.44 @uzay/gsc-earth-extension: npm info using node@v22.14.0
45.44 @uzay/gsc-earth-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.44 @uzay/gsc-earth-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.44 @uzay/gsc-earth-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.44 @uzay/gsc-earth-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.44 @uzay/gsc-earth-extension: npm warn config `--include=optional` to include them.
45.44 @uzay/gsc-earth-extension: npm warn config
45.44 @uzay/gsc-earth-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.44 @uzay/gsc-earth-extension: npm info config found workspace root at /home/theia
45.44 @uzay/gsc-settings-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.44 @uzay/gsc-settings-extension: npm info using npm@10.9.2
45.44 @uzay/gsc-settings-extension: npm info using node@v22.14.0
45.44 @uzay/gsc-settings-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.44 @uzay/gsc-settings-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.44 @uzay/gsc-settings-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.44 @uzay/gsc-settings-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.44 @uzay/gsc-settings-extension: npm warn config `--include=optional` to include them.
45.44 @uzay/gsc-settings-extension: npm warn config
45.44 @uzay/gsc-settings-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.44 @uzay/gsc-settings-extension: npm info config found workspace root at /home/theia
45.44 @uzay/gsc-earth-extension: npm verbose title npm run clean
45.44 @uzay/gsc-earth-extension: npm verbose argv "run" "clean"
45.44 @uzay/gsc-earth-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_856Z-
45.44 @uzay/gsc-settings-extension: npm verbose title npm run clean
45.44 @uzay/gsc-settings-extension: npm verbose argv "run" "clean"
45.44 @uzay/gsc-earth-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_856Z-debug-0.log
45.44 @uzay/gsc-settings-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_874Z-
45.44 @uzay/gsc-settings-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_874Z-debug-0.log
45.45 @uzay/gsc-moon-extension: > @uzay/gsc-moon-extension@1.0.0 clean
45.45 @uzay/gsc-moon-extension: > rimraf lib
45.46 @uzay/gsc-settings-extension: > @uzay/gsc-settings-extension@1.0.0 clean
45.46 @uzay/gsc-settings-extension: > rimraf lib
45.46 @uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 clean
45.46 @uzay/gsc-earth-extension: > rimraf lib
45.47 @uzay/gsc-pass-prediction-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.47 @uzay/gsc-pass-prediction-extension: npm info using npm@10.9.2
45.47 @uzay/gsc-pass-prediction-extension: npm info using node@v22.14.0
45.47 @uzay/gsc-pass-prediction-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.47 @uzay/gsc-pass-prediction-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.47 @uzay/gsc-pass-prediction-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
45.47 @uzay/gsc-pass-prediction-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.47 @uzay/gsc-pass-prediction-extension: npm warn config `--include=optional` to include them.
45.47 @uzay/gsc-pass-prediction-extension: npm warn config
45.47 @uzay/gsc-pass-prediction-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
45.47 @uzay/gsc-pass-prediction-extension: npm info config found workspace root at /home/theia
45.47 @uzay/gsc-pass-prediction-extension: npm verbose title npm run clean
45.47 @uzay/gsc-pass-prediction-extension: npm verbose argv "run" "clean"
45.47 @uzay/gsc-pass-prediction-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_14_59_902Z-
45.47 @uzay/gsc-pass-prediction-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_14_59_902Z-debug-0.log
45.47 @uzay/gsc-mission-extension: npm verbose cwd /home/theia/extensions/gsc-mission-extension
45.47 @uzay/gsc-mission-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.47 @uzay/gsc-mission-extension: npm verbose node v22.14.0
45.47 @uzay/gsc-mission-extension: npm verbose npm  v10.9.2
45.47 @uzay/gsc-mission-extension: npm verbose exit 0
45.47 @uzay/gsc-mission-extension: npm info ok
45.47 @uzay/gsc-files-extension: npm verbose cwd /home/theia/extensions/gsc-files-extension
45.47 @uzay/gsc-files-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.47 @uzay/gsc-pass-control-extension: npm verbose cwd /home/theia/extensions/gsc-pass-control-extension
45.47 @uzay/gsc-files-extension: npm verbose node v22.14.0
45.47 @uzay/gsc-files-extension: npm verbose npm  v10.9.2
45.47 @uzay/gsc-files-extension: npm verbose exit 0
45.47 @uzay/gsc-files-extension: npm info ok
45.47 @uzay/gsc-pass-control-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.47 @uzay/gsc-pass-control-extension: npm verbose node v22.14.0
45.47 @uzay/gsc-pass-control-extension: npm verbose npm  v10.9.2
45.47 @uzay/gsc-pass-control-extension: npm verbose exit 0
45.47 @uzay/gsc-pass-control-extension: npm info ok
45.48 @uzay/gsc-pass-prediction-extension: > @uzay/gsc-pass-prediction-extension@1.0.0 clean
45.48 @uzay/gsc-pass-prediction-extension: > rimraf lib
45.50 @uzay/gsc-settings-extension: npm verbose cwd /home/theia/extensions/gsc-settings-extension
45.50 @uzay/gsc-settings-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.50 @uzay/gsc-settings-extension: npm verbose node v22.14.0
45.50 @uzay/gsc-settings-extension: npm verbose npm  v10.9.2
45.50 @uzay/gsc-settings-extension: npm verbose exit 0
45.50 @uzay/gsc-settings-extension: npm info ok
45.51 @uzay/gsc-moon-extension: npm verbose cwd /home/theia/extensions/gsc-moon-extension
45.51 @uzay/gsc-moon-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.51 @uzay/gsc-moon-extension: npm verbose node v22.14.0
45.51 @uzay/gsc-moon-extension: npm verbose npm  v10.9.2
45.51 @uzay/gsc-moon-extension: npm verbose exit 0
45.51 @uzay/gsc-moon-extension: npm info ok
45.52 @uzay/gsc-pass-prediction-extension: npm verbose cwd /home/theia/extensions/gsc-pass-prediction-extension
45.52 @uzay/gsc-pass-prediction-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.52 @uzay/gsc-pass-prediction-extension: npm verbose node v22.14.0
45.52 @uzay/gsc-pass-prediction-extension: npm verbose npm  v10.9.2
45.52 @uzay/gsc-pass-prediction-extension: npm verbose exit 0
45.52 @uzay/gsc-pass-prediction-extension: npm info ok
45.53 @uzay/gsc-earth-extension: npm verbose cwd /home/theia/extensions/gsc-earth-extension
45.53 @uzay/gsc-earth-extension: npm verbose os Linux 6.12.69+deb13-amd64
45.53 @uzay/gsc-earth-extension: npm verbose node v22.14.0
45.53 @uzay/gsc-earth-extension: npm verbose npm  v10.9.2
45.53 @uzay/gsc-earth-extension: npm verbose exit 0
45.53 @uzay/gsc-earth-extension: npm info ok
45.54 
45.54 > gsc-browser-app:clean
45.54 
45.55 
45.55 > gsc-browser-app-cesium:clean
45.55 
45.76 gsc-browser-app: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.76 gsc-browser-app: npm info using npm@10.9.2
45.76 gsc-browser-app: npm info using node@v22.14.0
45.76 gsc-browser-app: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.76 gsc-browser-app: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.76 gsc-browser-app: npm warn config shrinkwrap Use the --package-lock setting instead.
45.76 gsc-browser-app: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.76 gsc-browser-app: npm warn config `--include=optional` to include them.
45.76 gsc-browser-app: npm warn config
45.76 gsc-browser-app: npm warn config       Default value does install optional deps unless otherwise omitted.
45.76 gsc-browser-app: npm info config found workspace root at /home/theia
45.76 gsc-browser-app: npm verbose title npm run clean
45.76 gsc-browser-app: npm verbose argv "run" "clean"
45.76 gsc-browser-app: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_15_00_190Z-
45.76 gsc-browser-app-cesium: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
45.76 gsc-browser-app-cesium: npm info using npm@10.9.2
45.76 gsc-browser-app-cesium: npm info using node@v22.14.0
45.76 gsc-browser-app-cesium: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
45.76 gsc-browser-app-cesium: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
45.76 gsc-browser-app-cesium: npm warn config shrinkwrap Use the --package-lock setting instead.
45.76 gsc-browser-app-cesium: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
45.76 gsc-browser-app-cesium: npm warn config `--include=optional` to include them.
45.76 gsc-browser-app-cesium: npm warn config
45.76 gsc-browser-app-cesium: npm warn config       Default value does install optional deps unless otherwise omitted.
45.76 gsc-browser-app-cesium: npm info config found workspace root at /home/theia
45.76 gsc-browser-app: npm verbose logfile /root/.npm/_logs/2026-08-24T13_15_00_190Z-debug-0.log
45.76 gsc-browser-app-cesium: npm verbose title npm run clean
45.76 gsc-browser-app-cesium: npm verbose argv "run" "clean"
45.76 gsc-browser-app-cesium: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_15_00_192Z-
45.76 gsc-browser-app-cesium: npm verbose logfile /root/.npm/_logs/2026-08-24T13_15_00_192Z-debug-0.log
45.77 gsc-browser-app: > gsc-browser-app@1.0.0 clean
45.77 gsc-browser-app: > theia clean && rimraf node_modules
45.77 gsc-browser-app-cesium: > gsc-browser-app-cesium@1.0.0 clean
45.77 gsc-browser-app-cesium: > theia clean && rimraf node_modules
46.28 gsc-browser-app-cesium: npm verbose cwd /home/theia/browser-app-cesium
46.28 gsc-browser-app-cesium: npm verbose os Linux 6.12.69+deb13-amd64
46.28 gsc-browser-app-cesium: npm verbose node v22.14.0
46.28 gsc-browser-app-cesium: npm verbose npm  v10.9.2
46.28 gsc-browser-app-cesium: npm verbose exit 0
46.28 gsc-browser-app-cesium: npm info ok
46.33 gsc-browser-app: npm verbose cwd /home/theia/browser-app
46.33 gsc-browser-app: npm verbose os Linux 6.12.69+deb13-amd64
46.33 gsc-browser-app: npm verbose node v22.14.0
46.33 gsc-browser-app: npm verbose npm  v10.9.2
46.33 gsc-browser-app: npm verbose exit 0
46.33 gsc-browser-app: npm info ok
46.34 
46.34 
46.34 
46.34  Lerna (powered by Nx)   Successfully ran target clean for 10 projects
46.34 
46.34 
46.38 npm verb unsafe-perm in lifecycle true
46.38 npm info compile gsc.scheduling.theia@
46.38 
46.38 > gsc.scheduling.theia@ compile /home/theia
46.38 > lerna run --scope="@uzay/gsc-core-extension" build && lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile
46.38 
46.84 lerna notice cli v9.0.7
46.88 lerna notice filter including "@uzay/gsc-core-extension"
46.88 lerna info filter [ '@uzay/gsc-core-extension' ]
46.91 
46.91 > @uzay/gsc-core-extension:build
46.91 
47.11 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
47.11 @uzay/gsc-core-extension: npm info using npm@10.9.2
47.11 @uzay/gsc-core-extension: npm info using node@v22.14.0
47.11 @uzay/gsc-core-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
47.11 @uzay/gsc-core-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
47.11 @uzay/gsc-core-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
47.11 @uzay/gsc-core-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
47.11 @uzay/gsc-core-extension: npm warn config `--include=optional` to include them.
47.11 @uzay/gsc-core-extension: npm warn config
47.11 @uzay/gsc-core-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
47.11 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
47.11 @uzay/gsc-core-extension: npm verbose title npm run build
47.11 @uzay/gsc-core-extension: npm verbose argv "run" "build"
47.11 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_15_01_548Z-
47.12 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_15_01_548Z-debug-0.log
47.13 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
47.13 @uzay/gsc-core-extension: > tsc
48.17 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
48.17 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
48.17 @uzay/gsc-core-extension: npm verbose node v22.14.0
48.17 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
48.17 @uzay/gsc-core-extension: npm verbose exit 0
48.17 @uzay/gsc-core-extension: npm info ok
48.18 
48.18 
48.18 
48.18  Lerna (powered by Nx)   Successfully ran target build for project @uzay/gsc-core-extension
48.18 
48.18 
48.67 lerna notice cli v9.0.7
48.71 lerna notice filter including "@uzay/*"
48.71 lerna info filter [ '@uzay/*' ]
48.74 
48.74  Lerna (powered by Nx)   Running target build for 8 projects:
48.74 
48.74 - @uzay/gsc-core-extension
48.74 - @uzay/gsc-earth-extension
48.74 - @uzay/gsc-files-extension
48.74 - @uzay/gsc-mission-extension
48.74 - @uzay/gsc-moon-extension
48.74 - @uzay/gsc-pass-control-extension
48.74 - @uzay/gsc-pass-prediction-extension
48.74 - @uzay/gsc-settings-extension
48.74 
48.74 
48.75 
48.75 > @uzay/gsc-core-extension:build
48.75 
48.96 @uzay/gsc-core-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
48.96 @uzay/gsc-core-extension: npm info using npm@10.9.2
48.96 @uzay/gsc-core-extension: npm info using node@v22.14.0
48.96 @uzay/gsc-core-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
48.96 @uzay/gsc-core-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
48.96 @uzay/gsc-core-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
48.96 @uzay/gsc-core-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
48.96 @uzay/gsc-core-extension: npm warn config `--include=optional` to include them.
48.96 @uzay/gsc-core-extension: npm warn config
48.96 @uzay/gsc-core-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
48.96 @uzay/gsc-core-extension: npm info config found workspace root at /home/theia
48.96 @uzay/gsc-core-extension: npm verbose title npm run build
48.96 @uzay/gsc-core-extension: npm verbose argv "run" "build"
48.96 @uzay/gsc-core-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_15_03_388Z-
48.96 @uzay/gsc-core-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_15_03_388Z-debug-0.log
48.97 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
48.97 @uzay/gsc-core-extension: > tsc
49.98 @uzay/gsc-core-extension: npm verbose cwd /home/theia/extensions/gsc-core-extension
49.98 @uzay/gsc-core-extension: npm verbose os Linux 6.12.69+deb13-amd64
49.98 @uzay/gsc-core-extension: npm verbose node v22.14.0
49.98 @uzay/gsc-core-extension: npm verbose npm  v10.9.2
49.98 @uzay/gsc-core-extension: npm verbose exit 0
49.98 @uzay/gsc-core-extension: npm info ok
49.99 
49.99 > @uzay/gsc-earth-extension:build
49.99 
50.19 @uzay/gsc-earth-extension: npm verbose cli /usr/local/bin/node /usr/local/bin/npm
50.19 @uzay/gsc-earth-extension: npm info using npm@10.9.2
50.19 @uzay/gsc-earth-extension: npm info using node@v22.14.0
50.19 @uzay/gsc-earth-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
50.19 @uzay/gsc-earth-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
50.19 @uzay/gsc-earth-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
50.19 @uzay/gsc-earth-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
50.19 @uzay/gsc-earth-extension: npm warn config `--include=optional` to include them.
50.19 @uzay/gsc-earth-extension: npm warn config
50.19 @uzay/gsc-earth-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
50.19 @uzay/gsc-earth-extension: npm info config found workspace root at /home/theia
50.20 @uzay/gsc-earth-extension: npm verbose title npm run build
50.20 @uzay/gsc-earth-extension: npm verbose argv "run" "build"
50.20 @uzay/gsc-earth-extension: npm verbose logfile logs-max:10 dir:/root/.npm/_logs/2026-08-24T13_15_04_628Z-
50.20 @uzay/gsc-earth-extension: npm verbose logfile /root/.npm/_logs/2026-08-24T13_15_04_628Z-debug-0.log
50.21 @uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
50.21 @uzay/gsc-earth-extension: > tsc
51.46 @uzay/gsc-earth-extension: src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
51.46 @uzay/gsc-earth-extension: src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
51.46 @uzay/gsc-earth-extension: src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
51.46 @uzay/gsc-earth-extension: src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
51.46 @uzay/gsc-earth-extension: src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
51.48 @uzay/gsc-earth-extension: npm verbose stack Error: command failed
51.48 @uzay/gsc-earth-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:22:22)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at spawnWithShell (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:124:10)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at promiseSpawn (/usr/local/lib/node_modules/npm/node_modules/@npmcli/promise-spawn/lib/index.js:12:12)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at runScriptPkg (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script-pkg.js:77:13)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at runScript (/usr/local/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/run-script.js:9:12)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at #run (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:131:13)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at RunScript.execWorkspaces (/usr/local/lib/node_modules/npm/lib/commands/run-script.js:63:24)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
51.48 @uzay/gsc-earth-extension: npm verbose stack     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5)
51.48 @uzay/gsc-earth-extension: npm verbose pkgid @uzay/gsc-earth-extension@1.0.0
51.48 @uzay/gsc-earth-extension: npm error Lifecycle script `build` failed with error:
51.48 @uzay/gsc-earth-extension: npm error code 2
51.48 @uzay/gsc-earth-extension: npm error path /home/theia/extensions/gsc-earth-extension
51.48 @uzay/gsc-earth-extension: npm error workspace @uzay/gsc-earth-extension@1.0.0
51.48 @uzay/gsc-earth-extension: npm error location /home/theia/extensions/gsc-earth-extension
51.48 @uzay/gsc-earth-extension: npm error command failed
51.48 @uzay/gsc-earth-extension: npm error command sh -c tsc
51.48 @uzay/gsc-earth-extension: npm verbose cwd /home/theia/extensions/gsc-earth-extension
51.48 @uzay/gsc-earth-extension: npm verbose os Linux 6.12.69+deb13-amd64
51.48 @uzay/gsc-earth-extension: npm verbose node v22.14.0
51.48 @uzay/gsc-earth-extension: npm verbose npm  v10.9.2
51.48 @uzay/gsc-earth-extension: npm verbose exit 2
51.48 @uzay/gsc-earth-extension: npm verbose code 2
51.48 
51.48 
51.48 
51.48  Lerna (powered by Nx)   Running target build for 8 projects failed
51.48 
51.48 Tasks not run because their dependencies failed or --nx-bail=true:
51.48 
51.48 - @uzay/gsc-files-extension:build
51.48 - @uzay/gsc-mission-extension:build
51.48 - @uzay/gsc-moon-extension:build
51.48 - @uzay/gsc-pass-control-extension:build
51.48 - @uzay/gsc-pass-prediction-extension:build
51.48 - @uzay/gsc-settings-extension:build
51.48 
51.48 Failed tasks:
51.48 
51.48 - @uzay/gsc-earth-extension:build
51.48 
51.52 
51.52 npm verb unsafe-perm in lifecycle true
51.52 npm info gsc.scheduling.theia@ Failed to exec compile script
51.52 npm verb stack Error: gsc.scheduling.theia@ compile: `lerna run --scope="@uzay/gsc-core-extension" build && lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile`
51.52 npm verb stack Exit status 130
51.52 npm verb stack     at EventEmitter.<anonymous> (/home/theia/node_modules/npm/lib/utils/lifecycle.js:217:16)
51.52 npm verb stack     at EventEmitter.emit (node:events:518:28)
51.52 npm verb stack     at ChildProcess.<anonymous> (/home/theia/node_modules/npm/lib/utils/spawn.js:24:14)
51.52 npm verb stack     at ChildProcess.emit (node:events:518:28)
51.52 npm verb stack     at maybeClose (node:internal/child_process:1101:16)
51.52 npm verb stack     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
51.52 npm verb pkgid gsc.scheduling.theia@
51.52 npm verb cwd /home/theia
51.52 npm ERR! Linux 6.12.69+deb13-amd64
51.52 npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "compile"
51.52 npm ERR! node v22.14.0
51.52 npm ERR! npm  v2.15.12
51.52 npm ERR! code ELIFECYCLE
51.52 npm ERR! gsc.scheduling.theia@ compile: `lerna run --scope="@uzay/gsc-core-extension" build && lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile`
51.52 npm ERR! Exit status 130
51.52 npm ERR! 
51.52 npm ERR! Failed at the gsc.scheduling.theia@ compile script 'lerna run --scope="@uzay/gsc-core-extension" build && lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile'.
51.52 npm ERR! This is most likely a problem with the gsc.scheduling.theia package,
51.52 npm ERR! not with npm itself.
51.52 npm ERR! Tell the author that this fails on your system:
51.52 npm ERR!     lerna run --scope="@uzay/gsc-core-extension" build && lerna run --scope="@uzay/*" build --concurrency=1 && lerna run compile
51.52 npm ERR! You can get information on how to open an issue for this project with:
51.52 npm ERR!     npm bugs gsc.scheduling.theia
51.52 npm ERR! Or if that isn't available, you can get their info via:
51.52 npm ERR! 
51.53 npm ERR!     npm owner ls gsc.scheduling.theia
51.53 npm ERR! There is likely additional logging output above.
51.53 npm verb exit [ 1, true ]
51.53 
51.53 npm ERR! Please include the following file with any support request:
51.53 npm ERR!     /home/theia/npm-debug.log
51.54 npm verbose cwd /home/theia
51.54 npm verbose os Linux 6.12.69+deb13-amd64
51.54 npm verbose node v22.14.0
51.54 npm verbose npm  v10.9.2
51.54 npm verbose exit 1
51.54 npm verbose code 1
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
