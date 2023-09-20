# Task 
The Nautilus DevOps team want to create a time check pod in a particular Kubernetes namespace and record the logs. This might be initially used only for testing purposes, but later can be implemented in an existing cluster. Please find more details below about the task and perform it.

Create a pod called time-check in the devops namespace. This pod should run a container called time-check, container should use the busybox image with latest tag only and remember to mention tag i.e busybox:latest.

Create a config map called time-config with the data TIME_FREQ=2 in the same namespace.

The time-check container should run the command: while true; do date; sleep $TIME_FREQ;done and should write the result to the location /opt/data/time/time-check.log. Remember you will also need to add an environmental variable TIME_FREQ in the container, which should pick value from the config map TIME_FREQ key.

Create a volume log-volume and mount the same on /opt/data/time within the container.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
Create a namespace named `devops`.

```sh
thor@jump_host ~$ kubectl create namespace devops
namespace/devops created
```

Create a file for ConfgiMap and Pod.
```sh
thor@jump_host ~$ vi time-check.yaml
```
```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: time-config
data:
  TIME_FREQ: '2'

---

apiVersion: v1
kind: Pod
metadata:
  name: time-check
spec:
  containers:
  - name: time-check
    image: busybox:latest
    args:
    - /bin/sh
    - -c
    - |
      while true; do date >> /opt/data/time/time-check.log; sleep $TIME_FREQ; done
    env:
      - name: TIME_FREQ
        valueFrom:
          configMapKeyRef:
            name: time-config
            key: TIME_FREQ
    volumeMounts:
    - name: log-volume
      mountPath: /opt/data/time
  volumes:
  - name: log-volume
    emptyDir: {}
```

Create the ConfigMap and the Pod.
```sh
thor@jump_host ~$ kubectl apply -f time-check.yaml -n devops
configmap/time-config created
pod/time-check created
```
## References

[ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/)

[Define a Command and Arguments for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/)

[Configure a Pod to Use a ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)

[Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
