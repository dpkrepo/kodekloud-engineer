## Task
There is a static website running in Stratos Datacenter. They have already configured the app servers and code is already deployed there. To make it work properly, they need to configure LBR server. There are number of options for that, but team has decided to go with HAproxy. FYI, apache is running on port 3000 on all app servers. Complete this task as per below details.

a. Install and configure HAproxy on LBR server using yum only and make sure all app servers are added to HAproxy load balancer. HAproxy must serve on default http port (Note: Please do not remove stats socket /var/lib/haproxy/stats entry from haproxy default config.).

b. Once done, you can access the website using StaticApp button on the top bar.
## Solution
Connect to LBR server.
```sh
thor@jump_host ~$ ssh loki@stlb01
```
Install HAProxy.

```sh
[loki@stlb01 ~]$ sudo yum install haproxy -y
```

Edit `/etc/haproxy/haproxy.cfg` file.
```sh
[loki@stlb01 ~]$ sudo vi /etc/haproxy/haproxy.cfg
```
Modify this file with below lines.
```
frontend main
    bind *:80
.
.backend app
    balance     roundrobin
    server  stapp01 172.16.238.10:3000 check
    server  stapp02 172.16.238.11:3000 check
    server  stapp03 172.16.238.12:3000 check
.

```

Validate haproxy configuration
```sh
[loki@stlb01 ~]$ sudo haproxy -f /etc/haproxy/haproxy.cfg
```
Enable and start haproxy service.
```sh
[loki@stlb01 ~]$ sudo systemctl enable haproxy && sudo systemctl start haproxy
```
## References

[HAProxy Configuration Basics: Load Balance Your Servers](https://www.haproxy.com/blog/haproxy-configuration-basics-load-balance-your-servers)
