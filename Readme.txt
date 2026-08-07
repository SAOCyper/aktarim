———————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 Lerna (powered by Nx)   Successfully ran target build for 8 projects



> gsc-browser-app@1.0.0 build /home/theia/browser-app
> npm run -s compile && npm run -s bundle

native node modules are already rebuilt for browser
Could not resolve optional peer dependency '@theia/electron'. Skipping...
[build/browser] Build started

[build/node] Build started

✘ [ERROR] Cannot read file "../node_modules/@parcel/watcher": is a directory


✘ [ERROR] Cannot read file "../node_modules/react": is a directory

    ../node_modules/@theia/core/shared/react/index.js:1:25:
      1 │ module.exports = require('react');
        ╵                          ~~~~~~~


✘ [ERROR] Cannot read file "../node_modules/react-dom": is a directory

    ../node_modules/react-dom/client.js:3:16:
      3 │ var m = require('react-dom');
        ╵                 ~~~~~~~~~~~


✘ [ERROR] Cannot read file "../node_modules/@vscode/ripgrep": is a directory

    ../node_modules/@theia/search-in-workspace/lib/node/search-in-workspace-backend-module.js:22:26:
      22 │ const ripgrep_1 = require("@vscode/ripgrep");
         ╵                           ~~~~~~~~~~~~~~~~~


✘ [ERROR] Cannot read file "../node_modules/@uzay/gsc-core-extension": is a directory

    ../extensions/gsc-earth-extension/lib/node/soc-backend-module.js:11:37:
      11 │ const gsc_core_extension_1 = require("@uzay/gsc-core-extension");
         ╵                                      ~~~~~~~~~~~~~~~~~~~~~~~~~~


✘ [ERROR] Cannot read file "../node_modules/@uzay/gsc-core-extension": is a directory

    ../extensions/gsc-settings-extension/lib/browser/soc-settings-widget.js:51:37:
      51 │ const gsc_core_extension_1 = require("@uzay/gsc-core-extension");
         ╵                                      ~~~~~~~~~~~~~~~~~~~~~~~~~~


[build/node] Finished with 3 errors in 398ms.

[esbuild] Build failed: Error: Build failed with 3 errors:
error: Cannot read file "../node_modules/@parcel/watcher": is a directory
../extensions/gsc-earth-extension/lib/node/soc-backend-module.js:11:37: ERROR: Cannot read file "../node_modules/@uzay/gsc-core-extension": is a directory
../node_modules/@theia/search-in-workspace/lib/node/search-in-workspace-backend-module.js:22:26: ERROR: Cannot read file "../node_modules/@vscode/ripgrep": is a directory
    at failureErrorWithLog (/home/theia/node_modules/esbuild/lib/main.js:1476:15)
    at /home/theia/node_modules/esbuild/lib/main.js:945:25
    at /home/theia/node_modules/esbuild/lib/main.js:1354:9 {
  errors: [Getter/Setter],
  warnings: [Getter/Setter]
}

Error: esbuild exited with an unexpected code: 1.
    at ChildProcess.<anonymous> (/home/theia/node_modules/@theia/application-manager/lib/application-process.js:86:28)
    at ChildProcess.emit (node:events:518:28)
    at maybeClose (node:internal/child_process:1101:16)
    at Socket.<anonymous> (node:internal/child_process:456:11)
    at Socket.emit (node:events:518:28)
    at Pipe.<anonymous> (node:net:351:12)
Uncaught Exception:  Error: esbuild exited with an unexpected code: 1.
Error: esbuild exited with an unexpected code: 1.
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
