# Task
On our Storage server in Stratos Datacenter we are having some issues where nfsuser user is holding hundred of processes, which is degrading the performance of the server. Therefore, we have a requirement to limit its maximum processes. Please set its maximum process limits as below:

a. soft limit = 1026

b. hard_limit = 2024
## Solution
Connect to Storage Server.
```sh
thor@jump_host ~$ ssh natasha@ststor01
```
Open `/etc/security/limits.conf` file.

```sh
sudo vi /etc/security/limits.conf
```

Add this two lines and save it.

```
nfsuser          soft    nproc           1026
nfsuser          hard    nproc           2024
```

## References

[How to set ulimit values](https://access.redhat.com/solutions/61334)
