
```
thor@jump_host ~$ kubectl get namespace
NAME                 STATUS   AGE
default              Active   45m
kube-node-lease      Active   45m
kube-public          Active   45m
kube-system          Active   45m
local-path-storage   Active   44m
```

```
thor@jump_host ~$ kubectl get pods
No resources found in default namespace.
```

```
thor@jump_host ~$ kubectl create namespace nautilus
namespace/nautilus created
```

```
thor@jump_host ~$ kubectl create -f /tmp/time.yaml 
configmap/time-config created
pod/time-check created
```

```
thor@jump_host ~$ kubectl get pods -n nautilus
NAME         READY   STATUS    RESTARTS   AGE
time-check   1/1     Running   0          38s
```
