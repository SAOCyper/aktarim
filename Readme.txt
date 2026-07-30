ent dependency.

Run `npm audit` for details.
npm verbose cwd /home/theia
npm verbose os Linux 6.12.69+deb13-amd64
npm verbose node v22.14.0
npm verbose npm  v10.9.2
npm verbose exit 0
npm info ok
root@0ca2e90b8761:/home/theia# npm run start:browser

> start:browser
> cd browser-app && npm run start


> gsc-browser-app@1.0.0 start /home/theia/browser-app
> theia start --hostname=0.0.0.0 --plugins=local-dir:../plugins

Backend main: entry point loaded [0.277 s since backend process start]
Backend server: loading modules... [0.280 s since backend process start]
Backend server: container created [0.375 s since backend process start]
[SOC Core] Backend module loaded (no additional bindings needed — handled by soc-earth-extension).
Backend server: modules loaded [0.552 s since backend process start]
Backend server: resolving application [0.566 s since backend process start]
Configuring to accept webviews on '^.+\.webview\..+$' hostname.
INFO [ArtemisService] [main.js:675] [init] Initializing @uzay/messaging connection to ws://10.1.11.24:61613/stomp
INFO [SatelliteApplicationService] [main.js:2011] [init] Starting SatelliteApplicationService GLOBAL initialization...
INFO [SatelliteApplicationService] [main.js:2015] [init] [Config Check] SPACETRACK_USERNAME: MISSING
INFO [SatelliteApplicationService] [main.js:2016] [init] [Config Check] USE_PROXY: undefined
INFO [SatelliteApplicationService] [main.js:2047] [initializeSatellites] initializeSatellites â†’ Constellation is empty.
INFO [SatelliteApplicationService] [main.js:2036] [init] SatelliteApplicationService initialization completed.
INFO [OdsListenerService] [main.js:1156] [init] Subscribing to GSC response queues...
INFO [OdsListenerService] [main.js:1182] [init] Subscribed to:
  - gsc.server.database_request_queue_/response
  - gsc.server.odsrunner_request_queue_/response
  - gsc.server.passcalculations_request_queue_/response
  - gsc.server.passoperations_request_queue_/response
  - gsc.server.administration_request_queue_/response
