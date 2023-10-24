## Task
Some of the developers from Nautilus project team have asked for SFTP access to at least one of the app server in Stratos DC. After going through the requirements, the system admins team has decided to configure the SFTP server on App Server 2 server in Stratos Datacenter. Please configure it as per the following instructions:

a. Create a SFTP user mariyam and set its password to YchZHRcLkL. There is already a group called ftp, you can utilise the same.

b. Password authentication should be enabled for this user.

c. SFTP user should only be allowed to make SFTP connections.
## Solution

Connect to the App Server 2.

```sh
thor@jump_host ~$ ssh steve@stapp02
```

Create a user and setup password.

```sh
[steve@stapp02 ~]$ sudo adduser mariyam
[steve@stapp02 ~]$ sudo passwd mariyam
```

Edit confguration file.
```sh
[steve@stapp02 ~]$ sudo vi /etc/ssh/sshd_config
```

Add setting for the SFTP user.
```
Match User mariyam
  PasswordAuthentication yes
  ForceCommand internal-sftp
```

Restart sshd service.


```sh
[steve@stapp02 ~]$ sudo systemctl restart sshd
```

## References

[Setting Up an SFTP Server](https://tecadmin.net/setup-sftp-server-on-centos/)
