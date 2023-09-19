
# Task
A developer named siva has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for siva. It’s a good idea to create a user with an expiration date so that the user won't be able to access servers beyond that point.

Therefore, create a user named siva on the App Server 3 in Stratos Datacenter. Set expiry date to 2021-01-28. Make sure the user is created as per standard and is in lowercase.


## Solution

Connect to the App Server 3.

```sh
thor@jump_host ~$ ssh banner@stapp03
```

Create a user named `siva` and set expiry date to 2021-01-28 (`-e` flag).

```sh
[banner@stapp03 ~]$ sudo useradd -e 2021-01-28 siva
```

Check if expiry date is set correctly for the siva.
```sh
[banner@stapp03 ~]$ sudo chage -l siva
Last password change                                    : Sep 19, 2023
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Jan 28, 2021
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires    
```


## References

[Creating a User With an Expiry Date in Linux](https://www.geeksforgeeks.org/creating-a-user-with-an-expiry-date-in-linux/)
