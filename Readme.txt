@uzay/gsc-settings-extension: > @uzay/gsc-settings-extension@1.0.0 build
@uzay/gsc-settings-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-mission-extension: > @uzay/gsc-mission-extension@1.0.0 build
@uzay/gsc-mission-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-pass-prediction-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
@uzay/gsc-pass-prediction-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
@uzay/gsc-pass-prediction-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
@uzay/gsc-pass-prediction-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
@uzay/gsc-pass-prediction-extension: npm warn config `--include=optional` to include them.
@uzay/gsc-pass-prediction-extension: npm warn config
@uzay/gsc-pass-prediction-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
@uzay/gsc-pass-control-extension: npm warn config cache-min This option has been deprecated in favor of `--prefer-offline`.
@uzay/gsc-pass-control-extension: npm warn config cache-max This option has been deprecated in favor of `--prefer-online`
@uzay/gsc-pass-control-extension: npm warn config shrinkwrap Use the --package-lock setting instead.
@uzay/gsc-pass-control-extension: npm warn config optional Use `--omit=optional` to exclude optional dependencies, or
@uzay/gsc-pass-control-extension: npm warn config `--include=optional` to include them.
@uzay/gsc-pass-control-extension: npm warn config
@uzay/gsc-pass-control-extension: npm warn config       Default value does install optional deps unless otherwise omitted.
@uzay/gsc-pass-prediction-extension: > @uzay/gsc-pass-prediction-extension@1.0.0 build
@uzay/gsc-pass-prediction-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-pass-control-extension: > @uzay/gsc-pass-control-extension@1.0.0 build
@uzay/gsc-pass-control-extension: > tsc && cpx "src/**/*.css" lib/

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Successfully ran target build for 8 projects



> gsc-browser-app@1.0.0 build /home/theia/browser-app
> npm run -s compile && npm run -s bundle

native node modules are already rebuilt for browser
Could not resolve optional peer dependency '@theia/electron'. Skipping...
assets by status 2.01 MiB [cached] 15 assets
assets by path cesium/ 6.77 MiB 389 assets
assets by path *.js 59 MiB
  assets by chunk 26 MiB (id hint: vendors)
    asset vendors-node_modules_react_jsx-runtime_js-node_modules_cesium_Source_Cesium_js.js 18.2 MiB [emitted] (id hint: vendors) 2 related assets
    + 56 assets
  + 19 assets
