# Task
During a routine security audit, the team identified an issue on the Nautilus App Server. Some malicious content was identified within the website code. After digging into the issue they found that there might be more infected files. Before doing a cleanup they would like to find all similar files and copy them to a safe location for further investigation. Accomplish the task as per the following requirements:

a. On App Server 3 at location /var/www/html/news find out all files (not directories) having .css extension.

b. Copy all those files along with their parent directory structure to location /news on same server.

c. Please make sure not to copy the entire /var/www/html/news directory content.
## Solution

Connect to the Application Server 3.
```sh
thor@jump_host ~$ ssh banner@stapp03
```

Find and copy the files with extension .css to the /news directory with keeping whole structure.
```sh
[banner@stapp03 ~]$ sudo find  /var/www/html/news -type f -name "*.css" -exec cp --parents {} /news \;
```
## References

[find](https://man7.org/linux/man-pages/man1/find.1.html)
