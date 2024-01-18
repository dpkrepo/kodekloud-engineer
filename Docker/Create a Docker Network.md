## Task
The Nautilus DevOps team needs to set up several docker environments for different applications. One of the team members has been assigned a ticket where he has been asked to create some docker networks to be used later. Complete the task based on the following ticket description:

a. Create a docker network named as ecommerce on App Server 1 in Stratos DC.

b. Configure it to use bridge drivers.

c. Set it to use subnet 10.10.1.0/24 and iprange 10.10.1.1/24.
## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Create a network.

```sh
[tony@stapp01 ~]$ sudo docker  network create --driver=bridge --subnet=10.10.1.0/24 --ip-range=10.10.1.1/24 ecommerce
04ec795810e7255a3c1449ad13b7564d58e2fe66b79fc60ae393b9a9c32976d3
```

## References

[docker network create](https://docs.docker.com/engine/reference/commandline/network_create/)
