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

# Browse the product types at http://localhost:8080/product/type

# How to some test types, Anchore is already in http://localhost:8080/test_type , so not needed at this time
# curl --header "Content-Type:application/json" \
#  --header "Accept:application/json" \
#  -X POST --data \
#  '{"tags": [ "tag123" ], "name": "Anchore Scan", "static_tool": true, "dynamic_tool": false}' \
#  -u admin:AdminPassword http://localhost:8080/api/v2/test_types/

```

