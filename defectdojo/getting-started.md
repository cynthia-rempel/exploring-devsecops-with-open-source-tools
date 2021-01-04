# TODO: insert README stuff

Mostly inspired by

https://github.com/DefectDojo/django-DefectDojo/blob/master/DOCKER.md

## installing

```
git clone https://github.com/DefectDojo/django-DefectDojo.git

cd django-DefectDojo

bash -c "bash -x docker/setEnv.sh release && docker-compose up"

# it takes a looong time, so run:
# when Admin password: XYZXYZ shows up, it's ready to be logged into
docker-compose logs -f initializer 

```
## quickstart
