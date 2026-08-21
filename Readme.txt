Backend main: entry point loaded [0.161 s since backend process start]
Backend server: loading modules... [0.169 s since backend process start]
Backend server: container created [0.304 s since backend process start]
[SOC Core] Backend module loaded. Registering all backend services & RPC.
Backend server: modules loaded [0.568 s since backend process start]
Backend server: resolving application [0.579 s since backend process start]
Configuring to accept webviews on '^.+\.webview\..+$' hostname.
INFO [EOe] [main.js:1945] [getCallerInfo] Initializing @uzay/gss-messaging connection to ws://10.1.80.15:61616/stomp
INFO [Pt] [main.js:1945] [getCallerInfo] Starting SatelliteApplicationService GLOBAL initialization...
INFO [Pt] [main.js:1945] [getCallerInfo] [Config Check] SPACETRACK_USERNAME: MISSING
INFO [Pt] [main.js:1945] [getCallerInfo] [Config Check] USE_PROXY: undefined
INFO [Pt] [main.js:1945] [getCallerInfo] initializeSatellites => Constellation is empty.
INFO [Pt] [main.js:1945] [getCallerInfo] SatelliteApplicationService initialization completed.
INFO [POe] [main.js:1945] [getCallerInfo] Subscribing to GSC response queues...
INFO [POe] [main.js:1945] [getCallerInfo] Subscribed to:
  - gsc.server.database_request_queue_/response
  - gsc.server.odsrunner_request_queue_/response
  - gsc.server.passcalculations_request_queue_/response
  - gsc.server.passoperations_request_queue_/response
  - gsc.server.administration_request_queue_/response
