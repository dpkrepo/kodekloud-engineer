## Task
The DevOps team of xFusionCorp Industries is planning to create a number of Jenkins jobs for different tasks. So to easily manage the jobs within Jenkins UI they decided to create different views for all Jenkins jobs based on usage/nature of these jobs, - for example nautilus-crons view for all cron jobs. Based on the requirements shared below please perform the below mentioned task:



Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

1. Create a Jenkins job named nautilus-test-job.

2. Configure this job to run a simple bash command i.e echo "hello world!!".

3. Create a view named nautilus-crons (it must be a global view of type List View) and make sure nautilus-test-job and nautilus-cron-job (which is already present on Jenkins) jobs are listed under this new view.

4. Schedule this newly created job to build periodically at every minute i.e * * * * * (please make sure to use the cron expression exactly same how it is mentioned here)

5. Make sure the job builds successfully.

Note:

1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case please make sure to refresh the UI page.

2. For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution
Create job named `nautilus-test-job`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/a22e40dd-13f6-423a-ac25-fafcccab98dc)


Configure job to run `echo "hello world!!"` .

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/267af26b-4b38-44f2-a811-16da49fdcb19)

Create a view named `nautilus-crons` with type `List view`.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/2fc92072-119c-45b3-8dc2-49c0a610eb15)

Add `nautilus-test-job` and `nautilus-cron-job` to this view.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/7b13de3e-0cc7-4eab-bcc5-8d940c0ea7ab)

Schedule this newly created job to build periodically at every minute.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/643fd46a-68e1-45d1-af64-89034e14d2c3)


## References

[Dashboard View](https://plugins.jenkins.io/dashboard-view/)
