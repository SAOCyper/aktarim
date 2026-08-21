27.74 
27.74  Lerna (powered by Nx)   Running target build for 8 projects:
27.74 
27.74 - @uzay/gsc-core-extension
27.74 - @uzay/gsc-earth-extension
27.74 - @uzay/gsc-files-extension
27.74 - @uzay/gsc-mission-extension
27.74 - @uzay/gsc-moon-extension
27.74 - @uzay/gsc-pass-control-extension
27.74 - @uzay/gsc-pass-prediction-extension
27.74 - @uzay/gsc-settings-extension
27.74 
27.74 
27.75 
27.75 > @uzay/gsc-core-extension:build
27.75 
27.98 @uzay/gsc-core-extension: > @uzay/gsc-core-extension@1.0.0 build
27.98 @uzay/gsc-core-extension: > tsc
29.13 
29.13 > @uzay/gsc-earth-extension:build
29.13 
29.37 @uzay/gsc-earth-extension: > @uzay/gsc-earth-extension@1.0.0 build
29.37 @uzay/gsc-earth-extension: > tsc
30.62 @uzay/gsc-earth-extension: src/browser/cesium-view-widget.tsx(11,77): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
30.62 @uzay/gsc-earth-extension: src/browser/components/EarthViewer.tsx(45,8): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
30.62 @uzay/gsc-earth-extension: src/browser/satellite-client-impl.ts(2,49): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
30.62 @uzay/gsc-earth-extension: src/browser/soc-frontend-contribution.ts(25,55): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
30.62 @uzay/gsc-earth-extension: src/browser/soc-frontend-module.ts(12,93): error TS2307: Cannot find module '@uzay/gsc-core-extension' or its corresponding type declarations.
30.64 @uzay/gsc-earth-extension: npm error Lifecycle script `build` failed with error:
30.64 @uzay/gsc-earth-extension: npm error code 2
30.64 @uzay/gsc-earth-extension: npm error path /home/theia/extensions/gsc-earth-extension
30.64 @uzay/gsc-earth-extension: npm error workspace @uzay/gsc-earth-extension@1.0.0
30.64 @uzay/gsc-earth-extension: npm error location /home/theia/extensions/gsc-earth-extension
30.64 @uzay/gsc-earth-extension: npm error command failed
30.64 @uzay/gsc-earth-extension: npm error command sh -c tsc
30.65 
30.65 
30.65 
30.65  Lerna (powered by Nx)   Running target build for 8 projects failed
30.65 
30.65 Tasks not run because their dependencies failed or --nx-bail=true:
30.65 
30.65 - @uzay/gsc-files-extension:build
30.65 - @uzay/gsc-mission-extension:build
30.65 - @uzay/gsc-moon-extension:build
30.65 - @uzay/gsc-pass-control-extension:build
30.65 - @uzay/gsc-pass-prediction-extension:build
30.65 - @uzay/gsc-settings-extension:build
30.65 
30.65 Failed tasks:
30.65 
30.65 - @uzay/gsc-earth-extension:build
30.65 
------
Dockerfile:33
--------------------
  32 |     # Download plugins and build application production mode
  33 | >>> RUN npm install --verbose && \
  34 | >>>     npx lerna run build --scope="@uzay/*" --concurrency=1 --skip-nx-cache && \
  35 | >>>     #npm run build:extensions --concurrency=1 --skip-nx-cache --verbose && \
  36 | >>>     npm run download:plugins --verbose && \
  37 | >>>     npm run build:browser:prod --verbose && \
  38 | >>>     find . -name \*.ts -o -name \*.ts.map -o -name \*.spec.* -type f -delete && \
  39 | >>>     rm -rf .git gsc-core-extension
  40 |     
--------------------
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npx lerna run build --scope=\"@uzay/*\" --concurrency=1 --skip-nx-cache &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.map -o -name \\*.spec.* -type f -delete &&     rm -rf .git gsc-core-extension" did not complete successfully: exit code: 130
mert@mertunubol:~/Development/gsc.scheduling.theia$ 
