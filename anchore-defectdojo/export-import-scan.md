# How to export scan from Anchore and import into Defectdojo

## Export from Anchore
To export from Anchore, first run the analysis, then export the results
```
# Run analysis
docker-compose exec api anchore-cli image add docker.io/library/debian:7
docker-compose exec api anchore-cli image wait docker.io/library/debian:7
docker-compose exec api anchore-cli image content docker.io/library/debian:7 os
docker-compose exec api anchore-cli image vuln docker.io/library/debian:7 all
docker-compose exec api anchore-cli evaluate check docker.io/library/debian:7

# Export results
docker-compose exec api anchore-cli --json image vuln docker.io/library/debian:7 all > debian_7.json
```

