## Task
Nautilus developers are actively working on one of the project repositories, /usr/src/kodekloudrepos/games. Recently, they decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. Below are the requirements that have been shared with the DevOps team:

On Storage server in Stratos DC create a new branch xfusioncorp_games from master branch in /usr/src/kodekloudrepos/games git repo.

Please do not try to make any changes in the code.
## Solution

Connect to the Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Go to the direcotry of repository.
```sh
[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos/games/
```

Check current branch.

```sh
[natasha@ststor01 games]$ sudo git branch --show-current
kodekloud_games
```

Switch to master branch.

```sh
[natasha@ststor01 games]$ sudo git checkout master
Switched to branch 'master'
```

Create new branch named xfusioncorp_games.

```sh
[natasha@ststor01 games]$ sudo git checkout -b xfusioncorp_games
Switched to a new branch 'xfusioncorp_games'
```
## References

[Git Branching - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
