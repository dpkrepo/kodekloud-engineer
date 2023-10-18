## Task
One of the Nautilus project developers need access to run docker commands on App Server 1. This user is already created on the server. Accomplish this task as per details given below:

User ammar is not able to run docker commands on App Server 1 in Stratos DC, make the required changes so that this user can run docker commands without sudo.
## Solution

Connect to the App Server 1.
```sh
thor@jump_host ~$ ssh tony@stapp01
```
Add user ammar to docker group.
```sh
[tony@stapp01 ~]$ sudo usermod -aG docker ammar
```
Activate changes to the group.
```sh
[tony@stapp01 ~]$ sudo newgrp docker
```
## References

[Manage Docker as a non-root user](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)
