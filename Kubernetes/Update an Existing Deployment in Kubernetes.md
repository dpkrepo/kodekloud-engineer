# Task
There is an application deployed on Kubernetes cluster. Recently, the Nautilus application development team developed a new version of the application that needs to be deployed now. As per new updates some new changes need to be made in this existing setup. So update the deployment and service as per details mentioned below:

We already have a deployment named nginx-deployment and service named nginx-service. Some changes need to be made in this deployment and service, make sure not to delete the deployment and service.

1.) Change the service nodeport from 30008 to 32165

2.) Change the replicas count from 1 to 5

3.) Change the image from nginx:1.18 to nginx:latest

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Update the nodePort to 32165.

```sh
thor@jump_host ~$ kubectl patch svc nginx-service -p '{"spec": {"ports": [{"port": 80, "nodePort": 32165}]}}'
service/nginx-service patched
```
Change the replicas to 5.
```sh
thor@jump_host ~$ kubectl scale deployment nginx-deployment --replicas=5
deployment.apps/nginx-deployment scaled
```
Change the image to `nginx:latest`
```sh
thor@jump_host ~$ kubectl set image deployment/nginx-deployment nginx-container=nginx:latest
deployment.apps/nginx-deployment image updated
```
## References
[Update API Objects in Place Using kubectl patch](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/update-api-object-kubectl-patch/)

[kubectl patch](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_patch/)

[kubectl scale](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_scale/)

[Updating a Deployment - kubectl set image](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment)
