# TODO: insert README stuff

Mostly inspired by

https://github.com/DefectDojo/django-DefectDojo/blob/master/DOCKER.md

## installing

The main tool
```
git clone https://github.com/DefectDojo/django-DefectDojo.git

cd django-DefectDojo

bash -c "bash -x docker/setEnv.sh release && docker-compose up"

# it takes a looong time, so run:
# when Admin password: XYZXYZ shows up, it's ready to be logged into
docker-compose logs -f initializer 

```

The cli

https://github.com/Braincoke/defectdojo-cli

```
# Temporarily "install" gradle
sudo mkdir /opt/gradle
sudo unzip -d /opt/gradle ~/Downloads/gradle-6.7.1-bin.zip

# gradle uses non-standard ports
sudo systemctl stop firewalld
sudo PATH=$PATH:/opt/gradle/gradle-6.7.1/bin /opt/gradle/gradle-6.7.1/bin/gradle installDist
sudo systemctl start firewalld
sudo cp -r build/install/defectdojo-cli/lib/* /usr/local/lib/
sudo cp build/install/defectdojo-cli/bin/defectdojo-cli /usr/local/bin
defectdojo-cli --help

sudo systemctl start firewalld
# optionally, uninstall gradle
rm -rf /opt/gradle
```

## quickstart

Note: docs can be found at, http://localhost:8080/api/v2/doc/

```
# login
curl --header "Content-Type:application/json" --header "Accept:application/json" -X POST --data '{"username":"admin","password":"MBX..."}' http://localhost:8080/api/v2/api-token-auth/

# add Business Operations, Misc product-types 
curl --header "Content-Type:application/json" \
  --header "Accept:application/json" \
  -X POST --data \
  '{"name": "Business Operations", "critical_product": true, "key_product": true, "authorized_users": []}' \
  -u admin:AdminPassword \
http://localhost:8080/api/v2/product_types/
curl --header "Content-Type:application/json" \
  --header "Accept:application/json" \
  -X POST --data \
  '{"name": "Miscellaneous", "critical_product": true, "key_product": true, "authorized_users": []}' \
  -u admin:AdminPassword \
http://localhost:8080/api/v2/product_types/

# Check your work at http://localhost:8080/product/type

```

