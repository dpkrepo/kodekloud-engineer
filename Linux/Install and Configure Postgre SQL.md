## Task
The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:



PostgreSQL database server is already installed on the Nautilus database server.


a. Create a database user kodekloud_gem and set its password to B4zNgHA7Ya.


b. Create a database kodekloud_db3 and grant full permissions to user kodekloud_gem on this database.

## Solution
1. Connect to the DB server.
2. Connect to Postgres DB.
   ```sh
   [root@stdb01 ~]# psql -U postgres
   ```
3. Add a new user with a password.
   ```
   postgres=# CREATE USER kodekloud_gem WITH PASSWORD 'B4zNgHA7Ya';
   ```
4. Create a database.

   ```
   postgres=# CREATE DATABASE kodekloud_db3;
   ```
5. Grant privileges to created database for created user.

   ```
   postgres=# GRANT ALL PRIVILEGES ON DATABASE kodekloud_db3 TO kodekloud_gem;
   ```
## References

[CREATE USER](https://www.postgresql.org/docs/8.0/sql-createuser.html)

[CREATE DATABASE](https://www.postgresql.org/docs/current/sql-createdatabase.html)

[GRANT](https://www.postgresql.org/docs/current/sql-grant.html)