assets by path ../ 66.9 KiB
  assets by path ../backend/shell-integrations/ 26.2 KiB 9 assets
  assets by path ../webview/pre/ 40.7 KiB
    assets by path ../webview/pre/*.js 40 KiB 3 assets
    assets by path ../webview/pre/*.html 726 bytes 2 assets
asset context/plugin-vscode-init-fe.js 1.52 KiB [compared for emit] [from: ../node_modules/@theia/plugin-ext-vscode/lib/node/context/plugin-vscode-init-fe.js] [copied] 1 related asset
asset secondary-window.html 531 bytes [compared for emit] [from: src-gen/frontend/secondary-window.html] [copied] 1 related asset
4753 modules
  

ERROR in unable to locate '/home/theia/gsc-core-extension/public/textures' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/imece-web2.gltf' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/earth' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/moon' glob

webpack 5.108.4 compiled with 4 errors in 21635 ms

assets by path cesium/Assets/ 4.18 MiB 205 assets
assets by path cesium/Workers/*.js 1.06 MiB
  asset cesium/Workers/chunk-E7EKLP3B.js 144 KiB [compared for emit] [from: ../node_modules/cesium/Build/Cesium/Workers/chunk-E7EKLP3B.js] [copied]
  asset cesium/Workers/chunk-LNJEJFV5.js 122 KiB [compared for emit] [from: ../node_modules/cesium/Build/Cesium/Workers/chunk-LNJEJFV5.js] [copied]
  asset cesium/Workers/transcodeKTX2.js 58.8 KiB [compared for emit] [from: ../node_modules/cesium/Build/Cesium/Workers/transcodeKTX2.js] [copied]
  + 107 assets
assets by path cesium/Widgets/ 503 KiB 67 assets
assets by path cesium/ThirdParty/ 1.05 MiB
  assets by path cesium/ThirdParty/*.wasm 843 KiB 4 assets
  assets by path cesium/ThirdParty/Workers/ 18.1 KiB 2 assets
  asset cesium/ThirdParty/google-earth-dbroot-parser.js 214 KiB [compared for emit] [from: ../node_modules/cesium/Build/Cesium/ThirdParty/google-earth-dbroot-parser.js] [copied]
asset editor.worker.js 1.31 MiB [compared for emit] (name: editor.worker) 1 related asset
runtime modules 1.07 KiB 3 modules
cacheable modules 1.1 MiB
  modules by path ../node_modules/@theia/monaco-editor-core/esm/vs/editor/common/ 430 KiB 45 modules
  modules by path ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/ 690 KiB
    modules by path ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/*.js 615 KiB 37 modules
    modules by path ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/worker/*.js 16.4 KiB
      ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/worker/webWork...(truncated) 1.08 KiB [built] [code generated]
      ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/worker/webWorker.js 15.3 KiB [built] [code generated]
    modules by path ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/diff/*.js 58.3 KiB
      ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/diff/diff.js 57 KiB [built] [code generated]
      ../node_modules/@theia/monaco-editor-core/esm/vs/base/common/diff/diffChange.js 1.32 KiB [built] [code generated]
  modules by path ../node_modules/@theia/monaco-editor-core/esm/vs/*.js 3.58 KiB
    ../node_modules/@theia/monaco-editor-core/esm/vs/nls.js 2.74 KiB [built] [code generated]
    ../node_modules/@theia/monaco-editor-core/esm/vs/nls.messages.js 854 bytes [built] [code generated]

ERROR in unable to locate '/home/theia/gsc-core-extension/public/imece-web2.gltf' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/earth' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/moon' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/textures' glob

webpack 5.108.4 compiled with 4 errors in 4941 ms

assets by status 2.01 MiB [cached] 15 assets
assets by path cesium/ 6.77 MiB
  assets by path cesium/Assets/ 4.18 MiB 205 assets
  assets by path cesium/Workers/*.js 1.06 MiB
    asset cesium/Workers/chunk-E7EKLP3B.js 144 KiB [compared for emit] [from: ../node_modules/cesium/Build/Cesium/Workers/chunk-E7EKLP3B.js] [copied]
    asset cesium/Workers/chunk-LNJEJFV5.js 122 KiB [compared for emit] [from: ../node_modules/cesium/Build/Cesium/Workers/chunk-LNJEJFV5.js] [copied]
    + 108 assets
  assets by path cesium/Widgets/ 503 KiB 67 assets
  assets by path cesium/ThirdParty/ 1.05 MiB
    assets by path cesium/ThirdParty/*.wasm 843 KiB 4 assets
    assets by path cesium/ThirdParty/Workers/ 18.1 KiB 2 assets
    + 1 asset
assets by chunk 27.1 MiB (name: secondary-window)
  asset secondary-window.js 26.6 MiB [compared for emit] (name: secondary-window) 1 related asset
  asset secondary-window.css 568 KiB [compared for emit] (name: secondary-window) 1 related asset
Entrypoint secondary-window 27.1 MiB (26.8 MiB) = secondary-window.css 568 KiB secondary-window.js 26.6 MiB 17 auxiliary assets
3054 modules
  

ERROR in unable to locate '/home/theia/gsc-core-extension/public/textures' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/imece-web2.gltf' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/moon' glob

ERROR in unable to locate '/home/theia/gsc-core-extension/public/earth' glob

webpack 5.108.4 compiled with 4 errors in 11820 ms

assets by path *.js 36.3 MiB
  assets by status 8.87 MiB [compared for emit]
    assets by chunk 8.79 MiB (id hint: vendors)
      asset vendors-node_modules_theia_core_lib_common_index_js-node_modules_theia_core_lib_common_menu_i-62760b.js 3.4 MiB [compared for emit] (id hint: vendors) 1 related asset
      asset vendors-node_modules_theia_core_lib_common_collections_js-node_modules_theia_core_lib_common_-16af40.js 2.57 MiB [compared for emit] (id hint: vendors) 1 related asset
      asset vendors-node_modules_theia_plugin-ext_lib_hosted_node_plugin-host_js.js 2.18 MiB [compared for emit] (id hint: vendors) 1 related asset
      + 5 assets
    + 6 assets
  assets by status 27.4 MiB [emitted]
    asset vendors-node_modules_stroncium_procfs_lib_parsers_cgroups_js-node_modules_stroncium_procfs_li-f98b31.js 27 MiB [emitted] (id hint: vendors) 1 related asset
    asset main.js 410 KiB [emitted] (name: main) 1 related asset
asset native/watcher.node 511 KiB [compared for emit] (auxiliary id hint: vendors)
asset worker/conoutSocketWorker.js 3.71 KiB [compared for emit] (name: worker/conoutSocketWorker) 1 related asset
runtime modules 27.8 KiB 61 modules
orphan modules 118 KiB [orphan] 2 modules
modules by path ../node_modules/ 29.7 MiB
  javascript modules 26.1 MiB 3514 modules
  json modules 3.67 MiB 51 modules
modules by path ../extensions/ 347 KiB
  modules by path ../extensions/gsc-core-extension/lib/ 175 KiB 13 modules
  modules by path ../extensions/gsc-earth-extension/lib/node/ 171 KiB 9 modules
  ../extensions/gsc-moon-extension/lib/node/soc-backend-module.js 1.18 KiB [optional] [built] [code generated]
modules by path ./ 9.31 KiB
  ./src-gen/backend/main.js 4.09 KiB [built] [code generated]
  ./src-gen/backend/server.js 5.11 KiB [built] [code generated]
  ./lib/backend/native-webpack-plugin/ripgrep.js 116 bytes [built] [code generated]
+ 63 modules

ERROR in ../extensions/gsc-earth-extension/lib/node/services/artemis.service.js 50:20-46
Module not found: Error: Can't resolve '@uzay/messaging' in '/home/theia/extensions/gsc-earth-extension/lib/node/services'
resolve '@uzay/messaging' in '/home/theia/extensions/gsc-earth-extension/lib/node/services'
  Parsed request is a module
  using description file: /home/theia/extensions/gsc-earth-extension/package.json (relative path: ./lib/node/services)
    resolve as module
      /home/theia/extensions/gsc-earth-extension/lib/node/services/node_modules doesn't exist or is not a directory
      /home/theia/extensions/gsc-earth-extension/lib/node/node_modules doesn't exist or is not a directory
      /home/theia/extensions/gsc-earth-extension/lib/node_modules doesn't exist or is not a directory
      /home/theia/extensions/gsc-earth-extension/node_modules doesn't exist or is not a directory
      /home/theia/extensions/node_modules doesn't exist or is not a directory
      looking for modules in /home/theia/node_modules
        single file module
          using description file: /home/theia/package.json (relative path: ./node_modules/@uzay/messaging)
            no extension
              /home/theia/node_modules/@uzay/messaging doesn't exist
            .js
              /home/theia/node_modules/@uzay/messaging.js doesn't exist
            .json
              /home/theia/node_modules/@uzay/messaging.json doesn't exist
            .wasm
              /home/theia/node_modules/@uzay/messaging.wasm doesn't exist
            .node
              /home/theia/node_modules/@uzay/messaging.node doesn't exist
        /home/theia/node_modules/@uzay/messaging doesn't exist
      /home/node_modules doesn't exist or is not a directory
      /node_modules doesn't exist or is not a directory
      looking for modules in /home/theia/node_modules
        single file module
          using description file: /home/theia/package.json (relative path: ./node_modules/@uzay/messaging)
            no extension
              /home/theia/node_modules/@uzay/messaging doesn't exist
            .js
              /home/theia/node_modules/@uzay/messaging.js doesn't exist
            .json
              /home/theia/node_modules/@uzay/messaging.json doesn't exist
            .wasm
              /home/theia/node_modules/@uzay/messaging.wasm doesn't exist
            .node
              /home/theia/node_modules/@uzay/messaging.node doesn't exist
        /home/theia/node_modules/@uzay/messaging doesn't exist
 @ ../extensions/gsc-earth-extension/lib/node/soc-backend-module.js 6:26-63
 @ ./src-gen/backend/server.js 90:19-83
 @ ./src-gen/backend/main.js 185:21-40

webpack 5.108.4 compiled with 1 error in 15711 ms

Error: webpack exited with an unexpected code: 1.
    at ChildProcess.<anonymous> (/home/theia/node_modules/@theia/application-manager/lib/application-process.js:86:28)
    at ChildProcess.emit (node:events:518:28)
    at maybeClose (node:internal/child_process:1101:16)
    at Socket.<anonymous> (node:internal/child_process:456:11)
    at Socket.emit (node:events:518:28)
    at Pipe.<anonymous> (node:net:351:12)
Uncaught Exception:  Error: webpack exited with an unexpected code: 1.
Error: webpack exited with an unexpected code: 1.
    at ChildProcess.<anonymous> (/home/theia/node_modules/@theia/application-manager/lib/application-process.js:86:28)
    at ChildProcess.emit (node:events:518:28)
    at maybeClose (node:internal/child_process:1101:16)
    at Socket.<anonymous> (node:internal/child_process:456:11)
    at Socket.emit (node:events:518:28)
    at Pipe.<anonymous> (node:net:351:12)

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
