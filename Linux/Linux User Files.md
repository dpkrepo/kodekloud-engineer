
# Task

There was some users data copied on Nautilus App Server 1 at /home/usersdata location by the Nautilus production support team in Stratos DC. Later they found that they mistakenly mixed up different user data there. Now they want to filter out some user data and copy it to another location. Find the details below:

On App Server 1 find all files (not directories) owned by user jim inside /home/usersdata directory and copy them all while keeping the folder structure (preserve the directories path) to /ecommerce directory.

## Solution

Connect to the App Server 1.
```sh
thor@jump_host ~$ ssh tony@stapp01
```
Find and copy files (not directories `-type f`) owned by user jim (`-user jim`) inside /home/usersdata directory too /ecommerce while keeping the folder structure (`--parents`).
```sh
[tony@stapp01 ~]$ sudo find /home/usersdata -type f -user jim -exec cp --parents "{}" /ecommerce \;
```

## References

[How To Find All The Files Owned By User](https://www.cyberciti.biz/faq/how-do-i-find-all-the-files-owned-by-a-particular-user-or-group/)
[cp\; Preserve Directory Path](https://tecadmin.net/cp-preserve-directory-path/)
[Find and Copy Files](https://ostechnix.com/find-copy-certain-type-files-one-directory-another-linux/)
