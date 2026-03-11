This is an example e-commerce app I use to testing out Owasp-zap tool to find out vulnerability.

Run the application using this commands
```sh
docker run -d \
--name juice-shop \
-p 3001:3000 \
bkimminich/juice-shop
```

access the app
```sh
localhost:3000
```

## Download and Scan application target by running zap trough CLI 
```sh
docker run --rm \
  -v "$(pwd):/zap/wrk" \
  -t ghcr.io/zaproxy/zaproxy:stable \
  zap-baseline.py \
  -t http://host.docker.internal:3000 \
  -r zap-report.html
```

It will scan thoroughly the application in a run time and send the output to the ``zap-report.html``

Scan the app trough UI with docker

```sh
docker run -it \
  -p 8080:8080 \
  ghcr.io/zaproxy/zaproxy:stable \
  zap-webswing.sh
```

