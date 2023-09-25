# Task
The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the sysops group of the team.

Setup a collaborative directory /sysops/data on app server 1 in Stratos Datacenter.

The directory should be group owned by the group sysops and the group should own the files inside the directory. The directory should be read/write/execute to the user and group owners, and others should not have any access.
## Solution
Connect to the Application Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Create the folder `/sysops/data`.

```sh
[tony@stapp01 ~]$ sudo mkdir -p /sysops/data
```

Check if group named `sysops` exist.

```sh
[tony@stapp01 ~]$ sudo cat /etc/group |grep sysops
sysops:x:1002:
```
Check current permission settings for `/sysops/data` directory.
```sh
[tony@stapp01 ~]$ sudo ls -alsd /sysops/data/
4 drwxr-xr-x 2 root root 4096 Sep 25 07:13 /sysops/data/
```

Set directory group to `sysops`.
```sh
[tony@stapp01 ~]$ sudo chgrp -R sysops /sysops/data/
```

Give this directory permission given in the task.
```sh
[tony@stapp01 ~]$ sudo chmod 2770 /sysops/data/
```
Check if directory has the correct permissions assigned.
```sh
[tony@stapp01 ~]$ sudo ls -alsd /sysops/data/
4 drwxrws--- 2 root sysops 4096 Sep 25 07:13 /sysops/data/
```
## References

[chmod](https://en.wikipedia.org/wiki/Chmod)

[chgrp](https://en.wikipedia.org/wiki/Chgrp)
