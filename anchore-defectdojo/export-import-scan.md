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
## Import into Anchore
**TODO**
see if the other curl commands can be rewritten into this format
and change X-CSRFToken into username/password
```
curl -X POST "http://localhost:8080/api/v2/import-scan/" \
  -H  "accept: application/json" \
  -H  "Content-Type: multipart/form-data" \
  -H "X-CSRFToken: 3O4kLGT2NkuzEj5N3NzDWuv8wHzqDhkb72waLAY87nNXczuWngotaiQ2XVDAkMvd" \
  -F "scan_date=2021-01-05" \
  -F "minimum_severity=Info" \
  -F "active=true" \
  -F "verified=true" \
  -F "scan_type=Anchore Engine Scan" \
  -F "file=@debian_7.json;type=application/json" \
  -F "engagement=1" \
  -F "close_old_findings=true" \
  -F "push_to_jira=false"
```
