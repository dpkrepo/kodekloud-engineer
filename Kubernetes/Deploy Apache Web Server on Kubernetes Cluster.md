## Task
There is an application that needs to be deployed on Kubernetes cluster under Apache web server. The Nautilus application development team has asked the DevOps team to deploy it. We need to develop a template as per requirements mentioned below:

Create a namespace named as httpd-namespace-nautilus.

Create a deployment named as httpd-deployment-nautilus under newly created namespace. For the deployment use httpd image with latest tag only and remember to mention the tag i.e httpd:latest, and make sure replica counts are 2.

Create a service named as httpd-service-nautilus under same namespace to expose the deployment, nodePort should be 30004.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster
## Solution
Create a namespace.

```sh
thor@jump_host ~$ kubectl create namespace httpd-namespace-nautilus
namespace/httpd-namespace-nautilus created
```

Create a deployment file.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deployment-nautilus
spec:
  replicas: 2
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
        - name: httpd-container
          image: httpd:latest

---

apiVersion: v1
kind: Service
metadata:
  name: httpd-service-nautilus
spec:
  type: NodePort
  selector:
    app: httpd
  ports:
    - port: 80
      nodePort: 30004                           
```

Apply deployment to the created namespace.

```sh
thor@jump_host ~$ kubectl apply -f httpd-deployment-nautilus.yaml -n httpd-namespace-nautilus 
deployment.apps/httpd-deployment-nautilus created
service/httpd-service-nautilus created
```

## References

[Deploy Apache Web Server on Kubernetes Cluster](https://www.devopstricks.in/deploy-apache-kubernetes/)
