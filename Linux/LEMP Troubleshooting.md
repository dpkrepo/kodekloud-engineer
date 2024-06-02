## Task
We have LEMP stack configured on apps and database server in Stratos DC. Its using Nginx + php-fpm, for now we have deployed a sample php page on these apps. Due to some misconfiguration the php page is not loading on the web server. Seems like at least two app servers are having issues. Find below more details and make sure website works on LBR URL and locally on each app as well.



1. Nginx is supposed to run on port 80 on all app servers.

2. Nginx document root is /var/www/html/

3. Test the webpage on LBR URL (use LBR button on the top bar) and locally on each app server to make sure it works. It must not display any error message or nginx default page.
## Solution
On the Application Server 1:

1. Change the nginx port in the configuration file to 80.
2. Add `index.php` to allowed default pages in the configuration file.

```
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /var/www/html/;
        index index.html index.htm index.php;
```
3. Restart the nginx service.
```sh
[root@stapp01 ~]# systemctl restart nginx
[root@stapp01 ~]# curl stapp01:80
App is able to connect to the database using user kodekloud_tim
```
  On the Application Server 2:

  1. There is an error in nginx configuration file in `location ~ \.php$` block.
  It should look exacly just like this lines below.
```
      location ~ .php$ {
           try_files $uri =404;
           fastcgi_pass unix:/var/opt/remi/php74/run/php-fpm/www.sock;
           fastcgi_index index.php;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           include fastcgi_params;
        }
```
2. Restart the nginx service.
On the Application Server 3:

1. There is a bad root directory provided. It should be `root         /var/www/html/;`.
2. Restart the nginx service.
## References
I didn't use resources during this task.
