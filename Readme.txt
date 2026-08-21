import { injectable } from '@theia/core/shared/inversify';
import { BackendApplicationContribution } from '@theia/core/lib/node';
import * as express from 'express';
import * as path from 'path';
import * as fs from 'fs';

@injectable()
export class StaticAssetsServerContribution implements BackendApplicationContribution {
    configure(app: express.Application): void {
        // Find the public assets directory
        // In production (Docker), PUBLIC_ASSETS_DIR can be set to the mount point (e.g., /app/public).
        // During local development, it defaults to the local 'public' folder inside gsc-core-extension.
        const publicDir = process.env.PUBLIC_ASSETS_DIR || path.resolve(__dirname, '../../public');
        
        if (fs.existsSync(publicDir)) {
            console.log(`[StaticAssetsServer] Serving static assets from ${publicDir}`);
            
            // Map the runtime directories/files to the expected web routes
            app.use('/textures', express.static(path.join(publicDir, 'textures')));
            app.use('/tiles',    express.static(path.join(publicDir, 'tiles')));
            app.use('/models',   express.static(path.join(publicDir, 'models')));
            app.use('/earth',    express.static(path.join(publicDir, 'earth')));
            app.use('/moon',     express.static(path.join(publicDir, 'moon')));
            console.log(`[StaticAssetsServer] Routes: /textures, /tiles, /models, /earth, /moon`);
        } else {
            console.warn(`[StaticAssetsServer] WARNING: Public assets directory not found at ${publicDir}. Ensure PUBLIC_ASSETS_DIR env var is set and the volume is mounted.`);
        }
    }
}
