---
title: Linux - Level 1 - Create a User
layout: template
filename: Linux/Create_a_user.md
--- 
<html>
<body style="background-color:aquamarine;">
  
### Task
For security reasons the xFusionCorp Industries security team has decided to use custom Apache users for each web application hosted, rather than its default user. This will be the Apache user, so it shouldn't use the default home directory. Create the user as per requirements given below:



a. Create a user named kirsty on the App server 1 in Stratos Datacenter.


b. Set its UID to 1233 and home directory to /var/www/kirsty.

### Solution

Connect to the App server 1 in Stratos Datacener.


<span style=" font-family: monospace;"><span style="color: green;">thor@jump_host ~$</span> ssh tony@stapp01</span>


Create a user named kirsty with UID (-u) 1233 and home directory (-d) /var/www/kirsty.

<span style=" font-family: monospace;"><span style="color: green;">[tony@stapp01 ~]$</span> sudo useradd kirsty -u 1233 -d /var/www/kirsty</span>

useradd - create a new user or update default new user information

**-u, --uid** *UID*

The numerical value of the user's ID. This value must be unique, unless the -o option is used. The value must be non-negative. The default is to use the smallest ID value greater than 999 and greater than every other user. Values between 0 and 999 are typically reserved for system accounts.

**-d, --home** *HOME_DIR*

The new user will be created using HOME_DIR as the value for the user's login directory. The default is to append the LOGIN name to BASE_DIR and use that as the login directory name. The directory HOME_DIR does not have to exist but will not be created if it is missing.


</body>
</html>
