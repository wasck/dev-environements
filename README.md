# Scripts to run environments

## Get project
- Clone from git
  ```Bash
  git clone https://github.com/wasck/dev-environements.git
  ```
- Switch to workspace
  ```Powershell
  Set-Location dev-environments
  ```

## Jenkins
### Run jenkins environment
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

### Shutdown jenkins service
```Bash
docker-compose -f jenkins/docker-compose.yml down
docker container rm local_jenkins_service
```

### Reset environment
Just delete everything in jenkins_home but README.md
- with Powershell
  ```Powershell
  Get-ChildItem -Path ./jenkins/jenkins_home -Recurse -Exclude README.md | Remove-Item -Force
  ```