# Task
The DevOps team of xFusionCorp Industries is planning to setup some CI/CD pipelines. After several meetings they have decided to use Jenkins server. So, we need to setup a Jenkins Server as soon as possible. Please complete the task as per requirements mentioned below:

1. Install jenkins on jenkins server using yum utility only, and start its service. You might face timeout issue while starting the Jenkins service, please refer [this](https://www.jenkins.io/doc/book/system-administration/systemd-services/#starting-services) link for help.

2. Jenkin's admin user name should be theadmin, password should be Adm!n321, full name should be Kirsty and email should be kirsty@jenkins.stratos.xfusioncorp.com.

Note:

1. For this task, ssh into the jenkins server using user root and password S3curePass from jump host.

2. After installing the Jenkins server, please click on the Jenkins button on the top bar to access Jenkins UI and follow the on-screen instructions to create an admin user.
## Solution
Connect to Jenkins Server.
```sh
thor@jump_host ~$ ssh root@jenkins
```

Create a bash script for Jenkins installation.
```sh
[root@jenkins ~]# vi jenkins-install
```
```bash
#!/bin/bash

sudo yum install wget -y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
# Add required dependencies for the jenkins package
sudo yum install java-17-openjdk -y
sudo yum install jenkins -y
sudo systemctl daemon-reload
```

Set permissions to execute a bash script.

```sh
[root@jenkins ~]# chmod u+x jenkins-install
```
Execute a bash script.
```sh
[root@jenkins ~]# ./jenkins-install
```

After Jenkins has beed installed, check status of jenkins service. If it is `inactive` run `systemctl restart jenkins`. After that Jenkins should be running.
```sh
[root@jenkins ~]# systemctl status jenkins
● jenkins.service - Jenkins Continuous Integration Server
   Loaded: loaded (/usr/lib/systemd/system/jenkins.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
[root@jenkins ~]# systemctl restart jenkins
[root@jenkins ~]# systemctl status jenkins
● jenkins.service - Jenkins Continuous Integration Server
   Loaded: loaded (/usr/lib/systemd/system/jenkins.service; disabled; vendor preset: disabled)
   Active: active (running) since Thu 2023-09-21 07:44:56 UTC; 14s ago
 Main PID: 4499 (java)
    Tasks: 86 (limit: 1340692)
   Memory: 1.3G
   CGroup: /docker/fd81c82f2e4450e667bb6f6861c57e3c139573b294f26e00ef65a039ab814ff8/system.slice/jenkins.service
           └─4499 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080

Sep 21 07:44:05 jenkins.stratos.xfusioncorp.com jenkins[4499]: Jenkins initial setup is required. An admin user has been created and a password generated.
Sep 21 07:44:05 jenkins.stratos.xfusioncorp.com jenkins[4499]: Please use the following password to proceed to installation:
Sep 21 07:44:05 jenkins.stratos.xfusioncorp.com jenkins[4499]: 6431a463028144e293a27b1ea0287f8e
Sep 21 07:44:05 jenkins.stratos.xfusioncorp.com jenkins[4499]: This may also be found at: /var/lib/jenkins/secrets/initialAdminPassword
Sep 21 07:44:05 jenkins.stratos.xfusioncorp.com jenkins[4499]: *************************************************************
Sep 21 07:44:56 jenkins.stratos.xfusioncorp.com jenkins[4499]: 2023-09-21 07:44:56.277+0000 [id=56]        INFO        jenkins.InitReactorRunner$1#onAttained: Completed initialization
Sep 21 07:44:56 jenkins.stratos.xfusioncorp.com jenkins[4499]: 2023-09-21 07:44:56.679+0000 [id=37]        INFO        hudson.lifecycle.Lifecycle#onReady: Jenkins is fully up and running
Sep 21 07:44:56 jenkins.stratos.xfusioncorp.com systemd[1]: Started Jenkins Continuous Integration Server.
Sep 21 07:44:57 jenkins.stratos.xfusioncorp.com jenkins[4499]: 2023-09-21 07:44:57.786+0000 [id=137]        INFO        h.m.DownloadService$Downloadable#load: Obtained the updated data file for hudson.tasks.Maven.MavenInstaller
Sep 21 07:44:57 jenkins.stratos.xfusioncorp.com jenkins[4499]: 2023-09-21 07:44:57.787+0000 [id=137]        INFO        hudson.util.Retrier#start: Performed the action check updates server successfully at the attempt #1
```

Setup Jenkins. Followe the steps on the screen.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/ef009a0b-95ea-4524-9346-63a0b5331922)

Copy passowrd and click `Continue`
```sh
[root@jenkins ~]# cat /var/lib/jenkins/secrets/initialAdminPassword
6431a463028144e293a27b1ea0287f8e
```

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/3a190c38-261b-462a-9ff4-83958fcfe210)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/c0731394-1cc3-46f1-8224-b59745792d71)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/cda85472-daee-453a-8d89-ce653ba9f4a9)

Jenkins is now working.

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/adf3b5a0-3a37-4e09-853a-0e4a8200fe3a)




## References

[Starting Services](https://www.jenkins.io/doc/book/system-administration/systemd-services/#starting-services)

[Install Jenkins](https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos)
