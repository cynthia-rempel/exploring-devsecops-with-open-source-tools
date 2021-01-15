# Getting Started

## Installing

```
sudo dnf install openscap-scanner \
    scap-security-guide \
    openscap-containers
```

## Using

```
# list the OSs that can be scanned, note the directory may be different if your not using Fedora
sudo ls /usr/share/xml/scap/ssg/content/ | grep ubuntu

# get the image to scan
docker pull ubuntu:18.04

# xccdf wasn't working, so use OVAL
sudo oscap-docker image docker.io/library/ubuntu:18.04 oval eval \
  --results oval-results.xml \
  --report report.html \
  --fetch-remote-resources \
  /usr/share/xml/scap/ssg/content/ssg-ubuntu1804-oval.xml
  
# view the results
sudo chown myuser:mygroup report.html
firefox report.html
```
