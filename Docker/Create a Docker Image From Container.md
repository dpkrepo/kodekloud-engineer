## Task
One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:

a. Create an image demo:xfusion on Application Server 2 from a container ubuntu_latest that is running on same server.
## Solution

Connect to the App Service 2.
```sh
thor@jump_host ~$ ssh steve@stapp02
```
Create an image demo:xfusion from a container ubuntu_latest.
```sh
[steve@stapp02 ~]$ sudo docker container commit ubuntu_latest demo:xfusion
```
List images.
```sh
[steve@stapp02 ~]$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
demo                xfusion             1d62a8edb85c        51 seconds ago      122MB
ubuntu              latest              e4c58958181a        13 days ago         77.8MB
```
## References

[How to Create Docker Image From a Container?](https://kodekloud.com/blog/docker-create-image-from-container/)
