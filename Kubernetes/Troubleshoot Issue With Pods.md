# Task 
One of the junior DevOps team members was working on to deploy a stack on Kubernetes cluster. Somehow the pod is not coming up and its failing with some errors. We need to fix this as soon as possible. Please look into it.

There is a pod named webserver and the container under it is named as httpd-container. It is using image httpd:latest

There is a sidecar container as well named sidecar-container which is using ubuntu:latest image.

Look into the issue and fix it, make sure pod is in running state and you are able to access the app.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
```sh
thor@jump_host ~$ kubectl describe pod webserver 
Name:             webserver
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Wed, 20 Sep 2023 12:09:07 +0000
Labels:           app=web-app
Annotations:      <none>
Status:           Pending
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  httpd-container:
    Container ID:   
    Image:          httpd:latests
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/log/httpd from shared-logs (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-q4qjt (ro)
  sidecar-container:
    Container ID:  containerd://044aa922f7ab488308fbe8b96b53b661b26ea98623439548184bd01b1895bc14
    Image:         ubuntu:latest
    Image ID:      docker.io/library/ubuntu@sha256:aabed3296a3d45cede1dc866a24476c4d7e093aa806263c27ddaadbdce3c1054
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      while true; do cat /var/log/httpd/access.log /var/log/httpd/error.log; sleep 30; done
    State:          Running
      Started:      Wed, 20 Sep 2023 12:09:12 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/log/httpd from shared-logs (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-q4qjt (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             False 
  ContainersReady   False 
  PodScheduled      True 
Volumes:
  shared-logs:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  kube-api-access-q4qjt:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                  From               Message
  ----     ------     ----                 ----               -------
  Normal   Scheduled  2m20s                default-scheduler  Successfully assigned default/webserver to kodekloud-control-plane
  Normal   Pulling    2m19s                kubelet            Pulling image "ubuntu:latest"
  Normal   Pulled     2m15s                kubelet            Successfully pulled image "ubuntu:latest" in 4.204621695s (4.204634473s including waiting)
  Normal   Created    2m15s                kubelet            Created container sidecar-container
  Normal   Started    2m15s                kubelet            Started container sidecar-container
  Normal   Pulling    92s (x3 over 2m19s)  kubelet            Pulling image "httpd:latests"
  Warning  Failed     92s (x3 over 2m19s)  kubelet            Failed to pull image "httpd:latests": rpc error: code = NotFound desc = failed to pull and unpack image "docker.io/library/httpd:latests": failed to resolve reference "docker.io/library/httpd:latests": docker.io/library/httpd:latests: not found
  Warning  Failed     92s (x3 over 2m19s)  kubelet            Error: ErrImagePull
  Normal   BackOff    55s (x6 over 2m14s)  kubelet            Back-off pulling image "httpd:latests"
  Warning  Failed     55s (x6 over 2m14s)  kubelet            Error: ImagePullBackOff
```

We can see that there is a typo in image tag `httpd:latests` and it shoud be `httpd:latest`.

Update image for the `httpd-container`.
```sh
thor@jump_host ~$ kubectl set image pod/webserver httpd-container=httpd:latest 
pod/webserver image updated
```

And now both containers are running.

```sh
thor@jump_host ~$ kubectl get pod webserver
NAME        READY   STATUS    RESTARTS   AGE
webserver   2/2     Running   0          6m32s
```

## References

[Debug Pods](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)
