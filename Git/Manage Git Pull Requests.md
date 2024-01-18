## Task

Max want to push some new changes to one of the repositories but we don't want people to push directly to master branch, since that would be the final version of the code. It should always only have content that has been reviewed and approved. We cannot just allow everyone to directly push to the master branch. So, let's do it the right way as discussed below:

SSH into storage server using user max, password Max_pass123 . There you can find an already cloned repo under Max user's home.

Max has written his story about The 🦊 Fox and Grapes 🍇

Max has already pushed his story to remote git repository hosted on Gitea branch story/fox-and-grapes

Check the contents of the cloned repository. Confirm that you can see Sarah's story and history of commits by running git log and validate author info, commit message etc.

Max has pushed his story, but his story is still not in the master branch. Let's create a Pull Request(PR) to merge Max's story/fox-and-grapes branch into the master branch

Click on the Gitea UI button on the top bar. You should be able to access the Gitea page.

UI login info:
- Username: max
- Password: Max_pass123
- 
PR title : Added fox-and-grapes story

PR pull from branch: story/fox-and-grapes (source)

PR merge into branch: master (destination)

Before we can add our story to the master branch, it has to be reviewed. So, let's ask tom to review our PR by assigning him as a reviewer

Add tom as reviewer through the Git Portal UI

Go to the newly created PR

Click on Reviewers on the right

Add tom as a reviewer to the PR

Now let's review and approve the PR as user Tom

Login to the portal with the user tom

Logout of Git Portal UI if logged in as max

UI login info:
- Username: tom
- Password: Tom_pass123

PR title : Added fox-and-grapes story

Review and merge it.

Great stuff!! The story has been merged! 👏

Note: For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution

Connect to the Storage Server as Max.

```sh
thor@jump_host ~$ ssh max@ststor01
```

Check commit logs for our branch.

```sh
max (story/fox-and-grapes)$ git log
commit da6d51d2566da7e1ff08743adaabb05052075050
Author: max <max@stratos.xfusioncorp.com>
Date:   Thu Jan 18 10:12:22 2024 +0000

    Added fox-and-grapes story

commit 9569a40ea5b07021d5e392b61e1907b676e2efbf
Merge: 7041b56 4c3b494
Author: sarah <sarah@stratos.xfusioncorp.com>
Date:   Thu Jan 18 10:12:21 2024 +0000

    Merge branch 'story/frogs-and-ox'

commit 7041b569d29a56a0320865bfbe0b51fe32b466f7
Author: sarah <sarah@stratos.xfusioncorp.com>
Date:   Thu Jan 18 10:12:21 2024 +0000

    Fix typo in story title

commit 4c3b494249a48e1d55449ab3c3c150b6eda5a6a1
Author: sarah <sarah@stratos.xfusioncorp.com>
Date:   Thu Jan 18 10:12:21 2024 +0000

    Completed frogs-and-ox story

commit 98caadefcc62433e335f274a78eae5a774b2f602
Author: sarah <sarah@stratos.xfusioncorp.com>
```

Login to Gitea.

Create a new PR.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/51768591-acae-47ff-94c2-9f0fd5acca2b)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/53ccf2ea-f2c8-423a-803c-760fcd594b98)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/a0235de1-80f2-4320-a93a-94d653334bb0)

Add tom to reviewers.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/3d1a8017-909d-4adc-ba9b-f3daf7b7e4b1)

Login as Tom.

Review PR and merge.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/ffa0d54c-6e99-4eac-9fc0-29638ffc9dff)




## References

[Pull Request](https://docs.gitea.com/next/usage/pull-request)
