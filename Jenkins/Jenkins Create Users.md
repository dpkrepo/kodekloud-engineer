# Task
The Nautilus team is planning to use Jenkins for some of their CI/CD pipelines. DevOps team has just installed a fresh Jenkins server and they are configuring it further to be available for use.

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

It has only a sample job for now. A new developer has joined the Nautilus application development team and they want this user to be added to the Jenkins server as per the details mentioned below:

1. Create a jenkins user named rose with Rc5C9EyvbU password, their full name should be Rose (it is case sensitive).

2. Using Project-based Matrix Authorization Strategy assign overall read permission to rose user.

3. Remember to remove all permissions for Anonymous users (if given) and make sure admin user has overall Administer permissions.

4. There is one existing job, make sure rose only has read permissions to that job (we are not worried about other permissions like Agent, SCM, etc.).

Note:

1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, in case Jenkins UI gets stuck when Jenkins service restarts in the back end, please make sure to refresh the UI page.

2. Do not immediately click on Finish button if you have restarted the Jenkins service, please wait for Jenkins login page to come back before finishing your task.

3. For these kind of scenarios that required changes to be done from a web UI, please take screenshots of your work so that you can share the same with us for review purpose (in case your task is marked incomplete or failed). You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution 

Got to `Manage Jenkins`.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/9e0a2412-09e8-4d35-bce3-e012ddc60390)

Click `Manage Users`.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/763c81ab-f91f-4c9d-b5f5-acb88d32123f)


Click `Create user`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/615c69eb-c334-46d3-91e4-340b38183019)

Fill information about user and click `Create User`.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/9fa74006-d34c-496c-ba28-5cb1b850bca2)

Install `Matrix Authorization Strategy` plugin.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/61092e66-81eb-4fba-9fda-3e6062010222)

Go to `Configure Global Security`
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/9745d08e-405a-4afe-b537-8c11bd033a51)

In Authorization select `Project-based Matrix Authorization Strategy`.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/4cdd6f7d-d81f-4517-9ea4-2f06f183e026)

Add user and set him in `Overall` and `Job` section `Read` permissions. Add admin user and set him in `Overall` section `Administer` and save configuration.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/0d69d819-3460-49e9-bcb7-e55995dd660a)


## References

[Managing Security](https://www.jenkins.io/doc/book/security/managing-security/)
