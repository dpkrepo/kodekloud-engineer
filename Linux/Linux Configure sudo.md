# Task
We have some users on all app servers in Stratos Datacenter. Some of them have been assigned some new roles and responsibilities, therefore their users need to be upgraded with sudo access so that they can perform admin level tasks.

a. Provide sudo access to user rose on all app servers.

b. Make sure you have set up password-less sudo for the user.
## Solution
Connect to the Application Server.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Edit `/etc/sudoers` file.
```sh
[tony@stapp01 ~]$ sudo visudo
```

Add below line in this file.
```
rose       ALL=(ALL)    NOPASSWD:ALL
```
## References

[How to Run Sudo Command Without a Password](https://www.cyberciti.biz/faq/linux-unix-running-sudo-command-without-a-password/)
