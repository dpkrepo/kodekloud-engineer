## Task
Our monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue, as its Apache service is not reachable on port 8084 (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.

Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

Once fixed, you can test the same using command curl http://stapp01:8084 command from jump host.
## Solution

Check telnet connection to tha App Server 1.
```sh
thor@jump_host ~$ telnet stapp01 8084
Trying 172.16.238.10...
telnet: connect to address 172.16.238.10: No route to host
```

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stpp01
```

Check if apache is running. We can see that somthing else is running on port 8084.
```sh
[tony@stapp01 ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor pre
set: disabled)
   Active: failed (Result: exit-code) since Tue 2023-10-24 09:55:29
 UTC; 7min ago
     Docs: man:httpd.service(8)
  Process: 702 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=e
xited, status=1/FAILURE)
 Main PID: 702 (code=exited, status=1/FAILURE)
   Status: "Reading configuration..."

Oct 24 09:55:29 stapp01.stratos.xfusioncorp.com httpd[702]: (98)Address alread
y in use: AH00072: make_sock: could not bind to address 0.0.0.0:8084
```
Check what is running on port 8084.

```sh
[tony@stapp01 ~]$ sudo netstat -tulnp
[sudo] password for tony: 
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.1:8084          0.0.0.0:*               LISTEN      639/sendmail: accep 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      485/sshd            
tcp        0      0 127.0.0.11:45017        0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      485/sshd            
udp        0      0 127.0.0.11:40552        0.0.0.0:*   
```

Kill the process with PID that is using 8084 port.

```sh
[tony@stapp01 ~]$ sudo kill 639
```

Restart apache service and check status.

```sh
[tony@stapp01 ~]$ sudo systemctl restart httpd
[tony@stapp01 ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disa
bled)
   Active: active (running) since Tue 2023-10-24 10:11:51 UTC; 36s ago
     Docs: man:httpd.service(8)
 Main PID: 934 (httpd)
   Status: "Running, listening on: port 8084"
    Tasks: 213 (limit: 1340692)
   Memory: 19.3M
   CGroup: /docker/10a423a1815314320dcdf5b3258f30f387b9acc865bc3da601bdbf3b6e4263fb/sys
tem.slice/httpd.service
           ├─934 /usr/sbin/httpd -DFOREGROUND
           ├─962 /usr/sbin/httpd -DFOREGROUND
           ├─963 /usr/sbin/httpd -DFOREGROUND
           ├─964 /usr/sbin/httpd -DFOREGROUND
           └─965 /usr/sbin/httpd -DFOREGROUND
```

Try telnet from jump host.

```sh
thor@jump_host ~$ telnet stapp01 8084
Trying 172.16.238.10...
telnet: connect to address 172.16.238.10: No route to host
```

There is still no connection.

On the App Service 1 validate apache configuraion files. And we can see that we need to set ServerName.
```sh
[tony@stapp01 ~]$ httpd -t
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using stapp01.stratos.xfusioncorp.com. Set the 'ServerName' directive globally to suppress this message
Syntax OK
```

Open apache config file and add ServerName.

```sh
[tony@stapp01 ~]$ sudo vi /etc/httpd/conf/httpd.conf 
```
```
ServerName 172.16.238.10:8084
```

Restart apache service.

```sh
[tony@stapp01 ~]$ sudo systemctl restart httpd
```

Check telnet from Jump Host. There is still no connection.

```sh
thor@jump_host ~$ telnet stapp01 8084
Trying 172.16.238.10...
telnet: connect to address 172.16.238.10: No route to host
```

Check iptables rules on App Server 1.

```sh
[tony@stapp01 ~]$ sudo iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere            
ACCEPT     all  --  anywhere             anywhere            
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
# Warning: iptables-legacy tables present, use iptables-legacy to see them
```

Delete all rules. 

```sh
[tony@stapp01 ~]$ sudo iptables -F
```

Now telnet is working.

```sh
thor@jump_host ~$ telnet stapp01 8084
Trying 172.16.238.10...
Connected to stapp01.
```
## References

[telnet](https://www.commandlinux.com/man-page/man1/telnet.1.html)

[netstat](https://linux.die.net/man/8/netstat)

[Configure Iptables](https://upcloud.com/resources/tutorials/configure-iptables-centos)
