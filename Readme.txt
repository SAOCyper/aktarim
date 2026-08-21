31.28  Lerna (powered by Nx)   Running target build for 8 projects failed
31.28 
31.28 Tasks not run because their dependencies failed or --nx-bail=true:
31.28 
31.28 - @uzay/gsc-files-extension:build
31.28 - @uzay/gsc-mission-extension:build
31.28 - @uzay/gsc-moon-extension:build
31.28 - @uzay/gsc-pass-control-extension:build
31.28 - @uzay/gsc-pass-prediction-extension:build
31.28 - @uzay/gsc-settings-extension:build
31.28 
31.28 Failed tasks:
31.28 
31.28 - @uzay/gsc-earth-extension:build
31.28 
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
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npx lerna run build --scope=\"@uzay/*\" --concurrency=1 --skip-nx-cache &&     npm run download:plugins --verbose &&     npm run bui
