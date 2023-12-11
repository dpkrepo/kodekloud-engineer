## Task
xFusionCorp Industries has hosted several static websites on Nautilus Application Servers in Stratos DC. There are some confidential directories in the document root that need to be password protected. Since they are using Apache for hosting the websites, the production support team has decided to use .htaccess with basic auth. There is a website that needs to be uploaded to /var/www/html/data on Nautilus App Server 3. However, we need to set up the authentication before that.

1. Create /var/www/html/data direcotry if doesn't exist.

2. Add a user james in htpasswd and set its password to B4zNgHA7Ya.

3. There is a file /tmp/index.html present on Jump Server. Copy the same to the directory you created, please make sure default document root should remain /var/www/html. Also website should work on URL http://<app-server-hostname>:8080/data/

## Solution

Connect to the App Server 3.

```sh
thor@jump_host ~$ ssh banner@stapp03
```

Create a data directory.

```sh
[banner@stapp03 ~]$ sudo mkdir /var/www/html/data
```

Add a user james with a password to .htpasswd file.

```sh
[banner@stapp03 data]$ sudo htpasswd -c /etc/httpd/.htpasswd james
[sudo] password for banner: 
New password: 
Re-type new password: 
Adding password for user james
```

Create a .htaccess file with the following parameters.

```
AuthUserFile /etc/httpd/.htpasswd
AuthName "Password Required"
AuthType Basic
Require valid-user
```
Edit /etc/httpd/conf/httpd.conf file. Change AllowOverride None to AllowOverride All for /var/www directory.

```
<Directory "/var/www">
    AllowOverride All
    # Allow open access:
    Require all granted
</Directory>
```


Copy index.html file to the App Server 3.
```sh
thor@jump_host ~$ scp /tmp/index.html banner@stapp03:/tmp/
banner@stapp03's password: 
index.html 
```

And copy it to the /var/www/html/data

```sh
[banner@stapp03 ~]$ sudo cp /tmp/index.html  /var/www/html/data/
```

## References

[.htaccess](https://httpd.apache.org/docs/2.4/howto/htaccess.html)
[.htpsswd](https://httpd.apache.org/docs/2.4/programs/htpasswd.html)
