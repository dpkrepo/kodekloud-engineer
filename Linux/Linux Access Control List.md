# Task

The Nautilus security team performed an audit on all servers present in Stratos DC. During the audit some critical data/files were identified which were having the wrong permissions as per security standards. Once the report was shared with the production support team, they started fixing the issues one by one. It has been identified that one of the files named /etc/hosts on Nautilus App 3 server has wrong permissions, so that needs to be fixed and the correct ACLs needs to be set.

1. The user owner and group owner of the file should be root user.

2. Others must have read only permissions on the file.

3. User kirsty must not have any permission on the file.

4. User garrett should have read only permission on the file.

## Solution
Connect to the App Server 3.

```sh
thor@jump_host ~$ ssh banner@stapp03
```

Change owner of the /etc/hosts file to root. Root is the owner of this file.
Others already have read only permissions.
```sh
[banner@stapp03 ~]$ sudo ls -al /etc/hosts
-rw-r--r-- 1 root root 374 Sep 19 11:46 /etc/hosts
```

Set up no permissions for kirsty on /etc/hosts file.


```sh
[banner@stapp03 ~]$ sudo setfacl -m u:kirsty:--- /etc/hosts
```

Set up read only permission for garrett on /etc/hosts file.

```sh
[banner@stapp03 ~]$ sudo setfacl -m u:garrett:r /etc/hosts
```
## References

[setfacl](https://manpages.ubuntu.com/manpages/lunar/en/man1/setfacl.1.html)

[chown](https://linuxize.com/post/linux-chown-command/)
