## Task
The Nautilus DevOps team is working on a Kubernetes template to deploy a web application on the cluster. There are some requirements to create/use persistent volumes to store the application code, and the template needs to be designed accordingly. Please find more details below:

Create a PersistentVolume named as pv-devops. Configure the spec as storage class should be manual, set capacity to 3Gi, set access mode to ReadWriteOnce, volume type should be hostPath and set path to /mnt/itadmin (this directory is already created, you might not be able to access it directly, so you need not to worry about it).

Create a PersistentVolumeClaim named as pvc-devops. Configure the spec as storage class should be manual, request 2Gi of the storage, set access mode to ReadWriteOnce.

Create a pod named as pod-devops, mount the persistent volume you created with claim name pvc-devops at document root of the web server, the container within the pod should be named as container-devops using image nginx with latest tag only (remember to mention the tag i.e nginx:latest).

Create a node port type service named web-devops using node port 30008 to expose the web server running within the pod.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
Create PersistentVolume.

```yml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
spec:
  storageClassName: manual
  capacity:
    storage: 3Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/itadmin
```

Create PersistentVolumeClaim.

```yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  storageClassName: manual
  resources:
    requests:
      storage: 2Gi
  accessModes:
    - ReadWriteOnce
```

Create Pod.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: pod-devops
  labels:
    app: nginx
spec:
  volumes:
    - name: pvc-devops-volume
      persistentVolumeClaim:
        claimName: pvc-devops
  containers:
    - name: container-devops
      image: nginx:latest
      volumeMounts:
        - name: pvc-devops-volume
          mountPath: /usr/share/nginx/html
```

Create Service.

```yml
apiVersion: v1
kind: Service
metadata:
  name: web-devops
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

Apply resources.

```sh
thor@jump_host ~$ kubectl apply -f persistent-volumes.yaml 
persistentvolume/pv-devops created
persistentvolumeclaim/pvc-devops created
pod/pod-devops created
service/web-devops created
```
## References

[Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

[Configure a Pod to Use a PersistentVolume for Storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
