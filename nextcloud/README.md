# [<](../README.md) | Nextcloud
## Run nextcloud environment
- start service from docker-compose.yml file:
  ```Bash
  docker-compose -f nextcloud/docker-compose.yml up -d
  ```
- Docker Container should running
  ```Bash
  docker ps
  ```

## Nextcloud setup
- Visit localhost:[your-port]
- Nextcloud admin:
  - Username: admin
  - Password: admin
- Database: postgres
  - Database_User: postgres
  - Database_Password: your-secret-password
  - Database_Name: nextcloud_db
  - Database_Host: Service-name-from-yml:[db_port]
> **Note**: The nextcloud database should be created via the setup menu and not via the yml file. Otherwise you may experience problems.

## Shutdown nextcloud service
```Bash
docker-compose -f nextcloud/docker-compose.yml down
docker container rm nextcloud nextcloud_db # remove nextcloud instances
docker volume rm -f nextcloud_postgres nextcloud_html # remove persisted data
```
## Control nextcloud as systemd service
- Feel free to use nextcloud-example.service to create your custom nextcloud.service
- Copy your service file to /etc/systemd/system/nextcloud.service
- Control commands:
  ```Bash
  sudo systemctl daemon-reload
  sudo systemctl enable nextcloud.service
  sudo systemctl start nextcloud
  sudo systemctl status nextcloud
  ```

## Backup and Restore
- Backup
  - nextcloud:
    ```Bash
    docker run --rm --volumes-from nextcloud_html -v $(pwd):/backup ubuntu tar cvf /backup/nextcloud_backup-`%Y-%m-%d"_"%H:%M:%S`.tar /nextcloud
    ```
  - postgres_db:
    ```Bash
    docker exec -t nextcloud_postgres pg_dumpall -c -U postgres > dump_`%Y-%m-%d"_"%H:%M:%S`.sql
    ```
- Restore
  - nextcloud:
    ```Bash
    docker run --rm --volumes-from nextcloud_html -v $(pwd):/backup ubuntu bash -c "cd /nextcloud_data && tar xvf /backup/nextcloud_backup-[date].tar --strip 1"
    ```
  - postgres_db:
    ```Bash
    cat dump_file.sql | docker exec -i nextcloud_db psql -U postgres
    ```