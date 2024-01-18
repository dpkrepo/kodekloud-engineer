## Task
One of the DevOps team members was working on to create a new custom docker image on App Server 1 in Stratos DC. He is done with his changes and image is saved on same server with name apps:devops. Recently a requirement has been raised by a team to use that image for testing, but the team wants to test the same on App Server 3. So we need to provide them that image on App Server 3 in Stratos DC.

a. On App Server 1 save the image apps:devops in an archive.

b. Transfer the image archive to App Server 3.

c. Load that image archive on App Server 3 with same name and tag which was used on App Server 1.

Note: Docker is already installed on both servers; however, if its service is down please make sure to start it.
## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Save the image in an archive.

```sh
[tony@stapp01 ~]$ docker save apps:devops  > apps.tar
```

Copy the archive to the App Server 3.

```sh
[tony@stapp01 ~]$ scp apps.tar banner@stapp03:/home/banner/
```

Load the image on the App Server 3.

```sh
[banner@stapp03 ~]$ docker load < apps.tar 
8e87ff28f1b5: Loading layer  80.38MB/80.38MB
e3aae516bf5c: Loading layer  47.07MB/47.07MB
Loaded image: apps:devops
```

## References

[docker save](https://docs.docker.com/engine/reference/commandline/save/)
[docker load](https://docs.docker.com/engine/reference/commandline/load/)
