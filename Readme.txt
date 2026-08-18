/**
 * Bu dosya esbuild yapilandirmasini ozellestirmek icin duzenlenebilir.
 * Sifirlamak icin bu dosyayi silip theia build komutunu tekrar calistirin.
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
const _require = createRequire(import.meta.url);

// ===================================================
// MERKEZI SABITLER
// ===================================================
const ROOT_NODE_MODULES = path.resolve(__dirname, '../node_modules');
const CESIUM_BUILD = path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium');

// ===================================================
// 1. ROOT MODULLERI ZORLAYICI PLUGIN
//    "Cannot apply @injectable decorator multiple times" hatasinin cozumu.
//
//    Neden olur: extensions/*/node_modules/ icinde @theia/core veya inversify
//    kopyasi varsa, esbuild ayni sinifi iki farkli fiziksel yoldan alir ve
//    bundle'a iki kez koyar. @injectable her iki kopyada da calisir -> hata.
//
//    Cozum: @theia/*, inversify, reflect-metadata importlarini her zaman
//    root /home/theia/node_modules/ icindeki TEK kopyaya yonlendir.
// ===================================================
const forceRootModulesPlugin = {
    name: 'force-root-modules',
    setup(build) {
        build.onResolve(
            { filter: /^(@theia\/|inversify(\/|$)|reflect-metadata(\/|$)|react(\/|-dom\/|$)|react-dom(\/|$))/ },
            (args) => {
                // Dosya icindeki goreli import degilse (ornegin node_modules'den gelen)
                if (args.kind === 'entry-point') return undefined;

                try {
                    // require.resolve: esbuild.mjs'nin konumundan (browser-app/) calisir
                    // Bu yuzden root node_modules'e hoisted olan surumu bulur
                    const resolved = _require.resolve(args.path);
                    return { path: resolved };
                } catch {
                    // Cozemezse esbuild'in varsayilan cozumleme mantigi devreye girer
                    return undefined;
                }
            }
        );
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
// 3. CESIUM RESOLVER
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

// forceRootModulesPlugin en BASA gelmeli ki diger pluginlerden once calissin
if (!browserOptions.plugins) browserOptions.plugins = [];
browserOptions.plugins.unshift(forceRootModulesPlugin);
browserOptions.plugins.push(cesiumResolverPlugin);
browserOptions.plugins.push(copyCesiumPlugin);
browserOptions.plugins.push(sourceMapPathsPlugin());

// ===================================================
// 5. BACKEND (NODE) YAPILANDIRMASI
// ===================================================

if (!nodeOptions.external) nodeOptions.external = [];
const nativeExternals = ['keytar', 'node-pty', 'nsfw', 'sqlite3', 'drivelist', 'cesium'];
for (const ext of nativeExternals) {
    if (!nodeOptions.external.includes(ext)) nodeOptions.external.push(ext);
}

if (!nodeOptions.nodePaths) nodeOptions.nodePaths = [];
nodeOptions.nodePaths.unshift(ROOT_NODE_MODULES);

if (!nodeOptions.plugins) nodeOptions.plugins = [];
nodeOptions.plugins.unshift(forceRootModulesPlugin);
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
