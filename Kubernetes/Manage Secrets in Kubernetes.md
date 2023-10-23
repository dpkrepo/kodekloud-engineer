## Task
The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that licence information needs to be stored securely within Kubernetes cluster. Therefore, the team wants to utilize Kubernetes secrets to store those secrets. Below you can find more details about the requirements:

We already have a secret key file official.txt under /opt location on jump host. Create a generic secret named official, it should contain the password/license-number present in official.txt file.

Also create a pod named secret-nautilus.

Configure pod's spec as container name should be secret-container-nautilus, image should be fedora preferably with latest tag (remember to mention the tag with image). Use sleep command for container so that it remains in running state. Consume the created secret and mount it under /opt/apps within the container.

To verify you can exec into the container secret-container-nautilus, to check the secret key under the mounted path /opt/apps. Before hitting the Check button please make sure pod/pods are in running state, also validation can take some time to complete so keep patience.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
Create a generic secret.

```sh
thor@jump_host ~$ kubectl create secret generic official --from-file=/opt/official.txt 
secret/official created
```
Create a pod.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: secret-nautilus
spec:
  containers:
    - name: secret-container-nautilus
      image: fedora:latest
      command: ['sh', '-c', 'sleep 600']
      volumeMounts:
        - name: official-volume
          mountPath: /opt/apps
  volumes:
  - name: official-volume
    secret:
      secretName: official
```

Apply the pod.

```sh
thor@jump_host ~$ kubectl apply -f secret-nautilus.yaml 
pod/secret-nautilus created
```

## References

[Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

[kubectl create secret generic](https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_create_secret_generic/)
