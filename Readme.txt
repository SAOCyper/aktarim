# Launch the backend application via shell so we can detect correct path
SHELL ["/bin/bash", "-c"]
ENTRYPOINT ["/bin/bash", "-c", "if [ -f /home/theia/browser-app/lib/backend/main.js ]; then exec node /home/theia/browser-app/lib/backend/main.js \"$@\"; elif [ -f /home/theia/browser-app/src-gen/backend/main.js ]; then exec node /home/theia/browser-app/src-gen/backend/main.js \"$@\"; else echo 'ERROR: main.js bulunamadi!' && find /home/theia/browser-app -name main.js 2>/dev/null && exit 1; fi", "--"]
# Arguments passed to the application
CMD [ "--root-dir=/home/project", "--hostname=0.0.0.0", "--port=3000"]
