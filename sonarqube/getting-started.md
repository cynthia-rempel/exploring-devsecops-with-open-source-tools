# Getting Started

# Installing Sonarqube
```
docker-compose up
```
## Installing the cli
```
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.5.0.2216.zip
unzip sonar-scanner-cli-4.5.0.2216.zip
```
## Configuring the cli
```
vi sonar-scanner-4.5.0.2216/conf/sonar-scanner.properties 
...
#Configure here general information about the environment, such as SonarQube server connection details for example
#No information about specific project should appear here

#----- Default SonarQube server
sonar.host.url=http://localhost:9000
sonar.login=admin
sonar.password=password
sonar.projectBaseDir=/home/cindy/django-DefectDojo
sonar.projectKey=my:project

#----- Default source code encoding
#sonar.sourceEncoding=UTF-8
```
# Using the scanner
```
sonarqube/sonar-scanner-4.5.0.2216/bin/sonar-scanner
```
 
 ## Generate the report
 ```
 sonar-report \
  --sonarurl="http://localhost:9000" \
  --sonarcomponent="sopra-steria:soprasteria_sonar-report" \
  --project="my:project" \
  --application="sonar-report" \
  --release="1.0.0" \
  --branch="feature/branch" \
  --sinceleakperiod="false" \
  --allbugs="false"
 ```
 ## References:
 https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/
