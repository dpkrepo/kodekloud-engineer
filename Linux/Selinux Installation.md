# Task

The xFusionCorp Industries security team recently did a security audit of their infrastructure and came up with ideas to improve the application and server security. They decided to use SElinux for an additional security layer. They are still planning how they will implement it; however, they have decided to start testing with app servers, so based on the recommendations they have the following requirements:

Install the required packages of SElinux on App server 2 in Stratos Datacenter and disable it permanently for now; it will be enabled after making some required configuration changes on this host. Don't worry about rebooting the server as there is already a reboot scheduled for tonight's maintenance window. Also ignore the status of SElinux command line right now; the final status after reboot should be disabled.
## Solution
Connect to the App Server 2.

```sh
thor@jump_host ~$ ssh steve@stapp02
```

Install SElinux.

```sh
thor@jump_host ~$ sudo yum install selinux* -y
```

Disable SElinux. Open `/etc/selinux/config` file and set `SELINUX=disabled`.

```sh
[steve@stapp02 ~]$ sudo vi /etc/selinux/config
```

## References
 [Disable SElinux](https://linuxize.com/post/how-to-disable-selinux-on-centos-7/)
