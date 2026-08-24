/**
 * Ozel esbuild yapilandirmasi.
 * - @uzay/*, @theia/* gibi paketleri root node_modules'den cozer
 * - Browser build'e Cesium statik dosyalarini kopyalar
 * - Node/backend build'de cesium'u external olarak isaret eder
 *   (Cesium browser-only bir kutuphanedir, backend bundle'ina girmemeli)
 */
import { browserOptions, watch } from './gen-esbuild.browser.mjs';
import { nodeOptions } from './gen-esbuild.node.mjs';
import esbuild from 'esbuild';
import * as path from 'path';
import * as fs from 'fs';
import { fileURLToPath } from 'url';
import { createRequire } from 'module';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
const _require = createRequire(import.meta.url);

const ROOT_NODE_MODULES = path.resolve(__dirname, '../node_modules');
const CESIUM_BUILD = path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium');

/**
 * Bu plugin; @theia/*, @uzay/*, inversify, reflect-metadata ve react gibi
 * singleton olmasi gereken paketleri root node_modules uzerinden cozer.
 * Uzantisiz subpath'ler icin once direkt dener, olmazsa .js ekleyerek tekrar dener.
 */
const forceRootModulesPlugin = {
    name: 'force-root-modules',
    setup(build) {
        build.onResolve(
            { filter: /^(@theia\/|@uzay\/|cesium(\/|$)|.*Build\/Cesium|inversify(\/|$)|reflect-metadata(\/|$)|react(\/|-dom\/|$)|react-dom(\/|$))/ },
            (args) => {
                if (args.kind === 'entry-point') return undefined;

                if (args.path.includes('Build/Cesium')) {
                    try {
                        const sub = args.path.substring(args.path.indexOf('Build/Cesium'));
                        return { path: _require.resolve('cesium/' + sub) };
                    } catch {}
                }

                if (args.path === 'cesium') {
                    try {
                        return { path: _require.resolve('cesium/Build/Cesium/index.cjs') };
                    } catch {}
                }

                // 1. Once standart _require.resolve ile dene (uzantisiz ve .js ile)
                const candidates = [args.path, args.path + '.js'];
                for (const candidate of candidates) {
                    try {
                        return { path: _require.resolve(candidate) };
                    } catch {}
                }

                // 2. Node 22 subpath require.resolve basarisiz olursa, @uzay/* paketlerini workspace extensions klasorunden acikca coz
                if (args.path.startsWith('@uzay/')) {
                    const parts = args.path.split('/');
                    const scope = parts[0];
                    const pkgName = parts[1];
                    const subpath = parts.slice(2).join('/');

                    if (subpath) {
                        const baseDirs = [
                            path.resolve(__dirname, '../extensions', pkgName),
                            path.resolve(ROOT_NODE_MODULES, scope, pkgName)
                        ];
                        const suffixes = ['.js', '', '/index.js'];
                        for (const base of baseDirs) {
                            for (const suf of suffixes) {
                                const fullPath = path.resolve(base, subpath + suf);
                                if (fs.existsSync(fullPath) && fs.statSync(fullPath).isFile()) {
                                    return { path: fullPath };
                                }
                            }
                        }
                    }
                }

                return undefined;
            }
        );
    }
};

/**
 * Cesium statik dosyalarini (Build/Cesium/) cikti klasorune kopyalar.
 */
const cesiumCopyPlugin = {
    name: 'cesium-copy',
    setup(build) {
        build.onEnd(async () => {
            const outdir = build.initialOptions.outdir;
            if (!outdir) return;

            const dest = path.join(outdir, 'cesium');
            if (fs.existsSync(dest)) return;

            if (!fs.existsSync(CESIUM_BUILD)) {
                console.warn('[cesium-copy] Cesium Build klasoru bulunamadi:', CESIUM_BUILD);
                return;
            }

            console.log('[cesium-copy] Cesium statik dosyalari kopyalaniyor...');
            fs.mkdirSync(dest, { recursive: true });
            copyDirSync(CESIUM_BUILD, dest);
            console.log('[cesium-copy] Cesium dosyalari kopyalandi.');
        });
    }
};

function copyDirSync(src, dest) {
    const entries = fs.readdirSync(src, { withFileTypes: true });
    for (const entry of entries) {
        const srcPath = path.join(src, entry.name);
        const destPath = path.join(dest, entry.name);
        if (entry.isDirectory()) {
            fs.mkdirSync(destPath, { recursive: true });
            copyDirSync(srcPath, destPath);
        } else {
            fs.copyFileSync(srcPath, destPath);
        }
    }
}

// Mevcut Theia plugin listesine ekle, hicbirini cikarma
const customBrowserOptions = {
    ...browserOptions,
    plugins: [
        forceRootModulesPlugin,
        cesiumCopyPlugin,
        ...(browserOptions.plugins || [])
    ],
    define: {
        ...(browserOptions.define || {}),
        CESIUM_BASE_URL: JSON.stringify('./cesium'),
        __dirname: '""',
        __filename: '""',
        global: 'window'
    }
};

const customNodeOptions = {
    ...nodeOptions,
    // Cesium browser-only kutuphanesidir, backend bundle'ina girmesin.
    // Girerse icindeki relative require('./Build/CesiumUnminified/...') calisma
    // zamaninda yanlis path'e bakar ve MODULE_NOT_FOUND hatasi verir.
    external: [...(nodeOptions.external || []), 'cesium'],
    plugins: [
        forceRootModulesPlugin,
        ...(nodeOptions.plugins || [])
    ]
};

if (watch) {
    const [browserCtx, nodeCtx] = await Promise.all([
        esbuild.context(customBrowserOptions),
        esbuild.context(customNodeOptions)
    ]);
    await Promise.all([
        browserCtx.watch(),
        nodeCtx.watch()
    ]);
} else {
    await Promise.all([
        esbuild.build(customBrowserOptions),
        esbuild.build(customNodeOptions)
    ]);
}
