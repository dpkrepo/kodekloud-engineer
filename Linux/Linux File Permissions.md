# Task
There are new requirements to automate a backup process that was performed manually by the xFusionCorp Industries system admins team earlier. To automate this task, the team has developed a new bash script xfusioncorp.sh. They have already copied the script on all required servers, however they did not make it executable on one the app server i.e App Server 3 in Stratos Datacenter.

Please give executable permissions to /tmp/xfusioncorp.sh script on App Server 3. Also make sure every user can execute it.

## Solution
Connect to the App Server 3.
```sh
thor@jump_host ~$ ssh banner@stapp03
```

Check current permissions for the `/tmp/xfusioncorp.sh` file.
```sh
[banner@stapp03 ~]$ ls -al /tmp/xfusioncorp.sh 
---------- 1 root root 40 Sep 19 11:22 /tmp/xfusioncorp.sh
```

Set executable (`+x`) permissions to `/tmp/xfusioncorp.sh` for other (`o`) users. Bash also needs to have read (`+r`) permission to execute script.

```sh
[banner@stapp03 ~]$ sudo chmod o+rx /tmp/xfusioncorp.sh
```

Check permission and see that read and executable permissions is set up for other users.
```sh
[banner@stapp03 ~]$ ls -al /tmp/xfusioncorp.sh 
-------r-x 1 root root 40 Sep 19 11:22 /tmp/xfusioncorp.sh
```

## References

[Set Up Permissions on a Script](https://bash.cyberciti.biz/guide/Setting_up_permissions_on_a_script)

[Chmod](https://en.wikipedia.org/wiki/Chmod)
