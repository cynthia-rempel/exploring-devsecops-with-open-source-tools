# Things for long-term thinking

## High Availability

Ensure docker starts
```
systemctl enable docker
```

Ensure the containers start

docker-compose.yaml
```
restart: always # for each service
```

## Archiving old image analysis

```
# list the current rules
docker-compose exec api anchore-cli analysis-archive rules list

# get some info
docker-compose exec api anchore-cli analysis-archive rules --help

# determine how to add a rule
docker-compose exec api anchore-cli analysis-archive rules add --help

# add a bad rule to show how to delete it
docker-compose exec api anchore-cli analysis-archive rules add --is-global 90 5 archive
docker-compose exec api anchore-cli analysis-archive rules del 61558228101c4fdb908e22832636e565

# Add a rule to archive all analysis that archives all scans over 90 days old, that have a newer version
docker-compose exec api anchore-cli analysis-archive rules add --is-global 90 1 archive
```
## Installing basic policies
```
# Find the basic policies that are available
docker-compose exec api anchore-cli policy hub list

# Install the basic policies
docker-compose exec api anchore-cli policy hub install anchore_security_only
docker-compose exec api anchore-cli policy hub install anchore_cis_1.13.0_base
docker-compose exec api anchore-cli policy hub install anchore_default_bundle

# Verify they have been installed
docker-compose exec api anchore-cli policy list

# Activate the default bundle
docker-compose exec api anchore-cli policy activate anchore_default_bundle

# Delete the human-unreadable default bundle
docker-compose exec api anchore-cli policy del 2c53a13c-1765-11e8-82ef-23527761d060

# Verify the policies are there
docker-compose exec api anchore-cli policy list

```
