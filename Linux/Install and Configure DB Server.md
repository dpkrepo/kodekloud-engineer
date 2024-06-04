## Task
We need to setup a database server on Nautilus DB Server in Stratos Datacenter. Please perform the below given steps on DB Server:



a. Install/Configure MariaDB server.


b. Create a database named kodekloud_db3.


c. Create a user called kodekloud_rin and set its password to dCV3szSGNA.


d. Grant full permissions to user kodekloud_rin on database kodekloud_db3.
## Solution
Fix yum issue wit the script below.

```bash
#! /usr/bin/bash

cd /etc/yum.repos.d/

sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*

sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
```

Install mariadb server.

```sh
[root@stdb01 ~]# yum install mariadb-server -y
```

Start mariadb service.

```sh
[root@stdb01 ~]# systemctl start mariadb.service
```

Create a script that configure db server.

```bash
#! /usr/bin/bash

DB_NAME="kodekloud_db3"
DB_USER="kodekloud_rin"
DB_USER_PASS="dCV3szSGNA"

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
```

## References
