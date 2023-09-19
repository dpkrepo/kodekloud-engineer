# Task

New tools have been installed on the app servers in Stratos Datacenter. Some of these tools can only be managed from the graphical user interface. Therefore, there are some requirements for these app servers as below.

On all App servers in Stratos Datacenter, change the default runlevel so that they can boot in GUI (graphical user interface) by default. Please do not try to reboot these servers after completing this task.

## Solution

Connect to the App 1 Server.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Check current default run level.

```sh
[tony@stapp01 ~]$ systemctl get-default
multi-user.target
```

Change default run level to `graphical.target`

```sh
[tony@stapp01 ~]$ sudo systemctl set-default graphical.target
```

## References

[Change Run Levels](https://www.cyberciti.biz/tips/linux-changing-run-levels.html)
