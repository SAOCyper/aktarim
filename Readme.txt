.78 
28.78 > postinstall
28.78 > theia check:theia-version
28.78 
28.94 Found 3 missing packages:
28.94 
28.94 * perf_hooks
28.94 * reflect-metadata
28.94 * module
28.94 
28.94 
28.96 
28.96 added 2199 packages in 29s
28.96 
28.96 314 packages are looking for funding
28.96   run `npm fund` for details
28.96 npm verbose cwd /home/theia
28.96 npm verbose os Linux 6.12.69+deb13-amd64
28.96 npm verbose node v22.14.0
28.96 npm verbose npm  v10.9.2
28.96 npm verbose exit 0
28.96 npm info ok
29.72 ERR! lerna Unknown arguments: npm, run, build:extensions
------
Dockerfile:33
--------------------
  32 |     # Download plugins and build application production mode
  33 | >>> RUN npm install --verbose && \
  34 | >>>     npx lerna run build --scope="@uzay/gsc-core-extension" \
  35 | >>>     npm run build:extensions --verbose && \
  36 | >>>     npm run download:plugins --verbose && \
  37 | >>>     npm run build:browser:prod --verbose && \
  38 | >>>     find . -name \*.ts -o -name \*.ts.map -o -name \*.spec.* -type f -delete && \
  39 | >>>     rm -rf .git gsc-core-extension
  40 |     
--------------------
ERROR: failed to solve: process "/bin/sh -c npm install --verbose &&     npx lerna run build --scope=\"@uzay/gsc-core-extension\"     npm run build:extensions --verbose &&     npm run download:plugins --verbose &&     npm run build:browser:prod --verbose &&     find . -name \\*.ts -o -name \\*.ts.map -o -name \\*.spec.* -type f -delete &&     rm -rf .git gsc-core-extension" did not complete successfully: exit code: 1
mert@mertunubol:~/Development/gsc.scheduling.theia$ 
