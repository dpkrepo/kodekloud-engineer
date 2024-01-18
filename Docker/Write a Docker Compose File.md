## Task

The Nautilus application development team shared static website content that needs to be hosted on the httpd web server using a containerised platform. The team has shared details with the DevOps team, and we need to set up an environment according to those guidelines. Below are the details:

a. On App Server 1 in Stratos DC create a container named httpd using a docker compose file /opt/docker/docker-compose.yml (please use the exact name for file).

b. Use httpd (preferably latest tag) image for container and make sure container is named as httpd; you can use any name for service.

c. Map 80 number port of container with port 8083 of docker host.

d. Map container's /usr/local/apache2/htdocs volume with /opt/finance volume of docker host which is already there. (please do not modify any data within these locations).
## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Write a docker compose file.

```yml
version: "3.8"

services:
  httpd:
    container_name: httpd
    image: httpd:latest
    ports:
      - "8083:80"
    volumes:
      - /opt/finance:/usr/local/apache2/htdocs
```

Run the docker compose up command.

```sh
[tony@stapp01 docker]$ docker compose up
```


## References

[docker compose](https://docs.docker.com/engine/reference/commandline/compose/)
