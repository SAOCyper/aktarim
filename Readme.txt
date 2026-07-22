root@c604f5f9045f:/home/theia# npm run build:extensions 

> build:extensions
> lerna run --scope="@uzay/*" build

lerna notice cli v9.0.7
lerna notice filter including "@uzay/*"
lerna info filter [ '@uzay/*' ]

 Lerna (powered by Nx)   Running target build for 9 projects:

- @uzay/gsc-core-extension
- @uzay/gsc-earth-extension
- @uzay/gsc-files-extension
- @uzay/gsc-mission-extension
- @uzay/gsc-moon-extension
- @uzay/gsc-pass-control-extension
- @uzay/gsc-pass-prediction-extension
- @uzay/gsc-settings-extension
- @uzay/gsc-common

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

> @uzay/gsc-common:build

@uzay/gsc-common: > @uzay/gsc-common@1.0.0 build
@uzay/gsc-common: > npm run build:lib
@uzay/gsc-common: > @uzay/gsc-common@1.0.0 build:lib /home/theia/gsc-common
@uzay/gsc-common: > vite build --mode lib
@uzay/gsc-common: vite v7.3.5 building client environment for lib...
@uzay/gsc-common: transforming...
@uzay/gsc-common: ✓ 11 modules transformed.
@uzay/gsc-common: rendering chunks...
@uzay/gsc-common: computing gzip size...
@uzay/gsc-common: dist/soc-widgets.es.js  115.90 kB │ gzip: 29.96 kB
@uzay/gsc-common: dist/soc-widgets.umd.js  89.26 kB │ gzip: 26.05 kB
@uzay/gsc-common: ✓ built in 3.89s

> @uzay/gsc-core-extension:build


> @uzay/gsc-files-extension:build


> @uzay/gsc-pass-prediction-extension:build


> @uzay/gsc-pass-control-extension:build


> @uzay/gsc-mission-extension:build


> @uzay/gsc-settings-extension:build


> @uzay/gsc-moon-extension:build

@uzay/gsc-files-extension: > @uzay/gsc-files-extension@1.0.0 build
@uzay/gsc-files-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-pass-prediction-extension: > @uzay/gsc-pass-prediction-extension@1.0.0 build
@uzay/gsc-pass-prediction-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-mission-extension: > @uzay/gsc-mission-extension@1.0.0 build
@uzay/gsc-mission-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
@uzay/gsc-core-extension: > tsc
@uzay/gsc-pass-control-extension: > @uzay/gsc-pass-control-extension@1.0.0 build
@uzay/gsc-pass-control-extension: > tsc && cpx "src/**/*.css" lib/
@uzay/gsc-moon-extension: npm warn config ignoring workspace config at /home/theia/extensions/gsc-moon-extension/.npmrc
@uzay/gsc-moon-extension: > @uzay/gsc-moon-extension@1.0.0 build
@uzay/gsc-moon-extension: > tsc -p tsconfig.json && cpx "src/**/*.css" lib/
@uzay/gsc-settings-extension: > @uzay/gsc-settings-extension@1.0.0 build
@uzay/gsc-settings-extension: > tsc && cpx "src/**/*.css" lib/

> @uzay/gsc-earth-extension:build

@uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
@uzay/gsc-earth-extension: > tsc

—————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Successfully ran target build for 9 projects


root@c604f5f9045f:/home/theia# cd browser-app
root@c604f5f9045f:/home/theia/browser-app# npx theia build
Could not resolve optional peer dependency '@theia/electron'. Skipping...
^C
root@c604f5f9045f:/home/theia/browser-app# npx theia build 2>&1 | tail -50 
^C
root@c604f5f9045f:/home/theia/browser-app# npx theia build
Could not resolve optional peer dependency '@theia/electron'. Skipping...
^C
root@c604f5f9045f:/home/theia/browser-app# npm run build

> gsc-browser-app@1.0.0 build
> npm run -s compile && npm run -s bundle

native node modules are already rebuilt for browser
Could not resolve optional peer dependency '@theia/electron'. Skipping...
assets by status 2.01 MiB [cached] 15 assets
assets by path cesium/ 6.76 MiB 389 assets
assets by path *.js 82.1 MiB
  assets by chunk 48.9 MiB (id hint: vendors) 63 assets
  + 18 assets
