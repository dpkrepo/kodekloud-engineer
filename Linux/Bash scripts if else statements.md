## Task
The Nautilus DevOps team is working on to develop a bash script to automate some tasks. As per the requirements shared with the team database related tasks needed to be automated. Below you can find more details about the same:



Write a bash script named /opt/scripts/database.sh on Database Server. The mariadb database server is already installed on this server.


Add code in the script to perform some database related operations as per conditions given below:


a. Create a new database named kodekloud_db01. If this database already exists on the server then script should print a message Database already exists and if the database does not exist then create the same and script should print Database kodekloud_db01 has been created. Further, create a user named kodekloud_roy and set its password to asdfgdsd, also give full access to this user on newly created database (remember to use wildcard host while creating the user).


b. Now check if the database (if it was already there) already contains some data (tables)if so then script should print 'database is not empty otherwise import the database dump /opt/db_backups/db.sql and print imported database dump into kodekloud_db01 database.


c. Take a mysql dump which should be named as kodekloud_db01.sql and save it under /opt/db_backups/ directory.
## Solution

```bash
#! /usr/bin/bash

DB_NAME="kodekloud_db01"
DB_USER="kodekloud_roy"
DB_USER_PASS="asdfgdsd"

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
sql_db_content="""
  USE '$DB_NAME';
  SELECT COUNT(*) AS table_count FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = '$DB_NAME';
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


DB_CONTENT=$(mysql -u root -e "$sql_db_content")
DB_TABLE_COUNT=$(echo $DB_CONTENT | awk '{print $2}')

if [[ $DB_TABLE_COUNT == 0 ]]; then
  mysql $DB_NAME < /opt/db_backups/db.sql
  echo "imported database dump into $DB_NAME database"
else
  echo "database is not empty"
fi

mysqldump $DB_NAME > /opt/db_backups/$DB_NAME.sql
```

## References
