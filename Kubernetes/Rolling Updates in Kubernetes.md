# Task
We have an application running on Kubernetes cluster using nginx web server. The Nautilus application development team has pushed some of the latest changes and those changes need be deployed. The Nautilus DevOps team has created an image nginx:1.18 with the latest changes.

Perform a rolling update for this application and incorporate nginx:1.18 image. The deployment name is nginx-deployment

Make sure all pods are up and running after the update.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
Check the name of the container inside the pod.

```sh
thor@jump_host ~$ kubectl get deployment nginx-deployment -o=jsonpath='{.spec.template.spec.containers[*].name}'
nginx-container
```

Update image to `nginx:1.18`.

```sh
thor@jump_host ~$ kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18
deployment.apps/nginx-deployment image updated
```

Confirm that the update was successfully applied to the deployment.

```sh
thor@jump_host ~$ kubectl rollout status deployment/nginx-deployment
deployment "nginx-deployment" successfully rolled out
```
## References

[Performing a Rolling Update](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/)
