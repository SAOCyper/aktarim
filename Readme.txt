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
