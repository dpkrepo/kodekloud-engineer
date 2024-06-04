## Task
xFusionCorp Industries is planning to host a WordPress website on their infra in Stratos Datacenter. They have already done infrastructure configuration—for example, on the storage server they already have a shared directory /vaw/www/html that is mounted on each app host under /var/www/html directory. Please perform the following steps to accomplish the task:



a. Install httpd, php and its dependencies on all app hosts.


b. Apache should serve on port 6300 within the apps.


c. Install/Configure MariaDB server on DB Server.


d. Create a database named kodekloud_db2 and create a database user named kodekloud_pop identified as password LQfKeWWxWD. Further make sure this newly created user is able to perform all operation on the database you created.


e. Finally you should be able to access the website on LBR link, by clicking on the App button on the top bar. You should see a message like App is able to connect to the database using user kodekloud_pop

## Solution

There was an issue with installing dependencies using yum.

```sh
[root@stapp01 ~]# yum install httpd -y
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

CentOS Stream 8 - AppStream                              144  B/s |  38  B     00:00    
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist
```
To fix it I wrote a bash script that changes URL repo pointing from official CentOS repo to `vault.centos.org`.
```bash
#! /usr/bin/bash

cd /etc/yum.repos.d/

sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*

sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
```

After executing this script we are able to install httpd and php, php-mysqlnd.

```sh
[root@stapp01 ~]# yum install httpd php php-mysqlnd -y 
```

In the `/etc/httpd/conf/http.conf` file change port from 80 to 6300.

```
Listen 6300
```

Start the httpd service.

```sh
[root@stapp01 ~]# systemctl start httpd
```

Repeat this steps on every App server.

On the DB server install `mariadb-server`.

Start maraidb service.

```sh
[root@stdb01 ~]# systemctl start mariadb.service
```

```bash
#! /usr/bin/bash

DB_NAME="kodekloud_db2"
DB_USER="kodekloud_pop"
DB_USER_PASS="LQfKeWWxWD"

sql_show="""
SHOW DATABASES LIKE '$DB_NAME';
"""
sql_create_db="""
  CREATE DATABASE $DB_NAME;
"""
sql_create_user="""
  CREATE USER '$DB_USER'@'%' IDENTIFIED BY '$DB_USER_PASS';
"""
sql_get_user="""
  SELECT COUNT(*) AS user_count FROM mysql.user WHERE User = '$DB_USER';
"""
sql_grant="""
  GRANT ALL PRIVILEGES ON $DB_NAME.* TO '$DB_USER'@'%';
"""
sql_flush_privileges="""
  FLUSH PRIVILEGES;
"""
CHECK_DB=$(mysql -e "$sql_show")
if [[ "$CHECK_DB" == *"$DB_NAME"* ]]; then
  echo "Database already exists."
else
  mysql -u root -e "$sql_create_db"
  echo "Database $DB_NAME has been created"
fi

DB_CHECK_USER=$(mysql -u root -e "$sql_get_user")
DB_USER_COUNT=$(echo $DB_CHECK_USER | awk '{print $2}')

if [[ $DB_USER_COUNT == 0 ]]; then
  mysql -u root -e "$sql_create_user"
  mysql -u root -e "$sql_grant"
  mysql -u root -e "$sql_flush_privileges"
fi
```

## References
