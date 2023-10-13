## Task
The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications. They are planning to deploy it on Kubernetes cluster. Below you can find more details.

1.) Create a deployment named grafana-deployment-devops using any grafana image for Grafana app. Set other parameters as per your choice.

2.) Create NodePort type service with nodePort 32000 to expose the app.

You need not to make any configuration changes inside the Grafana app once deployed, just make sure you are able to access the Grafana login page.

Note: The kubectl on jump_host has been configured to work with kubernetes cluster.
## Solution
Create a yaml file.

```sh
thor@jump_host ~$ vi grafana.yaml
```

Define specification of the deployment and the NodePort.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana-container
          image: grafana/grafana:latest


---

apiVersion: v1
kind: Service
metadata:
  name: grafana-service
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      nodePort: 32000
```

Create the deployment and the NodePort.

```sh
thor@jump_host ~$ kubectl apply -f grafana.yaml 
deployment.apps/grafana-deployment-devops created
service/grafana-service created
```

Check if pods are running.

```sh
thor@jump_host ~$ kubectl get pods
NAME                                         READY   STATUS    RESTARTS   AGE
grafana-deployment-devops-7dfcc6bf9c-427vl   1/1     Running   0          21s
```

Grafana should be available in a second.
## References

[NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport)

[Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
