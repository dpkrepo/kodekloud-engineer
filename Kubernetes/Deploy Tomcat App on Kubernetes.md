## Task
A new java-based application is ready to be deployed on a Kubernetes cluster. The development team had a meeting with the DevOps team to share the requirements and application scope. The team is ready to setup an application stack for it under their existing cluster. Below you can find the details for this:

Create a namespace named tomcat-namespace-datacenter.

Create a deployment for tomcat app which should be named as tomcat-deployment-datacenter under the same namespace you created. Replica count should be 1, the container should be named as tomcat-container-datacenter, its image should be gcr.io/kodekloud/centos-ssh-enabled:tomcat and its container port should be 8080.

Create a service for tomcat app which should be named as tomcat-service-datacenter under the same namespace you created. Service type should be NodePort and nodePort should be 32227.

Before clicking on Check button please make sure the application is up and running.

You can use any labels as per your choice.

Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.
## Solution
Create a new namespace named `tomcat-namespace-datacenter`.

```sh
thor@jump_host ~$ kubectl create namespace tomcat-namespace-datacenter
namespace/tomcat-namespace-datacenter created
```

Create a yaml file.

```sh
thor@jump_host ~$ vi tomcat.yaml
```

Define a specification of the deployment and the service.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deployment-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tomcat
  template:
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
        - name: tomcat-container-datacenter
          image: gcr.io/kodekloud/centos-ssh-enabled:tomcat
          ports:
            - containerPort: 8080


---

apiVersion: v1
kind: Service
metadata:
  name: tomcat-service-datacenter
spec:
  type: NodePort
  selector:
    app: tomcat
  ports:
    - port: 8080
      nodePort: 32227
```

Create the deployment and the servie.
```sh
thor@jump_host ~$ kubectl apply -f tomcat.yaml -n tomcat-namespace-datacenter deployment.apps/tomcat-deployment-datacenter created
service/tomcat-service-datacenter created
```

Check if pods are running.
```sh
thor@jump_host ~$ kubectl get pods -n tomcat-namespace-datacenter NAME                                            READY   STATUS    RESTARTS   AGE
tomcat-deployment-datacenter-6c696b4c7f-2nd5s   1/1     Running   0          2m12s
```

Tomacat app should be running.
## References

[NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport)

[Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
