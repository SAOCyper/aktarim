/**
 * This file can be edited to customize webpack configuration.
 * To reset delete this file and rerun theia build again.
 */
// @ts-check
const path = require('path');
const webpack = require('webpack');
const CopyPlugin = require('copy-webpack-plugin');
const configs = require('./gen-webpack.config.js');
const nodeConfig = require('./gen-webpack.node.config.js');

// ------ MERKEZİ SABİTLER ----
const ROOT_NODE_MODULES = path.resolve('/home/theia/node_modules');
const CESIUM_BUILD = path.resolve(__dirname, '../node_modules/cesium/Build/Cesium');


// ===================================================
// 1. SİSTEM SEVİYESİ YAMALAR (RESOLUTION HACKS)
// ===================================================
applyLowLevelResolutionHacks();

// ===================================================
// 2. BACKEND NATIVE MODÜL AYARLARI
// ===================================================
const nativeExternals = {
    'keytar': 'commonjs keytar',
    'node-pty': 'commonjs node-pty',
    'nsfw': 'commonjs nsfw',
    'parcel-watcher': 'commonjs parcel-watcher',
    'sqlite3' : 'commonjs sqlite3',
    'drivelist': 'commonjs drivelist'
};
injectNativeExternals(nodeConfig.config, nativeExternals);

// ===================================================
// 3. ANA YAPILANDIRMA YAMALAYICI (ORKESTRASYON)
// ===================================================
function patchConfig(config) {
    if (!config) return config;

    setupModulePaths(config);
    setupAliases(config);
    setupPlugins(config);

    return config;
}

// ===================================================
// EXPORT
// ===================================================
module.exports = [
    ...configs.map(patchConfig),
    patchConfig(nodeConfig.config)
];

// ===================================================
// YARDIMCI FONKSİYONLAR (ALT MANTIKLAR)
// ===================================================

/**
 * Parcel-watcher ve ripgrep gibi kritik araçların yollarını çalışma zamanından önce düzenltir.
 */
function applyLowLevelResolutionHacks() {
    const Module = require('module');
    // @ts-ignore
    const originalResolveFilename = Module._resolveFilename;

    Module._resolveFilename = function (request, parent, isMain) {
        if (request === '@theia/filesystem/lib/node/parcel-watcher' || request === 'parcel-watcher') {
            try { return originalResolveFilename.apply(this, [path.resolve(__dirname, '../../node_modules/@parcel/watcher'), parent, isMain]); } catch (e)  {}
        }
        if (request === '@vscode/ripgrep/bin/rg' || request === '@vscode/ripgrep') {
            try {
                const targetPath = request === '@vscode/ripgrep/bin/rg'
                    ? path.resolve(__dirname, '../../node_modules/@vscode/ripgrep/bin/rg')
                    : path.resolve(__dirname, '../../node_modules/@vscode/ripgrep');
                return originalResolveFilename.apply(this, [targetPath, parent, isMain]);
            } catch (e) { /* Fallback */ }
        }
        return originalResolveFilename.apply(this, arguments);
    };
}

/**
 * Node.js native addon'larının backend bundle'ına daghil edilmesini engeller.
 */
function injectNativeExternals(targetConfig,externals) {
    if (targetConfig.externals && typeof targetConfig.externals === 'object') {
        Object.assign(targetConfig.externals, externals);
    } else {
        targetConfig.externals = externals;
    }
}

/**
 * Modüllerin ve bağımlılıkların aranacağı ortak klasör önceliklerini belirler.
 */
function setupModulePaths(config) {
    if (!config.resolve) config.resolve = {};
    if (!config.resolve.modules) config.resolve.modules = ['node_modules'];

    const appNodeModules = path.resolve('/home/theia/node_modules');
    if (!config.resolve.modules.includes(appNodeModules)) config.resolve.modules.push(appNodeModules);
    if (!config.resolve.modules.includes(ROOT_NODE_MODULES)) config.resolve.modules.push(ROOT_NODE_MODULES);
}

/***
 * Çakışmaları önlemek için kütüphane takma adlarını (Alias) yapılandırır
 */
function setupAliases(config) {
    if (!config.resolve.alias) config.resolve.alias = {};

    config.resolve.alias['react'] = path.resolve(ROOT_NODE_MODULES, 'react');
    config.resolve.alias['react-dom'] = path.resolve(ROOT_NODE_MODULES, 'react-dom');
    config.resolve.alias['parcel-watcher'] = path.resolve(ROOT_NODE_MODULES, '@parcel/watcher');
    config.resolve.alias['@theia/filesystem/lib/node/parcel-watcher'] = path.resolve(ROOT_NODE_MODULES, '@parcel/watcher');
    
    // Add alias for @uzay/gsc-common to resolve from extensions folder
    config.resolve.alias['@uzay/gsc-common'] = path.resolve(ROOT_NODE_MODULES, '@uzay/gsc-common');

   // Cesium'un dinamik require() krizini çözmek için doğrudan ES kaynak koduna yönlendirme
    config.resolve.alias['cesium$'] = path.resolve(ROOT_NODE_MODULES, 'cesium/Source/Cesium.js');
}

function setupPlugins(config) {
    if (!config.plugins) config.plugins = [];

    // Global Değişken enjeksiyonları (Manuel import yükünü azaltır)
    config.plugins.push(new webpack.ProvidePlugin({
        React: 'react',
        jsx: ['react', 'createElement'],
        jsxs: ['react', 'createElement'],
        jsxDEV: ['react', 'createElement'],
        Cesium: 'cesium',
    }));

    // Sadece Frontend (Tarayıcı için geçerli olan eklentiler)
    if (config.target != 'node') {
        // Cesium'un harita ve worker bileşenlerini çalışma anında bulabilmesi için taban URL enjeksiyonu
        config.plugins.push(new webpack.DefinePlugin({
            'CESIUM_BASE_URL': JSON.stringify('/cesium/'),
        }));

        // Stil dosyası yönlendirmesi
        config.plugins.push(new webpack.NormalModuleReplacementPlugin(
            /^cesium\/Build\/Cesium\/Widgets\/widgets\.css$/,
            path.resolve(ROOT_NODE_MODULES, 'cesium/Build/Cesium/Widgets/widgets.css')
        ));

        // Statik Varlıkların ve Uydu modellerinin Dağıtım Klasörüne Kopyalanması
        config.plugins.push(new CopyPlugin({
            patterns: [
                { from: path.join(CESIUM_BUILD, 'Workers'), to: 'cesium/Workers' },
                { from: path.join(CESIUM_BUILD, 'ThirdParty'), to: 'cesium/ThirdParty' },
                { from: path.join(CESIUM_BUILD, 'Assets'), to: 'cesium/Assets' },
                { from: path.join(CESIUM_BUILD, 'Widgets'), to: 'cesium/Widgets' },
                { from: path.resolve(__dirname, '../gsc-common/public/textures'), to: 'textures' },
                { from: path.resolve(__dirname, '../gsc-common/public/imece-web2.gltf'), to: 'models/imece-web2.gltf'},
                { from: path.resolve(__dirname, '../gsc-common/public/earth'), to: 'earth' },
                { from: path.resolve(__dirname, '../gsc-common/public/moon'), to: 'moon' },
            ]
        }));

    }
}
