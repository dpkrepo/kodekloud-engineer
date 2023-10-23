## Task
The devops team of xFusionCorp Industries is working on to setup centralised logging management system to maintain and analyse server logs easily. Since it will take some time to implement, they wanted to gather some server logs on a regular basis. At least one of the app servers is having issues with the Apache server. The team needs Apache logs so that they can identify and troubleshoot the issues easily if they arise. So they decided to create a Jenkins job to collect logs from the server. Please create/configure a Jenkins job as per details mentioned below:

Click on the Jenkins button on the top bar to access the Jenkins UI. Login using username admin and password Adm!n321

1. Create a Jenkins jobs named copy-logs.

2. Configure it to periodically build every 4 minutes to copy the Apache logs (both access_log and error_logs) from App Server 2 (from default logs location) to location /usr/src/devops on Storage Server.

Note:

1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page i.e update centre. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case please make sure to refresh the UI page.

2. Please make sure to define you cron expression like this */10 * * * * (this is just an example to run job every 10 minutes).

3. For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.
## Solution
Install SSH and SSH Credentials plugins.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/69972ef8-25ef-46be-ae43-dcb2f0e7a16f)


Add credentials for Application Server 2.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/dd69b714-eda9-4b46-a1c0-a400f3b1479f)


Add the SSH host.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/6ffdd139-bf7e-4aaf-9abe-0de99e518f25)


Generete SSH keys on Application Server 2 and copy public key to Storage Server.

```sh
[steve@stapp02 ~]$ ssh-keygen
[steve@stapp02 ~]$ ssh-copy-id natasha@ststor01
```

Create a job named `copy-logs`

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/f2e44497-de2c-465f-af3c-ad24961ade68)

Create a build step to copy Apache log files to Storage Server.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/6a375056-0efa-49f4-824e-65a3ef7c4e34)


Set build to run every 4 minutes. 

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/5d4b2f62-f644-40b8-adf7-e4de85da5a20)


## References

[SSH Plugin](https://plugins.jenkins.io/ssh/)
