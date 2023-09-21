# Task
Nautilus developers are actively working on one of the project repositories, /usr/src/kodekloudrepos/blog. They were doing some testing and created few test branches, now they want to clean those test branches. Below are the requirements that have been shared with the DevOps team:

On Storage server in Stratos DC delete a branch named xfusioncorp_blog from /usr/src/kodekloudrepos/blog git repo.
## Solution

Connect to Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```
Go to the repo directory.

```sh
[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos/blog
```

List all branches in this repo.
```sh
[natasha@ststor01 blog]$ sudo git branch --list
  master
* xfusioncorp_blog
```

Change branch to `master`.

```sh
[natasha@ststor01 blog]$ sudo git checkout master
Switched to branch 'master'
```

Delete `xfusioncorp_blog` branch.

```sh
[natasha@ststor01 blog]$ sudo git branch -d xfusioncorp_blog
Deleted branch xfusioncorp_blog (was bc55b77).
```
## References

[git branch](https://git-scm.com/docs/git-branch)
