# Task
The Nautilus development team shared requirements with the DevOps team regarding new application development.—specifically, they want to set up a Git repository for that project. Create a Git repository on Storage server in Stratos DC as per details given below:

Install git package using yum on Storage server.

After that create a bare repository /opt/demo.git (make sure to use exact name).
## Solution

Connect to the Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Install Git on the Staroge Server.
```sh
[natasha@ststor01 ~]$ sudo yum install git -y
```

Create a bare repository `/opt/demo.git`
```sh
[natasha@ststor01 ~]$ cd /opt
[natasha@ststor01 opt]$ sudo git init --bare demo.git
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /opt/demo.git/
```

## References

[Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

[Git Basics - Getting a Git Repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository)

[git init](https://git-scm.com/docs/git-init)
