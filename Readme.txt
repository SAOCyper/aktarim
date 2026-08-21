import { injectable } from '@theia/core/shared/inversify';
import { SatelliteClient } from '../../common/theia-entry';
import { CustomLogger } from '../logging/custom-logger';

@injectable()
export class SatelliteClientManager {
    private readonly logger = new CustomLogger(SatelliteClientManager.name);
    private clients = new Set<SatelliteClient>();

    addClient(client: SatelliteClient) {
        this.clients.add(client);
    }

    removeClient(client: SatelliteClient) {
        this.clients.delete(client);
    }

    // Adapts the old Socket.io 'broadcast' signature to our new JSON-RPC client interface
    broadcast(event: string, data: any) {
        for (const client of this.clients) {
            try {
                switch (event) {
                    case 'satellite_updated':
                        client.onSatelliteUpdated(data);
                        break;
                    case 'ground_station_updated':
                        client.onGroundStationUpdated(data);
                        break;
                    case 'pass_prediction':
                        client.onPassPrediction(data);
                        break;
                    case 'current_pass':
                        client.onCurrentPass(data);
                        break;
                    case 'approaching_passes':
                        client.onApproachingPasses(data);
                        break;
                    case 'system_mode_update':
                        client.onSystemModeUpdate(data);
                        break;
                    case 'config_change_result':
                        client.onConfigChangeResult(data);
                        break;
                    case 'sat_config_names':
                        client.onSatConfigNames(data);
                        break;
                    case 'sat_config_details':
                        client.onSatConfigDetails(data);
                        break;
                    case 'global_config_names':
                        client.onGlobalConfigNames(data);
                        break;
                    case 'global_config_details':
                        client.onGlobalConfigDetails(data);
                        break;
                    case 'global_config_operation_result':
                    case 'sat_config_operation_result':
                    case 'system_mode_setting_result':
                        client.onConfigOperationResult(data);
                        break;
                    case 'latest_tle_update':
                        client.onLatestTleUpdate(data);
                        break;
                    case 'tle_renewal_result':
                        client.onTleRenewalResult(data);
                        break;
                    case 'pass_trajectory_update':
                    case 'gsc_pass_trajectory':
                        client.onPassTrajectoryUpdate(data);
                        break;
                    case 'pass_preferences':
                        client.onPassPreferences(data);
                        break;
                    case 'pass_settings_feedback':
                        client.onPassSettingsFeedback(data);
                        break;
                    case 'pass_schedule_setting_result':
                        client.onPassScheduleSettingResult(data);
                    default:
                        this.logger.warn(`Unmapped broadcast event: ${event}`);
                }
            } catch (err: any) {
                this.logger.error(`Error broadcasting ${event}: ${err.message}`);
            }
        }
    }
}
