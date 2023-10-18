## Task
The Nautilus application development team has been working on a project repository /opt/demo.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:

Create a new branch datacenter in /usr/src/kodekloudrepos/demo repo from master and copy the /tmp/index.html file (present on storage server itself) into the repo. Further, add/commit this file in the new branch and merge back that branch into master branch. Finally, push the changes to the origin for both of the branches.

## Solution
Connect to the Storage Server.

```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Go to the directory of repository.

```sh
[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos/demo/
```

Check on which we are currently on.

```sh
[natasha@ststor01 demo]$ sudo git branch --show-current
master
```

Create new branch named datacenter.

```sh
[natasha@ststor01 demo]$ sudo git checkout -b datacenter
Switched to a new branch 'datacenter'
```

Copy the /tmp/index.html to the repo directory.

```sh
[natasha@ststor01 demo]$ sudo cp /tmp/index.html .
```

Add this file to stage.

```sh
[natasha@ststor01 demo]$ sudo git add .
```

Commit changes.
```sh
[natasha@ststor01 demo]$ sudo git commit -m "Add index.html"
[datacenter 458bc72] Add index.html
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
```

Switch to the master branch.

```sh
[natasha@ststor01 demo]$ sudo git checkout master
Switched to branch 'master'
```

Merge master with datacenter branch.

```sh
[natasha@ststor01 demo]$ sudo git merge datacenter
Updating a334c2a..458bc72
Fast-forward
 index.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
```

And push the changes.

```sh
[natasha@ststor01 demo]$ sudo git push origin master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 36 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 332 bytes | 332.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To /opt/demo.git
   a334c2a..458bc72  master -> master
```
## References

[git-merge](https://git-scm.com/docs/git-merge)