2026-08-21T14:19:34.788Z root WARN Backend QA.initialize took longer than the expected maximum 50 milliseconds: 70.4 ms [0.657 s since backend process start]
2026-08-21T14:19:34.788Z root WARN Backend Object.initialize took longer than the expected maximum 50 milliseconds: 69.1 ms [0.657 s since backend process start]
2026-08-21T14:19:34.788Z root WARN Backend Sse.initialize took longer than the expected maximum 50 milliseconds: 69.7 ms [0.658 s since backend process start]
2026-08-21T14:19:34.799Z root INFO INFO [nNe] [main.js:1945] [getCallerInfo] [MBTILES] Initialized MBTILES_DIR at: "/home/theia/data/public/mbtiles"
2026-08-21T14:19:34.799Z root INFO INFO [nNe] [main.js:1945] [getCallerInfo] SOC Express routes registered: /satellite/trajectory, /mbtiles/*
2026-08-21T14:19:34.799Z root WARN [StaticAssetsServer] WARNING: Public assets directory not found at  /home/theia/data/public. Ensure PUBLIC_ASSETS_DIR env var is set and the volume is mounted.
2026-08-21T14:19:34.800Z core:BackendApplication INFO configured all backend app contributions
2026-08-21T14:19:34.805Z core:BackendApplication INFO Theia app listening on http://0.0.0.0:3000.
2026-08-21T14:19:34.815Z root INFO Configuration directory URI: 'file:///home/theia/.theia'
2026-08-21T14:19:34.817Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] TCP Port 61616 is confirmed OPEN at 10.1.80.15.
2026-08-21T14:19:34.819Z root INFO INFO [nNe] [main.js:1945] [getCallerInfo] SOC Native Backend successfully started and services are initialized.
2026-08-21T14:19:34.819Z root INFO Backend application startup sequence completed (async work may still be pending): 19.7 ms [0.689 s since backend process start]
2026-08-21T14:19:34.819Z root INFO All backend contributions settled: 109.2 ms [0.689 s since backend process start]
2026-08-21T14:19:34.819Z root INFO Settings file not found at '/home/theia/.theia/backend-settings.json'. Falling back to defaults.
2026-08-21T14:19:34.822Z root INFO 10.1.80.15:61616 adresine bağlantı kuruldu
2026-08-21T14:19:34.822Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] Successfully connected to ODS Artemis Broker at 10.1.80.15:61616
2026-08-21T14:19:34.822Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] Re-applying 5 pending subscriptions...
2026-08-21T14:19:34.822Z root INFO gsc.server.database_request_queue_/response abone olunuyor (ID: sub-gsc.server.database_request_queue_-response-l8v8e, ACK: auto)
2026-08-21T14:19:34.822Z root INFO gsc.server.odsrunner_request_queue_/response abone olunuyor (ID: sub-gsc.server.odsrunner_request_queue_-response-z77j4, ACK: auto)
2026-08-21T14:19:34.822Z root INFO gsc.server.passcalculations_request_queue_/response abone olunuyor (ID: sub-gsc.server.passcalculations_request_queue_-response-9kk9o, ACK: auto)
2026-08-21T14:19:34.822Z root INFO gsc.server.passoperations_request_queue_/response abone olunuyor (ID: sub-gsc.server.passoperations_request_queue_-response-fs008, ACK: auto)
2026-08-21T14:19:34.822Z root INFO gsc.server.administration_request_queue_/response abone olunuyor (ID: sub-gsc.server.administration_request_queue_-response-qxbil, ACK: auto)
2026-08-21T14:19:34.825Z root WARN The local plugin referenced by local-dir:/home/theia/plugins does not exist.
2026-08-21T14:19:34.825Z root WARN The local plugin referenced by local-dir:/home/theia/.theia/plugins does not exist.
2026-08-21T14:19:34.825Z root WARN The local plugin referenced by local-dir:/home/theia/.theia/deployedPlugins does not exist.
2026-08-21T14:19:34.826Z root INFO Resolve plugins list: 6.4 ms [0.695 s since backend process start]
2026-08-21T14:19:34.826Z root INFO Deploy plugins list: 6.7 ms [0.696 s since backend process start]
2026-08-21T14:19:36.717Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Satellite List...
2026-08-21T14:19:36.717Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1787321976717-ussekb9
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787321976717-ussekb9 | Keys: satelliteList
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (12 ITEMS) ###
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 47397 | Name: 47397 | Priority: 4 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 60342 | Name: 60342 | Priority: 3 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: 39030 | Priority: 7 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 66294 | Name: 66294 | Priority: 11 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 65478 | Name: 65478 | Priority: 10 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 67206 | Name: 67206 | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 69145 | Name: 69145 | Priority: 12 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 69097 | Name: 69097 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 66995 | Name: 66995 | Priority: 5 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 41875 | Name: 41875 | Priority: 8 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: 56178 | Priority: 6 | TLE Auto: true | Disabled: false
2026-08-21T14:19:36.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 65555 | Name: 65555 | Priority: 9 | TLE Auto: true | Disabled: false
2026-08-21T14:19:37.718Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Station List...
2026-08-21T14:19:37.718Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.StationListRequest | CorrId: req-1787321977717-wqe3ljn
2026-08-21T14:19:37.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787321977717-wqe3ljn | Keys: stationList
2026-08-21T14:19:37.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] ### GSC STATION LIST RECEIVED (2 ITEMS) ###
2026-08-21T14:19:37.722Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-SYNC] Synchronizing 2 ground stations...
2026-08-21T14:19:37.722Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-SYNC] Sync complete. Memory now contains 2 stations.
2026-08-21T14:19:37.722Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GS-SYNC] Auto initializing active station to first available: MIYEG
2026-08-21T14:19:37.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GS] Name: MIYEG | Lat: 39.8914 | Lon: 32.77857 | Alt: 0.925 | ElevMask: 5
2026-08-21T14:19:37.722Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GS] Name: Tromso | Lat: 69.3598 | Lon: 18.5993 | Alt: 0.142727 | ElevMask: 5
2026-08-21T14:19:39.718Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-PASS-PREDICTION] Requesting GLOBAL pass lists from GSC (Past + Future)...
2026-08-21T14:19:39.718Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.PastPassListRequest | CorrId: PAST_REFRESH_undefined_1787321979717
2026-08-21T14:19:39.718Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FuturePassListRequest | CorrId: FUTURE_REFRESH_undefined_1787321979718
2026-08-21T14:19:39.718Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Dispatched both Past and Future requests. IDs: PAST_REFRESH_undefined_1787321979717, FUTURE_REFRESH_undefined_1787321979718
2026-08-21T14:19:39.728Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: PAST_REFRESH_undefined_1787321979717 | Items: 23 | Keys: passList
2026-08-21T14:19:39.728Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:PAST_REFRESH_undefined_1787321979717
2026-08-21T14:19:39.728Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] PAST_REFRESH_undefined_1787321979717 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 23
2026-08-21T14:19:39.728Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 23 precalculated passes in memory...
2026-08-21T14:19:39.728Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":23}
2026-08-21T14:19:39.728Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 23
2026-08-21T14:19:40.769Z root INFO creating connection for 9bbf62c4-e3ae-4f00-bae7-0693b110009a
2026-08-21T14:19:44.721Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Executing Unified Dashboard Refresh (GS: ALL)...
2026-08-21T14:19:44.722Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passoperations_request_queue_ | Class: tr.gov.uzay.gsc.server.passoperations.api.messaging.requests.CurrentSatellitePassRequest | CorrId: DASHBOARD_CURRENT_DEFAULT_1787321984719
2026-08-21T14:19:44.722Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.NextSchedPassRequest | CorrId: DASHBOARD_NEXT_DEFAULT_1787321984720
2026-08-21T14:19:44.724Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] triggerGlobalPassRecalculation → Firing GSC Pass calculation for all 2 stations in memory
2026-08-21T14:19:44.724Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-PASS-CALC] Dispatching requestFilteredPasses for GS: MIYEG
2026-08-21T14:19:44.724Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Requesting filtered pass list for ground station: MIYEG
2026-08-21T14:19:44.724Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FilteredPassListGenerationRequest | CorrId: FILTEREDPASS:MIYEG_1787321984722
2026-08-21T14:19:44.724Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-PASS-CALC] Dispatching requestFilteredPasses for GS: Tromso
2026-08-21T14:19:44.724Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Requesting filtered pass list for ground station: Tromso
2026-08-21T14:19:44.724Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FilteredPassListGenerationRequest | CorrId: FILTEREDPASS:Tromso_1787321984723
2026-08-21T14:19:44.724Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-PASS-PREDICTION] Requesting GLOBAL pass lists from GSC (Past + Future)...
2026-08-21T14:19:44.725Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.PastPassListRequest | CorrId: PAST_REFRESH_undefined_1787321984724
2026-08-21T14:19:44.725Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FuturePassListRequest | CorrId: FUTURE_REFRESH_undefined_1787321984724
2026-08-21T14:19:44.725Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Dispatched both Past and Future requests. IDs: PAST_REFRESH_undefined_1787321984724, FUTURE_REFRESH_undefined_1787321984724
2026-08-21T14:19:44.725Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Unified Refresh commands dispatched successfully for GS: "ALL".
2026-08-21T14:19:44.728Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: DASHBOARD_NEXT_DEFAULT_1787321984720 | Items: 5 | Keys: passList
2026-08-21T14:19:44.728Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Dashboard Approaching (GS: DEFAULT) | Items: 5
2026-08-21T14:19:44.737Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: PAST_REFRESH_undefined_1787321984724 | Items: 23 | Keys: passList
2026-08-21T14:19:44.737Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:PAST_REFRESH_undefined_1787321984724
2026-08-21T14:19:44.737Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] PAST_REFRESH_undefined_1787321984724 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 23
2026-08-21T14:19:44.737Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 23 precalculated passes in memory...
2026-08-21T14:19:44.737Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":23}
2026-08-21T14:19:44.737Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 23
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787321996009-vksup19 | Keys: satelliteList
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (12 ITEMS) ###
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 47397 | Name: 47397 | Priority: 4 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 60342 | Name: 60342 | Priority: 3 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: 39030 | Priority: 7 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 66294 | Name: 66294 | Priority: 11 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 65478 | Name: 65478 | Priority: 10 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 67206 | Name: 67206 | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 69145 | Name: 69145 | Priority: 12 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 69097 | Name: 69097 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 66995 | Name: 66995 | Priority: 5 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 41875 | Name: 41875 | Priority: 8 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: 56178 | Priority: 6 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.038Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 65555 | Name: 65555 | Priority: 9 | TLE Auto: true | Disabled: false
2026-08-21T14:19:56.720Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC] Triggering batch positions request for all satellites...
2026-08-21T14:19:56.720Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 47397 from 2026-08-20T14:19:56.718Z to 2026-08-23T14:19:56.718Z
2026-08-21T14:19:56.720Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321996718-2d2k6f0
2026-08-21T14:19:57.221Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 60342 from 2026-08-20T14:19:57.220Z to 2026-08-23T14:19:57.220Z
2026-08-21T14:19:57.221Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321997220-24aewns
2026-08-21T14:19:57.723Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 39030 from 2026-08-20T14:19:57.722Z to 2026-08-23T14:19:57.722Z
2026-08-21T14:19:57.723Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321997723-2h1dylw
2026-08-21T14:19:58.225Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 66294 from 2026-08-20T14:19:58.224Z to 2026-08-23T14:19:58.224Z
2026-08-21T14:19:58.225Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321998224-g1prcj3
2026-08-21T14:19:58.727Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 65478 from 2026-08-20T14:19:58.726Z to 2026-08-23T14:19:58.726Z
2026-08-21T14:19:58.727Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321998726-ni1l8ni
2026-08-21T14:19:59.229Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 67206 from 2026-08-20T14:19:59.228Z to 2026-08-23T14:19:59.228Z
2026-08-21T14:19:59.230Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321999229-j3l0iww
2026-08-21T14:19:59.730Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 69145 from 2026-08-20T14:19:59.730Z to 2026-08-23T14:19:59.730Z
2026-08-21T14:19:59.730Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787321999730-iu1wnp5
2026-08-21T14:20:00.232Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 69097 from 2026-08-20T14:20:00.231Z to 2026-08-23T14:20:00.231Z
2026-08-21T14:20:00.232Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787322000231-kn1i1dr
2026-08-21T14:20:00.734Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 66995 from 2026-08-20T14:20:00.733Z to 2026-08-23T14:20:00.733Z
2026-08-21T14:20:00.734Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787322000733-lvljyr4
2026-08-21T14:20:01.235Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 41875 from 2026-08-20T14:20:01.234Z to 2026-08-23T14:20:01.234Z
2026-08-21T14:20:01.235Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787322001235-534lbgh
2026-08-21T14:20:01.737Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 56178 from 2026-08-20T14:20:01.736Z to 2026-08-23T14:20:01.736Z
2026-08-21T14:20:01.737Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787322001737-a3q1gim
2026-08-21T14:20:02.238Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 65555 from 2026-08-20T14:20:02.238Z to 2026-08-23T14:20:02.238Z
2026-08-21T14:20:02.238Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787322002238-6hzdh9u
2026-08-21T14:20:04.717Z root INFO INFO [Pt] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Satellite List...
2026-08-21T14:20:04.718Z root INFO INFO [EOe] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1787322004717-9kfwbdg
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787322004717-9kfwbdg | Keys: satelliteList
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (12 ITEMS) ###
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 47397 | Name: 47397 | Priority: 4 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 60342 | Name: 60342 | Priority: 3 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: 39030 | Priority: 7 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 66294 | Name: 66294 | Priority: 11 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 65478 | Name: 65478 | Priority: 10 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 67206 | Name: 67206 | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 69145 | Name: 69145 | Priority: 12 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 69097 | Name: 69097 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 66995 | Name: 66995 | Priority: 5 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 41875 | Name: 41875 | Priority: 8 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: 56178 | Priority: 6 | TLE Auto: true | Disabled: false
2026-08-21T14:20:04.721Z root INFO INFO [POe] [main.js:1945] [getCallerInfo] [SAT] No: 65555 | Name: 65555 | Priority: 9 | TLE Auto: true | Disabled: false GET
http://localhost:3301/favicon.ico
[HTTP/1.1 404 Not Found 0ms]

Frontend: loading modules... [1.493 s since frontend page start] bundle.js:20741:8019
Frontend: container created [1.524 s since frontend page start] bundle.js:20741:8019
sending initial connect on YGhLGrA0IjTNzemBAAAB bundle.js:443:110074
initial connect received on YGhLGrA0IjTNzemBAAAB bundle.js:443:109849
Frontend: preloaded [1.696 s since frontend page start] bundle.js:20741:8019
Frontend: core modules loaded [1.803 s since frontend page start] bundle.js:20741:8019
[SOC Core] Frontend module loading... bundle.js:20506:78195
[SOC Core] Frontend module bindings completed. bundle.js:20506:78838
Failed to start the frontend application. bundle.js:20741:10140
Error: Dynamic require of "@uzay/gsc-earth-extension/lib/browser/soc-frontend-module" is not supported
    Uzt http://localhost:3301/bundle.js:1
    exports http://localhost:3301/bundle.js:20741
    c9l http://localhost:3301/bundle.js:20741
    z http://localhost:3301/bundle.js:1
    <anonymous> http://localhost:3301/bundle.js:20741
    <anonymous> http://localhost:3301/bundle.js:20741
bundle.js:20741:10202
