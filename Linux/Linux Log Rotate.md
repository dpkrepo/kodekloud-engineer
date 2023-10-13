## Task 
The Nautilus DevOps team is ready to launch a new application, which they will deploy on app servers in Stratos Datacenter. They are expecting significant traffic/usage of tomcat on app servers after that. This will generate massive logs, creating huge log files. To utilise the storage efficiently, they need to compress the log files and need to rotate old logs. Check the requirements shared below:

a. In all app servers install tomcat package.

b. Using logrotate configure tomcat logs rotation to monthly and keep only 3 rotated logs.

(If by default log rotation is set, then please update configuration as needed)
## Solution

Connect to the Application Server.
```sh
thor@jump_host ~$ ssh tony@stapp01
```

Install tomcat on the Application Server.
```sh
[tony@stapp01 ~]$ sudo yum install tomcat -y
```

Create the logrotate configuration file for tomcat `/etc/logrotate.d/tomcat`.
```sh
[tony@stapp01 ~]$ sudo vi /etc/logrotate.d/tomcat 
```
Add to this configuration file `monthly` and `rotate 3` for the logs of tomcat that are stored in  `/var/log/tomcat/`.
```
/var/log/tomcat/
{
monthly
rotate 3
}
```

Apply the configuration file.

```sh
[tony@stapp01 ~]$ sudo logrotate -f /etc/logrotate.d/tomcat
```

## References

[Rotating Logs With Logrotate in Linux](https://www.baeldung.com/linux/rotating-logs-logrotate)
