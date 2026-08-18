/**
 * Bu dosya esbuild yapılandırmasını özelleştirmek için düzenlenebilir.
 * Sıfırlamak için bu dosyayı silip theia build komutunu tekrar çalıştırın.
 */
import { browserOptions, watch } from './gen-esbuild.browser.mjs';
import { nodeOptions } from './gen-esbuild.node.mjs';
import { sourceMapPathsPlugin } from '@theia/bundle-plugin';
import esbuild from 'esbuild';
import * as path from 'path';
import * as fs from 'fs';
import { fileURLToPath } from 'url';
import { createRequire } from 'module';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

// createRequire: ESM icinden require.resolve kullanabilmek icin
const _require = createRequire(import.meta.url);

// ===================================================
// MERKEZI SABITLER
// ===================================================
const ROOT_NODE_MODULES = path.resolve(__dirname, '../node_modules');
const CESIUM_BUILD = path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium');

// ===================================================
// 1. TEKIL MODUL ZORLAYICI (SINGLETON RESOLVER)
//    "Cannot apply @injectable decorator multiple times" hatasinin cozumu.
//    inversify, reflect-metadata ve react'in birden fazla kopyas
//    bundle'a girerse InversifyJS coker. Bu plugin hepsini
//    root node_modules'daki TEK kopyaya yonlendirir.
// ===================================================
function resolveToFile(pkgName) {
    try {
        return _require.resolve(pkgName);
    } catch {
        return null;
    }
}

const SINGLETON_PACKAGES = {
    'inversify':                    resolveToFile('inversify'),
    'reflect-metadata':             resolveToFile('reflect-metadata'),
    'react':                        resolveToFile('react'),
    'react-dom':                    resolveToFile('react-dom'),
    '@theia/core/shared/inversify': resolveToFile('inversify'),
};

const singletonResolverPlugin = {
    name: 'singleton-resolver',
    setup(build) {
        for (const [pkgName, resolvedPath] of Object.entries(SINGLETON_PACKAGES)) {
            if (!resolvedPath) continue;
            const escapedName = pkgName.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
            build.onResolve({ filter: new RegExp(`^${escapedName}$`) }, () => ({
                path: resolvedPath,
            }));
        }
    }
};

// ===================================================
// 2. CESIUM STATIK DOSYALARINI KOPYALAYAN PLUGIN
// ===================================================
const copyCesiumPlugin = {
    name: 'copy-cesium-assets',
    setup(build) {
        build.onEnd(() => {
            const outdir = build.initialOptions.outdir || path.resolve(__dirname, 'lib', 'frontend');
            const cesiumDest = path.join(outdir, 'cesium');

            const copies = [
                { from: path.join(CESIUM_BUILD, 'Workers'),    to: path.join(cesiumDest, 'Workers') },
                { from: path.join(CESIUM_BUILD, 'ThirdParty'), to: path.join(cesiumDest, 'ThirdParty') },
                { from: path.join(CESIUM_BUILD, 'Assets'),     to: path.join(cesiumDest, 'Assets') },
                { from: path.join(CESIUM_BUILD, 'Widgets'),    to: path.join(cesiumDest, 'Widgets') },
            ];

            for (const { from, to } of copies) {
                if (fs.existsSync(from)) {
                    fs.cpSync(from, to, { recursive: true });
                    console.log(`[CopyCesium] ${path.basename(from)} -> ${to}`);
                } else {
                    console.warn(`[CopyCesium] WARN: Source not found: ${from}`);
                }
            }
        });
    }
};

// ===================================================
// 3. CESIUM BARE IMPORT RESOLVER
// ===================================================
const cesiumResolverPlugin = {
    name: 'cesium-resolver',
    setup(build) {
        build.onResolve({ filter: /^cesium$/ }, () => ({
            path: path.resolve(ROOT_NODE_MODULES, 'cesium/Source/Cesium.js'),
        }));
        build.onResolve({ filter: /^cesium\/Build\/Cesium\/Widgets\/widgets\.css$/ }, () => ({
            path: path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium/Widgets/widgets.css'),
        }));
    }
};

// ===================================================
// 4. FRONTEND (BROWSER) YAPILANDIRMASI
// ===================================================

if (!browserOptions.define) browserOptions.define = {};
browserOptions.define['CESIUM_BASE_URL'] = JSON.stringify('/cesium/');
browserOptions.define['process.env.NODE_ENV'] = JSON.stringify(
    process.env.NODE_ENV || 'production'
);

if (!browserOptions.nodePaths) browserOptions.nodePaths = [];
browserOptions.nodePaths.unshift(ROOT_NODE_MODULES);

// singletonResolverPlugin en BASA gelmeli
if (!browserOptions.plugins) browserOptions.plugins = [];
browserOptions.plugins.unshift(singletonResolverPlugin);
browserOptions.plugins.push(cesiumResolverPlugin);
browserOptions.plugins.push(copyCesiumPlugin);
browserOptions.plugins.push(sourceMapPathsPlugin());

// ===================================================
// 5. BACKEND (NODE) YAPILANDIRMASI
// ===================================================

if (!nodeOptions.external) nodeOptions.external = [];
const nativeExternals = [
    'keytar', 'node-pty', 'nsfw', 'sqlite3', 'drivelist', 'cesium',
];
for (const ext of nativeExternals) {
    if (!nodeOptions.external.includes(ext)) nodeOptions.external.push(ext);
}

if (!nodeOptions.nodePaths) nodeOptions.nodePaths = [];
nodeOptions.nodePaths.unshift(ROOT_NODE_MODULES);

if (!nodeOptions.plugins) nodeOptions.plugins = [];
nodeOptions.plugins.unshift(singletonResolverPlugin);
nodeOptions.plugins.push(sourceMapPathsPlugin());

// ===================================================
// 6. BUILD CALISTIR
// ===================================================
const args = process.argv.slice(2);
const isWatch = args.includes('--watch') || watch;

async function runBuild() {
    try {
        if (isWatch) {
            const browserCtx = await esbuild.context(browserOptions);
            const nodeCtx = await esbuild.context(nodeOptions);
            await Promise.all([browserCtx.watch(), nodeCtx.watch()]);
            console.log('[esbuild] Watching for changes...');
        } else {
            await Promise.all([
                esbuild.build(browserOptions),
                esbuild.build(nodeOptions),
            ]);
            console.log('[esbuild] Build completed successfully.');
        }
    } catch (err) {
        console.error('[esbuild] Build failed:', err);
        process.exit(1);
    }
}

runBuild();
