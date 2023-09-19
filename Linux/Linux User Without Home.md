# Task

The system admins team of xFusionCorp Industries has set up a new tool on all app servers, as they have a requirement to create a service user account that will be used by that tool.

Create a user named yousuf in App Server 2 without a home directory.

## Solution

Connect to the App Server 2.

```sh
thor@jump_host ~$ ssh steve@stapp02
```

Create a user named `yousuf` with no home directory (`-M` flag).
```sh
[steve@stapp02 ~]$ sudo useradd -M yousuf
```

Check if the home directory of the user yousuf exists.

```sh
[steve@stapp02 ~]$ sudo ls -a /home/yousuf
ls: cannot access '/home/yousuf': No such file or directory
```

## References 

[Add User Linux](https://linuxhint.com/add-user-linux/)