2026-07-30T09:07:27.422Z root WARN Backend DefaultMessagingService.initialize took longer than the expected maximum 50 milliseconds: 59.7 ms [0.637 s since backend process start]
2026-07-30T09:07:27.423Z root WARN Backend Object.initialize took longer than the expected maximum 50 milliseconds: 58.4 ms [0.637 s since backend process start]
2026-07-30T09:07:27.426Z root WARN Backend PluginLocalizationServer.initialize took longer than the expected maximum 50 milliseconds: 58.9 ms [0.638 s since backend process start]
2026-07-30T09:07:27.426Z root INFO INFO [SocBackendContribution] [main.js:3514] [configure] [MBTILES] Initialized MBTILES_DIR at: "/home/theia/gsc-common/public"
2026-07-30T09:07:27.426Z root INFO INFO [SocBackendContribution] [main.js:3515] [configure] SOC Express routes registered: /satellite/trajectory, /mbtiles/*
2026-07-30T09:07:27.428Z root INFO configured all backend app contributions
2026-07-30T09:07:27.431Z root INFO Theia app listening on http://0.0.0.0:3000.
2026-07-30T09:07:27.440Z root INFO Configuration directory URI: 'file:///root/.theia'
2026-07-30T09:07:27.441Z root INFO INFO [ArtemisService] [678:29] [js] TCP Port 61613 is confirmed OPEN at 10.1.11.24.
2026-07-30T09:07:27.442Z root INFO Settings file not found at '/root/.theia/backend-settings.json'. Falling back to defaults.
2026-07-30T09:07:27.443Z root WARN The local plugin referenced by local-dir:/root/.theia/plugins does not exist.
2026-07-30T09:07:27.443Z root WARN The local plugin referenced by local-dir:/root/.theia/deployedPlugins does not exist.
2026-07-30T09:07:27.443Z root WARN The local plugin referenced by local-dir:../plugins does not exist.
2026-07-30T09:07:27.443Z root INFO Resolve plugins list: 1.1 ms [0.659 s since backend process start]
2026-07-30T09:07:27.443Z root INFO Deploy plugins list: 1.4 ms [0.659 s since backend process start]
2026-07-30T09:07:27.473Z root INFO 10.1.11.24:61613 adresine bağlantı kuruldu
2026-07-30T09:07:27.473Z root INFO INFO [ArtemisService] [721:29] [js] Successfully connected to ODS Artemis Broker at 10.1.11.24:61613
2026-07-30T09:07:27.473Z root INFO INFO [ArtemisService] [725:33] [js] Re-applying 5 pending subscriptions...
2026-07-30T09:07:27.473Z root INFO gsc.server.database_request_queue_/response abone olunuyor (ID: sub-gsc.server.database_request_queue_-response-gzjem, ACK: auto)
2026-07-30T09:07:27.473Z root INFO gsc.server.odsrunner_request_queue_/response abone olunuyor (ID: sub-gsc.server.odsrunner_request_queue_-response-wtkug, ACK: auto)
2026-07-30T09:07:27.473Z root INFO gsc.server.passcalculations_request_queue_/response abone olunuyor (ID: sub-gsc.server.passcalculations_request_queue_-response-5xxf1, ACK: auto)
2026-07-30T09:07:27.473Z root INFO gsc.server.passoperations_request_queue_/response abone olunuyor (ID: sub-gsc.server.passoperations_request_queue_-response-we097, ACK: auto)
2026-07-30T09:07:27.473Z root INFO gsc.server.administration_request_queue_/response abone olunuyor (ID: sub-gsc.server.administration_request_queue_-response-bruag, ACK: auto)
2026-07-30T09:07:27.477Z root INFO INFO [SocBackendContribution] [main.js:3518] [onStart] SOC Native Backend successfully started and services are initialized.
2026-07-30T09:07:27.477Z root INFO Backend application startup sequence completed (async work may still be pending): 50.5 ms [0.692 s since backend process start]
2026-07-30T09:07:27.477Z root INFO All backend contributions settled: 125.7 ms [0.692 s since backend process start]
2026-07-30T09:07:27.642Z root INFO Reconnecting failed for 00544f63-94db-4bbc-b04e-87e3e95081d6
2026-07-30T09:07:27.690Z root INFO creating connection for 00544f63-94db-4bbc-b04e-87e3e95081d6
2026-07-30T09:07:27.732Z root INFO reconnect failed on VdvB8gg2ehsfIBebAAAB
2026-07-30T09:07:27.732Z root INFO sending initial connect on undefined
2026-07-30T09:07:27.732Z root ERROR [SocDataService] Trigger refresh-all failed: ../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/</<@http://localhost:3300/bundle.js:83679:68
../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/<@http://localhost:3300/bundle.js:83679:34
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/</<@http://localhost:3300/bundle.js:83288:44
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/<@http://localhost:3300/bundle.js:83287:35
../node_modules/@theia/core/lib/common/disposable.js/push/disposable.dispose@http://localhost:3300/bundle.js:78934:13
dispose@http://localhost:3300/bundle.js:78911:40
dispose@http://localhost:3300/bundle.js:83388:24
onUnderlyingChannelClose@http://localhost:3300/bundle.js:83292:18
../node_modules/@theia/core/lib/common/message-rpc/channel.js/ChannelMultiplexer/<@http://localhost:3300/bundle.js:83271:58
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
reconnectListener@http://localhost:3300/bundle.js:56349:56
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
emitEvent@http://localhost:3300/bundle.js:485230:20
onevent@http://localhost:3300/bundle.js:485217:18
onpacket@http://localhost:3300/bundle.js:485185:22
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
../node_modules/socket.io-client/build/cjs/manager.js/ondecoded/<@http://localhost:3300/bundle.js:484471:18

2026-07-30T09:07:27.732Z root ERROR [SocDataService] fetchPasses failed: ../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/</<@http://localhost:3300/bundle.js:83679:68
../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/<@http://localhost:3300/bundle.js:83679:34
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/</<@http://localhost:3300/bundle.js:83288:44
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/<@http://localhost:3300/bundle.js:83287:35
../node_modules/@theia/core/lib/common/disposable.js/push/disposable.dispose@http://localhost:3300/bundle.js:78934:13
dispose@http://localhost:3300/bundle.js:78911:40
dispose@http://localhost:3300/bundle.js:83388:24
onUnderlyingChannelClose@http://localhost:3300/bundle.js:83292:18
../node_modules/@theia/core/lib/common/message-rpc/channel.js/ChannelMultiplexer/<@http://localhost:3300/bundle.js:83271:58
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
reconnectListener@http://localhost:3300/bundle.js:56349:56
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
emitEvent@http://localhost:3300/bundle.js:485230:20
onevent@http://localhost:3300/bundle.js:485217:18
onpacket@http://localhost:3300/bundle.js:485185:22
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
../node_modules/socket.io-client/build/cjs/manager.js/ondecoded/<@http://localhost:3300/bundle.js:484471:18

2026-07-30T09:07:27.732Z root ERROR [SocDataService] fetchSatellites failed: ../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/</<@http://localhost:3300/bundle.js:83679:68
../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/<@http://localhost:3300/bundle.js:83679:34
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/</<@http://localhost:3300/bundle.js:83288:44
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/<@http://localhost:3300/bundle.js:83287:35
../node_modules/@theia/core/lib/common/disposable.js/push/disposable.dispose@http://localhost:3300/bundle.js:78934:13
dispose@http://localhost:3300/bundle.js:78911:40
dispose@http://localhost:3300/bundle.js:83388:24
onUnderlyingChannelClose@http://localhost:3300/bundle.js:83292:18
../node_modules/@theia/core/lib/common/message-rpc/channel.js/ChannelMultiplexer/<@http://localhost:3300/bundle.js:83271:58
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
reconnectListener@http://localhost:3300/bundle.js:56349:56
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
emitEvent@http://localhost:3300/bundle.js:485230:20
onevent@http://localhost:3300/bundle.js:485217:18
onpacket@http://localhost:3300/bundle.js:485185:22
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
../node_modules/socket.io-client/build/cjs/manager.js/ondecoded/<@http://localhost:3300/bundle.js:484471:18

2026-07-30T09:07:27.732Z root ERROR [SocDataService] fetchDynamicPasses failed: ../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/</<@http://localhost:3300/bundle.js:83679:68
../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/<@http://localhost:3300/bundle.js:83679:34
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/</<@http://localhost:3300/bundle.js:83288:44
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/<@http://localhost:3300/bundle.js:83287:35
../node_modules/@theia/core/lib/common/disposable.js/push/disposable.dispose@http://localhost:3300/bundle.js:78934:13
dispose@http://localhost:3300/bundle.js:78911:40
dispose@http://localhost:3300/bundle.js:83388:24
onUnderlyingChannelClose@http://localhost:3300/bundle.js:83292:18
../node_modules/@theia/core/lib/common/message-rpc/channel.js/ChannelMultiplexer/<@http://localhost:3300/bundle.js:83271:58
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
reconnectListener@http://localhost:3300/bundle.js:56349:56
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
emitEvent@http://localhost:3300/bundle.js:485230:20
onevent@http://localhost:3300/bundle.js:485217:18
onpacket@http://localhost:3300/bundle.js:485185:22
../node_modules/@socket.io/component-emitter/lib/esm/index.js/Emitter.prototype.emit@http://localhost:3300/bundle.js:486355:20
../node_modules/socket.io-client/build/cjs/manager.js/ondecoded/<@http://localhost:3300/bundle.js:484471:18

2026-07-30T09:07:27.732Z root INFO sending reconnect on ypzSzlUl4a1vXb4JAAAD
2026-07-30T09:07:27.734Z root INFO initial connect received on ypzSzlUl4a1vXb4JAAAD
2026-07-30T09:07:27.736Z root INFO [5c50cd82-8eb0-4a27-9637-526e6224196e] Waiting for backend deployment: 2.0 ms [322.983 s since frontend page start]
2026-07-30T09:07:27.736Z root INFO [5c50cd82-8eb0-4a27-9637-526e6224196e] Loading plugin contributions
2026-07-30T09:07:29.364Z root INFO INFO [SatelliteApplicationService] [main.js:2238] [requestGscSatelliteList] [GSC-DB] Requesting Satellite List...
2026-07-30T09:07:29.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.SatListRequest | CorrId: req-1785402449363-g87cbg4
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [main.js:1196] [handleDatabaseResponse] [GSC-DB-INCOMING] Class:  | CorrId: req-1785402449363-g87cbg4 | Keys: satelliteList
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [main.js:1200] [handleDatabaseResponse] ### GSC SAT LIST RECEIVED (5 ITEMS) ###
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 56178 | Name: IMC | Priority: 1 | TLE Auto: true | Disabled: false
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 39030 | Name: GK-2 | Priority: 2 | TLE Auto: true | Disabled: false
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 69097 | Name: 69097 | Priority: 3 | TLE Auto: true | Disabled: false
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 67206 | Name: 67206 | Priority: 4 | TLE Auto: true | Disabled: false
2026-07-30T09:07:29.371Z root INFO INFO [OdsListenerService] [1204:33] [js] [SAT] No: 60342 | Name: 60342 | Priority: 5 | TLE Auto: true | Disabled: false
2026-07-30T09:07:30.362Z root INFO INFO [SatelliteApplicationService] [main.js:2250] [requestGscStationList] [GSC-DB] Requesting Station List...
2026-07-30T09:07:30.362Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.database_request_queue_ | Class: tr.gov.uzay.gsc.server.database.api.messaging.requests.StationListRequest | CorrId: req-1785402450362-epee6t4
2026-07-30T09:07:30.368Z root INFO INFO [OdsListenerService] [main.js:1196] [handleDatabaseResponse] [GSC-DB-INCOMING] Class:  | CorrId: req-1785402450362-epee6t4 | Keys: stationList
2026-07-30T09:07:30.369Z root INFO INFO [OdsListenerService] [main.js:1222] [handleDatabaseResponse] ### GSC STATION LIST RECEIVED (2 ITEMS) ###
2026-07-30T09:07:30.369Z root INFO INFO [SatelliteApplicationService] [main.js:2510] [syncGroundStations] [GSC-SYNC] Synchronizing 2 ground stations...
2026-07-30T09:07:30.369Z root INFO INFO [SatelliteApplicationService] [main.js:2529] [syncGroundStations] [GSC-SYNC] Sync complete. Memory now contains 2 stations.
2026-07-30T09:07:30.369Z root INFO INFO [SatelliteApplicationService] [main.js:2535] [syncGroundStations] [GS-SYNC] Auto initializing active station to first available: MIYEG
2026-07-30T09:07:30.369Z root INFO INFO [OdsListenerService] [1225:33] [js] [GS] Name: MIYEG | Lat: 39.8914 | Lon: 32.77857 | Alt: 0.925 | ElevMask: 5
2026-07-30T09:07:30.369Z root INFO INFO [OdsListenerService] [1225:33] [js] [GS] Name: TROMSO | Lat: 69.3598 | Lon: 18.5993 | Alt: 0.142727 | ElevMask: 5
2026-07-30T09:07:30.405Z root INFO [SocDataService] fetchGroundStations success: Received 2 stations.
2026-07-30T09:07:30.405Z root INFO [SocDataService] _updateGroundStations: Updating state with 2 sanitized stations.
2026-07-30T09:07:30.405Z root INFO [SocDataService] fetchGroundStations finished inFlight for key: groundstations
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:3036] [unifiedRefresh] [GSC-REFRESH] Executing Unified Dashboard Refresh (GS: ALL)...
2026-07-30T09:07:37.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.passoperations_request_queue_ | Class: tr.gov.uzay.gsc.server.passoperations.api.messaging.requests.CurrentSatellitePassRequest | CorrId: DASHBOARD_CURRENT_DEFAULT_1785402457362
2026-07-30T09:07:37.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.NextSchedPassRequest | CorrId: DASHBOARD_NEXT_DEFAULT_1785402457363
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2608] [triggerGlobalPassRecalculation] triggerGlobalPassRecalculation → Firing GSC Pass calculation for all 2 stations in memory
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2611] [triggerGlobalPassRecalculation] [GSC-PASS-CALC] Dispatching requestFilteredPasses for GS: MIYEG
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2902] [requestFilteredPasses] [GSC-PASSCALC] Requesting filtered pass list for ground station: MIYEG
2026-07-30T09:07:37.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FilteredPassListGenerationRequest | CorrId: FILTEREDPASS:MIYEG_1785402457363
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2611] [triggerGlobalPassRecalculation] [GSC-PASS-CALC] Dispatching requestFilteredPasses for GS: TROMSO
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2902] [requestFilteredPasses] [GSC-PASSCALC] Requesting filtered pass list for ground station: TROMSO
2026-07-30T09:07:37.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FilteredPassListGenerationRequest | CorrId: FILTEREDPASS:TROMSO_1785402457364
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2843] [requestAllSatellitesPassListsFromOds] [GSC-PASS-PREDICTION] Requesting GLOBAL pass lists from GSC (Past + Future)...
2026-07-30T09:07:37.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.PastPassListRequest | CorrId: PAST_REFRESH_undefined_1785402457364
2026-07-30T09:07:37.364Z root INFO INFO [ArtemisService] [main.js:846] [publish] [ARTEMIS] Message sent to gsc.server.passcalculations_request_queue_ | Class: tr.gov.uzay.gsc.server.passcalculations.api.messaging.requests.FuturePassListRequest | CorrId: FUTURE_REFRESH_undefined_1785402457364
2026-07-30T09:07:37.364Z root INFO INFO [SatelliteApplicationService] [main.js:2870] [requestAllSatellitesPassListsFromOds] [GSC-REFRESH] Dispatched both Past and Future requests. IDs: PAST_REFRESH_undefined_1785402457364, FUTURE_REFRESH_undefined_1785402457364
2026-07-30T09:07:37.365Z root INFO INFO [SatelliteApplicationService] [main.js:3049] [unifiedRefresh] [GSC-REFRESH] Unified Refresh commands dispatched successfully for GS: "ALL".
2026-07-30T09:07:37.367Z root INFO INFO [OdsListenerService] [main.js:1476] [handlePassCalcResponse] [GSC-PASSCALC] Received Message | ID: DASHBOARD_NEXT_DEFAULT_1785402457363 | Items: 5 | Keys: passList
2026-07-30T09:07:37.368Z root INFO INFO [OdsListenerService] [main.js:1514] [handlePassCalcResponse] [GSC-PASSCALC] Received Dashboard Approaching (GS: DEFAULT) | Items: 5
026-07-30T09:07:27.732Z root ERROR [SocDataService] Trigger refresh-all failed: ../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/</<@http://localhost:3300/bundle.js:83679:68
../node_modules/@theia/core/lib/common/message-rpc/rpc-protocol.js/RpcProtocol/<@http://localhost:3300/bundle.js:83679:34
../node_modules/@theia/core/lib/common/event.js/</</<@http://localhost:3300/bundle.js:79547:69
invoke@http://localhost:3300/bundle.js:79554:26
fire@http://localhost:3300/bundle.js:79685:36
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/</<@http://localhost:3300/bundle.js:83288:44
../node_modules/@theia/core/lib/common/message-rpc/channel.js/onUnderlyingChannelClose/<@http://localhost:3300/bundle.js:83287:35
../node_modules/@theia/^C
