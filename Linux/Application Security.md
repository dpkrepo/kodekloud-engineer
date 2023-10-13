## Task 
We have a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server. Apache and Nginx ports are 8083 and 8094, respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:

We want to open all incoming connections to Nginx's port and block all incoming connections to Apache's port. Also make sure rules are permanent.
## Solution
Connect to the Backup Server.
```sh
thor@jump_host ~$ ssh clint@stbkp01
```
Check if iptables service is running.
```sh
[clint@stbkp01 ~]$ sudo systemctl status iptables
● iptables.service - IPv4 firewall with iptables
   Loaded: loaded (/usr/lib/systemd/system/iptables.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
```

Start the iptables service.

```sh
[clint@stbkp01 ~]$ sudo systemctl start iptables
```

Allow connection on port 8094 for new and established connections.
```sh
[clint@stbkp01 ~]$ sudo iptables -A INPUT -p tcp --dport 8094 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```

Reject all new connections on port 8083.

```sh
[clint@stbkp01 ~]$ sudo iptables -A INPUT -p tcp --dport 8083 -m conntrack --ctstate NEW -j REJECT
```

Check iptables rules.

```sh
[clint@stbkp01 ~]$ sudo iptables -L --line-numbers
Chain INPUT (policy ACCEPT)
num  target     prot opt source               destination         
1    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:8092 ctstate NEW,ESTABLISHED
2    REJECT     tcp  --  anywhere             anywhere             tcp dpt:synchronet-db ctstate NEW reject-with icmp-port-unreachable

Chain FORWARD (policy ACCEPT)
num  target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
num  target     prot opt source               destination 
```

Save the rules so they are persistent and present after system reboot.
```sh
[clint@stbkp01 ~]$ sudo service iptables save
iptables: Saving firewall rules to /etc/sysconfig/iptables:[  OK  ]
```
## References

[Open/Close ports on Iptables](https://docs.e2enetworks.com/security/firewall/iptables.html)

[IPTables and Connection Tracking](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-security_guide-firewalls-iptables_and_connection_tracking)
