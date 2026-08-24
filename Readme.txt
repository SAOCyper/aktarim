import { injectable, inject } from '@theia/core/shared/inversify';
import { BackendApplicationContribution } from '@theia/core/lib/node';
import { ArtemisService } from './services/artemis.service';
import { SatelliteApplicationService } from './services/satellite-application.service';
import { OdsListenerService } from './services/ods-listener.service';
import { CustomLogger } from './logging/custom-logger';
import * as fs from 'fs';
import * as path from 'path';
// express type is intentionally omitted — Theia and root node_modules carry
// different @types/express versions that are incompatible at the TS level.
// The runtime object is a genuine express.Application; typed as `any` here.

/**
 * Directory where .mbtiles files are stored.
 * At runtime __dirname = packages/soc-earth-extension/lib/backend/
 * Three levels up lands in packages/, then we step into gsc-core-extension/public.
 * Override via MBTILES_DIR env var if files live elsewhere.
 */
const getMbtilesDir = () => {
    if (process.env.MBTILES_DIR) return process.env.MBTILES_DIR.trim();
    if (process.env.PUBLIC_ASSETS_DIR) {
        return path.join(process.env.PUBLIC_ASSETS_DIR.trim(), 'mbtiles');
    }
    return path.resolve(__dirname, '../../public/mbtiles');
};
const MBTILES_DIR = getMbtilesDir();
const MBTILES_STATE_FILE = path.join(MBTILES_DIR, '.mbtiles-state.json');

let memoryMbtilesState: Record<string, boolean> = {};

function ensureMbtilesDir() {
    try {
        if (!fs.existsSync(MBTILES_DIR)) {
            fs.mkdirSync(MBTILES_DIR, { recursive: true });
        }
        const earthDir = path.join(MBTILES_DIR, 'earth');
        const moonDir = path.join(MBTILES_DIR, 'moon');
        if (!fs.existsSync(earthDir)) fs.mkdirSync(earthDir, { recursive: true });
        if (!fs.existsSync(moonDir)) fs.mkdirSync(moonDir, { recursive: true });
    } catch (e: any) {
        console.warn(`[ensureMbtilesDir] Cannot create subdirectories in ${MBTILES_DIR}: ${e.message}`);
    }
}

function readMbtilesState(): Record<string, boolean> {
    try {
        if (fs.existsSync(MBTILES_STATE_FILE)) {
            const diskState = JSON.parse(fs.readFileSync(MBTILES_STATE_FILE, 'utf8'));
            return { ...diskState, ...memoryMbtilesState };
        }
    } catch { /* ignore */ }
    return { ...memoryMbtilesState };
}

function writeMbtilesState(state: Record<string, boolean>) {
    memoryMbtilesState = { ...memoryMbtilesState, ...state };
    try {
        ensureMbtilesDir();
        fs.writeFileSync(MBTILES_STATE_FILE, JSON.stringify(state, null, 2));
    } catch (err: any) {
        console.warn(`[writeMbtilesState] Could not write ${MBTILES_STATE_FILE} (${err.message}). Using memory state fallback.`);
    }
}

