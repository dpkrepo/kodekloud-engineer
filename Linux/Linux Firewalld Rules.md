# Task
The Nautilus system admins team recently deployed a web UI application for their backup utility running on the Nautilus backup server in Stratos Datacenter. The application is running on port 5003. They have firewalld installed on that server. The requirements that have come up include the following:

Open all incoming connection on 5003/tcp port. Zone should be public.
## Solution
Connect to Nautilus Backup Server.

```sh
thor@jump_host ~$ ssh clint@stbkp01
```

Add port 5003/tcp to public zone.
```sh
[clint@stbkp01 ~]$ sudo firewall-cmd --zone=public --add-port=5003/tcp
```
## References

[Set Up Firewalld CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)
