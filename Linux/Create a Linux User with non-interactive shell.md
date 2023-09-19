# Task

The System admin team of xFusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements they need to create a user with a non-interactive shell.

Therefore, create a user named john with a non-interactive shell on the App Server 1.

## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Create a user named `john` with the `nologin` shell. This can be achieved by using the `--shell` flag followed by the path of the desired shell. In our case, to create a user with a non-interactive shell, use `/usr/sbin/nologin`.  
```sh
[tony@stapp01 ~]$ sudo adduser john  --shell /usr/sbin/nologin
```
Check if the user john has assigned a correct shell.
```sh
[tony@stapp01 ~]$ sudo cat /etc/passwd | grep john
john:x:1002:1002::/home/john:/usr/sbin/nologin
```

## References

[Create Non Login User in Linux](https://www.baeldung.com/linux/create-non-login-user)