function listMbtilesForDataset(dataset: string, state: Record<string, boolean>) {
    const dir = path.join(MBTILES_DIR, dataset);
    let items: string[] = [];
    if (fs.existsSync(dir)) {
        try { items = fs.readdirSync(dir); } catch { /* ignore */ }
    }
    
    // Fallback for earth dataset: if earth/ subfolder is empty, check root MBTILES_DIR directly
    if (dataset === 'earth' && items.filter(f => f.endsWith('.mbtiles')).length === 0 && fs.existsSync(MBTILES_DIR)) {
        try {
            const rootFiles = fs.readdirSync(MBTILES_DIR).filter(f => f.endsWith('.mbtiles'));
            if (rootFiles.length > 0) {
                return rootFiles.map(filename => ({
                    filename,
                    dataset: 'earth',
                    enabled: state[`earth/${filename}`] ?? state[filename] ?? true,
                    path: path.join(MBTILES_DIR, filename)
                }));
            }
        } catch { /* ignore */ }
    }
    
    // Check if there are raw Z-level directories (e.g. "0", "1", "2") indicating extracted tiles
    let hasRawDirs = false;
    try {
        hasRawDirs = items.some(f => /^\d+$/.test(f) && fs.statSync(path.join(dir, f)).isDirectory());
    } catch { /* ignore stat errors */ }

    const dbs = items
        .filter(f => f.endsWith('.mbtiles'))
        .map(filename => ({
            filename,
            dataset,
            enabled: state[`${dataset}/${filename}`] ?? true,
            path: path.join(dir, filename)
        }));
        
    // If raw tiles exist, add a virtual entry so the frontend activates the layer
    if (hasRawDirs) {
        dbs.push({
            filename: 'raw_extracted_tiles_folder',
            dataset,
            enabled: state[`${dataset}/raw_extracted_tiles_folder`] ?? true,
            path: dir
        });
    }
    
    return dbs;
}

@injectable()
export class SocBackendContribution implements BackendApplicationContribution {
    private readonly logger = new CustomLogger(SocBackendContribution.name);

    constructor(
        @inject(ArtemisService) private readonly artemis: ArtemisService,
        @inject(SatelliteApplicationService) private readonly appService: SatelliteApplicationService,
        @inject(OdsListenerService) private readonly odsListener: OdsListenerService
    ) {}

