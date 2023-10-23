## Task

The Nautilus DevOps team want to deploy a static website on Kubernetes cluster. They are going to use Nginx, phpfpm and MySQL for the database. The team had already gathered the requirements and now they want to make this website live. Below you can find more details:

Create some secrets for MySQL.

Create a secret named mysql-root-pass wih key/value pairs as below:

name: password
value: R00t

Create a secret named mysql-user-pass with key/value pairs as below:

name: username
value: kodekloud_rin

name: password
value: YchZHRcLkL

Create a secret named mysql-db-url with key/value pairs as below:

name: database
value: kodekloud_db8

Create a secret named mysql-host with key/value pairs as below:

name: host
value: mysql-service

Create a config map php-config for php.ini with variables_order = "EGPCS" data.

Create a deployment named lemp-wp.

Create two containers under it. First container must be nginx-php-container using image webdevops/php-nginx:alpine-3-php7 and second container must be mysql-container from image mysql:5.6. Mount php-config configmap in nginx container at /opt/docker/etc/php/php.ini location.

5) Add some environment variables for both containers:

MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER, MYSQL_PASSWORD and MYSQL_HOST. Take their values from the secrets you created. Please make sure to use env field (do not use envFrom) to define the name-value pair of environment variables.

6) Create a node port type service lemp-service to expose the web application, nodePort must be 30008.

7) Create a service for mysql named mysql-service and its port must be 3306.

We already have a /tmp/index.php file on jump_host server.

Copy this file into the nginx container under document root i.e /app and replace the dummy values for mysql related variables with the environment variables you have set for mysql related parameters. Please make sure you do not hard code the mysql related details in this file, you must use the environment variables to fetch those values.

Once done, you must be able to access this website using Website button on the top bar, please note that you should see Connected successfully message while accessing this page.

Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create secrets.
```sh
thor@jump_host ~$ kubectl create secret generic mysql-root-pass --from-literal=password=R00t
secret/mysql-root-pass created
thor@jump_host ~$ kubectl create secret generic mysql-user-pass --from-literal=username=kodekloud_rin --from-literal=password=YchZHRcLkL
secret/mysql-user-pass created
thor@jump_host ~$ kubectl create secret generic mysql-db-url --from-literal=database=kodekloud_db8
secret/mysql-db-url created
thor@jump_host ~$ kubectl create secret generic mysql-host --from-literal=host=mysql-service
secret/mysql-host created
```

Creat a config map.

```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: php-config
data:
  php.ini: |
     variables_order = "EGPCS"
```

Create a deployment.


```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lemp-wp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: lemp-wp
  template:
    metadata:
      labels:
        app: lemp-wp
    spec:
      containers:
        - name: nginx-php-container
          image: webdevops/php-nginx:alpine-3-php7
          volumeMounts:
            - name: php-config-volume
              mountPath: /opt/docker/etc/php/php.ini
              subPath: php.ini
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-root-pass
                  key: password
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  name: mysql-db-url
                  key: database
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: username
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: password
            - name: MYSQL_HOST
              valueFrom:
                secretKeyRef:
                  name: mysql-host
                  key: host
        - name: mysql-container
          image: mysql:5.6
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-root-pass
                  key: password
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  name: mysql-db-url
                  key: database
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: username
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: password
            - name: MYSQL_HOST
              valueFrom:
                secretKeyRef:
                  name: mysql-host
                  key: host
      volumes:
        - name: php-config-volume
          configMap:
            name: php-config
```

Create services.

```yml
apiVersion: v1
kind: Service
metadata:
  name: lemp-service
spec:
  type: NodePort
  selector:
    app: lemp-wp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008


---

apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  selector:
    app: lemp-wp
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
```

Copy the index.php file into the nginx container.

```sh
thor@jump_host ~$ kubectl cp /tmp/index.php lemp-wp-56cf9b4485-svq6v:/app -c nginx-php-container
```

## References

[kubectl cp](https://www.mankier.com/1/kubectl-cp)

[Configure a Pod to Use a ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)

[Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

[kubectl create secret generic](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_create_secret_generic/)
