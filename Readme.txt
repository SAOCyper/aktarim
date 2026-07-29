const counts: Record<string, number> = {};
            allPasses.forEach((p: any) => {
                counts[p.gsId] = (counts[p.gsId] || 0) + 1;
            });
            console.log('[FILTER-DEBUG] Total passes in memory:', allPasses.length, 'Pass counts by gsId:', counts, 'Sample pass:', allPasses[0], 'Ground stations:', groundStations);