    // eslint-disable-next-line @typescript-eslint/no-explicit-any
    configure(app: any): void {
        const express = require('express');
        app.use(express.json());
        app.use(express.urlencoded({ extended: true }));

        // ── GET /satellite/trajectory/:id ─────────────────────────────────────
        app.get('/satellite/trajectory/:id', async (req: any, res: any) => {
            const satId = req.params.id;
            try {
                const points = await this.odsListener.getTrajectory(satId);
                if (points.length === 0) {
                    const sat = await this.appService.getAllSatellites()
                        .then((sats: any[]) => sats.find((s: any) => s.id === satId || s.noradId === satId));
                    if (sat?.noradId) {
                        this.logger.log(`[REST /trajectory] Cache cold for ${satId}. Triggering GSC positions for NORAD ${sat.noradId}...`);
                        this.appService.requestGscSatPositions(sat.noradId).catch(() => {});
                    }
                }
                res.json(points);
            } catch (err: any) {
                this.logger.error(`[REST /trajectory] Error for ${satId}: ${err.message}`);
                res.status(500).json({ error: err.message });
            }
        });

        // ── GET /mbtiles/list ─────────────────────────────────────────────────
        app.get('/mbtiles/list', (_req: any, res: any) => {
            try {
                ensureMbtilesDir();
                const state = readMbtilesState();
                const earth = listMbtilesForDataset('earth', state);
                const moon  = listMbtilesForDataset('moon',  state);
                res.json({ earth, moon });
            } catch (err: any) {
                this.logger.error(`[REST /mbtiles/list] Error: ${err.message}`);
                res.status(500).json({ error: err.message });
            }
        });

        // ── POST /mbtiles/toggle ──────────────────────────────────────────────
        app.post('/mbtiles/toggle', (req: any, res: any) => {
            try {
                const { dataset, filename, enabled } = req.body || {};
                if (!dataset || !filename || enabled === undefined) {
                    return res.status(400).json({ error: 'dataset, filename and enabled are required' });
                }
                const state = readMbtilesState();
                state[`${dataset}/${filename}`] = !!enabled;
                writeMbtilesState(state);
                this.logger.log(`[REST /mbtiles/toggle] ${dataset}/${filename} → ${enabled}`);
                res.json({ ok: true });
            } catch (err: any) {
                this.logger.error(`[REST /mbtiles/toggle] Error: ${err.message}`);
                res.status(500).json({ error: err.message });
            }
        });

        // ── POST /mbtiles/upload/:dataset ─────────────────────────────────────
        // Accepts multipart/form-data with a single "file" field.
        app.post('/mbtiles/upload/:dataset', (req: any, res: any) => {
            const dataset = req.params.dataset as string;
            const datasetDir = path.join(MBTILES_DIR, dataset);
            try {
                ensureMbtilesDir();
                if (!fs.existsSync(datasetDir)) fs.mkdirSync(datasetDir, { recursive: true });
            } catch (err: any) {
                return res.status(500).json({ error: `Cannot create directory: ${err.message}` });
            }

            let savedFilename = '';
            const busboy = require('busboy');
            const bb = busboy({ headers: req.headers });

            bb.on('file', (name: string, file: any, info: any) => {
                const { filename } = info;
                if (!filename.endsWith('.mbtiles')) { file.resume(); return; }
                savedFilename = filename;
                const dest = path.join(datasetDir, filename);
                const ws = fs.createWriteStream(dest);
                file.pipe(ws);
            });

            bb.on('close', () => {
                if (savedFilename) {
                    this.logger.log(`[REST /mbtiles/upload] Saved ${dataset}/${savedFilename}`);
                    res.json({ success: true, filename: savedFilename });
                } else {
                    res.status(400).json({ error: 'No valid .mbtiles file received' });
                }
            });

            bb.on('error', (err: any) => {
                this.logger.error(`[REST /mbtiles/upload] busboy error: ${err.message}`);
                res.status(500).json({ error: err.message });
            });

            req.pipe(bb);
        });

        // ── GET /mbtiles/:z/:x/:y (Earth) and /mbtiles/:dataset/:z/:x/:y (Moon, etc.) ──
        const sqlite3 = require('sqlite3');
        const dbCache: Record<string, any> = {};
        const getDb = (filepath: string) => {
            if (!dbCache[filepath]) {
                dbCache[filepath] = new sqlite3.Database(filepath, sqlite3.OPEN_READONLY);
            }
            return dbCache[filepath];
        };

        const serveTile = (dataset: string, z: string, x: string, y: string, res: any) => {
            const state = readMbtilesState();
            const files = listMbtilesForDataset(dataset, state).filter(f => f.enabled);
            if (files.length === 0) {
                return res.status(404).send('No enabled datasets');
            }

            const cleanY = y.replace('.png', '').replace('.jpg', '').replace(/\?.*/, '');
            const parsedZ = parseInt(z, 10);
            const parsedX = parseInt(x, 10);
            const parsedY = parseInt(cleanY, 10);
            if (isNaN(parsedZ) || isNaN(parsedX) || isNaN(parsedY)) {
                return res.status(400).send('Invalid tile coordinates');
            }

            // Cesium requests tiles top-to-bottom. MBTiles (TMS) stores them bottom-to-top.
            const tmsY = (1 << parsedZ) - 1 - parsedY;

            const tryNextDb = (idx: number) => {
                if (idx >= files.length) {
                    // Fallback to raw directory structure if SQLite didn't have it (or if no .mbtiles files exist)
                    try {
                        const rawXyzPathPng = path.join(MBTILES_DIR, dataset, z, x, `${parsedY}.png`);
                        const rawXyzPathJpg = path.join(MBTILES_DIR, dataset, z, x, `${parsedY}.jpg`);
                        const rawTmsPathPng = path.join(MBTILES_DIR, dataset, z, x, `${tmsY}.png`);
                        const rawTmsPathJpg = path.join(MBTILES_DIR, dataset, z, x, `${tmsY}.jpg`);

                        if (fs.existsSync(rawTmsPathPng)) return res.sendFile(rawTmsPathPng);
                        if (fs.existsSync(rawTmsPathJpg)) return res.sendFile(rawTmsPathJpg);
                        if (fs.existsSync(rawXyzPathPng)) return res.sendFile(rawXyzPathPng);
                        if (fs.existsSync(rawXyzPathJpg)) return res.sendFile(rawXyzPathJpg);
                    } catch (e: any) {
                        this.logger.error(`[serveTile] Raw folder check failed: ${e.message}`);
                    }

                    return res.status(404).send('Tile not found');
                }

                const file = files[idx];
                if (file.filename === 'raw_extracted_tiles_folder') {
                    // Skip sqlite check for virtual folder item
                    return tryNextDb(idx + 1);
                }

                try {
                    const db = getDb(file.path);
                    db.get('SELECT tile_data FROM tiles WHERE zoom_level = ? AND tile_column = ? AND tile_row = ?',
                        [parsedZ, parsedX, tmsY],
                        (err: any, row: any) => {
                            if (row && row.tile_data) {
                                res.set('Content-Type', 'image/png');
                                res.set('Cache-Control', 'public, max-age=86400');
                                return res.send(row.tile_data);
                            }
                            // Fallback: try raw XYZ Y if TMS Y returned no tile
                            db.get('SELECT tile_data FROM tiles WHERE zoom_level = ? AND tile_column = ? AND tile_row = ?',
                                [parsedZ, parsedX, parsedY],
                                (err2: any, row2: any) => {
                                    if (row2 && row2.tile_data) {
                                        res.set('Content-Type', 'image/png');
                                        res.set('Cache-Control', 'public, max-age=86400');
                                        return res.send(row2.tile_data);
                                    }
                                    tryNextDb(idx + 1);
                                });
                        });
                } catch (err: any) {
                    this.logger.error(`[serveTile] SQLite database read error: ${err.message}`);
                    tryNextDb(idx + 1);
                }
            };
            tryNextDb(0);
        };

        app.get('/mbtiles/:z/:x/:y', (req: any, res: any) => {
            serveTile('earth', req.params.z, req.params.x, req.params.y, res);
        });

        app.get('/mbtiles/:dataset/:z/:x/:y', (req: any, res: any) => {
            serveTile(req.params.dataset, req.params.z, req.params.x, req.params.y, res);
        });

        // ── DELETE /mbtiles/:dataset/:filename ────────────────────────────────
        app.delete('/mbtiles/:dataset/:filename', (req: any, res: any) => {
            try {
                const { dataset, filename } = req.params;
                if (!dataset || !filename) {
                    return res.status(400).json({ error: 'dataset and filename are required' });
                }
                ensureMbtilesDir();
                // Basic traversal protection
                const safeFilename = filename.replace(/\.\./g, '');
                const targetPath = path.join(MBTILES_DIR, dataset, safeFilename);
                
                if (fs.existsSync(targetPath)) {
                    // Close cached database connection to release the file handle
                    if (dbCache[targetPath]) {
                        try {
                            dbCache[targetPath].close();
                            delete dbCache[targetPath];
                        } catch (err: any) {
                            this.logger.error(`[REST DELETE /mbtiles] Error closing SQLite connection: ${err.message}`);
                        }
                    }
                    
                    fs.unlinkSync(targetPath);
                    
                    // Clean up from state file if present
                    const state = readMbtilesState();
                    const stateKey = `${dataset}/${safeFilename}`;
                    if (stateKey in state) {
                        delete state[stateKey];
                        writeMbtilesState(state);
                    }

                    this.logger.log(`[REST DELETE /mbtiles] Deleted: "${dataset}/${safeFilename}"`);
                    res.json({ ok: true });
                } else {
                    res.status(404).json({ error: 'File not found' });
                }
            } catch (err: any) {
                this.logger.error(`[REST DELETE /mbtiles] Error: ${err.message}`);
                res.status(500).json({ error: err.message });
            }
        });

        ensureMbtilesDir();
        this.logger.log(`[MBTILES] Initialized MBTILES_DIR at: "${MBTILES_DIR}"`);
        this.logger.log('SOC Express routes registered: /satellite/trajectory, /mbtiles/*');
    }

    async onStart(): Promise<void> {
        this.logger.log('SOC Native Backend successfully started and services are initialized.');
    }
}
