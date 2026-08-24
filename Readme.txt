mert@mertunubol:~/Development/gsc.scheduling.theia/browser-app$ docker logs -f gsc-gui-web2
Backend main: entry point loaded [0.231 s since backend process start]
Backend server: loading modules... [0.239 s since backend process start]
Backend server: container created [0.372 s since backend process start]
[SOC Core] Backend module loaded. Registering all backend services & RPC.
Backend server: modules loaded [0.613 s since backend process start]
Backend server: resolving application [0.625 s since backend process start]
Configuring to accept webviews on '^.+\.webview\..+$' hostname.
INFO [FAt] [main.js:1945] [getCallerInfo] Initializing @uzay/gss-messaging connection to ws://10.1.11.24:61613/stomp
INFO [pr] [main.js:1945] [getCallerInfo] Starting SatelliteApplicationService GLOBAL initialization...
INFO [pr] [main.js:1945] [getCallerInfo] [Config Check] SPACETRACK_USERNAME: MISSING
INFO [pr] [main.js:1945] [getCallerInfo] [Config Check] USE_PROXY: undefined
INFO [pr] [main.js:1945] [getCallerInfo] initializeSatellites => Constellation is empty.
INFO [pr] [main.js:1945] [getCallerInfo] SatelliteApplicationService initialization completed.
INFO [VAt] [main.js:1945] [getCallerInfo] Subscribing to GSC response queues...
INFO [VAt] [main.js:1945] [getCallerInfo] Subscribed to:
  - gsc.server.database_request_queue_/response
  - gsc.server.odsrunner_request_queue_/response
  - gsc.server.passcalculations_request_queue_/response
  - gsc.server.passoperations_request_queue_/response
  - gsc.server.administration_request_queue_/response
2026-08-24T09:10:22.375Z root WARN Backend z3.initialize took longer than the expected maximum 50 milliseconds: 68.3 ms [0.701 s since backend process start]
2026-08-24T09:10:22.375Z root WARN Backend Object.initialize took longer than the expected maximum 50 milliseconds: 67.0 ms [0.701 s since backend process start]
2026-08-24T09:10:22.375Z root WARN Backend L3e.initialize took longer than the expected maximum 50 milliseconds: 67.6 ms [0.702 s since backend process start]
2026-08-24T09:10:22.385Z root INFO [StaticAssetsServer] Serving static assets from /home/theia/data/public
2026-08-24T09:10:22.385Z root INFO [StaticAssetsServer] Routes: /textures, /tiles, /models, /earth, /moon
2026-08-24T09:10:22.385Z core:BackendApplication ERROR Could not configure contribution Error: unhandled module: "node_sqlite3.node"
    at Ffi.exports (/home/theia/browser-app/lib/backend/main.js:807:12745)
    at /home/theia/browser-app/lib/backend/main.js:20213:30607
    at /home/theia/browser-app/lib/backend/main.js:1:344
    at /home/theia/browser-app/lib/backend/main.js:20218:108
    at /home/theia/browser-app/lib/backend/main.js:1:344
    at ZHt.configure (/home/theia/browser-app/lib/backend/main.js:20218:8480)
    at /home/theia/browser-app/lib/backend/main.js:562:4293
    at /home/theia/browser-app/lib/backend/main.js:562:7439
    at Ftt.startAsync (/home/theia/browser-app/lib/backend/main.js:554:3046)
    at C2.measure (/home/theia/browser-app/lib/backend/main.js:562:7539)
