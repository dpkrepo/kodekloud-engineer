## Task

The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/cluster present on Storage server in Stratos DC. One of the developers mistakenly created a couple of files under this repository, but now they want to clean this repository without adding/pushing any new files. Find below more details:

Clean the /usr/src/kodekloudrepos/cluster git repository without adding/pushing any new files, make sure git status is clean.

## Solution

Connect to the Storage Server.

```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Go to the repo directory and run below command.

```sh
[natasha@ststor01 cluster]$ sudo git clean -f
```

Check status.

```sh
[natasha@ststor01 cluster]$ sudo git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

## References

[git-clean](https://git-scm.com/docs/git-clean)
