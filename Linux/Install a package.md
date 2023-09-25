# Task
As per new application requirements shared by the Nautilus project development team, serveral new packages need to be installed on all app servers in Stratos Datacenter. Most of them are completed except for vsftpd.

Therefore, install the vsftpd package on all app-servers.
## Solution
Connect to the Application Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install the `vsftpd` package.

```sh
[tony@stapp01 ~]$ sudo yum install -y vsftpd
```
## References

[yum](https://man7.org/linux/man-pages/man8/yum.8.html)
