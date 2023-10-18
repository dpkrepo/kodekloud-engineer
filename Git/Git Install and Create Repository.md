## Task
The Nautilus development team shared with the DevOps team requirements for new application development, setting up a Git repository for that project. Create a Git repository on Storage server in Stratos DC as per details given below:

Install git package using yum on Storage server.

After that, create/init a git repository named /opt/official.git (use the exact name as asked and make sure not to create a bare repository).
## Solution

Connect to the Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Install git package.
```sh
[natasha@ststor01 ~]$ sudo yum install git -y
```
Create new repository.
```sh
[natasha@ststor01 ~]$ sudo git init /opt/official.git
```
## References

[git init](https://git-scm.com/docs/git-init)
