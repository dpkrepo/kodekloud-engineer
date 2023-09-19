# Task

There is a static website running within a container named nautilus, this container is running on App Server 1. Suddenly, we started facing some issues with the static website on App Server 1. Look into the issue to fix the same, you can find more details below:

Container's volume /usr/local/apache2/htdocs is mapped with the host's volume /var/www/html.

The website should run on host port 8080 on App Server 1 i.e command curl http://localhost:8080/ should work on App Server 1.
## Solution
## Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Check if container is running.

```sh
[tony@stapp01 ~]$ sudo docker container list -a
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS                     PORTS               NAMES
a186716f49a5        httpd               "httpd-foreground"   4 minutes ago       Exited (0) 4 minutes ago                       nautilus
```

Start the container that is in Exited status.

```sh
[tony@stapp01 ~]$ sudo docker start a1
a1
```

Check if we can connect to localhost on port 8080 and see if static website is running.

```sh
[tony@stapp01 ~]$ curl http://localhost:8080/
Welcome to xFusionCorp Industries!
```

## References

[docker container ls](https://docs.docker.com/engine/reference/commandline/container_ls/)

[docker start](https://docs.docker.com/engine/reference/commandline/start/)
