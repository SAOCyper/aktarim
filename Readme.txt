

> gsc-browser-app@1.0.0 build /home/theia/browser-app
> npm run -s compile && npm run -s bundle

native node modules are already rebuilt for browser
Could not resolve optional peer dependency '@theia/electron'. Skipping...
[webpack-cli] ✖ Failed to load '/home/theia/browser-app/webpack.config.js' config
▶ ESM (`import`) failed:
  Error: Cannot find module 'ajv/dist/compile/codegen'
  Require stack:
  - /home/theia/node_modules/ajv-formats/dist/limit.js
  - /home/theia/node_modules/ajv-formats/dist/index.js
  - /home/theia/node_modules/schema-utils/dist/validate.js
  - /home/theia/node_modules/schema-utils/dist/index.js
  - /home/theia/node_modules/compression-webpack-plugin/dist/index.js
  - /home/theia/browser-app/gen-webpack.config.js
  - /home/theia/browser-app/webpack.config.js
      at Function._resolveFilename (node:internal/modules/cjs/loader:1225:15)
      at Function._load (node:internal/modules/cjs/loader:1055:27)
      at TracingChannel.traceSync (node:diagnostics_channel:322:14)
      at wrapModuleLoad (node:internal/modules/cjs/loader:220:24)
      at Module.require (node:internal/modules/cjs/loader:1311:12)
      at require (node:internal/modules/helpers:136:16)
      at Object.<anonymous> (/home/theia/node_modules/ajv-formats/dist/limit.js:5:19)
      at Module._compile (node:internal/modules/cjs/loader:1554:14)
      at Object..js (node:internal/modules/cjs/loader:1706:10)
      at Module.load (node:internal/modules/cjs/loader:1289:32)
  code: MODULE_NOT_FOUND

▶ CJS (`require`) failed:
  Error: Cannot find module 'ajv/dist/compile/codegen'
  Require stack:
  - /home/theia/node_modules/ajv-formats/dist/limit.js
  - /home/theia/node_modules/ajv-formats/dist/index.js
  - /home/theia/node_modules/schema-utils/dist/validate.js
  - /home/theia/node_modules/schema-utils/dist/index.js
  - /home/theia/node_modules/compression-webpack-plugin/dist/index.js
  - /home/theia/browser-app/gen-webpack.config.js
  - /home/theia/browser-app/webpack.config.js
      at Function._resolveFilename (node:internal/modules/cjs/loader:1225:15)
      at Function._load (node:internal/modules/cjs/loader:1055:27)
      at TracingChannel.traceSync (node:diagnostics_channel:322:14)
      at wrapModuleLoad (node:internal/modules/cjs/loader:220:24)
      at Module.require (node:internal/modules/cjs/loader:1311:12)
      at require (node:internal/modules/helpers:136:16)
      at Object.<anonymous> (/home/theia/node_modules/ajv-formats/dist/limit.js:5:19)
      at Module._compile (node:internal/modules/cjs/loader:1554:14)
      at Object..js (node:internal/modules/cjs/loader:1706:10)
      at Module.load (node:internal/modules/cjs/loader:1289:32)
  code: MODULE_NOT_FOUND

Error: webpack exited with an unexpected code: 2.
    at ChildProcess.<anonymous> (/home/theia/node_modules/@theia/application-manager/lib/application-process.js:86:28)
    at ChildProcess.emit (node:events:518:28)
    at maybeClose (node:internal/child_process:1101:16)
    at ChildProcess._handle.onexit (node:internal/child_process:304:5)
Uncaught Exception:  Error: webpack exited with an unexpected code: 2.
Error: webpack exited with an unexpected code: 2.
    at ChildProcess.<anonymous> (/home/theia/node_modules/@theia/application-manager/lib/application-process.js:86:28)
    at ChildProcess.emit (node:events:518:28)
    at maybeClose (node:internal/child_process:1101:16)
    at ChildProcess._handle.onexit (node:internal/child_process:304:5)

npm ERR! Linux 6.12.69+deb13-amd64
npm ERR! argv "/usr/local/bin/node" "/home/theia/node_modules/.bin/npm" "run" "build"
npm ERR! node v22.14.0
npm ERR! npm  v2.15.12
npm ERR! code ELIFECYCLE
npm ERR! gsc-browser-app@1.0.0 build: `npm run -s compile && npm run -s bundle`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the gsc-browser-app@1.0.0 build script 'npm run -s compile && npm run -s bundle'.
npm ERR! This is most likely a problem with the gsc-browser-app package,
npm ERR! not with npm itself.
npm ERR! Tell the author that this fails on your system:
npm ERR!     npm run -s compile && npm run -s bundle
npm ERR! You can get information on how to open an issue for this project with:
npm ERR!     npm bugs gsc-browser-app
npm ERR! Or if that isn't available, you can get their info via:
npm ERR! 
npm ERR!     npm owner ls gsc-browser-app
npm ERR! There is likely additional logging output above.

npm ERR! Please include the following file with any support request:
npm ERR!     /home/theia/browser-app/npm-debug.log
root@2a85f57da0c0:/home/theia# 
