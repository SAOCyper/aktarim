60.53 
60.53 > gsc-browser-app@1.0.0 build:prod /home/theia/browser-app
60.53 > npm run -s compile && npm run -s bundle:prod
60.53 
61.38 native node modules are already rebuilt for browser
61.78 Could not resolve optional peer dependency '@theia/electron'. Skipping...
61.94 [build/node] Build started
61.94 
61.94 [build/browser] Build started
61.94 
62.03 ✘ [ERROR] Cannot read file: /home/theia/extensions/gss-messaging/lib/stomp-messaging/stomp-messaging-contribution.js
62.03 
62.03     src-gen/backend/server.js:88:27:
62.03       88 │ ...d(require('@uzay/gss-messaging/lib/stomp-messaging/stomp-messag...
62.03          ╵              ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
62.03 
62.03 
62.10 ✘ [ERROR] Cannot read file: /home/theia/extensions/gss-messaging/lib/browser/common-index.js
62.10 
62.10     ../extensions/gsc-core-extension/lib/node/services/artemis.service.js:50:32:
62.10       50 │ const gss_messaging_1 = require("@uzay/gss-messaging");
62.10          ╵                                 ~~~~~~~~~~~~~~~~~~~~~
62.10 
62.10 
62.15 ✘ [ERROR] Cannot read file: /home/theia/extensions/gsc-earth-extension/lib/browser/soc-frontend-module.js
62.15 
62.15     src-gen/frontend/index.js:124:38:
62.15       124 │ ..., require('@uzay/gsc-earth-extension/lib/browser/soc-frontend-...
62.15           ╵              ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
62.15 
62.15 
62.18 [build/node] Finished with 2 errors in 240ms.
62.18 
62.20 [esbuild] Build failed: Error: Build failed with 2 errors:
62.20 src-gen/backend/server.js:88:27: ERROR: Cannot read file: /home/theia/extensions/gss-messaging/lib/stomp-messaging/stomp-messaging-contribution.js
62.20 ../extensions/gsc-core-extension/lib/node/services/artemis.service.js:50:32: ERROR: Cannot read file: /home/theia/extensions/gss-messaging/lib/browser/common-index.js
62.20     at failureErrorWithLog (/home/theia/node_modules/esbuild/lib/main.js:1467:15)
62.20     at /home/theia/node_modules/esbuild/lib/main.js:926:25
62.20     at /home/theia/node_modules/esbuild/lib/main.js:1345:9 {
62.20   errors: [Getter/Setter],
62.20   warnings: [Getter/Setter]
62.20 }
62.20 
62.23 Error: esbuild exited with an unexpected code: 1.
62.23     at ChildProcess.<anonymous> (/home/theia/browser-app/node_modules/@theia/application-manager/lib/application-process.js:97:28)
62.23     at ChildProcess.emit (node:events:518:28)
62.23     at maybeClose (node:internal/child_process:1101:16)
62.23     at Socket.<anonymous> (node:internal/child_process:456:11)
62.23     at Socket.emit (node:events:518:28)
62.23     at Pipe.<anonymous> (node:net:351:12)
62.23 Uncaught Exception:  Error: esbuild exited with an unexpected code: 1.
62.23 Error: esbuild exited with an unexpected code: 1.
62.23     at ChildProcess.<anonymous> (/home/theia/browser-app/node_modules/@theia/application-manager/lib/application-process.js:97:28)
62.23     at ChildProcess.emit (node:events:518:28)
62.23     at maybeClose (node:internal/child_process:1101:16)
62.23     at Socket.<anonymous> (node:internal/child_process:456:11)
62.23     at Socket.emit (node:events:518:28)
62.23     at Pipe.<anonymous> (node:net:351:12)
62.25 
62.25 npm verb unsafe-perm in lifecycle true
62.25 npm info gsc-browser-app@1.0.0 Failed to exec build:prod script
62.25 npm verb stack Error: gsc-browser-app@1.0.0 build:prod: `npm run -s compile && npm run -s bundle:prod`
62.25 npm verb stack Exit status 1
62.25 npm verb stack     at EventEmitter.<anonymous> (/home/theia/node_modules/npm/lib/utils/lifecycle.js:217:16)
62.25 npm verb stack     at EventEmitter.emit (node:events:518:28)
62.25 npm verb stack     at ChildProcess.<anonymous> (/home/theia/node_modules/npm/lib/utils/spawn.js:24:14)
62.25 npm verb stack     at ChildProcess.emit (node:events:518:28)
62.25 npm verb stack     at maybeClose (node:internal/child_process:1101:16)
62.25 npm verb stack     at ChildProcess._handle.onexit (node:internal/child_process:304:5)
62.25 npm verb pkgid gsc-browser-app@1.0.0
62.25 npm verb cwd /home/theia/browser-app
62.25 npm ERR! Linux 6.12.69+deb13-amd64
62.25 npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "build:prod"
62.25 npm ERR! node v22.14.0
62.25 npm ERR! npm  v2.15.12
62.25 npm ERR! code ELIFECYCLE
62.25 npm ERR! gsc-browser-app@1.0.0 build:prod: `npm run -s compile && npm run -s bundle:prod`
62.25 npm ERR! Exit status 1
62.25 npm ERR! 
62.25 npm ERR! Failed at the gsc-browser-app@1.0.0 build:prod script 'npm run -s compile && npm run -s bundle:prod'.
62.25 npm ERR! This is most likely a problem with the gsc-browser-app package,
62.25 npm ERR! not with npm itself.
62.25 npm ERR! Tell the author that this fails on your system:
62.25 npm ERR!     npm run -s compile && npm run -s bundle:prod
62.25 npm ERR! You can get information on how to open an issue for this project with:
62.25 npm ERR!     npm bugs gsc-browser-app
62.25 npm ERR! Or if that isn't available, you can get their info via:
62.25 npm ERR! 
62.25 npm ERR!     npm owner ls gsc-browser-app
62.25 npm ERR! There is likely additional logging output above.
62.25 npm verb exit [ 1, true ]
62.25 
62.25 npm ERR! Please include the following file with any support request:
62.25 npm ERR!     /home/theia/browser-app/npm-debug.log
62.25 npm verbose cwd /home/theia
62.25 npm verbose os Linux 6.12.69+deb13-amd64
62.25 npm verbose node v22.14.0
62.25 npm verbose npm  v10.9.2
62.25 npm verbose exit 1
62.25 npm verbose code 1
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
mert@mertunubol:~/Development/gsc.scheduling.theia$ 
