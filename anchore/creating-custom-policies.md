# How to create custom policies

## export/import policies locally
```
# get into the container
docker-compose exec api bash

# create the policy in a writable directory
anchore-cli policy get anchore_default_bundle --detail > /tmp/new-policy.json

# add the new policy
anchore-cli policy add /tmp/new-policy.json
```
