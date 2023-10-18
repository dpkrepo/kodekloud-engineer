## Task
The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/blog present on Storage server in Stratos DC. However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit. Below are more details about the task:

In /usr/src/kodekloudrepos/blog git repository, revert the latest commit ( HEAD ) to the previous commit (JFYI the previous commit hash should be with initial commit message ).

Use revert blog message (please use all small letters for commit message) for the new revert commit.
## Solution
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

```sh
[natasha@ststor01 blog]$ sudo git revert HEAD --edit
[master 71bae15] revert blog
 1 file changed, 1 insertion(+)
 create mode 100644 info.txt
```

Type the message provided in task and save the file.
## References

[git revert](https://git-scm.com/docs/git-revert)
