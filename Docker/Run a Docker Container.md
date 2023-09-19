# Task
Nautilus DevOps team is testing some applications deployment on some of the application servers. They need to deploy a nginx container on Application Server 3. Please complete the task as per details given below:

On Application Server 3 create a container named nginx_3 using image nginx with alpine tag and make sure container is in running state.
## Solution
Connect to the App Server 3.

```sh
thor@jump_host ~$ ssh banner@stapp03
```

Run a docker container.

```sh
[banner@stapp03 ~]$ sudo docker run --name nginx_3 nginx:alpine
```

Check if the container is running.

```sh
[banner@stapp03 ~]$ sudo docker container list 
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
e5e9e3096f5b        nginx:alpine        "/docker-entrypoint.…"   19 seconds ago      Up 16 seconds       80/tcp              nginx_3
```

## References

[docker run](https://docs.docker.com/engine/reference/commandline/run/)
