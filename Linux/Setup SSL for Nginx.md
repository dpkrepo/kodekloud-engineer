## Task
The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 3 in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:

1. Install and configure nginx on App Server 3.

2. On App Server 3 there is a self signed SSL certificate and key present at location /tmp/nautilus.crt and /tmp/nautilus.key. Move them to some appropriate location and deploy the same in Nginx.

3. Create an index.html file with content Welcome! under Nginx document root.

4. For final testing try to access the App Server 3 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/.
## Solution

Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh banner@stapp03
```

Install nginx.

```sh
[banner@stapp03 ~]$ sudo yum install nginx -y
```

Edit /etc/nginx/nginx.conf file.

```
    server {
        listen       443 ssl;
        server_name  172.16.238.12;
        root         /var/www/html;
        ssl_certificate     /etc/nginx/ssl/nautilus.crt;
        ssl_certificate_key /etc/nginx/ssl/nautilus.key;
        ssl_protocols       TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;
        ssl_ciphers         HIGH:!aNULL:!MD5;
```

Create /etc/nginx/ssl/ directory and Copy certificate and key to it.

```sh
[banner@stapp03 ~]$ sudo mkdir /etc/nginx/ssl
[banner@stapp03 ~]$ sudo cp /tmp/nautilus.crt /etc/nginx/ssl
[banner@stapp03 ~]$ sudo cp /tmp/nautilus.key /etc/nginx/ssl
```

Create /var/www/html directory and file index.html inside.

```sh
[banner@stapp03 ~]$ sudo mkdir -p /var/www/html
[banner@stapp03 ~]$ sudo vi /var/www/html/index.html
Welcome!
```
Start nginx service.

```sh
[banner@stapp03 ~]$ sudo systemctl start nginx
```


## References

[Configuring HTTPS servers](https://nginx.org/en/docs/http/configuring_https_servers.html)
