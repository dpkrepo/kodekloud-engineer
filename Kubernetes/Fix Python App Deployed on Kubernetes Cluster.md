## Task
One of the DevOps engineers was trying to deploy a python app on Kubernetes cluster. Unfortunately, due to some mis-configuration, the application is not coming up. Please take a look into it and fix the issues. Application should be accessible on the specified nodePort.

The deployment name is python-deployment-xfusion, its using poroko/flask-demo-appimage. The deployment and service of this app is already deployed.

nodePort should be 32345 and targetPort should be python flask app's default port.

Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.
## Solution
Check why pods are not running.

```sh
thor@jump_host ~$ kubectl describe pods
Name:             python-deployment-xfusion-5dcd4fff84-8qhdf
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Tue, 24 Oct 2023 07:25:15 +0000
Labels:           app=python_app
                  pod-template-hash=5dcd4fff84
Annotations:      <none>
Status:           Pending
IP:               10.244.0.5
IPs:
  IP:           10.244.0.5
Controlled By:  ReplicaSet/python-deployment-xfusion-5dcd4fff84
Containers:
  python-container-xfusion:
    Container ID:   
    Image:          poroko/flask-app-demo
    Image ID:       
    Port:           5000/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-q4gqp (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             False 
  ContainersReady   False 
  PodScheduled      True 
Volumes:
  kube-api-access-q4gqp:
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
  Type     Reason     Age                     From               Message
  ----     ------     ----                    ----               -------
  Normal   Scheduled  8m                      default-scheduler  Successfully assigned default/python-deployment-xfusion-5dcd4fff84-8qhdf to kodekloud-control-plane
  Normal   Pulling    6m30s (x4 over 8m)      kubelet            Pulling image "poroko/flask-app-demo"
  Warning  Failed     6m29s (x4 over 7m59s)   kubelet            Failed to pull image "poroko/flask-app-demo": rpc error: code = Unknown desc = failed to pull and unpack image "docker.io/poroko/flask-app-demo:latest": failed to resolve reference "docker.io/poroko/flask-app-demo:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     6m29s (x4 over 7m59s)   kubelet            Error: ErrImagePull
  Warning  Failed     6m16s (x6 over 7m59s)   kubelet            Error: ImagePullBackOff
  Normal   BackOff    2m54s (x20 over 7m59s)  kubelet            Back-off pulling image "poroko/flask-app-demo"
```

We can see that pod is failing due to incorrect image name. Image name should be `flask-demo-app` instead of `flask-app-demo`.
Update an image.

```sh
thor@jump_host ~$ kubectl set image deployments/python-deployment-xfusion python-container-xfusion=poroko/flask-demo-app
deployment.apps/python-deployment-xfusion image updated
```

And now pod is running.
```sh
thor@jump_host ~$ kubectl get pods
NAME                                         READY   STATUS    RESTARTS   AGE
python-deployment-xfusion-74f98d699b-xwcgc   1/1     Running   0          33s
```

Check services.

```sh
thor@jump_host ~$ kubectl describe service
Name:              kubernetes
Namespace:         default
Labels:            component=apiserver
                   provider=kubernetes
Annotations:       <none>
Selector:          <none>
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.96.0.1
IPs:               10.96.0.1
Port:              https  443/TCP
TargetPort:        6443/TCP
Endpoints:         172.17.0.2:6443
Session Affinity:  None
Events:            <none>


Name:                     python-service-xfusion
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=python_app
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.96.106.50
IPs:                      10.96.106.50
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  32345/TCP
Endpoints:                10.244.0.6:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

Flask default port should be `5000`, but in NodePort configuration is the `8080` port. We need to change port `8080` to `5000`.

Edit the `python-service-xfusion` service.
```sh
thor@jump_host ~$ kubectl edit service python-service-xfusion
```
And change to correct port.
```yml
  ports:
  - nodePort: 32345
    port: 5000
    protocol: TCP
    targetPort: 5000
```


## References

[Performing a Rolling Update](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/)

[kubectl edit](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_edit/)
