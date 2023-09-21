# Task
DevOps team created a new Git repository last week; however, as of now no team is using it. The Nautilus application development team recently asked for a copy of that repo on Storage server in Stratos DC. Please clone the repo as per details shared below:

The repo that needs to be cloned is /opt/official.git

Clone this git repository under /usr/src/kodekloudrepos directory. Please do not try to make any changes in the repo.
## Solution
Connect to the Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Clone the repo `/opt/official.git` to the `/usr/src/kodekloudrepos` directory.
```sh
[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos
[natasha@ststor01 kodekloudrepos]$  sudo git clone /opt/official.git
```

Check if git repo was cloned.

```sh
[natasha@ststor01 kodekloudrepos]$ ls -a
.  ..  official
```
## References

[git clone](https://git-scm.com/docs/git-clone)
