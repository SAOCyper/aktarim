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
        "esbuild":"^0.28.2",
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
        "webpack": "^5.89.0",
        "webpack-cli": "^5.1.4",
        "copy-webpack-plugin": "^11.0.0",
        "html-webpack-plugin": "^5.6.0",
        "ajv": "^8.12.0",
        "ajv-keywords": "^5.1.0",
        "ajv-formats": "^2.1.1"
    },
    "dependencies": {
        "@emotion/react": "^11.14.0",
        "@emotion/styled": "^11.14.1",
        "@tanstack/react-table": "8.21.3",
        "cesium": "^1.142.0",
        "dotenv": "^17.4.2",
        "drivelist": "^12.0.2",
        "react": "^18.2.0",
        "react-dom": "^18.2.0",
        "react-icons": "^5.6.0",
        "theia": "^2.1.2"
    },
    "overrides": {
        "@theia/core": "1.74.1",
        "@theia/application-package": "1.74.1",
        "@theia/request": "1.74.1",
        "@theia/application-manager": "1.74.1",
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
