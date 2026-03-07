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

scan target by running zap in CLI 
```sh
docker run --rm \                                                                                      ✔  8509  15:33:58
  -v "$(pwd):/zap/wrk" \
  -t ghcr.io/zaproxy/zaproxy:stable \
  zap-baseline.py \
  -t http://host.docker.internal:3000 \
  -r zap-report.html
```