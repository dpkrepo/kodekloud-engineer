## Task 
Some users of the monitoring app have reported issues with xFusionCorp Industries mail server. They have a mail server in Stork DC where they are using postfix mail transfer agent. Postfix service seems to fail. Try to identify the root cause and fix it.
## Solution
Connect to the Mail Server.
```sh
thor@jump_host ~$ ssh groot@stmail01
```

Check status of the postfix service.

```sh
[groot@stmail01 ~]$ sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
   Loaded: loaded (/usr/lib/systemd/system/postfix.service; disabled; vendor p
reset: disabled)
   Active: inactive (dead)

Oct 09 08:21:05 stmail01.stratos.xfusioncorp.com systemd[1]: 
postfix.service: Collecting.
```

Try to start the postfix service.

```sh
[groot@stmail01 ~]$ sudo systemctl start postfix
Job for postfix.service failed because the control process exited with error code.
See "systemctl status postfix.service" and "journalctl -xe" for details.
```

Check status of the postix service.

```sh
[groot@stmail01 ~]$ sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
   Loaded: loaded (/usr/lib/systemd/system/postfix.service; disabled; vendor p
reset: disabled)
   Active: failed (Result: exit-code) since Mon 2023-10-09 08:21:20
 UTC; 29s ago
  Process: 793 ExecStart=/usr/sbin/postfix start (code=exited, status=
1/FAILURE)
  Process: 792 ExecStartPre=/usr/libexec/postfix/chroot-update (code=exited, s
tatus=0/SUCCESS)
  Process: 776 ExecStartPre=/usr/libexec/postfix/aliasesdb (code=exite
d, status=75)
  Process: 762 ExecStartPre=/usr/sbin/restorecon -R /var/spool/postfix/pid/mas
ter.pid (code=exited, status=0/SUCCESS)

Oct 09 08:21:19 stmail01.stratos.xfusioncorp.com postfix[793]: 
warning: /etc/postfix/main.cf, line 135: overriding earlier entry: in
et_interfaces=all
Oct 09 08:21:19 stmail01.stratos.xfusioncorp.com postfix[793]: 
fatal: parameter inet_interfaces: no local interface found for ::1
```

We can see that problem is with `parameter inet_interfaces: no lcal interface found for ::1`.

Open `/etc/postfix/main.cf` file.

```sh
[groot@stmail01 ~]$ sudo vi /etc/postfix/main.cf
```

We see that inet_interfaces are uncommented, so we need to comment it out.

```
inet_interfaces = all
#inet_interfaces = $myhostname
#inet_interfaces = $myhostname, localhost
inet_interfaces = localhost
```

```
inet_interfaces = all
#inet_interfaces = $myhostname
#inet_interfaces = $myhostname, localhost
#inet_interfaces = localhost
```

Now start postfix service.

```sh
[groot@stmail01 ~]$ sudo systemctl start postfix
```

Check status of the postfix service.

```sh
[groot@stmail01 ~]$ sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
   Loaded: loaded (/usr/lib/systemd/system/postfix.service; disabled; vendor p
reset: disabled)
   Active: active (running) since Mon 2023-10-09 08:23:57 UTC; 3s a
go
```
Postfix service is active.
## References

[Postfix Debugging Howto](https://www.postfix.org/DEBUG_README.html)
