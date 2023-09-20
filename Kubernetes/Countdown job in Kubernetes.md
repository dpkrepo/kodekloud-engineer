# Task

The Nautilus DevOps team is working on to create few jobs in Kubernetes cluster. They might come up with some real scripts/commands to use, but for now they are preparing the templates and testing the jobs with dummy commands. Please create a job template as per details given below:

Create a job countdown-nautilus.

The spec template should be named as countdown-nautilus (under metadata), and the container should be named as container-countdown-nautilus

Use image fedora with latest tag only and remember to mention tag i.e fedora:latest, and restart policy should be Never.

Use command sleep 5

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution

Create a file for the Job.

```sh
thor@jump_host ~$ vi countdown-nautilus.yaml
```
```yml
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-nautilus
spec:
  template:
    metadata:
      name: countdown-nautilus
    spec:
      containers:
      - name: container-countdown-nautilus
        image: fedora:latest
        command: ["sleep 5"]
      restartPolicy: Never
```

Save the file and create the Job.

```sh
thor@jump_host ~$ kubectl apply -f countdown-nautilus.yaml 
job.batch/countdown-nautilus created
```

Check status of the created Job.
```sh
thor@jump_host ~$ kubectl describe job countdown-nautilus 
Name:             countdown-nautilus
Namespace:        default
Selector:         batch.kubernetes.io/controller-uid=55a656af-8369-492c-beb9-b12ac5f2ca5b
Labels:           batch.kubernetes.io/controller-uid=55a656af-8369-492c-beb9-b12ac5f2ca5b
                  batch.kubernetes.io/job-name=countdown-nautilus
                  controller-uid=55a656af-8369-492c-beb9-b12ac5f2ca5b
                  job-name=countdown-nautilus
Annotations:      batch.kubernetes.io/job-tracking: 
Parallelism:      1
Completions:      1
Completion Mode:  NonIndexed
Start Time:       Wed, 20 Sep 2023 10:44:56 +0000
Pods Statuses:    0 Active (0 Ready) / 0 Succeeded / 3 Failed
Pod Template:
  Labels:  batch.kubernetes.io/controller-uid=55a656af-8369-492c-beb9-b12ac5f2ca5b
           batch.kubernetes.io/job-name=countdown-nautilus
           controller-uid=55a656af-8369-492c-beb9-b12ac5f2ca5b
           job-name=countdown-nautilus
  Containers:
   container-countdown-nautilus:
    Image:      fedora:latest
    Port:       <none>
    Host Port:  <none>
    Command:
      sleep 5
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From            Message
  ----    ------            ----  ----            -------
  Normal  SuccessfulCreate  53s   job-controller  Created pod: countdown-nautilus-sqqsl
  Normal  SuccessfulCreate  31s   job-controller  Created pod: countdown-nautilus-978jj
  Normal  SuccessfulCreate  10s   job-controller  Created pod: countdown-nautilus-np4lr
```
## References

[Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)
