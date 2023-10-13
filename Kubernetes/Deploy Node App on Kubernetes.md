## Task
The Nautilus development team has completed development of one of the node applications, which they are planning to deploy on a Kubernetes cluster. They recently had a meeting with the DevOps team to share their requirements. Based on that, the DevOps team has listed out the exact requirements to deploy the app. Find below more details:

Create a deployment using gcr.io/kodekloud/centos-ssh-enabled:node image, replica count must be 2.

Create a service to expose this app, the service type must be NodePort, targetPort must be 8080 and nodePort should be 30012.

Make sure all the pods are in Running state after the deployment.

You can check the application by clicking on NodeApp button on top bar.

You can use any labels as per your choice.

Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a yaml file.
```sh
thor@jump_host ~$ vi node.yaml
```

Define a specification of the deployment and the service.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node
  template:
    metadata:
      labels:
        app: node
    spec:
      containers:
        - name: node-container
          image: gcr.io/kodekloud/centos-ssh-enabled:node
          ports:
            - containerPort: 8080


---

apiVersion: v1
kind: Service
metadata:
  name: node-service
spec:
  type: NodePort
  selector:
    app: node
  ports:
    - port: 8080
      nodePort: 30012
```

Create the deployment and the service.

```sh
thor@jump_host ~$ kubectl apply -f node.yaml 
deployment.apps/node-deployment created
service/node-service created
```

Check if pods are running.

```sh
thor@jump_host ~$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
node-deployment-5fc7855655-5cfnn   1/1     Running   0          85s
node-deployment-5fc7855655-w42z2   1/1     Running   0          85s
```
Node app should be running.
## References

[NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport)

[Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
