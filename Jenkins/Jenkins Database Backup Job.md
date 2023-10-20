## Task
There is a requirement to create a Jenkins job to automate the database backup. Below you can find more details to accomplish this task:

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321.

Create a Jenkins job named database-backup.

Configure it to take a database dump of the kodekloud_db01 database present on the Database server in Stratos Datacenter, the database user is kodekloud_roy and password is asdfgdsd.

The dump should be named in db_$(date +%F).sql format, where date +%F is the current date.

Copy the db_$(date +%F).sql dump to the Backup Server under location /home/clint/db_backups.

Further, schedule this job to run periodically at */10 * * * * (please use this exact schedule format).

Note:

You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case please make sure to refresh the UI page.

Please make sure to define you cron expression like this */10 * * * * (this is just an example to run job every 10 minutes).

For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution

Install SSH, Publish over SSH and SSH Credentials plugins.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/d2301ea4-ecb2-4e88-8c7c-4ed42a112f00)


Create a credentials for the DB Server.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/b4a33f72-50f2-4a79-9069-dd5d0d887a2f)



Add SSH host to the Jenkins confgiuration.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/472b30c5-9fb4-436d-8b46-a67d7b726211)

Add SSH server unde Publish over SSH.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/b3054c1f-7f9d-4ec9-87c8-49fae9619cb4)



Create a job.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/60c4e900-a70d-4a73-896f-34cf380f0ae7)

Create the build step that creates dump file of db and copy it to the Backup Server.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/27d58f58-49b4-47ce-a48d-884a2ad047eb)



```sh
mysqldump kodekloud_db01 -u kodekloud_roy -p asdfgdsd > db_$(date +%F).sql
```

Add build step tah send file to the Backup Server.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/2d37e3cc-bcc8-4353-bf0d-bef3fa425ca5)


Run this job every 10 minutes.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/c3b134ba-70c5-4fbb-9a24-7110aa6480d7)



## References
