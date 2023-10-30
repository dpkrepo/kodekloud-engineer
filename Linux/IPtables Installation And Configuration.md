## Task
We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e 6400 is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:

1. Install iptables and all its dependencies on each app host.

2. Block incoming port 6400 on all apps for everyone except for LBR host.

3. Make sure the rules remain, even after system reboot.
## Solution
Connect to the App Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install the iptables package.

```sh
[tony@stapp01 ~]$ sudo yum install iptables-services -y
```


Start the iptables service.

```sh
[tony@stapp01 ~]$ sudo systemctl start iptables
[tony@stapp01 ~]$ sudo systemctl status iptables
● iptables.service - IPv4 firewall with iptables
   Loaded: loaded (/usr/lib/systemd/system/iptables.service; disabled; vendor>
   Active: active (exited) since Thu 2023-10-26 08:35:53 UTC; 5s ago
  Process: 1752 ExecStart=/usr/libexec/iptables/iptables.init start (code=exi>
 Main PID: 1752 (code=exited, status=0/SUCCESS)
```

And enable it so it will start after system reboot.

```sh
[tony@stapp01 ~]$ sudo systemctl enable iptables
Created symlink /etc/systemd/system/multi-user.target.wants/iptables.service → /usr/lib/systemd/system/iptables.service.
```

Add rules that block port 6400 except for LBR host.

```sh
[tony@stapp01 ~]$ sudo iptables -A INPUT -p tcp --destination-port 6400 -s 172.16.238.14 -j ACCEPT
[tony@stapp01 ~]$ sudo iptables -A INPUT -p tcp --destination-port 6400 -j DROP
```

Add rule that block icmp protocol.
```sh
[tony@stapp01 ~]$ sudo iptables -R INPUT 5 -p icmp -j REJECT
```

Save rules to remain them after reboot.

```sh
[tony@stapp01 ~]$ sudo sh -c 'iptables-save > /etc/sysconfig/iptables'
```

Restart iptables service.

```sh
[tony@stapp01 ~]$ sudo systemctl restart iptables
```

## References


[How to Install Iptables on CentOS 7](https://linuxize.com/post/how-to-install-iptables-on-centos-7/)

[Linux Block Port With IPtables Command](https://www.cyberciti.biz/faq/iptables-block-port/)

[Saving Iptables Firewall Rules Permanently](https://www.thomas-krenn.com/en/wiki/Saving_Iptables_Firewall_Rules_Permanently)
