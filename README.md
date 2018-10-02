# Dockerized-NextCloud-MariaDB-LetsEncrypt
A NextCloud server with MariaDB as database. This server is behind a reverse proxy (Nginx), enabled with LetsEncrypt service for SSL encryption.

Special thanks to the following github users:
   - https://github.com/nextcloud/docker
   - https://github.com/jwilder/nginx-proxy
   - https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion

# Follow these steps in order to create your NextCloud service

1. First of all you have to clone this repository on your server.
```bash
    -$ mkdir -p ~/nextcloud
    -$ cd ~/nextcloud
    -$ git clone https://github.com/gregkoul/Dockerized-NextCloud-MariaDB-LetsEncrypt.git
```
2. Create a directory for your storage with owner www-data.
```bash
    -$ mkdir -p /media/storage/nextcloud
    -$ chown -R www-data:www-data /media/storage/nextcloud
```
3. Next edit the db.env file and modify your environment variables
```bash
    -$ cd ~/nextcloud/Dockerized-NextCloud-MariaDB-LetsEncrypt
    -$ vi db.env
```
4. Next edit the web.env file and modify your environment variables
```bash
    -$ vi web.env
```
5. Before you start up the dockers, you need to create only once a new virtual seperate network.
```bash
    -$ docker network create nginx-proxy
```
6. Now you have to spin up everything.
```bash
    -$ docker-compose up -d
```
7. Stay back and relax for a while! The docker-compose will spin up all the dockers one by one. Let about 2-3 minutes in order LetsEncrypt service create and pull the certs for your new domain. Be patient.

8. I hope NOW to have access your DOMAIN. You have to finalize the initial setup for NextCloud service.

9. During the initial setup, select the desired database type (eg. MariaDB). Fill the hostname field for the database server, with the database-container name. (eg. db). For the db credentials, use the environmental variables found in the db.env file.

# Follow these steps in order to update your NextCloud service

1. First of all you have to stop and remove the old dockers. 
```bash
    -$ cd ~/nextcloud/Dockerized-NextCloud-MariaDB-LetsEncrypt
    -$ docker-compose down
```
2. Now To update all of your containers with the latest updates by using the following command.
```bash
    -$ docker-compose pull
```
3. Now you have to spin up everything.
```bash
    -$ docker-compose up -d
```
