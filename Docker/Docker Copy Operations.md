# Task
The Nautilus DevOps team has some confidential data present on App Server 1 in Stratos Datacenter. There is a container ubuntu_latest running on the same server. We received a request to copy some of the data from the docker host to the container. Below are more details about the task:

On App Server 1 in Stratos Datacenter copy an encrypted file /tmp/nautilus.txt.gpg from docker host to ubuntu_latest container (running on same server) in /usr/src/ location. Please do not try to modify this file in any way.

## Solution 
Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Copy the encrypted file /tmp/nautilus.txt.gpg to ubuntu_latest container.

```sh
[tony@stapp01 ~]$ sudo docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/usr/src/
```

Check if the file was copied successfully.
```sh
[tony@stapp01 ~]$ docker exec ubuntu_latest  ls -ltr /usr/src
total 4
-rw-r--r-- 1 root root 105 Sep 19 19:46 nautilus.txt.gpg
```

## References

[docker cp](https://docs.docker.com/engine/reference/commandline/cp/)
