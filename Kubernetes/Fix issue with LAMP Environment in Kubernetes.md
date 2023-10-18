## Task
One of the DevOps team member was trying to install a WordPress website on a LAMP stack which is essentially deployed on Kubernetes cluster. It was working well and we could see the installation page a few hours ago. However something is messed up with the stack now due to a website went down. Please look into the issue and fix it:

FYI, deployment name is lamp-wp and its using a service named lamp-service. The Apache is using http default port and nodeport is 30008. From the application logs it has been identified that application is facing some issues while connecting to the database in addition to other issues. Additionally, there are some environment variables associated with the pods like MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER, MYSQL_PASSWORD, MYSQL_HOST.

Also do not try to delete/modify any other existing components like deployment name, service name, types, labels etc.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Check the deployment settings. We can see that container `httpd-php-contaier` has port set to 80.
```sh
thor@jump_host ~$ kubectl describe deployment/lamp-wp 
Name:               lamp-wp
Namespace:          default
CreationTimestamp:  Wed, 18 Oct 2023 08:04:26 +0000
Labels:             app=lamp
Annotations:        deployment.kubernetes.io/revision: 1
Selector:           app=lamp,tier=frontend
Replicas:           1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:       Recreate
MinReadySeconds:    0
Pod Template:
  Labels:  app=lamp
           tier=frontend
  Containers:
   httpd-php-container:
    Image:      webdevops/php-apache:alpine-3-php7
    Port:       80/TCP
```
Now check if service has correct settings. We can see that service has setup port 8080 as TrgetPort, so we need to change it to 80.
```sh
thor@jump_host ~$ kubectl describe service/lamp-service 
Name:                     lamp-service
Namespace:                default
Labels:                   app=lamp
Annotations:              <none>
Selector:                 app=lamp,tier=frontend
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.96.135.91
IPs:                      10.96.135.91
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  30008/TCP
Endpoints:                10.244.0.6:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```
Edit this service and change 8080 to 80.
```sh
thor@jump_host ~$ kubectl edit service/lamp-service 
```
Now connect to the httpd-php-container.
```sh
thor@jump_host ~$ kubectl exec --stdin --tty lamp-wp-56c7c454fc-ff9w8 -- /bin/bash
```
Check if the file index.php is correct. If not change any typos to state that is shown below.
```sh
bash-4.3# cat /app/index.php 
<?php
$dbname = $_ENV["MYSQL_DATABASE"];
$dbuser = $_ENV["MYSQL_USER"];
$dbpass = $_ENV["MYSQL_PASSWORD"];
$dbhost = $_ENV["MYSQL_HOST"];

$connect = mysqli_connect($dbhost, $dbuser, $dbpass) or die("Unable to Connect to '$dbhost'");

$test_query = "SHOW TABLES FROM $dbname";
$result = mysqli_query($test_query);

if ($result->connect_error) {
   die("Connection failed: " . $conn->connect_error);
}
  echo "Connected successfully";
```


## References

[Get a Shell to a Running Container](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)

[A visual guide on troubleshooting Kubernetes deployments](https://learnk8s.io/troubleshooting-deployments)
