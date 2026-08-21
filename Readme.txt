# Builder stage
FROM yeralti:8282/pardus25-1-node22.14-ci:1.0.0 as build-stage

WORKDIR /home/theia

# Copy repository files
COPY . .

ENV ELECTRON_GET_USE_PROXY "http://proxy.uzay.tubitak.gov.tr:3128"

RUN npm config set registry="http://uzayrepo.uzay.tubitak.gov.tr/repository/npm-proxy" -g && \
npm config set https-proxy="http://proxy.uzay.tubitak.gov.tr:3128" -g && \
npm config set proxy="http://proxy.uzay.tubitak.gov.tr:3128" -g

ENV http_proxy "http://proxy.uzay.tubitak.gov.tr:3128"
ENV https_proxy "http://proxy.uzay.tubitak.gov.tr:3128"
ENV no_proxy "localhost,127.0.0.1,.uzay.tubitak.gov.tr"
ENV PUPPETEER_SKIP_DOWNLOAD=true \
    PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true \
    npm_config_puppeteer_skip_download=true \
    NODE_OPTIONS="--max_old_space_size=8192"

RUN apt-get update && apt-get install -y \
    libx11-dev \
    libxkbfile-dev \
    libsecret-1-dev \
    build-essential python3 make g++ gcc  python3-setuptools && \
    rm -rf /var/lib/apt/lists/*

# Install dependencies, compile application
# Remove unnecesarry files for the browser application
# Download plugins and build application production mode
RUN npm install --verbose && \
    npx lerna run build --scope="@uzay/gsc-core-extension" \
    npm run build:extensions --verbose && \
    npm run download:plugins --verbose && \
    npm run build:browser:prod --verbose && \
    find . -name \*.ts -o -name \*.ts.map -o -name \*.spec.* -type f -delete && \
    rm -rf .git gsc-core-extension

# Production stage uses a small base image
FROM yeralti:8282/pardus25-1-node22.14-ci:1.0.0 as production-stage

USER root

# Copy application from builder-stage
COPY --from=build-stage --chown=theia:theia /home/theia /home/theia

# Create theia user and directories
# Application will be copied to /home/theia
# Default workspace is located at /home/project
#RUN addgroup theia && adduser --ingroup theia theia
RUN chmod g+rw /home && \
    mkdir -p /home/project && \
    mkdir -p /home/theia/.theia && \
    echo '{"security.workspace.trust.enabled": false}' > /home/theia/.theia/settings.json && \
    chown -R theia:theia /home/theia && \
    chown -R theia:theia /home/project && \
    #theia'ya şifre ata
    echo "theia:theia123" | chpasswd


# Copy jupyter config
#COPY jupyter_server_config.py /etc/jupyter/jupyter_server_config.py

#RUN apt-get update && apt-get install -y apt-transport-https && \
#    apt-get update && apt-get install -y git openssh-client openssh-server libsecret-1-0 nano sudo python3 python3-pip python3-venv make g++ && \
#    apt-get clean

ENV HOME /home/theia
WORKDIR /home/theia


#RUN python3 -m venv  /home/theia/jupyter-env && \
#    pip config set global.index-url http://uzayrepo.uzay.tubitak.gov.tr/repository/pypi-proxy/simple && \
#    pip config set global.trusted-host uzayrepo.uzay.tubitak.gov.tr && \
#    /home/theia/jupyter-env/bin/pip install --upgrade pip && \
#    /home/theia/jupyter-env/bin/pip install jupyterhub jupyter-server-proxy 



EXPOSE 3000 8000

# Specify default shell for Theia and the Built-In plugins directory
ENV SHELL=/bin/bash \
    THEIA_DEFAULT_PLUGINS=local-dir:/home/theia/plugins \
    MBTILES_DIR=/home/theia/data/public/mbtiles \
    PUBLIC_ASSETS_DIR=/home/theia/data/public

# Use installed git instead of dugite
#ENV USE_LOCAL_GIT true
#ENV PATH="/home/theia/jupyter-env/bin:$PATH"

# Swtich to Theia user
USER theia
WORKDIR /home/theia/browser-app

# Launch the backend application via node
ENTRYPOINT [ "node", "/home/theia/browser-app/lib/backend/main.js" ]

# Arguments passed to the application
CMD [ "--root-dir=/home/project", "--hostname=0.0.0.0", "--port=3000"]
