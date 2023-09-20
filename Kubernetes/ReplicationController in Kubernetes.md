# Task
The Nautilus DevOps team wants to create a ReplicationController to deploy several pods. They are going to deploy applications on these pods, these applications need highly available infrastructure. Below you can find exact details, create the ReplicationController accordingly.

Create a ReplicationController using httpd image, preferably with latest tag, and name it as httpd-replicationcontroller.

Labels app should be httpd_app, and labels type should be front-end. The container should be named as httpd-container and also make sure replica counts are 3.


All pods should be running state after deployment.


Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a file for a ReplicationController.

```sh
thor@jump_host ~$ vi httpd-replicationcontroller.yaml
```
```yml
apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller
spec:
  replicas: 3
  selector:
    app: httpd_app
  template:
    metadata:
      name: httpd_app
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
```

Deploy the ReplicationController.

```sh
thor@jump_host ~$ kubectl apply -f httpd-replicationcontroller.yaml 
replicationcontroller/httpd-replicationcontroller created
```

Check if the pods are running.

```sh
thor@jump_host ~$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
httpd-replicationcontroller-4fdh7   1/1     Running   0          16s
httpd-replicationcontroller-5xbnz   1/1     Running   0          16s
httpd-replicationcontroller-9dt4m   1/1     Running   0          16s
```
## References

[ReplicationController](https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/)
