# Task
The DevOps team of xFusionCorp Industries is planning to create a number of Jenkins jobs for different tasks. To easily manage the jobs within Jenkins UI they decided to create different Folders for all Jenkins jobs based on usage/nature of these jobs. Based on the requirements shared below please perform the below mentioned task:

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

1. There are already two jobs httpd-php and services.

2. Create a new folder called Apache under Jenkins UI.

3. Move the above mentioned two jobs under Apache folder.

Note:
1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case, please make sure to refresh the UI page.

2. For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution
Install plugin named `Folders`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/575fb0ad-3ff2-459b-885a-2f7646f5c913)

Click `+ New Item`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/528b8641-de31-49f9-a842-73694dcfcc6a)

Type name of the folder `Apache` and choose `Folder` and clikc `OK`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/c2fa8af0-051f-483c-8be4-6bb119812741)

In Display Name type `Apache` and clic `Save`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d2a34290-4233-4187-a6b2-76450e396696)

Click on job you want to add to the folder.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/e47abb7b-d1ca-450b-9770-c352674e5209)

Click on `Move` choose `Jenkins >> Apache` and click `Move`.
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d619f494-90e8-4051-9df0-06892824da4e)

Both jobs are now in the folder Apache.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/48496ca8-4c0b-42ed-9125-c13971ac6bf4)


## References

[Folders](https://docs.cloudbees.com/docs/cloudbees-ci/latest/cloud-secure-guide/folders)
