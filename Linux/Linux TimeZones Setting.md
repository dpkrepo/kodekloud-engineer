# Task
During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is Pacific/Fakaofo.

Correct the mismatch.

## Solution
Connect to the App 1 Server.

```sh
thor@jump_host ~$ ssh tony@stapp01
```

Change timezone to Pacific/Fakaofo.

```sh
[tony@stapp01 ~]$ sudo timedatectl set-timezone Pacific/Fakaofo
```
## References
 [How to Set or Change Timezone](https://linuxize.com/post/how-to-set-or-change-timezone-in-linux/)
