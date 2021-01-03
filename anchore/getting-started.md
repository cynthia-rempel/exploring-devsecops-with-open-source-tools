# TODO: insert README here

## quick-start

Mostly inspired by: https://engine.anchore.io/docs/quickstart/

### Install Anchore Engine
```
# create the containers
mkdir anchore
cd anchore
curl https://engine.anchore.io/docs/quickstart/docker-compose.yaml > docker-compose.yaml 

# verify the docker-compose.yaml wasn't moved
cat docker-compose.yaml 

# launch the docker-compose
docker-compose up -d

# watch the services start
watch docker-compose ps -a

# check the status of the services
docker-compose exec api anchore-cli system status

# check the status of the feeds
docker-compose exec api anchore-cli system feeds list
```
### Smoke test the install
Once the relevant feeds are sync'd start a second terminal
```
# Add an image to scan
docker-compose exec api anchore-cli image add docker.io/library/debian:7

# Watch the image import
docker-compose exec api anchore-cli image wait docker.io/library/debian:7

# Get a software list
docker-compose exec api anchore-cli image content docker.io/library/debian:7 os

# Get a list of vulnerabilities
docker-compose exec api anchore-cli image vuln docker.io/library/debian:7 all

# Check if the image is in compliance with policies
docker-compose exec api anchore-cli evaluate check docker.io/library/debian:7
``
