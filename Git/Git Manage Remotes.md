## Task
The xFusionCorp development team added updates to the project that is maintained under /opt/blog.git repo and cloned under /usr/src/kodekloudrepos/blog. Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on /usr/src/kodekloudrepos/blog repository as per details mentioned below:

a. In /usr/src/kodekloudrepos/blog repo add a new remote dev_blog and point it to /opt/xfusioncorp_blog.git repository.

b. There is a file /tmp/index.html on same server; copy this file to the repo and add/commit to master branch.

c. Finally push master branch to this new remote origin.
## Solution

Connect to the Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Go to the repo direcotry.

```sh
[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos/blog/
```

Add new remote.

```sh
[natasha@ststor01 blog]$ sudo git remote add dev_blog /opt/xfusioncorp_blog.git/
```

Copy the /tmp/index.html file to repo.

```sh
[natasha@ststor01 blog]$ sudo cp /tmp/index.html .
```

Add to stage and commit changes.

```sh
[natasha@ststor01 blog]$ sudo git add .
[natasha@ststor01 blog]$ sudo git commit -m ""Add index.html
[master 1ac3484] Add
 1 file changed, 10 insertions(+)
 create mode 100644 index.html
```

Push to the remote.

```sh
[natasha@ststor01 blog]$ sudo git push dev_blog
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 36 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 574 bytes | 574.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To /opt/xfusioncorp_blog.git/
 * [new branch]      master -> master
```

## References

[How to Add a New Remote to your Git Repo](https://articles.assembla.com/en/articles/1136998-how-to-add-a-new-remote-to-your-git-repo)
