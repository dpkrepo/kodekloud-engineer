## Task
The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/cluster present on Storage server in Stratos DC. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the HEAD and the branch itself to a commit with message add data.txt file. Find below more details:

In /usr/src/kodekloudrepos/cluster git repository, reset the git commit history so that there are only two commits in the commit history i.e initial commit and add data.txt file.

Also make sure to push your changes.
## Solution

Connect to the Storage Server.

```sh
thor@jump_host ~$ ssh natasha@ststor01
```

Check commit logs.

```sh
commit 3f2ca13a10afac01bb0babd138ebcb895daacce9 (HEAD -> master, origin/master)
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:39 2024 +0000

    Test Commit10

commit 47e10c96993ce24792c9155f3d6c2024c4d34946
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:39 2024 +0000

    Test Commit9

commit 6e70f466a0506af42cb65091cff08f4375127be6
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:39 2024 +0000

    Test Commit8

commit 4422e1e493451f8601543a37077986afd2a65497
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:39 2024 +0000

    Test Commit7

commit cf0d66f0d7486f3554d0ecfc38ea8b786b59e834
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:39 2024 +0000

    Test Commit6

commit df6c837a3e26359ac9f7f5a26ca92e168e7ea630
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    Test Commit5

commit b67ca950a6068ff2f2ff687294182eaeacf4c9f8
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    Test Commit4

commit 7409e8f3a14a2808200b6b9e90a7fabb732cb260
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    Test Commit3

commit 3cf9bf5b6ccb9f0ad8f079fb7cfb9d816c7b4b89
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    Test Commit2

commit 2cfedf98ca16f105192bc500e5a5c732e97bdbeb
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    Test Commit1

commit 92b99c96429c3ad060034f24287d16171ebfb186
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    add data.txt file

commit 02176bd4b3dd8fc95127baba790191aebc383e4c
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    initial commit
```
Reset git commit history to contain only first two commits.

```sh
[natasha@ststor01 cluster]$ sudo git reset --hard 92b99c96429c3ad060034f24287d16171ebfb186
HEAD is now at 92b99c9 add data.txt file
```

```sh
[natasha@ststor01 cluster]$ sudo git log
commit 92b99c96429c3ad060034f24287d16171ebfb186 (HEAD -> master)
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    add data.txt file

commit 02176bd4b3dd8fc95127baba790191aebc383e4c
Author: Admin <admin@kodekloud.com>
Date:   Thu Jan 18 10:28:38 2024 +0000

    initial commit
```

Push changes.

```sh
[natasha@ststor01 cluster]$ sudo git push -f origin master
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To /opt/cluster.git
 + 3f2ca13...92b99c9 master -> master (forced update)
```

## References

[git-reset](https://git-scm.com/docs/git-reset)
