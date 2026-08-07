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

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

// ===================================================
// MERKEZİ SABİTLER
// ===================================================
const ROOT_NODE_MODULES = path.resolve(__dirname, '../node_modules');
const CESIUM_BUILD = path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium');

// ===================================================
// 1. CESIUM STATIK DOSYALARINI KOPYALAYAN PLUGIN
// ===================================================
const copyCesiumPlugin = {
    name: 'copy-cesium-assets',
    setup(build) {
        build.onEnd(() => {
            const outdir = build.initialOptions.outdir || path.resolve(__dirname, 'lib', 'frontend');
            const cesiumDest = path.join(outdir, 'cesium');

            const copies = [
                { from: path.join(CESIUM_BUILD, 'Workers'), to: path.join(cesiumDest, 'Workers') },
                { from: path.join(CESIUM_BUILD, 'ThirdParty'), to: path.join(cesiumDest, 'ThirdParty') },
                { from: path.join(CESIUM_BUILD, 'Assets'), to: path.join(cesiumDest, 'Assets') },
                { from: path.join(CESIUM_BUILD, 'Widgets'), to: path.join(cesiumDest, 'Widgets') },
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
// 2. MODÜL ÇÖZÜMLEME (RESOLUTION) PLUGINİ
//    Webpack'teki resolve.alias ve Module._resolveFilename karşılığı
// ===================================================
const aliasMap = {
    'react': path.resolve(ROOT_NODE_MODULES, 'react'),
    'react-dom': path.resolve(ROOT_NODE_MODULES, 'react-dom'),
    'parcel-watcher': path.resolve(ROOT_NODE_MODULES, '@parcel/watcher'),
    '@theia/filesystem/lib/node/parcel-watcher': path.resolve(ROOT_NODE_MODULES, '@parcel/watcher'),
    '@uzay/gsc-core-extension': path.resolve(ROOT_NODE_MODULES, '@uzay/gsc-core-extension'),
};

const resolveAliasPlugin = {
    name: 'resolve-alias',
    setup(build) {
        // Cesium bare import -> ES module source
        build.onResolve({ filter: /^cesium$/ }, () => ({
            path: path.resolve(ROOT_NODE_MODULES, 'cesium/Source/Cesium.js'),
        }));

        // Cesium CSS yönlendirmesi
        build.onResolve({ filter: /^cesium\/Build\/Cesium\/Widgets\/widgets\.css$/ }, () => ({
            path: path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium/Widgets/widgets.css'),
        }));

        // Diğer alias'lar
        for (const [key, target] of Object.entries(aliasMap)) {
            const escapedKey = key.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
            build.onResolve({ filter: new RegExp(`^${escapedKey}$`) }, () => ({
                path: target,
            }));
        }

        // @vscode/ripgrep yönlendirmesi
        build.onResolve({ filter: /^@vscode\/ripgrep/ }, (args) => {
            const targetPath = args.path === '@vscode/ripgrep/bin/rg'
                ? path.resolve(ROOT_NODE_MODULES, '@vscode/ripgrep/bin/rg')
                : path.resolve(ROOT_NODE_MODULES, '@vscode/ripgrep');
            return { path: targetPath };
        });
    }
};

// ===================================================
// 3. FRONTEND (BROWSER) YAPILANDIRMASI
// ===================================================

// Webpack DefinePlugin karşılığı
if (!browserOptions.define) browserOptions.define = {};
browserOptions.define['CESIUM_BASE_URL'] = JSON.stringify('/cesium/');

// Modül arama yolları (webpack resolve.modules karşılığı)
if (!browserOptions.nodePaths) browserOptions.nodePaths = [];
if (!browserOptions.nodePaths.includes(ROOT_NODE_MODULES)) {
    browserOptions.nodePaths.push(ROOT_NODE_MODULES);
}

// Plugin'leri ekle
if (!browserOptions.plugins) browserOptions.plugins = [];
browserOptions.plugins.push(resolveAliasPlugin);
browserOptions.plugins.push(copyCesiumPlugin);
browserOptions.plugins.push(sourceMapPathsPlugin());

// ===================================================
// 4. BACKEND (NODE) YAPILANDIRMASI
// ===================================================

// Native modülleri bundle dışı bırak (webpack externals karşılığı)
if (!nodeOptions.external) nodeOptions.external = [];
const nativeExternals = ['keytar', 'node-pty', 'nsfw', 'parcel-watcher', 'sqlite3', 'drivelist'];
for (const ext of nativeExternals) {
    if (!nodeOptions.external.includes(ext)) {
        nodeOptions.external.push(ext);
    }
}

// Modül arama yolları
if (!nodeOptions.nodePaths) nodeOptions.nodePaths = [];
if (!nodeOptions.nodePaths.includes(ROOT_NODE_MODULES)) {
    nodeOptions.nodePaths.push(ROOT_NODE_MODULES);
}

// Plugin'leri ekle
if (!nodeOptions.plugins) nodeOptions.plugins = [];
nodeOptions.plugins.push(resolveAliasPlugin);
nodeOptions.plugins.push(sourceMapPathsPlugin());

// ===================================================
// 5. BUILD ÇALIŞTIR
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