assets by path ../ 66.9 KiB
  assets by path ../backend/shell-integrations/ 26.2 KiB 9 assets
  assets by path ../webview/pre/ 40.7 KiB 5 assets
assets by path textures/*.jpg 39 MiB
  asset textures/8k_moon.jpg 14.3 MiB [compared for emit] [from: ../gsc-common/public/textures/8k_moon.jpg] [copied]
  asset textures/8k_earth_clouds.jpg 11.1 MiB [compared for emit] [from: ../gsc-common/public/textures/8k_earth_clouds.jpg] [copied]
  + 3 assets
+ 5 assets
runtime modules 9.68 KiB 19 modules
orphan modules 132 KiB [orphan] 9 modules
modules by path ../ 52.9 MiB (javascript) 2.01 MiB (asset)
  modules by path ../node_modules/ 34.1 MiB (javascript) 2.01 MiB (asset) 3363 modules
  modules by path ../extensions/ 18.7 MiB 1688 modules
  + 1 module
modules by path ./ 12.7 MiB
  javascript modules 10.5 MiB 1529 modules
  json modules 2.27 MiB 62 modules
modules by mime type image/svg+xml 3.17 KiB
  data:image/svg+xml;base64,PHN2ZyB3aWR0aD0i.. 1.59 KiB [built] [code generated]
  data:image/svg+xml;base64,PHN2ZyB3aWR0aD0i.. 1.59 KiB [built] [code generated]
+ 6 modules
  
webpack 5.107.2 compiled successfully in 70856 ms

assets by status 1.62 GiB [compared for emit]
  assets by path cesium/Assets/ 4.18 MiB 205 assets
  assets by path cesium/Widgets/ 503 KiB 67 assets
  assets by path textures/*.jpg 39 MiB 5 assets
  assets by path cesium/ThirdParty/ 843 KiB 5 assets
  + 3 assets
assets by status 2.57 MiB [emitted]
  assets by path cesium/Workers/*.js 1.04 MiB
    asset cesium/Workers/chunk-55KTRCCC.js 137 KiB [emitted] [from: ../node_modules/cesium/Build/Cesium/Workers/chunk-55KTRCCC.js] [copied]
    + 109 assets
  assets by path cesium/ThirdParty/ 232 KiB
    asset cesium/ThirdParty/google-earth-dbroot-parser.js 214 KiB [emitted] [from: ../node_modules/cesium/Build/Cesium/ThirdParty/google-earth-dbroot-parser.js] [copied]
    asset cesium/ThirdParty/Workers/zip-web-worker.js 18.1 KiB [emitted] [from: ../node_modules/cesium/Build/Cesium/ThirdParty/Workers/zip-web-worker.js] [copied]
  asset editor.worker.js 1.31 MiB [emitted] (name: editor.worker) 1 related asset
runtime modules 670 bytes 3 modules
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
webpack 5.107.2 compiled successfully in 30839 ms

assets by status 2.01 MiB [cached] 15 assets
assets by path cesium/ 6.76 MiB 389 assets
assets by path textures/*.jpg 39 MiB
  asset textures/8k_moon.jpg 14.3 MiB [compared for emit] [from: ../gsc-common/public/textures/8k_moon.jpg] [copied]
  asset textures/8k_earth_clouds.jpg 11.1 MiB [compared for emit] [from: ../gsc-common/public/textures/8k_earth_clouds.jpg] [copied]
  asset textures/EARTH_DISPLACE_42K_16BITS_preview.jpg 6.19 MiB [compared for emit] [from: ../gsc-common/public/textures/EARTH_DISPLACE_42K_16BITS_preview.jpg] [copied]
  + 2 assets
assets by status 26.9 MiB [emitted]
  asset secondary-window.js 26.4 MiB [emitted] (name: secondary-window) 1 related asset
  asset secondary-window.css 568 KiB [emitted] (name: secondary-window) 1 related asset
asset earth/satellite-2017-11-02_europe_turkey.mbtiles 1.45 GiB [compared for emit] [from: ../gsc-common/public/earth/satellite-2017-11-02_europe_turkey.mbtiles] [copied]
asset moon/moon_wac.mbtiles 123 MiB [compared for emit] [from: ../gsc-common/public/moon/moon_wac.mbtiles] [copied]
asset models/imece-web2.gltf 10.7 MiB [compared for emit] [from: ../gsc-common/public/imece-web2.gltf] [copied]
Entrypoint secondary-window 26.9 MiB (26.5 MiB) = secondary-window.css 568 KiB secondary-window.js 26.4 MiB 17 auxiliary assets
runtime modules 111 KiB 490 modules
orphan modules 1.28 MiB (javascript) 1.55 MiB (asset) [orphan] 182 modules
javascript modules 20 MiB 2143 modules
css modules 505 KiB
  modules by path ../node_modules/ 342 KiB 114 modules
  modules by path ./ 163 KiB 42 modules
json modules 2.36 MiB
  modules by path ./node_modules/@theia/core/ 2.23 MiB 50 modules
  modules by path ../node_modules/ 89.8 KiB 10 modules
  modules by path ./node_modules/@theia/monaco/ 36.2 KiB 10 modules
asset modules 463 KiB (asset) 84 bytes (javascript)
  ../node_modules/vscode-oniguruma/release/onig.wasm 462 KiB (asset) 42 bytes (javascript) [built] [code generated]
  ../node_modules/@theia/monaco-editor-core/esm/vs/editor/common/services/editorWe...(truncated) 590 bytes (asset) 42 bytes (javascript) [built] [code generated]
  
webpack 5.107.2 compiled successfully in 30961 ms

assets by path *.js 38.5 MiB
  assets by status 38.1 MiB [compared for emit]
    asset vendors-node_modules_theia_ai-core_lib_node_ai-core-backend-module_js-node_modules_theia_ai-m-972455.js 29.2 MiB [compared for emit] (id hint: vendors) 1 related asset
    asset vendors-node_modules_theia_core_lib_common_index_js-node_modules_theia_core_lib_common_menu_i-62760b.js 3.48 MiB [compared for emit] (id hint: vendors) 1 related asset
    asset vendors-node_modules_theia_core_lib_common_collections_js-node_modules_theia_core_lib_common_-16af40.js 2.57 MiB [compared for emit] (id hint: vendors) 1 related asset
    asset vendors-node_modules_theia_plugin-ext_lib_hosted_node_plugin-host_js.js 2.2 MiB [compared for emit] (id hint: vendors) 1 related asset
    + 5 assets
  assets by status 419 KiB [emitted]
    asset main.js 335 KiB [emitted] (name: main) 1 related asset
    asset ipc-bootstrap.js 21.8 KiB [emitted] (name: ipc-bootstrap) 1 related asset
    asset plugin-host.js 17.3 KiB [emitted] (name: plugin-host) 1 related asset
    asset parcel-watcher.js 16.2 KiB [emitted] (name: parcel-watcher) 1 related asset
    + 3 assets
asset native/watcher.node 511 KiB [compared for emit] (auxiliary id hint: vendors)
asset worker/conoutSocketWorker.js 3.7 KiB [emitted] (name: worker/conoutSocketWorker) 1 related asset
runtime modules 23.9 KiB 56 modules
orphan modules 118 KiB [orphan] 2 modules
modules by path ../node_modules/ 25 MiB
  javascript modules 23 MiB 2984 modules
  json modules 2.09 MiB 36 modules
modules by path ./ 6.98 MiB 651 modules
modules by path ../extensions/ 162 KiB
  modules by path ../extensions/gsc-earth-extension/lib/node/services/*.js 127 KiB 4 modules
  optional modules 2.78 KiB [optional] 2 modules
  modules by path ../extensions/gsc-earth-extension/lib/node/rpc/*.js 13.5 KiB 2 modules
  + 2 modules
modules by path ../gsc-common/ 114 KiB
  ../gsc-common/dist/soc-widgets.es.js 113 KiB [built] [code generated]
  ../gsc-common/package.json 1.07 KiB [optional] [built] [code generated]
+ 63 modules
webpack 5.107.2 compiled successfully in 14749 ms
