#### Update an Existing Deployment in Kubernetes
```
Task: There is an application deployed on Kubernetes cluster. Recently the Nautilus application development team developed a new version of the application 
that needs to be deployed now. As per new updates some new changes need to be made in this existing setup. So update the deployment and service as per 
details mentioned below:

We already have a deployment named nginx-deployment and service named nginx-service. Some changes need to be made in this deployment and service, make sure 
not to delete the deployment and service.

1.) Change the service nodeport from 30008 to 32165
2.) Change replicas count from 1 to 5
3.) Change the image from nginx:1.18 to nginx:latest
```



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


