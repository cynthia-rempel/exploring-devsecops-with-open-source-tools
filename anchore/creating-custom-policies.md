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
## Policies that can be applied

https://engine.anchore.io/docs/usage/cli_usage/policies/

If the link isn't working here is an example:

```
# Get the list of policy categories
docker-compose exec api anchore-cli policy describe

# Get a list of policies
docker-compose exec api anchore-cli policy describe --gate vulnerabilities

# Get a list of tests in the policies
docker-compose exec api anchore-cli policy describe --gate vulnerabilities --trigger severity
```
