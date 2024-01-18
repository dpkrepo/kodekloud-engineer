## Task

The Nautilus DevOps team is testing applications containerization, which issupposed to be migrated on docker container-based environments soon. In today's stand-up meeting one of the team members has been assigned a task to create and test a docker container with certain requirements. Below are more details:

a. On App Server 3 in Stratos DC pull nginx image (preferably latest tag but others should work too).

b. Create a new container with name games from the image you just pulled.

c. Map the host volume /opt/itadmin with container volume /home. There is an sample.txt file present on same server under /tmp; copy that file to /opt/itadmin. Also please keep the container in running state.

## Solution

Connect to the App Server 3.

```sh
thor@jump_host ~$ ssh banner@stapp03
```

Pull the nginx image.

```sh
[banner@stapp03 ~]$ sudo docker pull nginx:latest
```

Run container with mounted volume.

```sh
[banner@stapp03 ~]$ sudo docker run  -d --name games -v /opt/itadmin:/home nginx:latest
```

Copy a file to /opt/itadmin directory.

```sh
[banner@stapp03 ~]$ sudo cp /tmp/sample.txt  /opt/itadmin/
```

## References

[Volumes]()https://docs.docker.com/storage/volumes/
