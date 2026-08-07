
 Lerna (powered by Nx)   Successfully ran target build for 8 projects



> gsc-browser-app@1.0.0 build /home/theia/browser-app
> npm run -s compile && npm run -s bundle

native node modules are already rebuilt for browser
Could not resolve optional peer dependency '@theia/electron'. Skipping...
these parameters are deprecated, see docs for addKeyword

these parameters are deprecated, see docs for addKeyword

these parameters are deprecated, see docs for addKeyword

these parameters are deprecated, see docs for addKeyword

these parameters are deprecated, see docs for addKeyword

these parameters are deprecated, see docs for addKeyword

[webpack-cli] ✖ Failed to load '/home/theia/browser-app/webpack.config.js' config
▶ ESM (`import`) failed:
  TypeError: Cannot read properties of undefined (reading 'date')
      at extendFormats (/home/theia/node_modules/ajv-keywords/keywords/_formatLimit.js:63:25)
      at defFunc (/home/theia/node_modules/ajv-keywords/keywords/_formatLimit.js:54:5)
      at defineKeywords (/home/theia/node_modules/ajv-keywords/index.js:17:22)
      at /home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:65:3
      at /home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:42:5
      at validateObject (/home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:208:22)
      at validate (/home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:187:14)
      at new CopyPlugin (/home/theia/node_modules/copy-webpack-plugin/dist/index.js:38:31)
      at Object.<anonymous> (/home/theia/browser-app/gen-webpack.config.js:28:5)
      at Module._compile (node:internal/modules/cjs/loader:1554:14)

▶ CJS (`require`) failed:
  TypeError: Cannot read properties of undefined (reading 'date')
      at extendFormats (/home/theia/node_modules/ajv-keywords/keywords/_formatLimit.js:63:25)
      at defFunc (/home/theia/node_modules/ajv-keywords/keywords/_formatLimit.js:54:5)
      at defineKeywords (/home/theia/node_modules/ajv-keywords/index.js:17:22)
      at /home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:65:3
      at /home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:42:5
      at validateObject (/home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:208:22)
      at validate (/home/theia/node_modules/copy-webpack-plugin/node_modules/schema-utils/dist/validate.js:187:14)
      at new CopyPlugin (/home/theia/node_modules/copy-webpack-plugin/dist/index.js:38:31)
      at Object.<anonymous> (/home/theia/browser-app/gen-webpack.config.js:28:5)
      at Module._compile (node:internal/modules/cjs/loader:1554:14)

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



{
    "name": "gsc.scheduling.theia",
    "private": true,
    "engines": {
        "node": ">=20"
    },
    "workspaces": [
        "extensions/*",
        "browser-app",
        "browser-app-cesium"
    ],
    "scripts": {
        "clean": "npm run -s rebuild:clean && npm run -s lint:clean && lerna run clean",
        "compile": "lerna run compile",
        "build:extensions": "lerna run --scope=\"@uzay/*\" build",
        "build:electron": "npm run compile && npm run build:extensions && cd electron-app && npm run build",
        "build:browser-app-cesium": "npm run compile && npm run build:extensions && cd browser-app-cesium && npm run build",
        "build:browser-app-cesium:prod": "npm run compile && npm run build:extensions && cd browser-app-cesium && npm run build:prod",
        "build:browser": "npm run compile && npm run build:extensions && cd browser-app && npm run build",
        "build:browser:prod": "npm run compile && npm run build:extensions && cd browser-app && npm run build:prod",
        "download:plugins": "theia download:plugins --rate-limit=15 --parallel=false --ignore-errors",
        "test": "lerna run test",
        "mimic": "cd mimic-viewer && npm run build",
        "lint": "lerna run lint",
        "lint:fix": "lerna run lint -- --fix",
        "postinstall": "theia check:theia-version",
        "rebuild:clean": "rimraf node_modules",
        "rebuild:browser": "cd browser-app && npm run rebuild",
        "rebuild:electron": "cd electron-app && npm run rebuild",
        "start:browser": "cd browser-app && npm run start",
        "start:electron": "cd electron-app && npm run start"
    },
    "devDependencies": {
        "@typescript-eslint/eslint-plugin": "^7.18.0",
        "@typescript-eslint/eslint-plugin-tslint": "^7.0.2",
        "@typescript-eslint/parser": "^7.18.0",
        "eslint": "8",
        "eslint-plugin-deprecation": "^3.0.0",
        "eslint-plugin-import": "^2.27.5",
        "eslint-plugin-no-null": "latest",
        "eslint-plugin-no-unsanitized": "latest",
        "eslint-plugin-react": "^7.31.10",
        "lerna": "^9.0.0",
        "rimraf": "^5.0.0",
        "terser-webpack-plugin": "^5.6.1",
        "typescript": "~5.9.3",
        "webpack-cli": "^7.2.2"
    },
    "dependencies": {
        "@emotion/react": "^11.14.0",
        "@emotion/styled": "^11.14.1",
        "@tanstack/react-table": "8.21.3",
        "@uzay/gsc-files-extension": "^1.0.0",
        "cesium": "^1.142.0",
        "dotenv": "^17.4.2",
        "drivelist": "^12.0.2",
        "react": "^18.2.0",
        "react-dom": "^18.2.0",
        "react-icons": "^5.6.0",
        "theia": "^2.1.2"
    },
    "overrides": {
        "ajv": "^8.12.0",
        "@theia/core": "1.72.0",
        "@theia/application-package": "1.72.0",
        "@theia/request": "1.72.0",
        "@theia/application-manager": "1.72.0",
        "typescript": "~5.9.3"
    },
    "theiaPluginsDir": "plugins",
    "theiaPlugins": {
        "vscode.theme-monokai": "https://open-vsx.org/api/vscode/theme-monokai/1.95.3/file/vscode.theme-monokai-1.95.3.vsix",
        "material-icon-theme": "https://open-vsx.org/api/PKief/material-icon-theme/5.30.0/file/PKief.material-icon-theme-5.30.0.vsix",
        "svg-code-editor": "https://open-vsx.org/api/jock/svg/1.5.3/file/jock.svg-1.5.3.vsix",
        "vscode.markdown": "https://open-vsx.org/api/vscode/markdown/1.95.3/file/vscode.markdown-1.95.3.vsix",
        "sqltools": "https://open-vsx.org/api/mtxr/sqltools/0.28.5/file/mtxr.sqltools-0.28.5.vsix",
        "sqltools-pg": "https://open-vsx.org/api/mtxr/sqltools-driver-pg/0.5.6/file/mtxr.sqltools-driver-pg-0.5.6.vsix"
    }
}
