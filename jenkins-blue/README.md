# [<](../README.md) | Jenkins Blueocean (recommended)
## Run jenkins-blue environment
- start service from docker-compose.yml file:
  ```Bash
  docker-compose -f jenkins-blue/docker-compose.yml up -d
  ```
- Docker Container should running
  ```Bash
  docker ps
  ```
- Copy admin password from ./jenkins_home/secrets/initialAdminPassword
- Walk through jenkins setup
- Open [jenkins](http://localhost:8090)
- Open [jenkins-blueocean](http://localhost:8090/blue)

## Shutdown jenkins blueocean service
- Shutdown from command line
```Bash
docker-compose -f jenkins-blue/docker-compose.yml down
docker container rm local_jenkins_service
```

## Reset environment
Just delete jenkins_home directory
- with Powershell
  ```Powershell
  Remove-Item jenkins-blue/jenkins_home -Recurse -Force; Remove-Item jenkins-blue/jenkins_docker_certs -Recurse -Force
  ```