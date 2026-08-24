const mergeDataset = (backendItems: any[], prevItems: any[]) => {
                        const prevMap = new Map((prevItems || []).map((i: any) => [`${i.dataset}/${i.filename}`, i]));
                        return (backendItems || []).map((m: any) => {
                            const key = `${m.dataset}/${m.filename}`;
                            const existing = prevMap.get(key);
                            return {
                                ...m,
                                enabled: existing ? existing.enabled : (m.enabled ?? true)
                            };
                        });
                    };
                    console.log('[EarthViewer] Successfully auto-discovered and applied MBTiles:', normalized);
                    // localStorage'a yaz ki reload'da hizli yuklensin
                    try { localStorage.setItem('soc_mbtiles', JSON.stringify(normalized)); } catch { }
                    return normalized;
                    const updated = {
                        earth: mergeDataset(data.earth || [], prev?.earth || []),
                        moon: mergeDataset(data.moon || [], prev?.moon || [])
                    };
                    console.log('[EarthViewer] Successfully auto-discovered and applied MBTiles:', updated);
                    try { localStorage.setItem('soc_mbtiles', JSON.stringify(updated)); } catch { }
                    return updated;
