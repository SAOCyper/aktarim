/**
 * Ozel esbuild yapilandirmasi.
 * Sadece @uzay/* ve @theia/* gibi paketlerin root node_modules'den
 * cozumlenmesini zorlar. Diger her sey Theia'nin urettigi ayarlarla devam eder.
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
            { filter: /^(@theia\/|@uzay\/|inversify(\/|$)|reflect-metadata(\/|$)|react(\/|-dom\/|$)|react-dom(\/|$))/ },
            (args) => {
                if (args.kind === 'entry-point') return undefined;

                // Once uzantisiz dene, olmadiysa .js ekle
                const candidates = [args.path, args.path + '.js'];
                for (const candidate of candidates) {
                    try {
                        return { path: _require.resolve(candidate) };
                    } catch {
                        // sonrakini dene
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
    }
};

const customNodeOptions = {
    ...nodeOptions,
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
