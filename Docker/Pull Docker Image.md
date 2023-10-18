## Task
Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features. As per details shared with DevOps team, we need to accomplish the following task:

a. Pull busybox:musl image on App Server 3 in Stratos DC and re-tag (create new tag) this image as busybox:media.
## Solution
Connect to the App Server 3.
```sh
thor@jump_host ~$ ssh banner@stapp03
```
Pull the busybox:musl image.
```sh
[banner@stapp03 ~]$ sudo docker pull busybox:musl
musl: Pulling from library/busybox
d2dce026a06e: Pull complete 
Digest: sha256:f553b7484625f0c73bfa3888e013e70e99ec6ae1c424ee0e8a85052bd135a28a
Status: Downloaded newer image for busybox:musl
docker.io/library/busybox:musl
```
Create a new tag for the busybox image.
```sh
[banner@stapp03 ~]$ sudo docker tag busybox:musl busybox:media
```
List docker images and tags.
```sh
[banner@stapp03 ~]$ sudo docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
busybox             media               46425a867adf        3 months ago        1.41MB
busybox             musl                46425a867adf        3 months ago        1.41MB
```


## References

[docker pull](https://docs.docker.com/engine/reference/commandline/pull/)

[docker tag](https://docs.docker.com/engine/reference/commandline/tag/)
