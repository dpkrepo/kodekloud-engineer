# Task 
The Nautilus DevOps team is planning to deploy some micro services on Kubernetes platform. The team has already set up a Kubernetes cluster and now they want set up some namespaces, deployments etc. Based on the current requirements, the team has shared some details as below:

Create a namespace named dev and create a POD under it; name the pod dev-nginx-pod and use nginx image with latest tag only and remember to mention tag i.e nginx:latest.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a namespace named `dev`.

```sh
thor@jump_host ~$ kubectl create namespace dev
namespace/dev created
```

Create a pod named `dev-nginx-pod` using `nginx:latest` image in `dev` namespace.
```sh
thor@jump_host ~$ kubectl run dev-nginx-pod --image=nginx:latest -n dev
pod/dev-nginx-pod created
```
Check if the pod is running in `dev` namespace.

```sh
thor@jump_host ~$ kubectl get pods -n dev
NAME            READY   STATUS    RESTARTS   AGE
dev-nginx-pod   1/1     Running   0          15s
```

## References

[Namespaces](https://kubernetes.io/docs/tasks/administer-cluster/namespaces-walkthrough/)

[kubectl create namespace](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_create_namespace/)

[kubectl run](https://jamesdefabia.github.io/docs/user-guide/pods/single-container/)
