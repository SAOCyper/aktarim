    // ─────────────────────────────────────────────────────────────────────────
    // BAGIMSIZ MBTILES KESFI
    // Files extension yuklu olmasa bile disk'te .mbtiles dosyasi varsa
    // otomatik olarak haritaya yukle.
    // Oncelik sirasi:
    //   1. BroadcastChannel (files extension aciksa, o yonetir)
    //   2. localStorage cache (onceki oturum)
    //   3. /mbtiles/list dogrudan fetch (files extension yok, disk'e bak)
    // ─────────────────────────────────────────────────────────────────────────
    useEffect(() => {
        const fetchMbtilesFromBackend = async () => {
            try {
                const res = await fetch(`${Config.API_URL}/mbtiles/list`);
                if (!res.ok) return;
                const data: { earth: any[]; moon: any[] } = await res.json();
                const hasAny =
                    (data.earth && data.earth.length > 0) ||
                    (data.moon  && data.moon.length  > 0);
                if (!hasAny) return; // disk'te hic dosya yok, state'i bozma
                // Tum bulunan dosyalari enabled olarak isle
                const normalized = {
                    earth: (data.earth || []).map((m: any) => ({ ...m, enabled: m.enabled ?? true })),
                    moon:  (data.moon  || []).map((m: any) => ({ ...m, enabled: m.enabled ?? true })),
                };
                setMbtilesData(prev => {
                    // Eger BroadcastChannel veya localStorage'dan zaten veri geldiyse dokunma
                    const prevHasAny =
                        (prev.earth && prev.earth.length > 0) ||
                        (prev.moon  && prev.moon.length  > 0);
                    if (prevHasAny) return prev;
                    console.log('[EarthViewer] Auto-discovered MBTiles from backend:', normalized);
                    // localStorage'a yaz ki reload'da hizli yuklensin
                    try { localStorage.setItem('soc_mbtiles', JSON.stringify(normalized)); } catch { }
                    return normalized;
                });
            } catch (e) {
                console.warn('[EarthViewer] Could not fetch /mbtiles/list:', e);
