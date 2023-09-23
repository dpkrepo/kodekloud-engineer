# Task  
During the monthly compliance meeting, it was pointed out that several servers in the Stratos DC do not have a valid banner. The security team has provided serveral approved templates which should be applied to the servers to maintain compliance. These will be displayed to the user upon a successful login.

Update the message of the day on all application and db servers for Nautilus. Make use of the approved template located at /home/thor/nautilus_banner on jump host
## Solution

Copy file to the Server.
```sh
thor@jump_host ~$ scp /home/thor/nautilus_banner tony@stapp01:/home/tony/
```
Connect to the Application Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```

Move the `nautilus_banner` file to the `/etc/motd`
```sh
[tony@stapp01 ~]$ sudo mv nautilus_banner /etc/motd
```

## References

[Update Banner in Linux](https://medium.com/@keshavsaxena/update-banner-in-linux-servers-3d6832f95f44)
