# Task

To stick with the security compliances, the Nautilus project team has decided to apply some restrictions on crontab access so that only allowed users can create/update the cron jobs. Limit crontab access to below specified users on App Server 2.

Allow crontab access to mariyam user and deny the same to ryan user.

## Solution

Connect to the App 2 Server.

```sh
thor@jump_host ~$ ssh steve@stapp02
```

Edit `/etc/cron.allow` file and add `mariyam` to it.

```sh
[steve@stapp02 ~]$ sudo vi /etc/cron.allow
```

Edit `/etc/cron.deny` file and add `ryan` to it.

```sh
[steve@stapp02 ~]$ sudo vi /etc/cron.deny
```

Restart `crond.service`
```sh
[steve@stapp02 ~]$ sudo systemctl restart crond.service
```

## References

[/etc/cron.allow](https://bash.cyberciti.biz/guide//etc/cron.allow)

[/etc/cron.deny](https://bash.cyberciti.biz/guide//etc/cron.deny)
