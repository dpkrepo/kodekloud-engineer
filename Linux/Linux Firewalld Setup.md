## Task
To secure our Nautilus infrastructure in Stratos Datacenter we have decided to install and configure firewalld on all app servers. We have Apache and Nginx services running on these apps. Nginx is running as a reverse proxy server for Apache. We might have more robust firewall settings in the future, but for now we have decided to go with the given requirements listed below:

a. Allow all incoming connections on Nginx port, i.e 80.

b. Block all incoming connections on Apache port, i.e 8080.

c. All rules must be permanent.

d. Zone should be public.

e. If Apache or Nginx services aren't running already, please make sure to start them.
## Solution

Connect to the App Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install `firewalld`.
```sh
[tony@stapp01 ~]$ sudo yum install firewalld -y
```

Start the `firewalld` service.
```sh
[tony@stapp01 ~]$ sudo systemctl enable --now firewalld
[tony@stapp01 ~]$ sudo firewall-cmd --state
running
```
Allow all incoming connections on port 80.
```sh
[tony@stapp01 ~]$ sudo firewall-cmd --add-port=80/tcp --permanent
```

Block all incoming connections on 8080 port.
```sh
[tony@stapp01 ~]$ sudo firewall-cmd --permanent --add-rich-rule='rule family=ipv4 port port="8080" protocol="tcp" reject'
```
Check if Appache and Nginx services are running.
```sh
[tony@stapp01 ~]$ systemctl status httpd &&  systemctl status nginx
```


## References

[How to configure a firewall on Linux with firewalld](https://www.redhat.com/sysadmin/firewalld-linux-firewall)

[Configuring Complex Firewall Rules with the "Rich Language" Syntax](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/configuring_complex_firewall_rules_with_the_rich-language_syntax)
