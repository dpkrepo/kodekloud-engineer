# Task
The Nautilus production support team and security team had a meeting last month in which they decided to use local yum repositories for maintaing packages needed for their servers. For now they have decided to configure a local yum repo on Nautilus Backup Server. This is one of the pending items from last month, so please configure a local yum repository on Nautilus Backup Server as per details given below.

a. We have some packages already present at location /packages/downloaded_rpms/ on Nautilus Backup Server.

b. Create a yum repo named localyum and make sure to set Repository ID to localyum. Configure it to use package's location /packages/downloaded_rpms/.

c. Install package wget from this newly created repo.
## Solution

Connect to the Backup Server.
```sh
thor@jump_host ~$ ssh clint@stbkp01
```

Create repository configuration file.

```sh
[clint@stbkp01 ~]$ sudo vi /etc/yum.repos.d/localyum.repo
```

```
[localyum]
name=localyum
baseurl=file:///packages/downloaded_rpms/
enabled = 1
gpgcheck = 0
```
Check if repo has been created.
```sh
[clint@stbkp01 ~]$ sudo yum repolist
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

repo id                                repo name
localyum                               localyum
```

Install wget package.

```sh
[clint@stbkp01 ~]$ sudo yum install wget
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

localyum                                      8.1 MB/s |  59 kB     00:00    
Last metadata expiration check: 0:00:01 ago on Mon Sep 25 10:12:34 2023.
Dependencies resolved.
==============================================================================
 Package            Architecture  Version               Repository       Size
==============================================================================
Installing:
 wget               x86_64        1.19.5-11.el8         localyum        734 k
Installing dependencies:
 libmetalink        x86_64        0.1.3-7.el8           localyum         32 k

Transaction Summary
==============================================================================
Install  2 Packages

Total size: 766 k
Installed size: 2.8 M
Is this ok [y/N]: y
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                      1/1 
  Installing       : libmetalink-0.1.3-7.el8.x86_64                       1/2 
  Installing       : wget-1.19.5-11.el8.x86_64                            2/2 
  Running scriptlet: wget-1.19.5-11.el8.x86_64                            2/2 
  Verifying        : libmetalink-0.1.3-7.el8.x86_64                       1/2 
  Verifying        : wget-1.19.5-11.el8.x86_64                            2/2 
Installed products updated.

Installed:
  libmetalink-0.1.3-7.el8.x86_64           wget-1.19.5-11.el8.x86_64          

Complete!
```
## References

[Add Yum Repository](https://www.redhat.com/sysadmin/add-yum-repository)
