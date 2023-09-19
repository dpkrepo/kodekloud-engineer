# Task

On Nautilus storage server in Stratos DC, there is a storage location named /data, which is used by different developers to keep their data (non confidential data). One of the developers named james has raised a ticket and asked for a copy of their data present in /data/james directory on storage server. /home is a FTP location on storage server itself where developers can download their data. Below are the instructions shared by the system admin team to accomplish this task.

a. Make a james.tar.gz compressed archive of /data/james directory and move the archive to /home directory on Storage Server.

## Solution

Connect to the Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Compress `/data/james` directory to `james.tar.gz` archive.
```sh
[natasha@ststor01 ~]$ sudo tar -czvf james.tar.gz /data/james/
```

Move james.tar.gz file to `/home` directory.
```sh
[natasha@ststor01 ~]$ sudo mv james.tar.gz /home/james.tar.gz
```

## References

[How to Create tar gz File in Linux](https://www.cyberciti.biz/faq/how-to-create-tar-gz-file-in-linux-using-command-line/)
