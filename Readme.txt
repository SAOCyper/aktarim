// Guncellenen yer istasyonlarini bulalim
        const gsIdsToUpdate = new Set<string>();
        passes.forEach(p => {
            const gsIdStr = String(p.gsId || p.groundStationId);
            if (gsIdStr && gsIdStr !== 'undefined' && gsIdStr !== 'null') {
                gsIdsToUpdate.add(gsIdStr);
            }
        });

        // Sadece guncellenen istasyonlarin hafizadaki eski pass'lerini temizleyelim
        const currentPasses = SatelliteApplicationService.inMemoryPrecalculatedPasses.filter(p => {
            const gsIdStr = String(p.gsId || p.groundStationId);
            return !gsIdsToUpdate.has(gsIdStr);
        });
