# Task
The Nautilus development team started with new project development. They have created different Git repositories to manage respective project's source code. One of the repositories /opt/cluster.git was created recently. The team has given us a sample index.html file that is currently present on jump host under /tmp directory. The repository has been cloned at /usr/src/kodekloudrepos on storage server in Stratos DC.

Copy sample index.html file from jump host to storage server under cloned repository at /usr/src/kodekloudrepos/cluster, further add/commit the file and push to the master branch.
## Solution

Copy the `index.html` file to home directory of natasha.
```sh
thor@jump_host ~$ scp /tmp/index.html natasha@ststor01:/home/natashanatasha@ststor01's password: 
index.html                                  100%   27    26.0KB/s   00:00
```

Connect to Storage Server.

```sh
thor@jump_host ~$ ssh natasha@ststor01
```
Copy `index.html` to `/usr/src/kodekloudrepos/cluster/`.
```sh
[natasha@ststor01 ~]$ sudo cp index.html /usr/src/kodekloudrepos/cluster/
```
Go to the `/usr/src/kodekloudrepos/cluster/`.

```sh
[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos/cluster/
```

Add, commit and push.
```sh
[natasha@ststor01 cluster]$ sudo git add index.html
[natasha@ststor01 cluster]$ sudo git commit -m "Add index.html file"
[master d0844cc] Add index.html file
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
[natasha@ststor01 cluster]$ sudo git push origin master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 36 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 334 bytes | 334.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To /opt/cluster.git
   5a47ee0..d0844cc  master -> master
```
## References

[git add](https://git-scm.com/docs/git-add)

[git commit](https://git-scm.com/docs/git-commit)

[git push](https://git-scm.com/docs/git-push)
