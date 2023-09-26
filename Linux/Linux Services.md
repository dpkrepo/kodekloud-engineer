# Task 
As per details shared by the development team, the new application release has some dependencies on the back end. There are some packages/services that need to be installed on all app servers under Stratos Datacenter. As per requirements please perform the following steps:

a. Install nscd package on all the application servers.

b. Once installed, make sure it is enabled to start during boot.
## Solution

Connect to the Application Server.

```sh
thor@jump_host ~$ ssh tony@stapp01
```
Install the `nscd` package.
```sh
[tony@stapp01 ~]$ sudo yum install -y nscd
```

Start and enable `nscd` service.
```sh
[tony@stapp01 ~]$ sudo systemctl status nscd
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor pres
et: disabled)
   Active: inactive (dead)

Sep 26 11:36:27 stapp01.stratos.xfusioncorp.com systemd[1]: 
nscd.service: Collecting.
[tony@stapp01 ~]$ sudo systemctl start nscd
[tony@stapp01 ~]$ sudo systemctl enable nscd
Created symlink /etc/systemd/system/multi-user.target.wants/nscd.service → /usr/lib/systemd/system/nscd.service.
Created symlink /etc/systemd/system/sockets.target.wants/nscd.socket → /usr/lib/systemd/system/nscd.socket.
[tony@stapp01 ~]$ sudo systemctl status nscd
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor prese
t: disabled)
   Active: active (running) since Tue 2023-09-26 11:36:44 UTC; 12s 
ago
 Main PID: 842 (nscd)
    Tasks: 11 (limit: 1340692)
   Memory: 2.3M
   CGroup: /docker/ac6b58597576c39c0d7136e480ec7b69577888923a96d7214a4fa300f5f
4d50e/system.slice/nscd.service
           └─842 /usr/sbin/nscd
```
## References

[Enabling and Disabling Services](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units#enabling-and-disabling-services)
