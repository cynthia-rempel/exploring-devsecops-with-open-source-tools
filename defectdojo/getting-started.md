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

# Add some users:
#   product_manager
#   technical_contact
#   team_manager
# picked names from: http://donatellanobatti.blogspot.com/2012/02/list.html
curl --header "Content-Type:application/json" \
  --header "Accept:application/json" \
  -X POST --data \
  '{
      "username": "mario.speedwagon",
      "first_name": "mario",
      "last_name": "speedwagon",
      "email": "mario.speedwagon@example.com",
      "is_active": true,
      "is_staff": true,
      "is_superuser": false
  }' \
  -u admin:AdminPassword \
  http://localhost:8080/api/v2/users/

curl --header "Content-Type:application/json" \
  --header "Accept:application/json" \
  -X POST --data \
  '{
      "username": "anna.sthesia",
      "first_name": "anna",
      "last_name": "sthesia",
      "email": "anna.sthesia@example.com",
      "is_active": true,
      "is_staff": true,
      "is_superuser": false
  }' \
  -u admin:AdminPassword \
  http://localhost:8080/api/v2/users/

curl --header "Content-Type:application/json" \
  --header "Accept:application/json" \
  -X POST --data \
  '{
      "username": "anna.mull",
      "first_name": "anna",
      "last_name": "mull",
      "email": "anna.mull@example.com",
      "is_active": true,
      "is_staff": true,
      "is_superuser": false
  }' \
  -u admin:AdminPassword \
  http://localhost:8080/api/v2/users/

# Create a product
curl --header "Content-Type:application/json" \
  --header "Accept:application/json" \
  -X POST --data   '{
  "tags": [
    "string"
  ],
  "name": "string",
  "description": "string",
  "prod_numeric_grade": 0,
  "business_criticality": "very high",
  "platform": "web service",
  "lifecycle": "construction",
  "origin": "third party library",
  "user_records": 0,
  "revenue": "6000",
  "external_audience": true,
  "internet_accessible": true,
  "product_manager": 1,
  "technical_contact": 2,
  "team_manager": 3,
  "prod_type": 1,
  "authorized_users": [],
  "regulations": [
    2
  ]
}'   -u admin:AdminPassword http://localhost:8080/api/v2/products/

# Create an engagement
curl --header "Content-Type:application/json"   --header "Accept:application/json"   -X POST --data   '{
  "tags": [
    "string"
  ],
  "name": "string",
  "description": "string",
  "version": "string",
  "first_contacted": "2021-01-05",
  "target_start": "2021-01-05",
  "target_end": "2021-01-05",
  "reason": "string",
  "tracker": "https://bugs.example.com",
  "test_strategy": "https://tests.example.com",
  "threat_model": true,
  "api_test": true,
  "pen_test": true,
  "check_list": true,
  "status": "Not Started",
  "engagement_type": "Interactive",
  "build_id": "string",
  "commit_hash": "string",
  "branch_tag": "string",
  "source_code_management_uri": "https://gitlab.example.com",
  "deduplication_on_engagement": true,
  "eng_type": "",
  "lead": 1,
  "requester": "",
  "preset": "",
  "report_type": "",
  "product": 1,
  "build_server": "",
  "source_code_management_server": "",
  "orchestration_engine": ""
}'   -u admin:AdminPassword   http://localhost:8080/api/v2/engagements/


# How to some test types, Anchore is already in http://localhost:8080/test_type , so not needed at this time
# curl --header "Content-Type:application/json" \
#  --header "Accept:application/json" \
#  -X POST --data \
#  '{"tags": [ "tag123" ], "name": "Anchore Scan", "static_tool": true, "dynamic_tool": false}' \
#  -u admin:AdminPassword http://localhost:8080/api/v2/test_types/

```

