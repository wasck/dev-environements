# [<](../README.md) | Jenkins
## Run jenkins environment
- start service from docker-compose.yml file:
  ```Bash
  docker-compose -f jenkins/docker-compose.yml up -d
  ```
- Docker Container should running
  ```Bash
  docker ps
  ```
- Copy admin password from ./jenkins_home/secrets/initialAdminPassword
- Walk through jenkins setup
- Open [jenkins](http://localhost:8090)

## Shutdown jenkins service
```Bash
docker-compose -f jenkins/docker-compose.yml down
docker container rm local_jenkins_service
```

## Reset environment
Just delete jenkins_home directory
- with Powershell
  ```Powershell
  Remove-Item jenkins/jenkins_home -Recurse -Force
  ```