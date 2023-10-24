## Task
The Nautilus devops team got some requirements related to some Apache config changes. They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:

1.) httpd is already installed on app server 1. Configure Apache to listen on port 5000.

Configure Apache to add some redirects as mentioned below:

a.) Redirect http://stapp01.stratos.xfusioncorp.com:<Port>/ to http://www.stapp01.stratos.xfusioncorp.com:<Port>/ i.e non www to www. This must be a permanent redirect i.e 301

b.) Redirect http://www.stapp01.stratos.xfusioncorp.com:<Port>/blog/ to http://www.stapp01.stratos.xfusioncorp.com:<Port>/news/. This must be a temporary redirect i.e 302.
## Solution

Edit port in the `/etc/httpd/conf/httpd.conf` file.
```sh
[tony@stapp01 ~]$ sudo vi /etc/httpd/conf/httpd.conf
```
```
Listen 5000
```
Create new configuration file under `/etc/httpd/conf.d/`

```sh
[tony@stapp01 ~]$ sudo vi /etc/httpd/conf.d/main.conf
```
```
<VirtualHost *:5000>
        ServerName stapp01.stratos.xfusioncorp.com:5000/
        Redirect 301 / http://www.stapp01.stratos.xfusioncorp.com:5000/
</VirtualHost>

<VirtualHost *:5000>
        ServerName www.stapp01.stratos.xfusioncorp.com:5000/blog/
        Redirect 302 / http://www.stapp01.stratos.xfusioncorp.com:5000/news/
</VirtualHost>
```

Restart `httpd` service.

```sh
[tony@stapp01 ~]$ sudo systemctl restart httpd
```
Check if redirects are working.
```sh
[tony@stapp01 ~]$ curl http://www.stapp01.stratos.xfusioncorp.com:5000/blog/
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>302 Found</title>
</head><body>
<h1>Found</h1>
<p>The document has moved <a href="http://www.stapp01.stratos.xfusioncorp.com:5000/news/blog/">here</a>.</p>
</body></html>
[tony@stapp01 ~]$ curl http://stapp01.stratos.xfusioncorp.com:5000
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.stapp01.stratos.xfusioncorp.com:5000/">here</a>.</p>
</body></html>
```
## References

[How to Redirect a Web Page with Apache](https://www.w3docs.com/snippets/apache/how-to-redirect-a-web-page-with-apache.html)
