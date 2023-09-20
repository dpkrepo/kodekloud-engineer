# Task 
The Nautilus DevOps team has started practicing some pods and services deployment on Kubernetes platform, as they are planning to migrate most of their applications on Kubernetes. Recently one of the team members has been assigned a task to create a deployment as per details mentioned below:

Create a deployment named httpd to deploy the application httpd using the image httpd:latest (remember to mention the tag as well)

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a deployment named `httpd` using image `httpd:latest`.
```sh
thor@jump_host ~$ kubectl create deployment httpd --image=httpd:latest
deployment.apps/httpd created
```

Check if the deployment is running.

```sh
thor@jump_host ~$ kubectl get deployments
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
httpd   1/1     1            1           21s
```
## References

[Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

[Using kubectl to Create a Deployment](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/)