2026-08-24T09:10:22.387Z core:BackendApplication INFO configured all backend app contributions
2026-08-24T09:10:22.391Z core:BackendApplication INFO Theia app listening on http://0.0.0.0:3000.
2026-08-24T09:10:22.401Z root INFO Configuration directory URI: 'file:///home/theia/.theia'
2026-08-24T09:10:22.402Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] TCP Port 61613 is confirmed OPEN at 10.1.11.24.
2026-08-24T09:10:22.404Z root INFO INFO [ZHt] [main.js:1945] [getCallerInfo] SOC Native Backend successfully started and services are initialized.
2026-08-24T09:10:22.404Z root INFO Backend application startup sequence completed (async work may still be pending): 18.5 ms [0.731 s since backend process start]
2026-08-24T09:10:22.404Z root INFO All backend contributions settled: 105.6 ms [0.731 s since backend process start]
2026-08-24T09:10:22.404Z root INFO Settings file not found at '/home/theia/.theia/backend-settings.json'. Falling back to defaults.
2026-08-24T09:10:22.405Z root WARN The local plugin referenced by local-dir:/home/theia/.theia/plugins does not exist.
2026-08-24T09:10:22.405Z root WARN The local plugin referenced by local-dir:/home/theia/.theia/deployedPlugins does not exist.
2026-08-24T09:10:22.405Z root WARN The local plugin referenced by local-dir:/home/theia/plugins does not exist.
2026-08-24T09:10:22.406Z root INFO Resolve plugins list: 1.0 ms [0.732 s since backend process start]
2026-08-24T09:10:22.406Z root INFO Deploy plugins list: 1.3 ms [0.733 s since backend process start]
2026-08-24T09:10:22.408Z root INFO 10.1.11.24:61613 adresine bağlantı kuruldu
2026-08-24T09:10:22.408Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] Successfully connected to ODS Artemis Broker at 10.1.11.24:61613
2026-08-24T09:10:22.408Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] Re-applying 5 pending subscriptions...
2026-08-24T09:10:22.408Z root INFO gsc.server.database_request_queue_/response abone olunuyor (ID: sub-gsc.server.database_request_queue_-response-o8rfi, ACK: auto)
2026-08-24T09:10:22.408Z root INFO gsc.server.odsrunner_request_queue_/response abone olunuyor (ID: sub-gsc.server.odsrunner_request_queue_-response-rnhhx, ACK: auto)
2026-08-24T09:10:22.408Z root INFO gsc.server.passcalculations_request_queue_/response abone olunuyor (ID: sub-gsc.server.passcalculations_request_queue_-response-4z5y5, ACK: auto)
2026-08-24T09:10:22.408Z root INFO gsc.server.passoperations_request_queue_/response abone olunuyor (ID: sub-gsc.server.passoperations_request_queue_-response-tliy5, ACK: auto)
2026-08-24T09:10:22.408Z root INFO gsc.server.administration_request_queue_/response abone olunuyor (ID: sub-gsc.server.administration_request_queue_-response-rlxoi, ACK: auto)
2026-08-24T09:10:24.309Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Satellite List...
2026-08-24T09:10:24.309Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1787562624307-yr3p5c3
2026-08-24T09:10:24.312Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562624307-yr3p5c3 | Keys: satelliteList
2026-08-24T09:10:24.312Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:10:24.312Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:10:24.312Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:10:25.306Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Station List...
2026-08-24T09:10:25.306Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.StationListRequest | CorrId: req-1787562625306-m2myojo
2026-08-24T09:10:25.310Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562625306-m2myojo | Keys: stationList
2026-08-24T09:10:25.310Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC STATION LIST RECEIVED (1 ITEMS) ###
2026-08-24T09:10:25.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-SYNC] Synchronizing 1 ground stations...
2026-08-24T09:10:25.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-SYNC] Sync complete. Memory now contains 1 stations.
2026-08-24T09:10:25.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GS-SYNC] Auto initializing active station to first available: MIYEG
2026-08-24T09:10:25.310Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GS] Name: MIYEG | Lat: 39.8914 | Lon: 32.77857 | Alt: 0.925 | ElevMask: 5
2026-08-24T09:10:27.042Z root INFO creating connection for f4574411-8aaf-402c-a501-caabb1be88e5
2026-08-24T09:10:27.306Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASS-PREDICTION] Requesting GLOBAL pass lists from GSC (Past + Future)...
2026-08-24T09:10:27.306Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.PastPassListRequest | CorrId: PAST_REFRESH_undefined_1787562627306
2026-08-24T09:10:27.306Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FuturePassListRequest | CorrId: FUTURE_REFRESH_undefined_1787562627306
2026-08-24T09:10:27.306Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Dispatched both Past and Future requests. IDs: PAST_REFRESH_undefined_1787562627306, FUTURE_REFRESH_undefined_1787562627306
2026-08-24T09:10:27.310Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FUTURE_REFRESH_undefined_1787562627306 | Items: 14 | Keys: futurePassList
2026-08-24T09:10:27.310Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:FUTURE_REFRESH_undefined_1787562627306
2026-08-24T09:10:27.310Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] FUTURE_REFRESH_undefined_1787562627306 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 14
2026-08-24T09:10:27.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 14 precalculated passes in memory...
2026-08-24T09:10:27.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":14}
2026-08-24T09:10:27.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 14
2026-08-24T09:10:27.311Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: PAST_REFRESH_undefined_1787562627306 | Items: 4 | Keys: passList
2026-08-24T09:10:27.311Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:PAST_REFRESH_undefined_1787562627306
2026-08-24T09:10:27.311Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] PAST_REFRESH_undefined_1787562627306 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 4
2026-08-24T09:10:27.311Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 4 precalculated passes in memory...
2026-08-24T09:10:27.311Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":4}
2026-08-24T09:10:27.311Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 4
2026-08-24T09:10:27.399Z root INFO [SOC Earth] Extension loaded. RPC already initialized by gsc-core-extension
2026-08-24T09:10:27.426Z root INFO Detected keyboard layout from pressed keys: Turkish Q (PC)
2026-08-24T09:10:27.539Z root INFO [SOC Core] Initializing RPC connection to backend...
2026-08-24T09:10:27.539Z root INFO [SocDataService] Starting locked refresh flow (force=true)...
2026-08-24T09:10:27.539Z root INFO [SOC Core] SocDataService RPC client initialized.
2026-08-24T09:10:27.539Z root INFO [SOC] Satellite Ops Center extension loaded.
2026-08-24T09:10:27.539Z root INFO [SOC] Satellite Ops Center extension loaded.
2026-08-24T09:10:27.539Z root INFO [SOC] Files Panel extension loaded.
2026-08-24T09:10:27.539Z root INFO [SOC] Settings Panel extension loaded.
2026-08-24T09:10:27.539Z root INFO [SOC] Mission Panel extension loaded.
2026-08-24T09:10:27.542Z root INFO [SOC] Pass Control Panel extension loaded.
2026-08-24T09:10:27.559Z root INFO Start frontend contributions: 235.0 ms [2.094 s since frontend page start]
2026-08-24T09:10:27.559Z root INFO Changed application state from 'init' to 'started_contributions'.
2026-08-24T09:10:27.562Z root INFO Changed application state from 'started_contributions' to 'attached_shell'.
2026-08-24T09:10:27.562Z root INFO >>> Restoring the layout state...
2026-08-24T09:10:27.605Z terminal WARN Couldn't attach - can't find terminal with id: 1174796084 
2026-08-24T09:10:27.675Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [SYSTEM-MODE] Sending SystemModeRequest
2026-08-24T09:10:27.675Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.administration_request_queue_ | Class: tr.gov.uzay.gsc.server.administration.api.messaging.requests.SystemModeRequest | CorrId: SYSTEM_MODE_GET_1787562627674
2026-08-24T09:10:27.690Z root INFO [SocDataService] Acquire. refCount: 1
2026-08-24T09:10:27.690Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN-INCOMING] Class:  | CorrId: SYSTEM_MODE_GET_1787562627674 | Keys: systemMode
2026-08-24T09:10:27.690Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN] Received System Mode response: MANUAL
2026-08-24T09:10:27.842Z root WARN Linked preference "workbench.colorCustomizations" not found.
2026-08-24T09:10:27.842Z root WARN Linked preference "editor.experimental.preferTreeSitter" not found.
2026-08-24T09:10:27.846Z root INFO [e1d41405-5923-4b9b-9389-8aee75b71563] Waiting for backend deployment: 311.0 ms [2.401 s since frontend page start]
2026-08-24T09:10:27.859Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [SYSTEM-MODE] Sending SystemModeRequest
2026-08-24T09:10:27.859Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.administration_request_queue_ | Class: tr.gov.uzay.gsc.server.administration.api.messaging.requests.SystemModeRequest | CorrId: SYSTEM_MODE_GET_1787562627858
2026-08-24T09:10:27.859Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [SYSTEM-MODE] Sending SystemModeRequest
2026-08-24T09:10:27.859Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.administration_request_queue_ | Class: tr.gov.uzay.gsc.server.administration.api.messaging.requests.SystemModeRequest | CorrId: SYSTEM_MODE_GET_1787562627858
2026-08-24T09:10:27.859Z root INFO [SocDataService] Acquire. refCount: 2
2026-08-24T09:10:27.859Z root INFO [SocDataService] Acquire. refCount: 3
2026-08-24T09:10:27.861Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN-INCOMING] Class:  | CorrId: SYSTEM_MODE_GET_1787562627858 | Keys: systemMode
2026-08-24T09:10:27.861Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN] Received System Mode response: MANUAL
2026-08-24T09:10:27.862Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN-INCOMING] Class:  | CorrId: SYSTEM_MODE_GET_1787562627858 | Keys: systemMode
2026-08-24T09:10:27.862Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN] Received System Mode response: MANUAL
2026-08-24T09:10:27.867Z terminal WARN Failed attaching to terminal id 1174796084, the terminal is most likely gone. Starting up a new terminal instead.
2026-08-24T09:10:27.875Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [SYSTEM-MODE] Sending SystemModeRequest
2026-08-24T09:10:27.875Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.administration_request_queue_ | Class: tr.gov.uzay.gsc.server.administration.api.messaging.requests.SystemModeRequest | CorrId: SYSTEM_MODE_GET_1787562627874
2026-08-24T09:10:27.875Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [SYSTEM-MODE] Sending SystemModeRequest
2026-08-24T09:10:27.875Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.administration_request_queue_ | Class: tr.gov.uzay.gsc.server.administration.api.messaging.requests.SystemModeRequest | CorrId: SYSTEM_MODE_GET_1787562627874
2026-08-24T09:10:27.875Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [SYSTEM-MODE] Sending SystemModeRequest
2026-08-24T09:10:27.875Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.administration_request_queue_ | Class: tr.gov.uzay.gsc.server.administration.api.messaging.requests.SystemModeRequest | CorrId: SYSTEM_MODE_GET_1787562627874
2026-08-24T09:10:27.877Z root INFO [SocDataService] Acquire. refCount: 4
2026-08-24T09:10:27.877Z root INFO [SocDataService] Acquire. refCount: 5
2026-08-24T09:10:27.877Z root INFO [EarthViewer] Auto-discovery initialized. Querying /mbtiles/list from backend... http://localhost:3301/mbtiles/list
2026-08-24T09:10:27.877Z root INFO [SocDataService] Acquire. refCount: 6
2026-08-24T09:10:27.877Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Executing Unified Dashboard Refresh (GS: ALL)...
2026-08-24T09:10:27.877Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passoperations_request_queue_ | Class: tr.gov.uzay.gsc.server.passoperations.api.messaging.requests.CurrentSatellitePassRequest | CorrId: DASHBOARD_CURRENT_DEFAULT_1787562627876
2026-08-24T09:10:27.877Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.NextSchedPassRequest | CorrId: DASHBOARD_NEXT_DEFAULT_1787562627876
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Executing Unified Dashboard Refresh (GS: DEFAULT)...
2026-08-24T09:10:27.878Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passoperations_request_queue_ | Class: tr.gov.uzay.gsc.server.passoperations.api.messaging.requests.CurrentSatellitePassRequest | CorrId: DASHBOARD_CURRENT_DEFAULT_1787562627876
2026-08-24T09:10:27.878Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.NextSchedPassRequest | CorrId: DASHBOARD_NEXT_DEFAULT_1787562627876
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] triggerGlobalPassRecalculation → Firing GSC Pass calculation for all 1 stations in memory
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASS-CALC] Dispatching requestFilteredPasses for GS: MIYEG
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Requesting filtered pass list for ground station: MIYEG
2026-08-24T09:10:27.878Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FilteredPassListGenerationRequest | CorrId: FILTEREDPASS:MIYEG_1787562627878
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Unified Refresh commands dispatched successfully for GS: "DEFAULT".
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASS-PREDICTION] Requesting GLOBAL pass lists from GSC (Past + Future)...
2026-08-24T09:10:27.878Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.PastPassListRequest | CorrId: PAST_REFRESH_undefined_1787562627878
2026-08-24T09:10:27.878Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FuturePassListRequest | CorrId: FUTURE_REFRESH_undefined_1787562627878
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Dispatched both Past and Future requests. IDs: PAST_REFRESH_undefined_1787562627878, FUTURE_REFRESH_undefined_1787562627878
2026-08-24T09:10:27.878Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Unified Refresh commands dispatched successfully for GS: "ALL".
2026-08-24T09:10:27.879Z root ERROR (node:1) MaxListenersExceededWarning: Possible EventEmitter memory leak detected. 11 error listeners added to [pAt]. MaxListeners is 10. Use emitter.setMaxListeners() to increase limit
(Use `node --trace-warnings ...` to show where the warning was created)
2026-08-24T09:10:27.879Z root INFO [SocDataService] fetchGroundStations success: Received 1 stations.
2026-08-24T09:10:27.879Z root INFO [SocDataService] _updateGroundStations: Updating state with 1 sanitized stations.
2026-08-24T09:10:27.879Z root INFO [SocDataService] Triggering GLOBAL Pass Sync for initial load...
2026-08-24T09:10:27.879Z root INFO [SocDataService] fetchGroundStations finished inFlight for key: groundstations
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN-INCOMING] Class:  | CorrId: SYSTEM_MODE_GET_1787562627874 | Keys: systemMode
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN] Received System Mode response: MANUAL
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN-INCOMING] Class:  | CorrId: SYSTEM_MODE_GET_1787562627874 | Keys: systemMode
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN] Received System Mode response: MANUAL
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN-INCOMING] Class:  | CorrId: SYSTEM_MODE_GET_1787562627874 | Keys: systemMode
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-ADMIN] Received System Mode response: MANUAL
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: DASHBOARD_NEXT_DEFAULT_1787562627876 | Items: 5 | Keys: passList
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Dashboard Approaching (GS: DEFAULT) | Items: 5
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: DASHBOARD_NEXT_DEFAULT_1787562627876 | Items: 5 | Keys: passList
2026-08-24T09:10:27.881Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Dashboard Approaching (GS: DEFAULT) | Items: 5
2026-08-24T09:10:27.883Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FUTURE_REFRESH_undefined_1787562627878 | Items: 14 | Keys: futurePassList
2026-08-24T09:10:27.883Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:FUTURE_REFRESH_undefined_1787562627878
2026-08-24T09:10:27.883Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] FUTURE_REFRESH_undefined_1787562627878 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 14
2026-08-24T09:10:27.883Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 14 precalculated passes in memory...
2026-08-24T09:10:27.883Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":14}
2026-08-24T09:10:27.883Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 14
2026-08-24T09:10:27.883Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: PAST_REFRESH_undefined_1787562627878 | Items: 4 | Keys: passList
2026-08-24T09:10:27.883Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:PAST_REFRESH_undefined_1787562627878
2026-08-24T09:10:27.883Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] PAST_REFRESH_undefined_1787562627878 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 4
2026-08-24T09:10:27.883Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 4 precalculated passes in memory...
2026-08-24T09:10:27.883Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":4}
2026-08-24T09:10:27.883Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 4
2026-08-24T09:10:27.914Z root INFO [e1d41405-5923-4b9b-9389-8aee75b71563] Loading plugin contributions
2026-08-24T09:10:27.919Z root INFO [EarthViewer] [soc-cmd] Processing command: "selectSatellite" null
2026-08-24T09:10:27.974Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:27.983Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:27.991Z root INFO [EarthViewer] Received MBTiles state sync update: {
  earth: [
    {
      filename: 'satellite-2017-11-02_europe_turkey.mbtiles',
      dataset: 'earth',
      enabled: true,
      path: '/home/theia/data/public/mbtiles/earth/satellite-2017-11-02_europe_turkey.mbtiles'
    }
  ],
  moon: [
    {
      filename: 'moon_wac.mbtiles',
      dataset: 'moon',
      enabled: true,
      path: '/home/theia/data/public/mbtiles/moon/moon_wac.mbtiles'
    }
  ]
}
2026-08-24T09:10:28.007Z root INFO <<< The layout has been successfully restored.
2026-08-24T09:10:28.008Z root INFO Initialize the workbench layout: 449.0 ms [2.564 s since frontend page start]
2026-08-24T09:10:28.009Z root INFO Changed application state from 'attached_shell' to 'initialized_layout'.
2026-08-24T09:10:28.016Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:28.017Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:28.018Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:28.018Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:28.020Z root INFO [EarthViewer] Received mbtiles response list: {
  earth: [
    {
      filename: 'satellite-2017-11-02_europe_turkey.mbtiles',
      dataset: 'earth',
      enabled: true,
      path: '/home/theia/data/public/mbtiles/earth/satellite-2017-11-02_europe_turkey.mbtiles'
    }
  ],
  moon: [
    {
      filename: 'moon_wac.mbtiles',
      dataset: 'moon',
      enabled: true,
      path: '/home/theia/data/public/mbtiles/moon/moon_wac.mbtiles'
    }
  ]
}
2026-08-24T09:10:28.031Z root INFO [EarthViewer] Successfully auto-discovered and applied MBTiles: {
  earth: [
    {
      filename: 'satellite-2017-11-02_europe_turkey.mbtiles',
      dataset: 'earth',
      enabled: true,
      path: '/home/theia/data/public/mbtiles/earth/satellite-2017-11-02_europe_turkey.mbtiles'
    }
  ],
  moon: [
    {
      filename: 'moon_wac.mbtiles',
      dataset: 'moon',
      enabled: true,
      path: '/home/theia/data/public/mbtiles/moon/moon_wac.mbtiles'
    }
  ]
}
2026-08-24T09:10:28.083Z root INFO INFO [ZHt] [main.js:1945] [getCallerInfo] [REST /trajectory] Cache cold for 39030. Triggering GSC positions for NORAD 39030...
2026-08-24T09:10:28.083Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 39030 from 2026-08-23T09:10:28.082Z to 2026-08-26T09:10:28.082Z
2026-08-24T09:10:28.083Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787562628082-u1pgr20
2026-08-24T09:10:28.083Z root INFO INFO [ZHt] [main.js:1945] [getCallerInfo] [REST /trajectory] Cache cold for 56178. Triggering GSC positions for NORAD 56178...
2026-08-24T09:10:28.083Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 56178 from 2026-08-23T09:10:28.083Z to 2026-08-26T09:10:28.083Z
2026-08-24T09:10:28.083Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787562628083-1do422k
2026-08-24T09:10:28.096Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FILTEREDPASS:MIYEG_1787562627878 | Items: 65 | Keys: passList
2026-08-24T09:10:28.096Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Catch-all routing for ID: "FILTEREDPASS:MIYEG_1787562627878" | Resolved GS ID: "MIYEG" | Items: 65
2026-08-24T09:10:28.096Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 65 precalculated passes in memory...
2026-08-24T09:10:28.096Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":65}
2026-08-24T09:10:28.096Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 65
2026-08-24T09:10:28.186Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-CORR] Resolved meta "POSITIONS:39030" from correlation req-1787562628082-u1pgr20
2026-08-24T09:10:28.186Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-POSITIONS] Processed 4320 points for 39030
2026-08-24T09:10:28.223Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-CORR] Resolved meta "POSITIONS:56178" from correlation req-1787562628083-1do422k
2026-08-24T09:10:28.223Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-POSITIONS] Processed 4320 points for 56178
2026-08-24T09:10:28.974Z root INFO Frontend application startup sequence completed (async work may still be pending): 1597.3 ms [7.301 s since backend process start]
2026-08-24T09:10:28.974Z root INFO Replace loading indicator with ready workbench UI (animation): 963.0 ms [3.528 s since frontend page start]
2026-08-24T09:10:28.974Z root INFO Changed application state from 'initialized_layout' to 'ready'.
2026-08-24T09:10:28.974Z root INFO All frontend contributions settled: 1669.0 ms [3.528 s since frontend page start]
2026-08-24T09:10:31.074Z core:ApplicationShell WARN Widget was activated, but did not accept focus after 2000ms: soc:pass-list
2026-08-24T09:10:31.075Z core:ApplicationShell WARN Widget was activated, but did not accept focus after 2000ms: soc:pass-summary
2026-08-24T09:10:32.307Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Debouncing redundant request. Unified Refresh for "ALL" is ignored (cooldown: 1s).
2026-08-24T09:10:39.232Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 1 Y: 0 Level: 1.
2026-08-24T09:10:39.237Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 1 Y: 1 Level: 1.
2026-08-24T09:10:39.238Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 0 Y: 0 Level: 1.
2026-08-24T09:10:39.238Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 0 Y: 1 Level: 1.
2026-08-24T09:10:39.380Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 0 Y: 0 Level: 0.
2026-08-24T09:10:39.742Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 2 Y: 0 Level: 2.
2026-08-24T09:10:39.742Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 2 Y: 1 Level: 2.
2026-08-24T09:10:39.743Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 0 Level: 2.
2026-08-24T09:10:39.743Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 1 Level: 2.
2026-08-24T09:10:39.779Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 4 Y: 2 Level: 3.
2026-08-24T09:10:39.779Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 4 Y: 3 Level: 3.
2026-08-24T09:10:39.779Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 5 Y: 2 Level: 3.
2026-08-24T09:10:39.796Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 5 Y: 3 Level: 3.
2026-08-24T09:10:39.796Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 1 Y: 0 Level: 2.
2026-08-24T09:10:39.796Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 1 Y: 1 Level: 2.
2026-08-24T09:10:39.796Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 2 Level: 3.
2026-08-24T09:10:39.796Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 3 Level: 3.
2026-08-24T09:10:39.820Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 11 Y: 6 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 11 Y: 7 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 12 Y: 5 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 12 Y: 6 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 12 Y: 7 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 9 Y: 5 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 9 Y: 6 Level: 4.
2026-08-24T09:10:39.821Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 8 Y: 5 Level: 4.
2026-08-24T09:10:39.822Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 8 Y: 6 Level: 4.
2026-08-24T09:10:39.868Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 18 Y: 11 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 18 Y: 12 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 19 Y: 11 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 19 Y: 12 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 17 Y: 11 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 17 Y: 12 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 20 Y: 11 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 20 Y: 12 Level: 5.
2026-08-24T09:10:39.874Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 20 Y: 13 Level: 5.
2026-08-24T09:10:39.903Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 10 Y: 5 Level: 4.
2026-08-24T09:10:39.903Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 10 Y: 6 Level: 4.
2026-08-24T09:10:39.904Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 16 Y: 11 Level: 5.
2026-08-24T09:10:39.904Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 16 Y: 12 Level: 5.
2026-08-24T09:10:39.906Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 21 Y: 11 Level: 5.
2026-08-24T09:10:39.906Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 21 Y: 12 Level: 5.
2026-08-24T09:10:39.906Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 16 Y: 13 Level: 5.
2026-08-24T09:10:39.907Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 21 Y: 13 Level: 5.
2026-08-24T09:10:39.907Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 15 Y: 11 Level: 5.
2026-08-24T09:10:39.907Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 15 Y: 12 Level: 5.
2026-08-24T09:10:39.950Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 7 Y: 5 Level: 4.
2026-08-24T09:10:39.951Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 7 Y: 6 Level: 4.
2026-08-24T09:10:39.951Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 22 Y: 11 Level: 5.
2026-08-24T09:10:39.951Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 22 Y: 12 Level: 5.
2026-08-24T09:10:39.952Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 15 Y: 13 Level: 5.
2026-08-24T09:10:39.952Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 22 Y: 13 Level: 5.
2026-08-24T09:10:39.952Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 7 Y: 7 Level: 4.
2026-08-24T09:10:39.953Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 14 Y: 12 Level: 5.
2026-08-24T09:10:39.953Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 14 Y: 13 Level: 5.
2026-08-24T09:10:39.988Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 2 Level: 3.
2026-08-24T09:10:39.988Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 3 Level: 3.
2026-08-24T09:10:39.998Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 11 Y: 5 Level: 4.
2026-08-24T09:10:39.999Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 23 Y: 12 Level: 5.
2026-08-24T09:10:40.000Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 23 Y: 13 Level: 5.
2026-08-24T09:10:40.000Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 5 Level: 4.
2026-08-24T09:10:40.000Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 6 Level: 4.
2026-08-24T09:10:40.000Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 7 Level: 4.
2026-08-24T09:10:40.505Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 37 Y: 24 Level: 6.
2026-08-24T09:10:40.505Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 37 Y: 25 Level: 6.
2026-08-24T09:10:40.505Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 37 Y: 23 Level: 6.
2026-08-24T09:10:40.505Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 38 Y: 24 Level: 6.
2026-08-24T09:10:40.505Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 38 Y: 25 Level: 6.
2026-08-24T09:10:40.505Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 38 Y: 23 Level: 6.
2026-08-24T09:10:40.565Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 75 Y: 48 Level: 7.
2026-08-24T09:10:40.565Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 75 Y: 49 Level: 7.
2026-08-24T09:10:40.565Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 75 Y: 50 Level: 7.
2026-08-24T09:10:40.565Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 75 Y: 47 Level: 7.
2026-08-24T09:10:40.566Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 76 Y: 48 Level: 7.
2026-08-24T09:10:40.567Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 76 Y: 49 Level: 7.
2026-08-24T09:10:40.567Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 76 Y: 50 Level: 7.
2026-08-24T09:10:40.568Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 76 Y: 47 Level: 7.
2026-08-24T09:10:40.568Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 74 Y: 48 Level: 7.
2026-08-24T09:10:40.568Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 74 Y: 49 Level: 7.
2026-08-24T09:10:40.569Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 74 Y: 50 Level: 7.
2026-08-24T09:10:40.601Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 151 Y: 97 Level: 8.
2026-08-24T09:10:40.601Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 151 Y: 98 Level: 8.
2026-08-24T09:10:40.601Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 151 Y: 96 Level: 8.
2026-08-24T09:10:40.601Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 152 Y: 97 Level: 8.
2026-08-24T09:10:40.602Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 152 Y: 98 Level: 8.
2026-08-24T09:10:40.602Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 152 Y: 96 Level: 8.
2026-08-24T09:10:40.602Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 150 Y: 97 Level: 8.
2026-08-24T09:10:40.603Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 150 Y: 98 Level: 8.
2026-08-24T09:10:40.635Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 150 Y: 96 Level: 8.
2026-08-24T09:10:40.636Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 153 Y: 97 Level: 8.
2026-08-24T09:10:40.636Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 153 Y: 98 Level: 8.
2026-08-24T09:10:40.636Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 153 Y: 96 Level: 8.
2026-08-24T09:10:40.637Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 149 Y: 97 Level: 8.
2026-08-24T09:10:40.637Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 149 Y: 98 Level: 8.
2026-08-24T09:10:40.638Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 149 Y: 96 Level: 8.
2026-08-24T09:10:40.684Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 154 Y: 97 Level: 8.
2026-08-24T09:10:40.703Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 154 Y: 98 Level: 8.
2026-08-24T09:10:40.703Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 154 Y: 96 Level: 8.
2026-08-24T09:10:40.703Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 148 Y: 96 Level: 8.
2026-08-24T09:10:40.705Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 148 Y: 97 Level: 8.
2026-08-24T09:10:40.705Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 74 Y: 47 Level: 7.
2026-08-24T09:10:40.705Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 77 Y: 47 Level: 7.
2026-08-24T09:10:40.706Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 77 Y: 48 Level: 7.
2026-08-24T09:10:40.732Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 77 Y: 49 Level: 7.
2026-08-24T09:10:40.732Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 77 Y: 50 Level: 7.
2026-08-24T09:10:41.030Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 36 Y: 23 Level: 6.
2026-08-24T09:10:41.030Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 36 Y: 24 Level: 6.
2026-08-24T09:10:41.091Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 73 Y: 47 Level: 7.
2026-08-24T09:10:41.091Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 73 Y: 48 Level: 7.
2026-08-24T09:10:41.092Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 73 Y: 49 Level: 7.
2026-08-24T09:10:41.092Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 73 Y: 50 Level: 7.
2026-08-24T09:10:41.137Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 36 Y: 25 Level: 6.
2026-08-24T09:10:41.138Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 78 Y: 47 Level: 7.
2026-08-24T09:10:41.138Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 78 Y: 48 Level: 7.
2026-08-24T09:10:41.138Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 78 Y: 49 Level: 7.
2026-08-24T09:10:41.138Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 78 Y: 50 Level: 7.
2026-08-24T09:10:41.139Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 72 Y: 47 Level: 7.
2026-08-24T09:10:41.139Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 72 Y: 48 Level: 7.
2026-08-24T09:10:41.139Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 72 Y: 49 Level: 7.
2026-08-24T09:10:41.152Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 72 Y: 50 Level: 7.
2026-08-24T09:10:41.152Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 79 Y: 47 Level: 7.
2026-08-24T09:10:41.152Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 79 Y: 48 Level: 7.
2026-08-24T09:10:41.178Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 39 Y: 23 Level: 6.
2026-08-24T09:10:41.178Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 39 Y: 24 Level: 6.
2026-08-24T09:10:41.178Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 39 Y: 25 Level: 6.
2026-08-24T09:10:41.178Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 79 Y: 49 Level: 7.
2026-08-24T09:10:41.178Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 79 Y: 50 Level: 7.
2026-08-24T09:10:41.178Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 35 Y: 23 Level: 6.
2026-08-24T09:10:41.180Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 35 Y: 24 Level: 6.
2026-08-24T09:10:41.180Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 35 Y: 25 Level: 6.
2026-08-24T09:10:41.181Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 40 Y: 23 Level: 6.
2026-08-24T09:10:41.181Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 40 Y: 24 Level: 6.
2026-08-24T09:10:41.182Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 40 Y: 25 Level: 6.
2026-08-24T09:10:42.068Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 2 Y: 2 Level: 3.
2026-08-24T09:10:42.068Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 2 Y: 3 Level: 3.
2026-08-24T09:10:42.142Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 7 Y: 2 Level: 3.
2026-08-24T09:10:42.142Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 7 Y: 3 Level: 3.
2026-08-24T09:10:42.145Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 2 Level: 2.
2026-08-24T09:10:42.145Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 3 Level: 2.
2026-08-24T09:10:42.145Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 1 Y: 2 Level: 2.
2026-08-24T09:10:42.146Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 1 Y: 3 Level: 2.
2026-08-24T09:10:42.199Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 4 Level: 3.
2026-08-24T09:10:42.199Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 6 Y: 5 Level: 3.
2026-08-24T09:10:42.200Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 4 Level: 3.
2026-08-24T09:10:42.200Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 3 Y: 5 Level: 3.
2026-08-24T09:10:42.648Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 34 Y: 24 Level: 6.
2026-08-24T09:10:42.649Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 34 Y: 25 Level: 6.
2026-08-24T09:10:42.649Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 41 Y: 24 Level: 6.
2026-08-24T09:10:42.649Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 41 Y: 25 Level: 6.
2026-08-24T09:10:43.035Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562643031-ca2klj3 | Keys: satelliteList
2026-08-24T09:10:43.035Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:10:43.035Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:10:43.035Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:10:43.073Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:43.074Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:43.078Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [PASS-CONTROL] Sending PassTrajectoryRequest for Sat: 56178 (Type: REAL)
2026-08-24T09:10:43.078Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.PassTrajectoryRequest | CorrId: PASSTRAJECTORY:56178:REAL_1787562643078
2026-08-24T09:10:43.079Z root INFO [PassControlPanel] Auto-fetching actual pass trajectory for sat #56178 (Pass ID/Time: 2026-08-24T10:03:50.973102618Z)...
2026-08-24T09:10:43.668Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-CORR] Resolved meta "PASSTRAJECTORY:56178:REAL" from correlation PASSTRAJECTORY:56178:REAL_1787562643078
2026-08-24T09:10:43.668Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASS-TRAJECTORY] Received 353 trajectory points. SatelliteNo/Norad: 56178, GS: REAL
2026-08-24T09:10:43.836Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 34 Y: 23 Level: 6.
2026-08-24T09:10:44.306Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC] Triggering batch positions request for all satellites...
2026-08-24T09:10:44.306Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 39030 from 2026-08-23T09:10:44.306Z to 2026-08-26T09:10:44.306Z
2026-08-24T09:10:44.306Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787562644306-sooe41u
2026-08-24T09:10:44.392Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-CORR] Resolved meta "POSITIONS:39030" from correlation req-1787562644306-sooe41u
2026-08-24T09:10:44.392Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-POSITIONS] Processed 4320 points for 39030
2026-08-24T09:10:44.807Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-ODSRUNNER] Requesting positions for NORAD 56178 from 2026-08-23T09:10:44.806Z to 2026-08-26T09:10:44.806Z
2026-08-24T09:10:44.807Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.odsrunner_request_queue_ | Class: tr.gov.uzay.gsc.server.odsrunner.api.messaging.requests.SatPositionsMapRequest | CorrId: req-1787562644807-a0f6xy5
2026-08-24T09:10:44.882Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-CORR] Resolved meta "POSITIONS:56178" from correlation req-1787562644807-a0f6xy5
2026-08-24T09:10:44.882Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-POSITIONS] Processed 4320 points for 56178
2026-08-24T09:10:45.537Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 2 Y: 2 Level: 2.
2026-08-24T09:10:45.542Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 2 Y: 3 Level: 2.
2026-08-24T09:10:45.542Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 0 Y: 0 Level: 2.
2026-08-24T09:10:45.542Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 0 Y: 1 Level: 2.
2026-08-24T09:10:46.016Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 4 Y: 0 Level: 3.
2026-08-24T09:10:46.017Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 4 Y: 1 Level: 3.
2026-08-24T09:10:46.167Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 14 Y: 11 Level: 5.
2026-08-24T09:10:46.810Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 303 Y: 192 Level: 9.
2026-08-24T09:10:46.815Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 303 Y: 193 Level: 9.
2026-08-24T09:10:46.815Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 303 Y: 194 Level: 9.
2026-08-24T09:10:46.816Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 304 Y: 192 Level: 9.
2026-08-24T09:10:46.837Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 304 Y: 193 Level: 9.
2026-08-24T09:10:46.838Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 304 Y: 194 Level: 9.
2026-08-24T09:10:46.838Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 302 Y: 192 Level: 9.
2026-08-24T09:10:46.838Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 302 Y: 193 Level: 9.
2026-08-24T09:10:46.840Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 302 Y: 194 Level: 9.
2026-08-24T09:10:46.840Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 305 Y: 192 Level: 9.
2026-08-24T09:10:46.841Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 305 Y: 193 Level: 9.
2026-08-24T09:10:46.841Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 305 Y: 194 Level: 9.
2026-08-24T09:10:46.842Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 301 Y: 192 Level: 9.
2026-08-24T09:10:46.842Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 301 Y: 193 Level: 9.
2026-08-24T09:10:46.842Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 301 Y: 194 Level: 9.
2026-08-24T09:10:46.889Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 306 Y: 192 Level: 9.
2026-08-24T09:10:46.889Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 306 Y: 193 Level: 9.
2026-08-24T09:10:46.889Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 306 Y: 194 Level: 9.
2026-08-24T09:10:46.892Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 300 Y: 192 Level: 9.
2026-08-24T09:10:46.892Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 300 Y: 193 Level: 9.
2026-08-24T09:10:46.892Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 300 Y: 194 Level: 9.
2026-08-24T09:10:46.892Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 307 Y: 192 Level: 9.
2026-08-24T09:10:46.893Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 307 Y: 193 Level: 9.
2026-08-24T09:10:46.908Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 307 Y: 194 Level: 9.
2026-08-24T09:10:47.148Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 155 Y: 96 Level: 8.
2026-08-24T09:10:47.149Z root INFO An error occurred in "MAt": Failed to obtain image tile X: 155 Y: 97 Level: 8.
2026-08-24T09:10:47.307Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] triggerGlobalPassRecalculation → Firing GSC Pass calculation for all 1 stations in memory
2026-08-24T09:10:47.307Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASS-CALC] Dispatching requestFilteredPasses for GS: MIYEG
2026-08-24T09:10:47.307Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Requesting filtered pass list for ground station: MIYEG
2026-08-24T09:10:47.307Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FilteredPassListGenerationRequest | CorrId: FILTEREDPASS:MIYEG_1787562647306
2026-08-24T09:10:47.308Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-PASS-PREDICTION] Requesting GLOBAL pass lists from GSC (Past + Future)...
2026-08-24T09:10:47.308Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.PastPassListRequest | CorrId: PAST_REFRESH_undefined_1787562647307
2026-08-24T09:10:47.308Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FuturePassListRequest | CorrId: FUTURE_REFRESH_undefined_1787562647307
2026-08-24T09:10:47.308Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-REFRESH] Dispatched both Past and Future requests. IDs: PAST_REFRESH_undefined_1787562647307, FUTURE_REFRESH_undefined_1787562647307
2026-08-24T09:10:47.313Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FUTURE_REFRESH_undefined_1787562647307 | Items: 14 | Keys: futurePassList
2026-08-24T09:10:47.313Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:FUTURE_REFRESH_undefined_1787562647307
2026-08-24T09:10:47.313Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] FUTURE_REFRESH_undefined_1787562647307 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 14
2026-08-24T09:10:47.313Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 14 precalculated passes in memory...
2026-08-24T09:10:47.313Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":14}
2026-08-24T09:10:47.313Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 14
2026-08-24T09:10:47.315Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: PAST_REFRESH_undefined_1787562647307 | Items: 4 | Keys: passList
2026-08-24T09:10:47.315Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:PAST_REFRESH_undefined_1787562647307
2026-08-24T09:10:47.315Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] PAST_REFRESH_undefined_1787562647307 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 4
2026-08-24T09:10:47.315Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 4 precalculated passes in memory...
2026-08-24T09:10:47.315Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":4}
2026-08-24T09:10:47.315Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 4
2026-08-24T09:10:47.547Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FILTEREDPASS:MIYEG_1787562647306 | Items: 65 | Keys: passList
2026-08-24T09:10:47.547Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Catch-all routing for ID: "FILTEREDPASS:MIYEG_1787562647306" | Resolved GS ID: "MIYEG" | Items: 65
2026-08-24T09:10:47.547Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 65 precalculated passes in memory...
2026-08-24T09:10:47.547Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":65}
2026-08-24T09:10:47.547Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 65
2026-08-24T09:10:52.306Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Satellite List...
2026-08-24T09:10:52.306Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1787562652305-1w7a706
2026-08-24T09:10:52.308Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562652305-1w7a706 | Keys: satelliteList
2026-08-24T09:10:52.308Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:10:52.308Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:10:52.308Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:10:52.352Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:52.352Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:10:54.836Z root INFO [EarthViewer] Tab hidden. Throttling render loop.
2026-08-24T09:11:13.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562673031-ucghd8l | Keys: satelliteList
2026-08-24T09:11:13.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:11:13.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:11:13.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:11:13.064Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:13.064Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:22.308Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Satellite List...
2026-08-24T09:11:22.309Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1787562682308-y6hpznc
2026-08-24T09:11:22.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562682308-y6hpznc | Keys: satelliteList
2026-08-24T09:11:22.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:11:22.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:11:22.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:11:22.343Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:22.343Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:31.330Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: DASHBOARD_NEXT_DEFAULT_1787562691326 | Items: 5 | Keys: passList
2026-08-24T09:11:31.331Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Dashboard Approaching (GS: DEFAULT) | Items: 5
2026-08-24T09:11:31.332Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FUTURE_REFRESH_undefined_1787562691327 | Items: 14 | Keys: futurePassList
2026-08-24T09:11:31.332Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:FUTURE_REFRESH_undefined_1787562691327
2026-08-24T09:11:31.332Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] FUTURE_REFRESH_undefined_1787562691327 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 14
2026-08-24T09:11:31.332Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 14 precalculated passes in memory...
2026-08-24T09:11:31.332Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":14}
2026-08-24T09:11:31.332Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 14
2026-08-24T09:11:31.332Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: PAST_REFRESH_undefined_1787562691327 | Items: 4 | Keys: passList
2026-08-24T09:11:31.332Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Raw Correlation ID:PAST_REFRESH_undefined_1787562691327
2026-08-24T09:11:31.332Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] PAST_REFRESH_undefined_1787562691327 ID'li tüm geçişleri yakala. Yer İstasyonu ID: ALL Items: 4
2026-08-24T09:11:31.332Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 4 precalculated passes in memory...
2026-08-24T09:11:31.332Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":4}
2026-08-24T09:11:31.332Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 4
2026-08-24T09:11:31.543Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Received Message | ID: FILTEREDPASS:MIYEG_1787562691327 | Items: 65 | Keys: passList
2026-08-24T09:11:31.543Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-PASSCALC] Catch-all routing for ID: "FILTEREDPASS:MIYEG_1787562691327" | Resolved GS ID: "MIYEG" | Items: 65
2026-08-24T09:11:31.543Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Updating 65 precalculated passes in memory...
2026-08-24T09:11:31.543Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Current memory counts by GS: {"MIYEG":65}
2026-08-24T09:11:31.543Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [InMemory-Passes] Total precalculated passes in memory cache: 65
2026-08-24T09:11:43.035Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562703031-q89ewdf | Keys: satelliteList
2026-08-24T09:11:43.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:11:43.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:11:43.036Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:11:43.070Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:43.070Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:52.310Z root INFO INFO [pr] [main.js:1945] [getCallerInfo] [GSC-DB] Requesting Satellite List...
2026-08-24T09:11:52.310Z root INFO INFO [FAt] [main.js:1945] [getCallerInfo] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1787562712309-weza874
2026-08-24T09:11:52.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [GSC-DB-INCOMING] Class:  | CorrId: req-1787562712309-weza874 | Keys: satelliteList
2026-08-24T09:11:52.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] ### GSC SAT LIST RECEIVED (2 ITEMS) ###
2026-08-24T09:11:52.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 39030 | Name: GK-2 | Priority: 1 | TLE Auto: true | Disabled: false
2026-08-24T09:11:52.314Z root INFO INFO [VAt] [main.js:1945] [getCallerInfo] [SAT] No: 56178 | Name: IMC | Priority: 2 | TLE Auto: true | Disabled: false
2026-08-24T09:11:52.350Z root INFO [SocDataService] Merged 1 dynamic passes into main state for normalized IDs.
2026-08-24T09:11:52.350Z root INFO [SocDataService] Merged 5 dynamic passes into main state for normalized IDs.
