## Task
The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks. One of the tickets has been assigned to set up a nginx container on Application Server 2 in Stratos Datacenter. Please perform the task as per details mentioned below:

a. Pull nginx:stable docker image on Application Server 2.

b. Create a container named beta using the image you pulled.

c. Map host port 3002 to container port 80. Please keep the container in running state.
## Solution 

Connect to the App Server 2.

```sh
thor@jump_host ~$ ssh steve@stapp02
```

Pull the docker image.

```sh
[steve@stapp02 ~]$ sudo docker pull nginx:stable
```

Run a container and map ports.

```sh
[steve@stapp02 ~]$ docker run -d --name beta -p 3002:80 nginx:stable
```


## References

[docker run](https://docs.docker.com/engine/reference/commandline/run/)
