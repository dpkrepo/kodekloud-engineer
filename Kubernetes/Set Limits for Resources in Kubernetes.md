# Task
Recently some of the performance issues were observed with some applications hosted on Kubernetes cluster. The Nautilus DevOps team has observed some resources constraints, where some of the applications are running out of resources like memory, cpu etc., and some of the applications are consuming more resources than needed. Therefore, the team has decided to add some limits for resources utilization. Below you can find more details.

Create a pod named httpd-pod and a container under it named as httpd-container, use httpd image with latest tag only and remember to mention tag i.e httpd:latest and set the following limits:

Requests: Memory: 15Mi, CPU: 100m

Limits: Memory: 20Mi, CPU: 100m

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a yaml file for pod.

```sh
thor@jump_host ~$ vi httpd-pod.yaml
```
```yml
---
apiVersion: v1
kind: Pod
metadata:
  name: frontend
spec:
  containers:
  - name: app
    image: images.my-company.example/app:v4
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

Save the file and run the pod.

```sh
thor@jump_host ~$ kubectl apply -f httpd-pod.yaml 
pod/httpd-pod created
```
Check if requests and limits are set for the `httpd-pod` pod.
```sh
thor@jump_host ~$ kubectl describe pod httpd-pod
Name:             httpd-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Wed, 20 Sep 2023 06:49:16 +0000
Labels:           <none>
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  httpd-container:
    Container ID:   containerd://3de9e41993548503ab43bb675586a553fe63d2277f61507c6554a21f2f64083a
    Image:          httpd:latest
    Image ID:       docker.io/library/httpd@sha256:aa9b4711bf5bfab3288bbe3126c5b86796d2f06f9e4fbaf68b8aea57f72f50fb
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 20 Sep 2023 06:49:25 +0000
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     100m
      memory:  20Mi
    Requests:
      cpu:        100m
      memory:     15Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-4lnwq (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-4lnwq:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  3m3s   default-scheduler  Successfully assigned default/httpd-pod to kodekloud-control-plane
  Normal  Pulling    3m2s   kubelet            Pulling image "httpd:latest"
  Normal  Pulled     2m55s  kubelet            Successfully pulled image "httpd:latest" in 7.276101955s (7.276117618s including waiting)
  Normal  Created    2m55s  kubelet            Created container httpd-container
  Normal  Started    2m54s  kubelet            Started container httpd-container
```
## References

[Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
