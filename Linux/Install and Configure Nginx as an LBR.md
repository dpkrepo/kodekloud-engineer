## Task
Day by day traffic is increasing on one of the websites managed by the Nautilus production support team. Therefore, the team has observed a degradation in website performance. Following discussions about this issue, the team has decided to deploy this application on a high availability stack i.e on Nautilus infra in Stratos DC. They started the migration last month and it is almost done, as only the LBR server configuration is pending. Configure LBR server as per the information given below:



a. Install nginx on LBR (load balancer) server.


b. Configure load-balancing with the an http context making use of all App Servers.


c. Make sure you do not update the apache port that is already defined in the apache configuration on all app servers, also make sure apache service is up and running on all app servers.


d. Once done, you can access the website using StaticApp button on the top bar.
## Solution 
1. Check OS version and install nginx.
```sh
   [root@stlb01 ~]# cat /etc/os-release 
NAME="CentOS Stream"
VERSION="8"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="8"
PLATFORM_ID="platform:el8"
PRETTY_NAME="CentOS Stream 8"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:8"
HOME_URL="https://centos.org/"
BUG_REPORT_URL="https://bugzilla.redhat.com/"
REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux 8"
REDHAT_SUPPORT_PRODUCT_VERSION="CentOS Stream"
```

```sh
[root@stlb01 ~]# yum install nginx -y
```

2. Edit /etc/nginx/nginx.conf file.

   Add backend servers to the nginx configuration file.

   ```
    upstream backend {
        server stapp01.stratos.xfusioncorp.com:5000;
        server stapp02.stratos.xfusioncorp.com:5000;
        server stapp03.stratos.xfusioncorp.com:5000;
    }
   ```

In `server` section add below lines of code.

```
        location / {
            proxy_pass http://backend;
        }
```

3. Start nginx service.

```sh
   [root@stlb01 ~]# systemctl start nginx
[root@stlb01 ~]# systemctl status nginx
● nginx.service - The nginx HTTP and reverse proxy server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
   Active: active (running) since Sun 2024-06-02 12:29:07 UTC; 4s ago
   ```
## References

[HTTP Load Balancing](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/)
