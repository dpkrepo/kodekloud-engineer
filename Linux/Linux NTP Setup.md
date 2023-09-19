# Task
The system admin team of xFusionCorp Industries has noticed an issue with some servers in Stratos Datacenter where some of the servers are not in sync w.r.t time. Because of this, several application functionalities have been impacted. To fix this issue the team has started using common/standard NTP servers. They are finished with most of the servers except App Server 1. Therefore, perform the following tasks on this server:

1. Install and configure NTP server on App Server 1.

2. Add NTP server 3.pool.ntp.org in NTP configuration on App Server 1.

3. Please do not try to start/restart/stop ntp service, as we already have a restart for this service scheduled for tonight and we don't want these changes to be applied right now.
## Solution

Connect to App Server 1.
```sh
thor@jump_host ~$ ssh tony@stapp01
```
Install NTP.

```sh
[tony@stapp01 ~]$  sudo yum install ntp
```

Open configuration file of NTP.

```sh
[tony@stapp01 ~]$ sudo vi /etc/ntp.conf
```

Add `server 3.pool.ntp.org` to the /etc/ntp.conf file.
## References
[Install and Configure NTP on CentOS](https://www.cyberithub.com/how-to-install-configure-ntp-server-in-rhel-centos-7-8/)
