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
// ===================================================
// Theia, inversify, react gibi singleton olmasi gereken paketleri her zaman
// root node_modules'den coz. Bu sayede birden fazla ornekten kaynakli
// "Cannot find symbol" hatalari onlenir.
//
// @uzay/* paketleri icin: subpath importlari uzantisiz olabilir (ornegin
// "lib/browser/soc-frontend-module") -- bunlari once direkt resolve etmeyi
// dene, olmazsa ".js" ekleyerek tekrar dene.
const forceRootModulesPlugin = {
    name: 'force-root-modules',
    setup(build) {
        build.onResolve(
            { filter: /^(@theia\/|@uzay\/|inversify(\/|$)|reflect-metadata(\/|$)|react(\/|-dom\/|$)|react-dom(\/|$))/ },
            (args) => {
                if (args.kind === 'entry-point') return undefined;

                // Once uzantisiz olarak dene, sonra .js ekleyerek
                const candidates = [args.path, args.path + '.js'];
                for (const candidate of candidates) {
                    try {
                        const resolved = _require.resolve(candidate);
                        return { path: resolved };
                    } catch {
                        // bir sonrakini dene
                    }
                }
                return undefined;
            }
        );
    }
};

// ===================================================
// 2. CESIUM STATIK DOSYALARI KOPYALAYAN PLUGIN
// ===================================================
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

// ===================================================
// 3. BROWSER BUILD
// ===================================================
const customBrowserPlugins = [
    forceRootModulesPlugin,
    sourceMapPathsPlugin,
    cesiumCopyPlugin
];

const customBrowserOptions = {
    ...browserOptions,
    plugins: [
        ...(browserOptions.plugins || []).filter(p =>
            p.name !== 'force-root-modules' &&
            p.name !== 'cesium-copy'
        ),
        ...customBrowserPlugins
    ],
    define: {
        ...(browserOptions.define || {}),
        CESIUM_BASE_URL: JSON.stringify('./cesium'),
    }
};

// ===================================================
// 4. NODE BUILD
// ===================================================
const customNodeOptions = {
    ...nodeOptions,
    plugins: [
        ...(nodeOptions.plugins || []).filter(p =>
            p.name !== 'force-root-modules'
        ),
        forceRootModulesPlugin,
        sourceMapPathsPlugin
    ]
};

// ===================================================
// 5. BUILD CALISTIR
// ===================================================
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
