# Task
The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

a. Install cronie package on all Nautilus app servers and start crond service.

b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.
## Solution
Connect to the Application Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```
Install the `cronie` package.
```sh
[tony@stapp01 ~]$ sudo yum install cronie -y
```

Start `crond` service.

```sh
[tony@stapp01 ~]$ sudo systemctl start crond
```

Check status of the crond service.

```sh
[tony@stapp01 ~]$ sudo systemctl status crond
● crond.service - Command Scheduler
   Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor pres
et: enabled)
   Active: active (running) since Fri 2023-09-22 11:24:50 UTC; 13mi
n ago
 Main PID: 441 (crond)
    Tasks: 1 (limit: 1340692)
   Memory: 1.1M
   CGroup: /docker/f69034b1fb44921cafcf68a3469170924a9459aa0852bb48ed4db34e13c
6c704/system.slice/crond.service
           └─441 /usr/sbin/crond -n

Sep 22 11:24:50 stapp01.stratos.xfusioncorp.com systemd[1]: Started Command Sc
heduler.
Sep 22 11:24:51 stapp01.stratos.xfusioncorp.com systemd[441]: 
crond.service: Executing: /usr/sbin/crond -n
Sep 22 11:24:51 stapp01.stratos.xfusioncorp.com crond[441]: (CRON) STARTUP (1.
5.2)
Sep 22 11:24:51 stapp01.stratos.xfusioncorp.com crond[441]: (CRON) INFO (Syslo
g will be used instead of sendmail.)
Sep 22 11:24:51 stapp01.stratos.xfusioncorp.com crond[441]: (CRON) INFO (RANDO
M_DELAY will be scaled with factor 98% if used.)
Sep 22 11:24:51 stapp01.stratos.xfusioncorp.com crond[441]: (CRON) INFO (runni
ng with inotify support)
Sep 22 11:37:47 stapp01.stratos.xfusioncorp.com systemd[1]: 
crond.service: Trying to enqueue job crond.service/start/replace
Sep 22 11:37:47 stapp01.stratos.xfusioncorp.com systemd[1]:
```

Create a crontab file.
```sh
[tony@stapp01 ~]$ sudo crontab -e
```
Job will run every 5 minutes.
```
*/5 * * * * echo hello > /tmp/cron_text
```

Verify the Cron Job.

```sh
[tony@stapp01 ~]$ sudo crontab -l -u root
*/5 * * * * echo hello > /tmp/cron_text
```
## References

[Cron Jobs](https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/)
