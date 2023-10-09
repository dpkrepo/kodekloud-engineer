## Task
xFusionCorp Industries has an application running on Nautlitus infrastructure in Stratos Datacenter. The monitoring tool recognised that there is an issue with the haproxy service on LBR server. That needs to fixed to make the application work properly.

Troubleshoot and fix the issue, and make sure haproxy service is running on Nautilus LBR server. Once fixed, make sure you are able to access the website using StaticApp button on the top bar.
## Solution

Connect to the LBR Server.
```sh
thor@jump_host ~$ ssh loki@stlb01
```

Check status of the haproxy service.

```sh
[loki@stlb01 ~]$ sudo systemctl status haproxy
● haproxy.service - HAProxy Load Balancer
   Loaded: loaded (/usr/lib/systemd/system/haproxy.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
```

Try to start the haproxy service and check if it started.

```sh
[loki@stlb01 ~]$ sudo systemctl start haproxy
[loki@stlb01 ~]$ sudo systemctl status haproxy -l
● haproxy.service - HAProxy Load Balancer
   Loaded: loaded (/usr/lib/systemd/system/haproxy.service; disabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Mon 2023-10-09 09:43:26 UTC; 2s ago
```

Validate the configuration file.

```sh
[loki@stlb01 ~]$ sudo haproxy -f /etc/haproxy/haproxy.cfg 
[ALERT] 281/094538 (385) : parsing [/etc/haproxy/haproxy.cfg:50] : balance only supports 'roundrobin', 'static-rr', 'leastconn', 'source', 'uri', 'url_param', 'hdr(name)' and 'rdp-cookie(name)' options.
[ALERT] 281/094538 (385) : parsing [/etc/haproxy/haproxy.cfg:57] : balance only supports 'roundrobin', 'static-rr', 'leastconn', 'source', 'uri', 'url_param', 'hdr(name)' and 'rdp-cookie(name)' options.
[ALERT] 281/094538 (385) : Error(s) found in configuration file : /etc/haproxy/haproxy.cfg
[ALERT] 281/094538 (385) : Fatal errors found in configuration.
```

Open the `/etc/haproxy/haproxy.cfg` file.
```sh
[loki@stlb01 ~]$ sudo vi /etc/haproxy/haproxy.cfg
```
Ensure that the correct value is provided for balace.
```
balance     roundrobin
```

Save file and again validate.
And if the file is validated without error start the haproxy service.
```sh
[loki@stlb01 ~]$ sudo haproxy -f /etc/haproxy/haproxy.cfg 
[loki@stlb01 ~]$ sudo systemctl start haproxy
[loki@stlb01 ~]$ sudo systemctl status haproxy
● haproxy.service - HAProxy Load Balancer
   Loaded: loaded (/usr/lib/systemd/system/haproxy.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2023-10-09 09:49:01 UTC; 5s ago
```
## References

[How To Troubleshoot Common HAProxy Errors](https://www.digitalocean.com/community/tutorials/how-to-troubleshoot-common-haproxy-errors)
