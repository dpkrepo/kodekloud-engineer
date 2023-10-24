## Task
There is an iron gallery app that the Nautilus DevOps team was developing. They have recently customized the app and are going to deploy the same on the Kubernetes cluster. Below you can find more details:

Create a namespace iron-namespace-datacenter

Create a deployment iron-gallery-deployment-datacenter for iron gallery under the same namespace you created.

:- Labels run should be iron-gallery.

:- Replicas count should be 1.

:- Selector's matchLabels run should be iron-gallery.

:- Template labels run should be iron-gallery under metadata.

:- The container should be named as iron-gallery-container-datacenter, use kodekloud/irongallery:2.0 image ( use exact image name / tag ).

:- Resources limits for memory should be 100Mi and for CPU should be 50m.

:- First volumeMount name should be config, its mountPath should be /usr/share/nginx/html/data.

:- Second volumeMount name should be images, its mountPath should be /usr/share/nginx/html/uploads.

:- First volume name should be config and give it emptyDir and second volume name should be images, also give it emptyDir.

Create a deployment iron-db-deployment-datacenter for iron db under the same namespace.

:- Labels db should be mariadb.

:- Replicas count should be 1.

:- Selector's matchLabels db should be mariadb.

:- Template labels db should be mariadb under metadata.

:- The container name should be iron-db-container-datacenter, use kodekloud/irondb:2.0 image ( use exact image name / tag ).

:- Define environment, set MYSQL_DATABASE its value should be database_apache, set MYSQL_ROOT_PASSWORD and MYSQL_PASSWORD value should be with some complex passwords for DB connections, and MYSQL_USER value should be any custom user ( except root ).

:- Volume mount name should be db and its mountPath should be /var/lib/mysql. Volume name should be db and give it an emptyDir.

Create a service for iron db which should be named iron-db-service-datacenter under the same namespace. Configure spec as selector's db should be mariadb. Protocol should be TCP, port and targetPort should be 3306 and its type should be ClusterIP.

Create a service for iron gallery which should be named iron-gallery-service-datacenter under the same namespace. Configure spec as selector's run should be iron-gallery. Protocol should be TCP, port and targetPort should be 80, nodePort should be 32678 and its type should be NodePort.

Note:

We don't need to make connection b/w database and front-end now, if the installation page is coming up it should be enough for now.

The kubectl on jump_host has been configured to work with the kubernetes cluster.
## Solution
Create a namespace.

```sh
thor@jump_host ~$ kubectl create namespace iron-namespace-datacenter
namespace/iron-namespace-datacenter created
```

Create a deployment named `iron-gallery-deployment-datacenter`
```yml
piVersion: apps/v1
kind: Deployment
metadata:
  name: iron-gallery-deployment-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      run: iron-gallery
  template:
    metadata:
      labels:
        run: iron-gallery
    spec:
      containers:
        - name: iron-gallery-container-datacenter
          image: kodekloud/irongallery:2.0
          resources:
            limits:
              memory: "100Mi"
              cpu: "50m"
          volumeMounts:
            - name: config
              mountPath: /usr/share/nginx/html/data
            - name: images
              mountPath: /usr/share/nginx/html/uploads
      volumes:
        - name: config
          emptyDir: {}
        - name: images
          emptyDir: {}
```

```sh
thor@jump_host ~$ kubectl apply -f iron-gallery-deployment-datacenter.yaml -n iron-namespace-datacenter 
```

Create a deployment named `iron-db-deployment-datacenter`.
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-db-deployment-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      db: mariadb
  template:
    metadata:
      labels:
        db: mariadb
    spec:
      containers:
        - name: iron-db-container-datacenter
          image: kodekloud/irondb:2.0
          env:
            - name: MYSQL_DATABASE
              value: "database_apache"
            - name: MYSQL_ROOT_PASSWORD
              value: "P@ssw0rd1"
            - name: MYSQL_PASSWORD
              value: "P@ssw0rd1"
            - name: MYSQL_USER
              value: "adam"
          volumeMounts:
            - name: db
              mountPath: /var/lib/mysql
      volumes:
        - name: db
          emptyDir: {}
```

```sh
thor@jump_host ~$ kubectl apply -f iron-db-deployment-datacenter.yaml -n iron-namespace-datacenter 
deployment.apps/iron-db-deployment-datacenter created
```

Create services.

```yml
apiVersion: v1
kind: Service
metadata:
  name: iron-db-service-datacenter
spec:
  selector:
    db: mariadb
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306

---

apiVersion: v1
kind: Service
metadata:
  name: iron-gallery-service-datacenter
spec:
  type: NodePort
  selector:
    run: iron-gallery
  ports:
    - port: 80
      targetPort: 80
      nodePort: 32678
```

```sh
thor@jump_host ~$ kubectl apply -f services.yaml -n iron-namespace-datacenter  
service/iron-db-service-datacenter created
service/iron-gallery-service-datacenter created
```

## References

[Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

[Define an environment variable for a container](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)
