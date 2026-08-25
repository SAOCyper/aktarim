# esbuild node bundler outputs to lib/backend/main.js
ENTRYPOINT [ "node", "/home/theia/browser-app/lib/backend/main.js" ]
CMD [ "--root-dir=/home/project", "--hostname=0.0.0.0", "--port=3000" ]
