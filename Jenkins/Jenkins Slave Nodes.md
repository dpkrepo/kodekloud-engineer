## Task

The Nautilus DevOps team has installed and configured new Jenkins server in Stratos DC which they will use for CI/CD and for some automation tasks. There is a requirement to add all app servers as slave nodes in Jenkins so that they can perform tasks on these servers using Jenkins. Find below more details and accomplish the task accordingly.

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

1. Add all app servers as SSH build agent/slave nodes in Jenkins. Slave node name for app server 1, app server 2 and app server 3 must be App_server_1, App_server_2, App_server_3 respectively.

2. Add labels as below:

App_server_1 : stapp01

App_server_2 : stapp02

App_server_3 : stapp03

3. Remote root directory for App_server_1 must be /home/tony/jenkins, for App_server_2 must be /home/steve/jenkins and for App_server_3 must be /home/banner/jenkins.

4. Make sure slave nodes are online and working properly.

Note:

1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case, please make sure to refresh the UI page.

2. For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.

## Solution

Install SSH and SSH Build Agents plugins.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/085878c6-338c-4073-9eaa-e5edd32a2321)

Create credentials.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/ad5fe57b-c9ab-4061-ae7d-5d825b253d9f)

Add new agents.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/fdc39f42-72f5-4392-9502-9891189da1fc)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/5bb675e0-b240-486b-a607-9792d0cef315)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/a7a937ad-9676-4b5b-bc7e-fe35ce8b4394)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d8ff4fec-df6c-4212-a42e-a613e938c94b)

Agents failed because they don't have installed Java.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/f421d4e9-47c5-46d2-a345-41a3edb0ef87)

Creating a Jenkins Job to install Java on agents.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/603922e6-dad1-456d-9f41-c4e0990956f7)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d761ff52-d234-4b73-b57b-ca1e38f36ae4)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/c33431d1-530d-4032-9f0e-9979ad1eba12)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/8e6b40c3-21ef-4642-8502-b41c1fc4446f)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/20895091-3c0f-4a8c-8993-6126e962029c)






## References

[Using Agents](https://www.jenkins.io/doc/book/using/using-agents/)
