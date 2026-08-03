> gsc.scheduling.theia@ compile /home/theia
> lerna run compile

lerna notice cli v9.0.7

 Lerna (powered by Nx)   Running target compile for 2 projects:

- gsc-browser-app
- gsc-browser-app-cesium

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

> gsc-browser-app-cesium:compile


> gsc-browser-app:compile

gsc-browser-app-cesium: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
gsc-browser-app-cesium: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
gsc-browser-app-cesium: npm warn config shrinkwrap Use the --package-lock setting instead.
gsc-browser-app-cesium: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
gsc-browser-app-cesium: npm warn config `--include=optional` to include them.
gsc-browser-app-cesium: npm warn config
gsc-browser-app-cesium: npm warn config       Default value does install optional deps unless otherwise omitted.
gsc-browser-app-cesium: > gsc-browser-app-cesium@1.0.0 compile
gsc-browser-app-cesium: > tsc -b
gsc-browser-app: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
gsc-browser-app: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
gsc-browser-app: npm warn config shrinkwrap Use the --package-lock setting instead.
gsc-browser-app: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
gsc-browser-app: npm warn config `--include=optional` to include them.
gsc-browser-app: npm warn config
gsc-browser-app: npm warn config       Default value does install optional deps unless otherwise omitted.
gsc-browser-app: > gsc-browser-app@1.0.0 compile
gsc-browser-app: > tsc -b
gsc-browser-app-cesium: error TS5083: Cannot read file '/home/theia/gsc-core-extension/tsconfig.json'.
gsc-browser-app-cesium: npm error Lifecycle script `compile` failed with error:
gsc-browser-app-cesium: npm error code 2
gsc-browser-app-cesium: npm error path /home/theia/browser-app-cesium
gsc-browser-app-cesium: npm error workspace gsc-browser-app-cesium@1.0.0
gsc-browser-app-cesium: npm error location /home/theia/browser-app-cesium
gsc-browser-app-cesium: npm error command failed
gsc-browser-app-cesium: npm error command sh -c tsc -b

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Running target compile for 2 projects failed

Failed tasks:

- gsc-browser-app-cesium:compile


npm ERR! Linux 6.12.69+deb13-amd64
npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "compile"
npm ERR! node v22.14.0
npm ERR! npm  v2.15.12
npm ERR! code ELIFECYCLE
npm ERR! gsc.scheduling.theia@ compile: `lerna run compile`
npm ERR! Exit status 130
npm ERR! 
npm ERR! Failed at the gsc.scheduling.theia@ compile script 'lerna run compile'.
npm ERR! This is most likely a problem with the gsc.scheduling.theia package,
npm ERR! not with npm itself.
npm ERR! Tell the author that this fails on your system:
npm ERR!     lerna run compile
npm ERR! You can get information on how to open an issue for this project with:
npm ERR!     npm bugs gsc.scheduling.theia
npm ERR! Or if that isn't available, you can get their info via:
npm ERR! 
npm ERR!     npm owner ls gsc.scheduling.theia
npm ERR! There is likely additional logging output above.

npm ERR! Please include the following file with any support request:
npm ERR!     /home/theia/npm-debug.log
