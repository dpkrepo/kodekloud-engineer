## Task 

xFusionCorp Industries uses some monitoring tools to check the status of every service, application, etc running on the systems. Recently, the monitoring system identified that Apache service is not running on some of the Nautilus Application Servers in Stratos Datacenter.

1. Identify the faulty Nautilus Application Server and fix the issue. Also, make sure Apache service is up and running on all Nautilus Application Servers. Do not try to stop any kind of firewall that is already running.

2. Apache is running on 8087 port on all Nautilus Application Servers and its document root must be /var/www/html on all app servers.

3. Finally you can test from jump host using curl command to access Apache on all app servers and it should be reachable and you should get some static page. E.g. curl http://172.16.238.10:8087/.
## Solution

Login to all application servers.
```sh
thor@jump_host ~$ ssh tony@stapp01
```
Check status of the httpd service.
```sh
thor@jump_host ~$ sudo systemctl status httpd
```
Try to start it.

```sh
thor@jump_host ~$ sudo systemctl start httpd
```

If status is failed open `/etc/httpd/conf/httpd.conf` file and find typos in it. eg. addiotional ", characters at the end of path etc.
```sh
thor@jump_host ~$ sudo vi /etc/httpd/conf/httpd.conf
```
## References

[How To Troubleshoot Common Apache Errors](https://www.digitalocean.com/community/tutorials/how-to-troubleshoot-common-apache-errors)
