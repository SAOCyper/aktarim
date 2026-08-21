import { ContainerModule } from '@theia/core/shared/inversify';
import { BackendApplicationContribution } from '@theia/core/lib/node';
import { ConnectionHandler, JsonRpcConnectionHandler } from '@theia/core/lib/common/messaging';

import { ArtemisService } from './services/artemis.service';
import { SatelliteApplicationService } from './services/satellite-application.service';
import { OdsListenerService } from './services/ods-listener.service';
import { SatelliteClientManager } from './rpc/satellite-client-manager';
import { SatelliteServerImpl } from './rpc/satellite-server-impl';
import { satelliteServerPath, SatelliteClient, SatelliteServer, SatelliteServerSymbol } from '../common/theia-entry';
import { SocBackendContribution } from './soc-backend-contribution';
import { StaticAssetsServerContribution } from './static-assets-server-contribution';

export default new ContainerModule(bind => {
    console.log('[SOC Core] Backend module loaded. Registering all backend services & RPC.');

    // Static Assets Server (Existing binding)
    bind(StaticAssetsServerContribution).toSelf().inSingletonScope();
    
    // Migrated Background Services
    bind(ArtemisService).toSelf().inSingletonScope();
    bind(SatelliteApplicationService).toSelf().inSingletonScope();
    bind(OdsListenerService).toSelf().inSingletonScope();
    
    // JSON-RPC Infrastructure
    bind(SatelliteClientManager).toSelf().inSingletonScope();
    bind(SatelliteServerSymbol).to(SatelliteServerImpl).inSingletonScope();
    
    // Bind Connection Handler for WebSocket JSON-RPC
    bind(ConnectionHandler).toDynamicValue(ctx =>
        new JsonRpcConnectionHandler<SatelliteClient>(satelliteServerPath, client => {
            const server = ctx.container.get<SatelliteServer>(SatelliteServerSymbol);
            (server as SatelliteServerImpl).setClient(client);
            client.onDidCloseConnection(() => {
                (server as SatelliteServerImpl).dispose(client);
            });
            return server;
        })
    ).inSingletonScope();

    // Lifecycle Contributions
    bind(BackendApplicationContribution).to(SocBackendContribution).inSingletonScope();
    bind(BackendApplicationContribution).toService(StaticAssetsServerContribution);
});
