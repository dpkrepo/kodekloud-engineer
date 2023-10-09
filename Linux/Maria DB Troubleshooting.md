## Task
There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.

Look into the issue and fix the same.
## Solution
```sh
thor@jump_host ~$ ssh peter@stdb01
```
Try to start 
```sh
[peter@stdb01 ~]$ sudo systemctl start mariadb
Job for mariadb.service failed because the control process exited with error code.
See "systemctl status mariadb.service" and "journalctl -xe" for details.
```

Run `journalctl -xe` command and look for the errors.

We can notice that MariaDB can't be initialized and it is related to the folder `/var/lib/mysql`.
```
Oct 09 10:57:58 stdb01.stratos.xfusioncorp.com mysql-prepare-db-dir[1027]: Database MariaDB is not initialized, but the directory /var/lib/mysql is not empty, so initialization cannot be done.
```

When we check the `/var/lib/mysql` folder we can see that it doesn't exist.

```sh
[peter@stdb01 ~]$ sudo ls /var/lib/mysql
ls: cannot access '/var/lib/mysql': No such file or directory
```

So let's look inside the `var/lib` folder.

```sh
[peter@stdb01 ~]$ sudo ls -al  /var/lib/
total 80
drwxr-xr-x 1 root  root  4096 Oct  9 10:55 .
drwxr-xr-x 1 root  root  4096 Oct  9 10:55 ..
drwxr-xr-x 1 root  root  4096 Feb  8  2023 alternatives
drwxr-xr-x 1 root  root  4096 Feb  7  2023 dbus
drwxr-xr-x 1 root  root  4096 Mar  4  2023 dnf
drwxr-xr-x 1 root  root  4096 Jun 21  2021 games
drwxr-xr-x 1 root  root  4096 Jun 21  2021 misc
drwxr-xr-x 4 mysql mysql 4096 Oct  9 10:55 mysqld
drwx------ 1 root  root  4096 Feb  7  2023 portables
drwx------ 1 root  root  4096 Feb  7  2023 private
drwxr-x--- 1 root  root  4096 Feb  8  2023 rhsm
drwxr-xr-x 1 root  root  4096 Oct  9 10:55 rpm
drwxr-xr-x 1 root  root  4096 Jun 21  2021 rpm-state
drwxr-xr-x 1 root  root  4096 Feb  7  2023 selinux
drwxr-xr-x 1 root  root  4096 Feb  8  2023 systemd
```

Instead of folder `mysql` there is `mysqld`. We need to rename this folder to `mysql`

```sh
[peter@stdb01 ~]$ sudo mv /var/lib/mysqld /var/lib/mysql
```

Now try start the mariadb service.
And the MariaDB service is running.
```sh
[peter@stdb01 ~]$ sudo systemctl start mariadb
[peter@stdb01 ~]$ sudo systemctl status mariadb
● mariadb.service - MariaDB 10.3 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor pr
eset: disabled)
   Active: active (running) since Mon 2023-10-09 11:28:18 UTC; 7s a
go
```
## References

[Troubleshooting systemd Services](https://photobyte.org/troubleshooting-systemd-services/)
