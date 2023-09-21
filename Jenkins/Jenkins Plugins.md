# Task
The Nautilus DevOps team has recently setup a Jenkins server, which they want to use for some CI/CD jobs. Before that they want to install some plugins which will be used in most of the jobs. Please find below more details about the task

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and Adm!n321 password.

1. Once logged in, install Git and GitLab plugins. You might need to restart Jenkins service to install these plugins, so we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre.

Note:

1. Once you restart Jenkins service it will go down for some time so please wait for the Jenkins login page to come back before clicking on the Check button.

2. For these scenarios requiring changes to be done in a web UI, please take screenshots so you can share them with us for review in case your task is marked incomplete. You may also consider using screen recording software like loom.com to record and share your work.
## Solution
Go to Jenkins UI and click `Manage Jenkins`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/e61be96b-55e4-42ce-aab3-bb4419ac5a1c)

Click on `Manage Plugins`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/9985bb4d-7c89-49c7-9a59-b1813b3f9f2b)

Click on `Available Plugins`

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/6647aee6-fe16-440f-965f-ff39c2820e80)

Search for `Git` and `GitLab` and check them and click `Install without restart`

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/8b5dff1c-dcbf-47b0-a180-4c7b27750db3)

On the bottom of the page check `Restart Jenkins when installation is complete and no jobs are running`

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/16a1275f-44df-400c-a359-ed95a93f28cd)

After a while we can see that Git and GitLab plugins are installed.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/28ab9180-78d4-4c9c-8a95-be31b9c4bae3)



## References

[Managing Plugins](https://www.jenkins.io/doc/book/managing/plugins/)
