Could not resolve optional peer dependency '@theia/electron'. Skipping...
[build/browser] Build started

[build/node] Build started

[build/node] Finished with 0 errors in 802ms.

[build/browser] Finished with 0 errors in 1394ms.

[CopyCesium] Workers -> lib/frontend/cesium/Workers

[CopyCesium] ThirdParty -> lib/frontend/cesium/ThirdParty

[CopyCesium] Assets -> lib/frontend/cesium/Assets

[CopyCesium] Widgets -> lib/frontend/cesium/Widgets

[esbuild] Build completed successfully.

root@2a85f57da0c0:/home/theia# npm run start:browser

> start:browser
> cd browser-app && npm run start


> gsc-browser-app@1.0.0 start /home/theia/browser-app
> theia start --hostname=0.0.0.0 --plugins=local-dir:../plugins

Backend main: entry point loaded [0.148 s since backend process start]
Backend server: loading modules... [0.151 s since backend process start]
Backend server: container created [0.271 s since backend process start]
[SOC Core] Backend module loaded (no additional bindings needed — handled by soc-earth-extension).
Failed to start the backend application:
Error: Cannot find module '/home/theia/browser-app/lib/backend/Build/CesiumUnminified/index.cjs'
Require stack:
- /home/theia/browser-app/lib/backend/main.js
    at Function._resolveFilename (node:internal/modules/cjs/loader:1225:15)
    at Function._load (node:internal/modules/cjs/loader:1055:27)
    at TracingChannel.traceSync (node:diagnostics_channel:322:14)
    at wrapModuleLoad (node:internal/modules/cjs/loader:220:24)
    at Module.require (node:internal/modules/cjs/loader:1311:12)
    at require (node:internal/modules/helpers:136:16)
    at ../node_modules/cesium/index.cjs (/home/theia/browser-app/lib/backend/main.js:417713:83)
    at __require (/home/theia/browser-app/lib/backend/main.js:16:50)
    at ../extensions/gsc-core-extension/lib/common/features/satellite/services/CesiumEntityManager.js (/home/theia/browser-app/lib/backend/main.js:417778:20)
    at __require (/home/theia/browser-app/lib/backend/main.js:16:50) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [ '/home/theia/browser-app/lib/backend/main.js' ]
}
/home/theia/browser-app/lib/backend/main.js:331
      throw reason;
      ^

Error: Cannot find module '/home/theia/browser-app/lib/backend/Build/CesiumUnminified/index.cjs'
Require stack:
- /home/theia/browser-app/lib/backend/main.js
    at Function._resolveFilename (node:internal/modules/cjs/loader:1225:15)
    at Function._load (node:internal/modules/cjs/loader:1055:27)
    at TracingChannel.traceSync (node:diagnostics_channel:322:14)
    at wrapModuleLoad (node:internal/modules/cjs/loader:220:24)
    at Module.require (node:internal/modules/cjs/loader:1311:12)
    at require (node:internal/modules/helpers:136:16)
    at ../node_modules/cesium/index.cjs (/home/theia/browser-app/lib/backend/main.js:417713:83)
    at __require (/home/theia/browser-app/lib/backend/main.js:16:50)
    at ../extensions/gsc-core-extension/lib/common/features/satellite/services/CesiumEntityManager.js (/home/theia/browser-app/lib/backend/main.js:417778:20)
    at __require (/home/theia/browser-app/lib/backend/main.js:16:50) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [ '/home/theia/browser-app/lib/backend/main.js' ]
}

Node.js v22.14.0
