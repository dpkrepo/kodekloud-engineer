## Task
The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter, and they need to create a bash script named beta_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).

a. Create a zip archive named xfusioncorp_beta.zip of /var/www/html/beta directory.

b. Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.

c. Copy the created archive to Nautilus Backup Server server in /backup/ location.

d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.
## Solution

Connect to the App 2 Server.
```sh
thor@jump_host ~$ ssh steve@stapp02
```

Generate keys.

```sh
[steve@stapp02 scripts]$ ssh-keygen
```

Copy public key to Backup Server.

```sh
ssh-copy-id -i /home/steve/.ssh/id_rsa.pub clint@stbkp01
```
Create a script in `/scripts/` folder on App 2 Server.
```bash
#!/bin/bash

zip xfusioncorp_beta.zip /var/www/html/beta
mv -f xfusioncorp_beta.zip /backup/xfusioncorp_beta.zip
scp /backup/xfusioncorp_beta.zip clint@stbkp01:/backup/
```

Give permission to execute this script.

```sh
[steve@stapp02 scripts]$ sudo chmod +x beta_backup.sh 
```

## References

[How to Zip Files and Directories in Linux](https://linuxize.com/post/how-to-zip-files-and-directories-in-linux/)

[How to use the Linux ‘scp’ command without a password to make remote backups](https://alvinalexander.com/linux-unix/how-use-scp-without-password-backups-copy/)

