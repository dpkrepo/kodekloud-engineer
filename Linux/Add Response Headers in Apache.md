## Task
We are working on hardening Apache web server on all app servers. As a part of this process we want to add some of the Apache response headers for security purpose. We are testing the settings one by one on all app servers. As per details mentioned below enable these headers for Apache:


Install httpd package on App Server 1 using yum and configure it to run on 8086 port, make sure to start its service.


Create an index.html file under Apache's default document root i.e /var/www/html and add below given content in it.

Welcome to the xFusionCorp Industries!

Configure Apache to enable below mentioned headers:

X-XSS-Protection header with value 1; mode=block

X-Frame-Options header with value SAMEORIGIN

X-Content-Type-Options header with value nosniff

Note: You can test using curl on the given app server as LBR URL will not work for this task.
## Solution

Connect to the App 1 Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```
Install httpd.
```sh
[tony@stapp01 ~]$ sudo yum install httpd -y
```

Edit httpd.conf file with 8083 port and headers.
```sh
[tony@stapp01 ~]$ sudo vi /etc/httpd/conf/httpd.conf
```

```
Listen 8086
```

```
<IfModule mod_headers.c>
  <Directory />
    Header always set X-XSS-Protection "1; mode=block"
    Header always set x-Frame-Options "SAMEORIGIN"    Header always set X-Content-Type-Options "nosniff"
  </Directory>
</IfModule>
```


Create index.html file with content.
```sh
[tony@stapp01 ~]$ sudo cat /var/www/html/index.html
Welcome to the xFusionCorp Industries!
```

Start the httpd service.

```sh
[tony@stapp01 ~]$ sudo systemctl start httpd
```
## References

[HTTP Security Headers](https://www.ryadel.com/en/apache-setup-httpd-conf-file-send-http-security-headers-web-site/?utm_content=cmp-true)
