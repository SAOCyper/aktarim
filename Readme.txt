{
    "name": "@uzay/gsc-core-extension",
    "version": "1.0.0",
    "description": "SOC Core — Theia RPC bridge (backend → SocDataService). Required by all other SOC extensions.",
    "license": "MIT",
    "main":"lib/browser/common-index.js",
    "typings":"lib/browser/common-index.d.ts",
    "keywords": [
        "theia-extension",
        "satellite"
    ],
    "files": [
        "lib",
        "src"
    ],
    "theiaExtensions": [
        {
            "frontend": "lib/browser/soc-core-frontend-module",
            "backend": "lib/node/soc-core-backend-module"
        }
    ],
    "dependencies": {
        "recharts": "^2.15.1",
        "@uzay/gss-messaging": "^0.1.1",
        "sqlite3": "^5.1.7",
        "busboy": "^1.6.0"
    },
    "peerDependencies": {
        "@theia/core": "1.72.0",
        "cesium":"1.138.0",
        "react": "^18.2.0",
        "react-dom": "^18.2.0"
    },
    "devDependencies": {
        "@types/react":"^18.2.0",
        "@types/react-dom": "^18.2.0",
        "react": "^18.2.0",
        "react-dom":"^18.2.0",
        "rimraf": "^5.0.0",
        "typescript": "~5.9.3"
    },
    "scripts": {
        "clean": "rimraf lib",
        "build": "tsc",
        "watch": "tsc -w"
    }
}
