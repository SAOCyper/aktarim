/**
 * SOC Core Backend Module
 *
 * Theia InversifyJS bağlantıları: Node.js (sunucu) tarafı.
 *
 * NOT: Ağır backend servisleri (ArtemisService, OdsListenerService,
 * SatelliteApplicationService, SatelliteServerImpl) kasıtlı olarak
 * soc-earth-extension içinde bırakıldı. Bunlar Earth eklentisine
 * özgü servislerdir.
 *
 * Bu backend modülü şimdilik yalnızca bir yer tutucu (placeholder) olarak
 * vardır. İleride core-extension'a özgü backend işlevleri buraya eklenebilir
 * (örneğin genel-amaçlı sağlık kontrolü, versiyon bilgisi endpoint'i vb.).
 */
import { ContainerModule } from '@theia/core/shared/inversify';
import { BackendApplicationContribution } from '@theia/core/lib/node';
import { StaticAssetsServerContribution } from './static-assets-server-contribution';

export default new ContainerModule(bind => {
    console.log('[SOC Core] Backend module loaded. Binding StaticAssetsServerContribution.');
    
    bind(StaticAssetsServerContribution).toSelf().inSingletonScope();
    bind(BackendApplicationContribution).toService(StaticAssetsServerContribution);
});
