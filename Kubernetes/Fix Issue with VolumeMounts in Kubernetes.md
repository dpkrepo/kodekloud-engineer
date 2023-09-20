# Test
We deployed a Nginx and PHP-FPM based setup on Kubernetes cluster last week and it had been working fine so far. This morning one of the team members made a change somewhere which caused some issues, and it stopped working. Please look into the issue and fix it:

The pod name is nginx-phpfpm and configmap name is nginx-config. Figure out the issue and fix the same.

Once issue is fixed, copy /home/thor/index.php file from the jump host to the nginx-container under nginx document root and you should be able to access the website using Website button on top bar.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution


Check configuration of the `nginx-config`. We can see that in nginx configuration root directory is set to `/var/www/html`.
```sh
thor@jump_host ~$ kubectl describe configmap nginx-config
Name:         nginx-config
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
nginx.conf:
----
events {
}
http {
  server {
    listen 8099 default_server;
    listen [::]:8099 default_server;

    # Set nginx to serve files from the shared volume!
    root /var/www/html;
    index  index.html index.htm index.php;
    server_name _;
    location / {
      try_files $uri $uri/ =404;
    }
    location ~ \.php$ {
      include fastcgi_params;
      fastcgi_param REQUEST_METHOD $request_method;
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      fastcgi_pass 127.0.0.1:9000;
    }
  }
}


BinaryData
====

Events:  <none>
```

Check where is mounted volume in container.

```sh
thor@jump_host ~$ kubectl get pod nginx-phpfpm -o yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"php-app"},"name":"nginx-phpfpm","namespace":"default"},"spec":{"containers":[{"image":"php:7.2-fpm-alpine","name":"php-fpm-container","volumeMounts":[{"mountPath":"/usr/share/nginx/html","name":"shared-files"}]},{"image":"nginx:latest","name":"nginx-container","volumeMounts":[{"mountPath":"/var/www/html","name":"shared-files"},{"mountPath":"/etc/nginx/nginx.conf","name":"nginx-config-volume","subPath":"nginx.conf"}]}],"volumes":[{"emptyDir":{},"name":"shared-files"},{"configMap":{"name":"nginx-config"},"name":"nginx-config-volume"}]}}
  creationTimestamp: "2023-09-20T13:13:51Z"
  labels:
    app: php-app
  name: nginx-phpfpm
  namespace: default
  resourceVersion: "1273"
  uid: 8dab9578-b5dc-4c91-98ea-d3513ad12c1a
spec:
  containers:
  - image: php:7.2-fpm-alpine
    imagePullPolicy: IfNotPresent
    name: php-fpm-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /usr/share/nginx/html
      name: shared-files
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-pbgxm
      readOnly: true
  - image: nginx:latest
    imagePullPolicy: Always
    name: nginx-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/www/html
      name: shared-files
    - mountPath: /etc/nginx/nginx.conf
      name: nginx-config-volume
      subPath: nginx.conf
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-pbgxm
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: kodekloud-control-plane
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: shared-files
  - configMap:
      defaultMode: 420
      name: nginx-config
    name: nginx-config-volume
  - name: kube-api-access-pbgxm
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2023-09-20T13:13:51Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2023-09-20T13:14:04Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2023-09-20T13:14:04Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2023-09-20T13:13:51Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://484a777ff935a6c521a3846473bbfe072374e07cbc9d7551ef98961dc61d3b82
    image: docker.io/library/nginx:latest
    imageID: docker.io/library/nginx@sha256:f84caae4439aa1d6b8b645f9bb0557d2ad7b8f654c9f360f24f48eb1363f9deb
    lastState: {}
    name: nginx-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2023-09-20T13:14:04Z"
  - containerID: containerd://ac8383d7e80685ecf6013b5c5cb7615a7ee9c495f80269888a6808b5478d8833
    image: docker.io/library/php:7.2-fpm-alpine
    imageID: docker.io/library/php@sha256:2e2d92415f3fc552e9a62548d1235f852c864fcdc94bcf2905805d92baefc87f
    lastState: {}
    name: php-fpm-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2023-09-20T13:13:56Z"
  hostIP: 172.17.0.2
  phase: Running
  podIP: 10.244.0.5
  podIPs:
  - ip: 10.244.0.5
  qosClass: BestEffort
  startTime: "2023-09-20T13:13:51Z"
```

We can see that volume is mouted in `/usr/share/nginx/html`, so we need to change it to `/var/www/html`.

Create a yaml file with current pod confiiguration.
```sh
thor@jump_host ~$ kubectl get pod nginx-phpfpm -o yaml > nginx-phpfpm.yaml
```

Replace all instances of `/usr/share/nginx/html` to `/var/www/html` in this file.
```sh
thor@jump_host ~$ sed -i 's@/usr/share/nginx/html@/var/www/html@g' yourfile.yml
```
Force replacment of the pod.
```sh
thor@jump_host ~$ kubectl replace -f nginx-phpfpm.yaml --force
pod "nginx-phpfpm" deleted
pod/nginx-phpfpm replaced
```

Copy `/home/thor/index.php` to `nginx-container`. 
```sh
thor@jump_host ~$ kubectl cp /home/thor/index.php default/nginx-phpfpm:/var/www/html -c nginx-container
```

## References

[kube replace](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_replace/)

[Debug Pods](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)
