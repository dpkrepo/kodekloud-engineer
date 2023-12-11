## Task
We have a requirement where we want to password protect a directory in the Apache web server document root. We want to password protect http://<website-url>:<apache_port>/protected URL as per the following requirements (you can use any website-url for it like localhost since there are no such specific requirements as of now). Setup the same on App server 1 as per below mentioned requirements:

a. We want to use basic authentication.

b. We do not want to use htpasswd file based authentication. Instead, we want to use PAM authentication, i.e Basic Auth + PAM so that we can authenticate with a Linux user.

c. We already have a user ravi with password TmPcZjtRQx which you need to provide access to.

d. You can test the same using a curl command from jump host curl http://<website-url>:<apache_port>/protected.
## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install pwauth.

```sh
[tony@stapp01 ~]$ sudo yum --enablerepo=epel -y install mod_authnz_external pwauth
```

Add at the end of the /etc/httpd/conf.d/authnz_external.conf file below lines.

```
<Directory /var/www/html/protected>
    AuthType Basic
    AuthName "PAM Authentication"
    AuthBasicProvider external
    AuthExternal pwauth
    require valid-user
</Directory>
```

Start apache server.

```sh
[tony@stapp01 ~]$ sudo systemctl start httpd
```




## References

[Basic Auth + PAM](https://www.server-world.info/en/note?os=CentOS_7&p=httpd&f=10)
