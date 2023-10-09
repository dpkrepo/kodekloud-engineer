## Task
The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . App Server 3 in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.

As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

## Solution

Connect to the App Server 3.
```sh
thor@jump_host ~$ ssh banner@stapp03
```

Open `/etc/resolv.conf` file.
```sh
[banner@stapp03 ~]$ sudo vi /etc/resolv.conf
```
Add in new line `nameserver 8.8.8.8` and save the file.
```
eserver 127.0.0.11
options ndots:0
nameserver 8.8.8.8
```

## References

[How to Change DNS on Linux](https://www.linuxfordevices.com/tutorials/linux/change-dns-on-linux)

[Google Public DNS IP addresses](https://developers.google.com/speed/public-dns/docs/using)
