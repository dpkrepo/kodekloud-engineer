## Task
Some of the Nautilus team developers are developing a static website and they want to deploy it on Kubernetes cluster. They want it to be highly available and scalable. Therefore, based on the requirements, the DevOps team has decided to create a deployment for it with multiple replicas. Below you can find more details about it:

Create a deployment using nginx image with latest tag only and remember to mention the tag i.e nginx:latest. Name it as nginx-deployment. The container should be named as nginx-container, also make sure replica counts are 3.

Create a NodePort type service named nginx-service. The nodePort should be 30011.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a yaml file.

```sh
thor@jump_host ~$ vi nginx-deployment.yaml
```

Write a deployment and service specification.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-container
  template:
    metadata:
      labels:
        app: nginx-container
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx-container
  ports:
    - port: 80
      nodePort: 30011
```

Check if pods are running.

```sh
thor@jump_host ~$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
nginx-deployment-bcbc899bb-cq454   1/1     Running   0          2m47s
nginx-deployment-bcbc899bb-qdwl7   1/1     Running   0          2m32s
nginx-deployment-bcbc899bb-qjwn5   1/1     Running   0          2m30s
```
## References

[Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

[Services](https://kubernetes.io/docs/concepts/services-networking/service/)
