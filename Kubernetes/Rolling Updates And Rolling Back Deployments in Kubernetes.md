## Task
There is a production deployment planned for next week. The Nautilus DevOps team wants to test the deployment update and rollback on Dev environment first so that they can identify the risks in advance. Below you can find more details about the plan they want to execute.

Create a namespace devops. Create a deployment called httpd-deploy under this new namespace, It should have one container called httpd, use httpd:2.4.28 image and 2 replicas. The deployment should use RollingUpdate strategy with maxSurge=1, and maxUnavailable=2. Also create a NodePort type service named httpd-service and expose the deployment on nodePort: 30008.

Now upgrade the deployment to version httpd:2.4.43 using a rolling update.

Finally, once all pods are updated undo the recent update and roll back to the previous/original version.

Note:

a. The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

b. Please make sure you only use the specified image(s) for this deployment and as per the sequence mentioned in the task description. If you mistakenly use a wrong image and fix it later, that will also distort the revision history which can eventually fail this task.
## Solution
Create the `devops` namespace.

```sh
thor@jump_host ~$ kubectl create namespace devops
namespace/devops created
```
Create a yaml file.

```sh
thor@jump_host ~$ vi httpd-deploy.yaml
```

Define deployment and NodePort.
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: httpd
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
        - name: httpd
          image: httpd:2.4.28

---

apiVersion: v1
kind: Service
metadata:
  name: httpd-service
spec:
  type: NodePort
  selector:
    app: httpd
  ports:
    - port: 80
      nodePort: 30008
```

Create the deployment and the NodePort.

```sh
thor@jump_host ~$ kubectl apply -f httpd-deploy.yaml -n devops
deployment.apps/httpd-deploy unchanged
service/httpd-service created
```
Check the current image of the `httpd` container.

```sh
thor@jump_host ~$ kubectl describe deployment httpd-deploy -n devops | grep "Image:" | awk '{print $2}'
httpd:2.4.28
```

Perform a update to `2.4.43` version.

```sh
thor@jump_host ~$ kubectl set image deployments/httpd-deploy httpd=httpd:2.4.43 -n devops
deployment.apps/httpd-deploy image updated
```

Check the image again.

```sh
thor@jump_host ~$ kubectl describe deployment httpd-deploy -n devops | grep "Image:" | awk '{print $2}'
httpd:2.4.43
```

Now undo the update.

```sh
thor@jump_host ~$ kubectl rollout undo -n devops deployment/httpd-deploy
deployment.apps/httpd-deploy rolled back
```

Check the image version.

```sh
thor@jump_host ~$ kubectl describe deployment httpd-deploy -n devops | grep "Image:" | awk '{print $2}'
httpd:2.4.28
```

## References

[Rolling Update Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

[kubectl rollback undo](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_rollout_undo/)
