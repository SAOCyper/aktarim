npm http fetch GET 200 https://registry.npmjs.org/normalize-package-data 37ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/init-package-json 38ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/read-installed 57ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/npm-install-checks 278ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/npm-package-arg 279ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/npm-registry-client 280ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/@modelcontextprotocol%2fsdk 55ms (cache revalidated)
npm http fetch GET 200 https://registry.npmjs.org/nx 46ms (cache revalidated)
npm info run @uzay/gsc-core-extension@1.0.0 prepare { code: 0, signal: null }
npm http fetch GET 200 https://registry.npmjs.org/config-chain 41ms (cache revalidated)
npm info run @uzay/gsc-earth-extension@1.0.0 prepare { code: 1, signal: null }
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
npm verbose pkgid @uzay/gsc-earth-extension@1.0.0
npm error code 1
npm error path /home/theia/extensions/gsc-earth-extension
npm error command failed
npm error command sh -c npm run clean && npm run build
npm error > @uzay/gsc-earth-extension@1.0.0 clean /home/theia/extensions/gsc-earth-extension
npm error > rimraf lib
npm error
npm error
npm error > @uzay/gsc-earth-extension@1.0.0 build /home/theia/extensions/gsc-earth-extension
npm error > tsc
npm error
npm error src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/node/rpc/satellite-client-manager.ts(2,33): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/node/rpc/satellite-server-impl.ts(2,84): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/node/services/satellite-application.service.ts(2,50): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error src/node/soc-backend-module.ts(10,94): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
npm error npm info it worked if it ends with ok
npm error npm verb cli [
npm error npm verb cli   '/usr/local/bin/node',
npm error npm verb cli   '/home/theia/node_modules/.bin/npm',
npm error npm verb cli   'run',
npm error npm verb cli   'clean'
npm error npm verb cli ]
npm error npm info using npm@2.15.12
npm error npm info using node@v22.14.0
npm error npm verb run-script [ 'preclean', 'clean', 'postclean' ]
npm error npm info preclean @uzay/gsc-earth-extension@1.0.0
npm error npm info clean @uzay/gsc-earth-extension@1.0.0
npm error npm verb unsafe-perm in lifecycle true
npm error npm info postclean @uzay/gsc-earth-extension@1.0.0
npm error npm verb exit [ 0, true ]
npm error npm info ok 
npm error npm info it worked if it ends with ok
npm error npm verb cli [
npm error npm verb cli   '/usr/local/bin/node',
npm error npm verb cli   '/home/theia/node_modules/.bin/npm',
npm error npm verb cli   'run',
npm error npm verb cli   'build'
npm error npm verb cli ]
npm error npm info using npm@2.15.12
npm error npm info using node@v22.14.0
npm error npm verb run-script [ 'prebuild', 'build', 'postbuild' ]
npm error npm info prebuild @uzay/gsc-earth-extension@1.0.0
npm error npm info build @uzay/gsc-earth-extension@1.0.0
npm error
npm error npm verb unsafe-perm in lifecycle true
npm error npm info @uzay/gsc-earth-extension@1.0.0 Failed to exec build script
npm error npm verb stack Error: @uzay/gsc-earth-extension@1.0.0 build: `tsc`
npm error npm verb stack Exit status 2
npm error npm verb stack     at EventEmitter.<anonymous> (/home/theia/node_modules/npm/lib/utils/lifecycle.js:217:16)
npm error npm verb stack     at EventEmitter.emit (node:events:518:28)
npm error npm verb stack     at ChildProcess.<anonymous> (/home/theia/node_modules/npm/lib/utils/spawn.js:24:14)
npm error npm verb stack     at ChildProcess.emit (node:events:518:28)
npm error npm verb stack     at maybeClose (node:internal/child_process:1101:16)
npm error npm verb stack     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
npm error npm verb pkgid @uzay/gsc-earth-extension@1.0.0
npm error npm verb cwd /home/theia/extensions/gsc-earth-extension
npm error npm ERR! Linux 6.12.69+deb13-amd64
npm error npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "build"
npm error npm ERR! node v22.14.0
npm error npm ERR! npm  v2.15.12
npm error npm ERR! code ELIFECYCLE
npm error npm ERR! @uzay/gsc-earth-extension@1.0.0 build: `tsc`
npm error npm ERR! Exit status 2
npm error npm ERR! 
npm error npm ERR! Failed at the @uzay/gsc-earth-extension@1.0.0 build script 'tsc'.
npm error npm ERR! This is most likely a problem with the @uzay/gsc-earth-extension package,
npm error npm ERR! not with npm itself.
npm error npm ERR! Tell the author that this fails on your system:
npm error npm ERR!     tsc
npm error npm ERR! You can get information on how to open an issue for this project with:
npm error npm ERR!     npm bugs @uzay/gsc-earth-extension
npm error npm ERR! Or if that isn't available, you can get their info via:
npm error npm ERR! 
npm error npm ERR!     npm owner ls @uzay/gsc-earth-extension
npm error npm ERR! There is likely additional logging output above.
npm error npm verb exit [ 1, true ]
npm error
npm error npm ERR! Please include the following file with any support request:
npm error npm ERR!     /home/theia/extensions/gsc-earth-extension/npm-debug.log
npm verbose cwd /home/theia
npm verbose os Linux 6.12.69+deb13-amd64
npm verbose node v22.14.0
npm verbose npm  v10.9.2
npm verbose exit 1
npm verbose code 1
npm error A complete log of this run can be found in: /root/.npm/_logs/2026-08-03T11_05_50_959Z-debug-0.log
