# Task
Last week the Nautilus DevOps team met with the application development team and decided to containerize several of their applications. The DevOps team wants to do some testing per the following:

Install docker-ce and docker-compose packages on App Server 1.

Start docker service.
## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install the yum-utils package (which provides the yum-config-manager utility) and set up the repository.

```sh
thor@jump_host ~$ sudo yum install -y yum-utils
```

```sh
thor@jump_host ~$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

Install docker-ce and docker-compose.
```sh
thor@jump_host ~$ sudo yum install docker-ce docker-compose-plugin -y
```
Start docker service.

```sh
thor@jump_host ~$ sudo systemctl start docker
```

## References
[Install Docker Engine on CentOS](https://docs.docker.com/engine/install/centos/)
