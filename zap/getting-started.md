```
docker run --rm \
   --name zap \
   -u zap \
   -p 8090:8090 \
   -d owasp/zap2docker-stable \
      zap.sh \
         -daemon \
         -port 8090 \
         -host 0.0.0.0 \
         -config api.disablekey=true
```
```
docker exec -ti zap \
   zap-cli \
   --zap-url 'http://localhost' --port 8090 \
   quick-scan \
   'http://192.168.0.11:8080'
```
