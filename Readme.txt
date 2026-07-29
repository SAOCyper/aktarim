if (passList.length > 0) {
        let gsIdFromCorr = 'ALL';
        
        // Burası correlation ID başlığından istasyonu (örn. TROMSO) ayıklar
        if (rawCorrId.startsWith('FILTEREDPASS:')) {
          const parts = rawCorrId.substring('FILTEREDPASS:'.length).split('_');
          if (parts.length > 0 && parts[0]) {
            gsIdFromCorr = parts[0];
          }
        }
        this.logger.log(`[GSC-PASSCALC] Catch-all routing for ID: "${rawCorrId}" | Resolved GS ID: "${gsIdFromCorr}" | Items: ${passList.length}`);
        
        // Ayıklanan istasyon bilgisini normalleştirme metoduna gönderir
        const normalizedPasses = passList.map(p => this.normalizePass(p, gsIdFromCorr));
        
        // Backend hafızasına kaydeder
        await this.satelliteAppService.saveInMemoryPrecalculatedPasses(normalizedPasses);
        this.gateway.broadcast('pass_prediction', { count: normalizedPasses.length, gsId: gsIdFromCorr, passes: normalizedPasses });
      } else {
        this.logger.debug(`[GSC-PASSCALC] Discarded message (Empty or Non-relevant) | ID: ${rawCorrId}`);
      }
