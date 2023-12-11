## Task
The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC.

Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not hosted any code yet on these servers so you need not to worry about if Apache isn't serving any pages or not, just make sure service is up and running. Also, make sure Apache is running on port 6300 on all app servers.
## Solution
Check which one of app servers have a problem with apache.

```sh
thor@jump_host ~$ telnet stapp01 6300
Trying 172.16.238.10...
telnet: connect to address 172.16.238.10: Connection refused
thor@jump_host ~$ telnet stapp02 6300
Trying 172.16.238.11...
Connected to stapp02.
Escape character is '^]'.

thor@jump_host ~$ telnet stapp03 6300
Trying 172.16.238.12...
Connected to stapp03.
Escape character is '^]'.

```

Connect to that server.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Try to start httpd service and then check status of this service.

```sh
[tony@stapp01 ~]$ sudo systemctl status httpd
[sudo] password for tony: 
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Mon 2023-12-11 12:15:33 UTC; 14min ago
     Docs: man:httpd(8)
           man:apachectl(8)
  Process: 659 ExecStop=/bin/kill -WINCH ${MAINPID} (code=exited, status=1/FAILURE)
  Process: 658 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=exited, status=1/FAILURE)
 Main PID: 658 (code=exited, status=1/FAILURE)

Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: AH00558: h...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: (98)Addres...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: no listeni...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: AH00015: U...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.serv...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com kill[659]: kill: canno...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.serv...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: Failed to ...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: Unit httpd...
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.serv...
Hint: Some lines were ellipsized, use -l to show in full.
[tony@stapp01 ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Mon 2023-12-11 12:15:33 UTC; 14min ago
     Docs: man:httpd(8)
           man:apachectl(8)
  Process: 659 ExecStop=/bin/kill -WINCH ${MAINPID} (code=exited, status=1/FAILURE)
  Process: 658 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=exited, status=1/FAILURE)
 Main PID: 658 (code=exited, status=1/FAILURE)

Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: AH00558: httpd: Could not reliably determine the server's fully ...ssage
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: (98)Address already in use: AH00072: make_sock: could not bind t...:6300
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: no listening sockets available, shutting down
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com httpd[658]: AH00015: Unable to open logs
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: main process exited, code=exited, status=1/FAILURE
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com kill[659]: kill: cannot find process ""
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: control process exited, code=exited status=1
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: Failed to start The Apache HTTP Server.
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: Unit httpd.service entered failed state.
Dec 11 12:15:33 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service failed.
Hint: Some lines were ellipsized, use -l to show in full.
```

We can see that "(98)Address already in use: AH00072: make_sock: could not bind t...:6300" this mean that other service is using 6300 port.

Check which service is using this port.

```sh
[tony@stapp01 ~]$ sudo netstat -tulnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/init              
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      472/sshd            
tcp        0      0 127.0.0.1:6300          0.0.0.0:*               LISTEN      584/sendmail: accep 
tcp        0      0 127.0.0.11:42755        0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::111                  :::*                    LISTEN      433/rpcbind         
tcp6       0      0 :::22                   :::*                    LISTEN      472/sshd            
udp        0      0 0.0.0.0:111             0.0.0.0:*                           1/init              
udp        0      0 0.0.0.0:607             0.0.0.0:*                           433/rpcbind         
udp        0      0 127.0.0.11:42842        0.0.0.0:*                           -                   
udp6       0      0 :::111                  :::*                                433/rpcbind         
udp6       0      0 :::607                  :::*                                433/rpcbind  
```
Process with PID 584 is using 6300 port.

Stop this process.

```sh
[tony@stapp01 ~]$ sudo kill 584
```

Restart httpd service and check its status.

```sh
[tony@stapp01 ~]$ sudo systemctl restart httpd
[tony@stapp01 ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2023-12-11 12:36:53 UTC; 9s ago
     Docs: man:httpd(8)
           man:apachectl(8)
  Process: 659 ExecStop=/bin/kill -WINCH ${MAINPID} (code=exited, status=1/FAILURE)
 Main PID: 821 (httpd)
   Status: "Total requests: 0; Current requests/sec: 0; Current traffic:   0 B/sec"
   CGroup: /docker/c1b86e081b8d29f4fec96693afa7029914d199833ad06fcac9ffd461c1bcabf2/system.slice/httpd.service
           ├─821 /usr/sbin/httpd -DFOREGROUND
           ├─822 /usr/sbin/httpd -DFOREGROUND
           ├─823 /usr/sbin/httpd -DFOREGROUND
           ├─824 /usr/sbin/httpd -DFOREGROUND
           ├─825 /usr/sbin/httpd -DFOREGROUND
           └─826 /usr/sbin/httpd -DFOREGROUND

Dec 11 12:36:53 stapp01.stratos.xfusioncorp.com systemd[1]: Starting The Apache HTTP Server...
Dec 11 12:36:53 stapp01.stratos.xfusioncorp.com httpd[821]: AH00558: httpd: Could not reliably determine the server's fully ...ssage
Dec 11 12:36:53 stapp01.stratos.xfusioncorp.com systemd[1]: Started The Apache HTTP Server.
Hint: Some lines were ellipsized, use -l to show in full.
```

## References

[netstat](https://man7.org/linux/man-pages/man8/netstat.8.html)

[kill](https://man7.org/linux/man-pages/man2/kill.2.html)

[telnet](https://www.commandlinux.com/man-page/man1/telnet.1.html)
