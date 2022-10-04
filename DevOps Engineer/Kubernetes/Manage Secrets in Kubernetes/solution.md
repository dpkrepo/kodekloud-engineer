
```
thor@jump_host ~$ cat /opt/news.txt 
5ecur3
```


```
thor@jump_host ~$ kubectl create secret generic news --from-file=/opt/news.txt 
secret/news created
```

```
thor@jump_host ~$ kubectl create -f /tmp/secret.yml 
pod/secret-nautilus created
thor@jump_host ~$ kubectl get pods
NAME              READY   STATUS              RESTARTS   AGE
secret-nautilus   0/1     ContainerCreating   0          9s
thor@jump_host ~$ kubectl get pods
NAME              READY   STATUS    RESTARTS   AGE
secret-nautilus   1/1     Running   0          49s
thor@jump_host ~$ kubectl exec secret-nautilus -- cat /opt/apps/news.txt
5ecur3
```
