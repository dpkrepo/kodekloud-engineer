## Task
Some developers are working on a common repository where they are testing some features for an application. They are having three branches (excluding the master branch) in this repository where they are adding changes related to these different features. They want to test these changes on Stratos DC app servers so they need a Jenkins job using which they can deploy these different branches as per requirements. Configure a Jenkins job accordingly.

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

Similarly, click on Gitea button to access the Gitea page. Login to Gitea server using username sarah and password Sarah_pass123.

There is a Git repository named web_app on Gitea where developers are pushing their changes. It has three branches version1, version2 and version3 (excluding the master branch). You need not to make any changes in the repository.

Create a Jenkins job named app-job.

Configure this job to have a choice parameter named Branch with choices as given below:

version1

version2

version3

Configure the job to fetch changes from above mentioned Git repository and make sure it should fetches the changes from the respective branch which you are passing as a choice in the choice parameter while building the job. For example if you choose version1 then it must fetch and deploy the changes from branch version1.

Configure this job to use custom workspace rather than a default workspace and custom workspace directory should be created under /var/lib/jenkins (for example /var/lib/jenkins/version1) location rather than under any sub-directory etc. The job should use a workspace as per the value you will pass for Branch parameter while building the job. For example if you choose version1 while building the job then it should create a workspace directory called version1 and should fetch Git repository etc within that directory only.

Configure the job to deploy code (fetched from Git repository) on storage server (in Stratos DC) under /var/www/html directory. Since its a shared volume.

You can access the website by clicking on App button.

Note:

You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case please make sure to refresh the UI page.

For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.

CheckCompleteIncompleteTry Later
## Solutiom
Install the Git, SSH and Publish Over SSH plugin.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/bfa904e7-c0dd-45a4-9bab-c34f97e72d48)


![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/eb686cb6-5ee5-4f43-acaa-364a87c30735)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/a183bf0e-7316-4277-95b2-162016c91914)


Create the credentials for Gitea and Storage Server.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/0c0f7e5c-bbd0-47a4-920d-0c96c94c9961)

Add SSH server to Jenkins.


![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/930169f0-b670-4d5d-8b1c-0fc4e1053ce4)


Create job named `app-job`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/176ac81b-ac48-43af-a4bc-8bdb0efc8673)

Create a parameter for the job.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/7c7490f6-7ede-4569-a5a9-b45b14b306cf)

Add git repo and credentials.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/91c367f6-1ea6-48a4-a6ed-dffb33bbe8aa)

Set in branches to build a branch from parameters.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/09db0ff1-d0f0-4b36-bc3b-9e25012dddc4)

Set the custom workspace.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/3307534d-2d32-4377-a07d-89130a654bbc)

Set SSH server in job configuration to send all files to the Storage Server.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/e897bc42-5699-426c-8c04-a4f2d1d796e2)



## References

[Git Plugin](https://plugins.jenkins.io/git/)

[Publish Over SSH](https://plugins.jenkins.io/publish-over-ssh/)
