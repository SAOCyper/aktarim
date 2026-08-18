4.24 
54.25 npm verb unsafe-perm in lifecycle true
54.25 npm info postbuild:extensions gsc.scheduling.theia@
54.26 npm verb exit [ 0, true ]
54.26 npm info ok 
54.32 npm info it worked if it ends with ok
54.32 npm verb cli [
54.32 npm verb cli   '/usr/local/bin/node',
54.32 npm verb cli   '/home/theia/node_modules/.bin/npm',
54.32 npm verb cli   'run',
54.32 npm verb cli   'build:prod'
54.32 npm verb cli ]
54.32 npm info using npm@2.15.12
54.32 npm info using node@v22.14.0
54.37 npm verb run-script [ 'prebuild:prod', 'build:prod', 'postbuild:prod' ]
54.37 npm info prebuild:prod gsc-browser-app@1.0.0
54.38 npm info build:prod gsc-browser-app@1.0.0
54.38 
54.38 > gsc-browser-app@1.0.0 build:prod /home/theia/browser-app
54.38 > npm run -s compile && npm run -s bundle:prod
54.38 
55.23 native node modules are already rebuilt for browser
55.63 Could not resolve optional peer dependency '@theia/electron'. Skipping...
55.73 node:internal/modules/cjs/loader:1225
55.73   const err = new Error(message);
55.73               ^
55.73 
55.73 Error: Cannot find module 'esbuild'
55.73 Require stack:
55.73 - /home/theia/node_modules/esbuild-plugins-node-modules-polyfill/dist/index.js
55.73     at Function._resolveFilename (node:internal/modules/cjs/loader:1225:15)
55.73     at Function._load (node:internal/modules/cjs/loader:1055:27)
55.73     at TracingChannel.traceSync (node:diagnostics_channel:322:14)
55.73     at wrapModuleLoad (node:internal/modules/cjs/loader:220:24)
55.73     at Module.require (node:internal/modules/cjs/loader:1311:12)
55.73     at require (node:internal/modules/helpers:136:16)
55.73     at Module.<anonymous> (/home/theia/node_modules/esbuild-plugins-node-modules-polyfill/dist/index.js:35:15)
55.73     at Module._compile (node:internal/modules/cjs/loader:1554:14)
55.73     at Object..js (node:internal/modules/cjs/loader:1706:10)
55.73     at Module.load (node:internal/modules/cjs/loader:1289:32) {
55.73   code: 'MODULE_NOT_FOUND',
55.73   requireStack: [
55.73     '/home/theia/node_modules/esbuild-plugins-node-modules-polyfill/dist/index.js'
55.73   ]
55.73 }
55.73 
55.73 Node.js v22.14.0
55.73 
55.73 Error: esbuild exited with an unexpected code: 1.
55.73     at ChildProcess.<anonymous> (/home/theia/browser-app/node_modules/@theia/application-manager/lib/application-process.js:97:28)
55.73     at ChildProcess.emit (node:events:518:28)
55.73     at maybeClose (node:internal/child_process:1101:16)
55.73     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
55.73 Uncaught Exception:  Error: esbuild exited with an unexpected code: 1.
55.73 Error: esbuild exited with an unexpected code: 1.
55.73     at ChildProcess.<anonymous> (/home/theia/browser-app/node_modules/@theia/application-manager/lib/application-process.js:97:28)
55.73     at ChildProcess.emit (node:events:518:28)
55.73     at maybeClose (node:internal/child_process:1101:16)
55.73     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
55.75 
55.75 npm verb unsafe-perm in lifecycle true
55.75 npm info gsc-browser-app@1.0.0 Failed to exec build:prod script
55.75 npm verb stack Error: gsc-browser-app@1.0.0 build:prod: `npm run -s compile && npm run -s bundle:prod`
55.75 npm verb stack Exit status 1
55.75 npm verb stack     at EventEmitter.<anonymous> (/home/theia/node_modules/npm/lib/utils/lifecycle.js:217:16)
55.75 npm verb stack     at EventEmitter.emit (node:events:518:28)
55.75 npm verb stack     at ChildProcess.<anonymous> (/home/theia/node_modules/npm/lib/utils/spawn.js:24:14)
55.75 npm verb stack     at ChildProcess.emit (node:events:518:28)
55.75 npm verb stack     at maybeClose (node:internal/child_process:1101:16)
55.75 npm verb stack     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
55.75 npm verb pkgid gsc-browser-app@1.0.0
55.75 npm verb cwd /home/theia/browser-app
55.75 npm ERR! Linux 6.12.69+deb13-amd64
55.75 npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "build:prod"
55.75 npm ERR! node v22.14.0
55.75 npm ERR! npm  v2.15.12
55.75 npm ERR! code ELIFECYCLE
55.75 npm ERR! gsc-browser-app@1.0.0 build:prod: `npm run -s compile && npm run -s bundle:prod`
55.75 npm ERR! Exit status 1
55.75 npm ERR! 
55.75 npm ERR! Failed at the gsc-browser-app@1.0.0 build:prod script 'npm run -s compile && npm run -s bundle:prod'.
55.75 npm ERR! This is most likely a problem with the gsc-browser-app package,
55.75 npm ERR! not with npm itself.
55.75 npm ERR! Tell the author that this fails on your system:
55.75 npm ERR!     npm run -s compile && npm run -s bundle:prod
55.75 npm ERR! You can get information on how to open an issue for this project with:
55.75 npm ERR!     npm bugs gsc-browser-app
55.75 npm ERR! Or if that isn't available, you can get their info via:
55.75 npm ERR! 
55.75 npm ERR!     npm owner ls gsc-browser-app
55.75 npm ERR! There is likely additional logging output above.
55.75 npm verb exit [ 1, true ]
55.75 
55.75 npm ERR! Please include the following file with any support request:
55.75 npm ERR!     /home/theia/browser-app/npm-debug.log
55.76 npm verbose cwd /home/theia
55.76 npm verbose os Linux 6.12.69+deb13-amd64
55.76 npm verbose node v22.14.0
55.76 npm verbose npm  v10.9.2
55.76 npm verbose exit 1
55.76 npm verbose code 1
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
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npm run build:extensions --verbose &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.map -o -name \\*.spec.* -type f -delete &&     rm -rf .git gsc-core-extension" did not complete successfully: exit code: 1
mert@mertunubol:~/Development/gsc.scheduling.theia$ 
