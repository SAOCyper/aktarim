const counts: Record<string, number> = {};
        SatelliteApplicationService.inMemoryPrecalculatedPasses.forEach(p => {
            counts[p.gsId] = (counts[p.gsId] || 0) + 1;
        });
        this.logger.log(`[InMemory-Passes] Current memory counts by GS: ${JSON.stringify(counts)}`);
