---
title: Linux - Level 1 - Create a User
layout: template
filename: Linux/Create_a_user.md
--- 
<center>
  
### Task
For security reasons the xFusionCorp Industries security team has decided to use custom Apache users for each web application hosted, rather than its default user. This will be the Apache user, so it shouldn't use the default home directory. Create the user as per requirements given below:



a. Create a user named kirsty on the App server 1 in Stratos Datacenter.


b. Set its UID to 1233 and home directory to /var/www/kirsty.

### Solution

Connect to the App server 1 in Stratos Datacener.


<span style=" font-family: monospace;"><span style="color: green;">thor@jump_host ~$</span> ssh tony@stapp01</span>


Create a user named kirsty with UID (-u) 1233 and home directory (-d) /var/www/kirsty.

<span style=" font-family: monospace;"><span style="color: green;">[tony@stapp01 ~]$</span> sudo useradd kirsty -u 1233 -d /var/www/kirsty</span>

</center>
