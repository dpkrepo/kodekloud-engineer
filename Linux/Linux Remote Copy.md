# Task

One of the Nautilus developers has copied confidential data on the jump host in Stratos DC. That data must be copied to one of the app servers. Because developers do not have access to app servers, they asked the system admins team to accomplish the task for them.

Copy /tmp/nautilus.txt.gpg file from jump server to App Server 2 at location /home/opt.

## Solution

Copy file `/tmp/nautulus.txt.gpg` to the `/home/opt/` directory on the App Server 2.
```sh
thor@jump_host ~$ scp /tmp/nautilus.txt.gpg steve@stapp02:/home/opt/
```


## References

[Transfer Files Remotely](https://www.cyberciti.biz/faq/how-to-copy-and-transfer-files-remotely-on-linux-using-scp-and-rsync/)
