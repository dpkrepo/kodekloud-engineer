# Task
After doing some security audits of servers, xFusionCorp Industries security team has implemented some new security policies. One of them is to disable direct root login through SSH.

Disable direct SSH root login on all app servers in Stratos Datacenter.

## Solution

Connect to the App Server1.
```sh
thor@jump_host ~$ ssh tony@stapp01
```

Edit `/etc/ssh/sshd_config` file and change `PermitRootLogin yes` to `PermitRootLogin no`. Save the file.
```sh
[tony@stapp01 ~]$ sudo vi /etc/ssh/sshd_config 
```

Restart sshd service.
```sh
[tony@stapp01 ~]$ sudo systemctl restart sshd
```
## Reference

[Disable Root Login in Linux](https://www.tecmint.com/disable-root-login-in-linux/)
