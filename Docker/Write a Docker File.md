## Task
As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file /opt/docker/Dockerfile (please keep D capital of Dockerfile) on App server 3 in Stratos DC and configure to build an image with the following requirements:

a. Use ubuntu as the base image.

b. Install apache2 and configure it to work on 6000 port. (do not update any other Apache configuration settings like document root etc).
## Solution

Connect to the App Server 3.
```sh
thor@jump_host ~$ ssh banner@stapp03
```
Create a Dockerfile.
```sh
[banner@stapp03 ~]$ sudo vi /opt/docker/Dockerfile 
```

Write the Dockerfile that installs apache2 and changes the default port to 6000 and restarts apache2 service.
```dockerfile
FROM ubuntu
RUN apt-get update && apt-get install -y apache2
RUN sed -i 's/Listen 80/Listen 6000/g' /etc/apache2/ports.conf
RUN service apache2 restart
```
## References

[Containerize an application](https://docs.docker.com/get-started/02_our_app/)
