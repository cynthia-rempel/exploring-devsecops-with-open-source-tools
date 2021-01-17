note: need to set ADMIN environment variable while bringing up docker-compose for archerysec

docker-compose exec archerysec bash
source /home/archerysec/app/venv/bin/activate
ADMIN=admin
python manage.py initadmin
pip install archerysec-cli

# Get a list of projects
archerysec-cli --server http://127.0.0.1:8000 --user admin --password admin \
  --projectlist

# There are no projects
archerysec-cli --server http://127.0.0.1:8000 --user admin --password admin \
  --createproject \
  --project_name="My Project" \
  --project_disc="My Project's Description" \
  --project_start="2018-01-11" \
  --project_end="2024-01-11" \
  --project_owner="first.last"

# Verify the project is created
archerysec-cli --server http://127.0.0.1:8000 --user admin --password admin \
  --projectlist
  
# There are no scans
archerysec-cli --server http://127.0.0.1:8000 --user admin --password admin   --zapscanlist


archerysec-cli -s http://127.0.0.1:8000 -u admin -p admin -t
