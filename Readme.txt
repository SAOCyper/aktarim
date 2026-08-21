const cleanTarget = String(idOrNo).replace('SAT-', '').trim();
        return socState.satellites?.find((s: any) => {
            const sIdClean = String(s.id || '').replace('SAT-', '').trim();
            const sNoradClean = String(s.noradId || '').replace('SAT-', '').trim();
            return sIdClean === cleanTarget || sNoradClean === cleanTarget;
        });
