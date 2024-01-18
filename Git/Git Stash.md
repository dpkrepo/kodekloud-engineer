## Task

The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/blog present on Storage server in Stratos DC. One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes. Find below more details to accomplish this task:

Look for the stashed changes under /usr/src/kodekloudrepos/blog git repository, and restore the stash with stash@{1} identifier. Further, commit and push your changes to the origin.
## Solution

Connect to the Storage Server 1.

```sh
thor@jump_host ~$ ssh natasha@ststor01
```

List stash.

```sh
[natasha@ststor01 blog]$ sudo git stash list
stash@{0}: WIP on master: 34a9846 initial commit
stash@{1}: WIP on master: 34a9846 initial commit
```

Restore stash with index 1.

```sh
[natasha@ststor01 blog]$ sudo git stash pop --index 1
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   welcome.txt

Dropped refs/stash@{1} (6eefd6bd639280e04da8c70aac1d4b7bf32a129a)
```

Commit and push to the remote repo.

```sh
[natasha@ststor01 blog]$ sudo git commit -m "pop from stash index 1"
[master 0106aa2] pop from stash index 1
 1 file changed, 1 insertion(+)
 create mode 100644 welcome.txt
[natasha@ststor01 blog]$ sudo git push origin master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 36 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To /opt/blog.git
   34a9846..0106aa2  master -> master
```

## References

[git-stash](https://git-scm.com/docs/git-stash)
