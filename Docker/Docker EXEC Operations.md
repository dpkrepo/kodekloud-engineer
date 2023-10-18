## Task
One of the Nautilus DevOps team members was working to configure services on a kkloud container that is running on App Server 2 in Stratos Datacenter. Due to some personal work he is on PTO for the rest of the week, but we need to finish his pending work ASAP. Please complete the remaining work as per details given below:

a. Install apache2 in kkloud container using apt that is running on App Server 2 in Stratos Datacenter.

b. Configure Apache to listen on port 6300 instead of default http port. Do not bind it to listen on specific IP or hostname only, i.e it should listen on localhost, 127.0.0.1, container ip, etc.

c. Make sure Apache service is up and running inside the container. Keep the container in running state at the end.
## Solution

Connect to the App Server 2.
```sh
thor@jump_host ~$ ssh steve@stapp02
```
Install apache2 on the kkloud container.
```sh
[steve@stapp02 ~]$ sudo docker exec -it kkloud sh -c "apt install apache2"
```
Change Apache listen port to 6300 and restart apache2 service.
```sh
[steve@stapp02 ~]$ sudo docker exec -it kkloud /bin/bash -c "sed -i 's/Listen 80/Listen 6300/g' /etc/apache2/ports.conf && service apache2 restart"
```

## References

[docker exec](https://docs.docker.com/engine/reference/commandline/exec/)
