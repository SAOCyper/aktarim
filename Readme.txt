2026-07-29T08:00:44.846Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-07-29T08:00:44.846Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-07-29T08:00:44.846Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-07-29T08:00:45.706Z root INFO INFO [OdsListenerService] [main.js:1398] [handleOdsRunnerResponse] [GSC-CORR] Resolved meta "PASSTRAJECTORY:56178:REAL" from correlation PASSTRAJECTORY:56178:REAL_1785312044756
2026-07-29T08:00:45.706Z root INFO INFO [OdsListenerService] [main.js:1807] [handlePassTrajectoryResponse] [GSC-PASS-TRAJECTORY] Received 667 trajectory points. SatelliteNo/Norad: 56178, GS: REAL
2026-07-29T08:00:45.857Z root INFO Frontend application startup sequence completed (async work may still be pending): 1895.6 ms [46.440 s since backend process start]
2026-07-29T08:00:45.857Z root INFO Replace loading indicator with ready workbench UI (animation): 1406.0 ms [4.538 s since frontend page start]
2026-07-29T08:00:45.858Z root INFO Changed application state from 'initialized_layout' to 'ready'.
2026-07-29T08:00:45.858Z root INFO All frontend contributions settled: 1964.0 ms [4.538 s since frontend page start]
2026-07-29T08:00:46.111Z root INFO INFO [OdsListenerService] [main.js:1476] [handlePassCalcResponse] [GSC-PASSCALC] Received Message | ID: FILTEREDPASS:MIYEG_1785312044140 | Items: 173 | Keys: passList
2026-07-29T08:00:46.111Z root INFO INFO [OdsListenerService] [main.js:1529] [handlePassCalcResponse] [GSC-PASSCALC] Catch-all routing for ID: "FILTEREDPASS:MIYEG_1785312044140" | Resolved GS ID: "MIYEG" | Items: 173
2026-07-29T08:00:46.111Z root INFO INFO [SatelliteApplicationService] [main.js:2791] [saveInMemoryPrecalculatedPasses] [InMemory-Passes] Updating 173 precalculated passes in memory...
2026-07-29T08:00:46.111Z root INFO INFO [SatelliteApplicationService] [main.js:2832] [saveInMemoryPrecalculatedPasses] [InMemory-Passes] Current memory counts by GS: {"MIYEG":173}
2026-07-29T08:00:46.111Z root INFO INFO [SatelliteApplicationService] [main.js:2833] [saveInMemoryPrecalculatedPasses] [InMemory-Passes] Total precalculated passes in memory cache: 173
2026-07-29T08:00:46.191Z root INFO INFO [OdsListenerService] [main.js:1476] [handlePassCalcResponse] [GSC-PASSCALC] Received Message | ID: FILTEREDPASS:TROMSO_1785312044140 | Items: 290 | Keys: passList
2026-07-29T08:00:46.191Z root INFO INFO [OdsListenerService] [main.js:1529] [handlePassCalcResponse] [GSC-PASSCALC] Catch-all routing for ID: "FILTEREDPASS:TROMSO_1785312044140" | Resolved GS ID: "TROMSO" | Items: 290
2026-07-29T08:00:46.191Z root INFO INFO [SatelliteApplicationService] [main.js:2791] [saveInMemoryPrecalculatedPasses] [InMemory-Passes] Updating 290 precalculated passes in memory...
2026-07-29T08:00:46.191Z root INFO INFO [SatelliteApplicationService] [main.js:2832] [saveInMemoryPrecalculatedPasses] [InMemory-Passes] Current memory counts by GS: {"MIYEG":173,"TROMSO":290}
2026-07-29T08:00:46.191Z root INFO INFO [SatelliteApplicationService] [main.js:2833] [saveInMemoryPrecalculatedPasses] [InMemory-Passes] Total precalculated passes in memory cache: 463
2026-07-29T08:00:47.915Z root WARN Widget was activated, but did not accept focus after 2000ms: soc:pass-list
2026-07-29T08:00:47.915Z root WARN Widget was activated, but did not accept focus after 2000ms: soc:pass-summary
2026-07-29T08:01:00.015Z root INFO INFO [SatelliteApplicationService] [main.js:2238] [requestGscSatelliteList] [GSC-DB] Requesting Satellite List...
2026-07-29T08:01:00.015Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1785312060015-wzfr113
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [main.js:1196] [handleDatabaseResponse] [GSC-DB-INCOMING] Class:  | CorrId: req-1785312060015-wzfr113 | Keys: satelliteList
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [main.js:1200] [handleDatabaseResponse] ### GSC SAT LIST RECEIVED (5 ITEMS) ###
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 56178 | Name: IMC | Priority: 1 | TLE Auto: true | Disabled: false
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 39030 | Name: GK-2 | Priority: 2 | TLE Auto: true | Disabled: false
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 69097 | Name: 69097 | Priority: 3 | TLE Auto: true | Disabled: false
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 67206 | Name: 67206 | Priority: 4 | TLE Auto: true | Disabled: false
2026-07-29T08:01:00.020Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 60342 | Name: 60342 | Priority: 5 | TLE Auto: true | Disabled: false
2026-07-29T08:01:00.354Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-07-29T08:01:00.354Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
^C
