## Task

The Nautilus application development team has been working on a project repository /opt/demo.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with the DevOps team:

There are two branches in this repository, master and feature. One of the developers is working on the feature branch and their work is still in progress, however they want to merge one of the commits from the feature branch to the master branch, the message for the commit that needs to be merged into master is Update info.txt. Accomplish this task for them, also remember to push your changes eventually.
## Solution

Connect to the Storage Server.

```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Go to the repo folder and check commit id of commit with the message "Update info.txt"

```sh
[natasha@ststor01 demo]$ sudo git log --grep "Update info.txt"
commit f7d1eafe1810b5651ee23c2a4f29ed25f3cfcb0a
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 09:57:58 2024 +0000

    Update info.txt
```

Change branch to master.

```sh
[natasha@ststor01 demo]$ sudo git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```

Merge the commit with id that we checked before with master branch.

```sh
[natasha@ststor01 demo]$ sudo git cherry-pick f7d1eafe1810b5651ee23c2a4f29ed25f3cfcb0a
[master cc5065d] Update info.txt
 Date: Thu Jan 18 09:57:58 2024 +0000
 1 file changed, 1 insertion(+), 1 deletion(-)
[natasha@ststor01 demo]$ sudo git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 36 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 316 bytes | 316.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To /opt/demo.git
   b5be287..cc5065d  master -> master
```

## References

[git-cherry-pick](https://git-scm.com/docs/git-cherry-pick)
