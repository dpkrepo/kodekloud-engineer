# Create a group

There are specific access levels for users defined by the xFusionCorp Industries system admin team. Rather than providing access levels to every individual user, the team has decided to create groups with required access levels and add users to that groups as needed. See the following requirements:



a. Create a group named nautilus_admin_users in all App servers in Stratos Datacenter.


b. Add the user kano to nautilus_admin_users group in all App servers. (create the user if doesn't exist).

## Solution 

Connect to the Nautilus App 1 using ssh.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Create a group named nautilus_admin_users.
```sh
[tony@stapp01 ~]$ sudo groupadd nautilus_admin_users
```
Check if user kano is already created.
```sh
[tony@stapp01 ~]$ sudo getent passwd | grep kano
```

Create a new user named kano and assign group nautilus_admin_users.
```sh
[tony@stapp01 ~]$ sudo useradd -G nautilus_admin_users kano
```

Check if the user kano is created.
```sh
[tony@stapp01 ~]$ sudo getent passwd | grep kano
kano:x:1002:1003::/home/kano:/bin/bash
```
Check if the group nautilus_admin_users is assigned to the user kano.
```sh
[tony@stapp01 ~]$ id kano
uid=1002(kano) gid=1003(kano) groups=1003(kano),1002(nautilus_admin_users)
```

## References

[How to Create Groups in Linux](https://linuxize.com/post/how-to-create-groups-in-linux/)

[How to List Users in Linux](https://linuxize.com/post/how-to-list-users-in-linux/)

[How to Create Users in Linux](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/)
