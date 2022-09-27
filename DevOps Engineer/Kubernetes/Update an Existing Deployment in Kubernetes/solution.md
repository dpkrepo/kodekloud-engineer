check created deployments
```
kubectl get deployments 
```
check created services
```
kubectl get services
```

check created pods
```
kubectl ger pods
```

edit configuration of a service 
change nodePort from 30008 to 32165
```
kubectl edit service nginx-service
```

edit configuration of a deployment
change replicas from 1 to 5 and image from nginx:1.18 to nginx:latest
```
kubectl edit deployment nginx-deployment
```
