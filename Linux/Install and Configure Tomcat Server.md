## Task
The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:

a. Install tomcat server on App Server 1.

b. Configure it to run on port 8087.

c. There is a ROOT.war file on Jump host at location /tmp.

Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e curl http://stapp01:8087
## Solution
Connect to the App Server 1.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install tomcat.

```sh
[tony@stapp01 ~]$ sudo yum install tomcat -y
```
Open configuration file of tomcat and edit default port.

```sh
[tony@stapp01 ~]$ sudo vi /etc/tomcat/server.xml
```
```
   <Connector port="8087" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

Copy the WAR file from jump host to the App Server 1.

```sh
thor@jump_host ~$ scp /tmp/ROOT.war tony@stapp01:/home/tony
```

Connect to the App Server 1 and copy this file into `/var/lib/tomcat/webapps/` directory.

```sh
[tony@stapp01 ~]$ sudo cp ROOT.war /var/lib/tomcat/webapps/
```

Restart tomcat service.

```sh
[tony@stapp01 ~]$ sudo systemctl restart tomcat
```

Check if website is working.

```sh
thor@jump_host ~$ curl http://stapp01:8087
<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html>
    <head>
        <title>SampleWebApp</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
    </head>
    <body>
        <h2>Welcome to xFusionCorp Industries!</h2>
        <br>
    
    </body>
</html>
```
## References

[How to change Tomcat's default HTTP port number](https://community.bmc.com/s/article/Inquira-KA335422)

[How to deploy a WAR file to Tomcat](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Top-5-ways-to-deploy-a-WAR-file-to-Tomcat)
