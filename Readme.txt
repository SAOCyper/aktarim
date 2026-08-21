this.fetchPasses(true).catch(console.error);
            this.fetchDynamicPasses(this.state.gsFilterId).catch(console.error);
        } else if (event === 'config_change_result') {
            console.log('[SocDataService] Received config_change_result broadcast. Reloading passes...');
            this._broadcastEvent(event, data);
            this.fetchPasses(true).catch(console.error);
            this.fetchDynamicPasses(this.state.gsFilterId).catch(console.error);
