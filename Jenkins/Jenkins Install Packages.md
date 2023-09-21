# Task
Some new requirements have come up to install and configure some packages on the Nautilus infrastructure under Stratos Datacenter. The Nautilus DevOps team installed and configured a new Jenkins server so they wanted to create a Jenkins job to automate this task. Find below more details and complete the task accordingly:



Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and Adm!n321 password.

Create a Jenkins job named install-packages and configure it to accomplish below given tasks.

Add a string parameter named PACKAGE.
Configure it to install a package on the storage server in Stratos Datacenter provided to the $PACKAGE parameter.

Note:

1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also some times Jenkins UI gets stuck when Jenkins service restarts in the back end so in such case please make sure to refresh the UI page.

2. Make sure Jenkins job passes even on repetitive runs as validation may try to build the job multiple times.

3. For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution
Install SSH Plugin.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/7817e320-6816-4840-9f55-7958fd5965c3)

Go to `Credentials`.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/71427d8e-96c3-4a46-ab76-e90b41de4195)

Click on `(global)`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/796cd41a-2b7f-44c7-b342-072a0fb93f4b)

Click `+ Add Credentials`

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d43019b1-48a9-453a-aaf7-8c510a2652f4)

Choose 'Username and Password'. Scope set to `Global`. Fill the credentials. In ID type hostname of Storage Server and hit `Create`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/b89126b4-b272-417f-a01e-4787854a23db)

Go to `Configure system`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/05c5dd34-bbdf-4c5b-9c75-3242c392d410)

And click `Add` under `SSH remote hosts`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/fb2a3133-e3fb-46a4-9bea-467bcf9172e1)

Type hostname of Storage Server. Port set to 22. Choose created previously credentials for natasha. Check `Pty` chcekbox. Click `Save`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/3d67c7e8-66c7-4b4c-ab53-6088f5d6ed6f)


Click on `Create a job`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/94713188-d6dc-408f-b590-c8fd3ea46681)

Type a name for a job and select `Freestyle Project` and click `OK`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/8d22482f-b7b7-41da-89a0-fdfd9bd0bb05)

Select `This project is parameterized` and choose `String parameter` and type `PACKAGE` in name.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/f7b7aebc-fd96-45d2-97f1-3688e9b4f1e6)


Check `Execute concurrent builds if necessary` checkbox.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d7efb597-93c7-4fce-a5b4-e57e61344361)


In `Build Steps` add a build step of type `Execute shell script on remote host using SSH`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/79c86633-b099-4dde-9b81-b58f2a4f2bfc)


Choose `natasha@ststor01:22`. Write a command that will be executed when job is triggered. 

```sh
echo Bl@kW | sudo -S yum install $PACKAGE -y
```

Click `Save`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/074ec8a6-2f92-4662-b77c-0735b737fd60)




## References

[SSH](https://plugins.jenkins.io/ssh/)

[Using Credentials](https://www.jenkins.io/doc/book/using/using-credentials/)

