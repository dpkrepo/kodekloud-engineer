## Task
We are working on an application that will be deployed on multiple containers within a pod on Kubernetes cluster. There is a requirement to share a volume among the containers to save some temporary data. The Nautilus DevOps team is developing a similar template to replicate the scenario. Below you can find more details about it.

Create a pod named volume-share-nautilus.

For the first container, use image debian with latest tag only and remember to mention the tag i.e debian:latest, container should be named as volume-container-nautilus-1, and run a sleep command for it so that it remains in running state. Volume volume-share should be mounted at path /tmp/news.

For the second container, use image debian with the latest tag only and remember to mention the tag i.e debian:latest, container should be named as volume-container-nautilus-2, and again run a sleep command for it so that it remains in running state. Volume volume-share should be mounted at path /tmp/apps.

Volume name should be volume-share of type emptyDir.

After creating the pod, exec into the first container i.e volume-container-nautilus-1, and just for testing create a file news.txt with any content under the mounted path of first container i.e /tmp/news.

The file news.txt should be present under the mounted path /tmp/apps on the second container volume-container-nautilus-2 as well, since they are using a shared volume.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a yaml file.
```sh
hor@jump_host ~$ vi shared-volume.yaml
```
This yaml file creates a pod with 2 containers and shared volume.
```yml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-nautilus
spec:

  volumes:
  - name: volume-share
    emptyDir: {}

  containers:

  - name: volume-container-nautilus-1
    image: debian:latest
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/news
    command: ["/bin/sh"]
    args: ["-c", "sleep 600"]

  - name: volume-container-nautilus-2
    image: debian:latest
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/apps
    command: ["/bin/sh"]
    args: ["-c", "sleep 600"]
```

Create the pod defined in this file.

```sh
thor@jump_host ~$ kubectl apply -f shared-volume.yaml
```
Check if containers are running.

```sh
thor@jump_host ~$ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
volume-share-nautilus   2/2     Running   0          7s
```

Open shell of the first container and create `news.txt` file under /tmp/news.

```sh
thor@jump_host ~$ kubectl exec -i -t volume-share-nautilus --container volume-container-nautilus-1 -- /bin/bash
root@volume-share-nautilus:/# touch /tmp/news/news.txt
```

Check on second container if the `news.txt` file is present in the /tmp/apps directory.

```sh
thor@jump_host ~$ kubectl exec -i -t volume-share-nautilus --container volume-container-nautilus-2 -- /bin/bash
root@volume-share-nautilus:/# ls /tmp/apps
news.txt
```
## References

[Communicate Between Containers in the Same Pod Using a Shared Volume](https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/)


[Get a Shell to a Running Container](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)
