# Task 
This morning the Nautilus DevOps team rolled out a new release for one of the applications. Recently one of the customers logged a complaint which seems to be about a bug related to the recent release. Therefore, the team wants to rollback the recent release.

There is a deployment named nginx-deployment; roll it back to the previous revision.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
Rollback the deployemnt to previous revision.

```sh
thor@jump_host ~$ kubectl rollout undo deployment/nginx-deployment
deployment.apps/nginx-deployment rolled back
```

Check if rollback was successful nad the pods are running.

```sh
thor@jump_host ~$ kubectl get deployment nginx-deployment
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   3/3     3            3           4m
```


## References

[Rolling Back to a Previous Revision](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-to-a-previous-revision)
