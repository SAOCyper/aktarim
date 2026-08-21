const cleanSId = String(s.id || '').replace('SAT-', '').trim();
                const cleanSNorad = String(s.noradId || '').replace('SAT-', '').trim();
                const cleanTarget = String(selectedNode.satNo || '').replace('SAT-', '').trim();
                return cleanSId === cleanTarget || cleanSNorad === cleanTarget;
