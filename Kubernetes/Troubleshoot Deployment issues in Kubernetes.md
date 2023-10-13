## Task
Last week, the Nautilus DevOps team deployed a redis app on Kubernetes cluster, which was working fine so far. This morning one of the team members was making some changes in this existing setup, but he made some mistakes and the app went down. We need to fix this as soon as possible. Please take a look.

The deployment name is redis-deployment. The pods are not in running state right now, so please look into the issue and fix the same.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
View the specification of the deployment.

```sh
thor@jump_host ~$ kubectl describe deployment redis-deployment 
Name:                   redis-deployment
Namespace:              default
CreationTimestamp:      Fri, 13 Oct 2023 11:42:34 +0000
Labels:                 app=redis
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=redis
Replicas:               1 desired | 1 updated | 1 total | 0 available | 1 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=redis
  Containers:
   redis-container:
    Image:      redis:alpin
    Port:       6379/TCP
    Host Port:  0/TCP
    Requests:
      cpu:        300m
    Environment:  <none>
    Mounts:
      /redis-master from config (rw)
      /redis-master-data from data (rw)
  Volumes:
   data:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
   config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      redis-conig
    Optional:  false
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      False   MinimumReplicasUnavailable
  Progressing    True    ReplicaSetUpdated
OldReplicaSets:  <none>
NewReplicaSet:   redis-deployment-54cdf4f76d (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  70s   deployment-controller  Scaled up replica set redis-deployment-54cdf4f76d to 1
```

And we can see that there is a typo in image name. Instead of `redis:alpin` should be `redis:alpine`. Also we can see that there is another typo in the name of ConfigMap. Should be `redis-config` instead of `redis-conig`

To change the image in the container we can use this command:

```sh
thor@jump_host ~$ kubectl set image deployment/redis-deployment redis-container=redis:alpine
deployment.apps/redis-deployment image updated
```

To change ConfigMap name we can edit the deployment and change name to the correct value.

```sh
thor@jump_host ~$ kubectl edit deployment redis-deployment 
deployment.apps/redis-deployment edited
```

```yml
      - configMap:
          defaultMode: 420
          name: redis-config
```


And pod should be now running.

```sh
thor@jump_host ~$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
redis-deployment-7c8d4f6ddf-zfh89   1/1     Running   0          4m13s
```
## References

[A visual guide on troubleshooting Kubernetes deployments](https://learnk8s.io/troubleshooting-deployments)
