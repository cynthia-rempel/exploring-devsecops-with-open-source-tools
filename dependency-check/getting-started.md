# Getting Started

# Installing/Running



```

# Copy the source to be analyzed
git clone https://github.com/WebGoat/WebGoat.git

# Ensure the container can write to the directory
sudo chmod -R 777 WebGoat/

cd WebGoat/

# Copy the instructions on how to run the dependecy check container
vi dependency-check-docker.sh
bash dependency-check-docker.sh 

# Look at the format of the output
ls odc-reports/

# Look at the results
firefox odc-reports/dependency-check-report.html 

```

## Reference

- https://hub.docker.com/r/owasp/dependency-check
- https://jeremylong.github.io/DependencyCheck/dependency-check-cli/index.html
