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
