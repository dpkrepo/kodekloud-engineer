# Task
There is some data on Nautilus App Server 3 in Stratos DC. Data needs to be altered in several of the files. On Nautilus App Server 3, alter the /home/BSD.txt file as per details given below:

a. Delete all lines containing word software and save results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)

b. Replace all occurrence of word and to is and save results in /home/BSD_REPLACE.txt file.

Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing the string itself; for example upto, contributor etc.
## Solution

Connect to the Application Server 3.
```sh
thor@jump_host ~$ ssh banner@stapp03
```
Change to te root user.
```sh
thor@jump_host ~$ sudo su -
```

Delete all lines containing word software and save results in /home/BSD_DELETE.txt file.
```sh
[root@stapp03 ~]# sed "/software/d" /home/BSD.txt > /home/BSD_DELETE.txt
```

Replace all occurrence of word and to is and save results in /home/BSD_REPLACE.txt file.
```sh
[root@stapp03 ~]# sed "s/\band\b/is/g" /home/BSD.txt > /home/BSD_REPLACE.txt
```
## References

[sed](https://www.gnu.org/software/sed/manual/sed.html)
