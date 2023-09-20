# Task
There are some jobs/tasks that need to be run regularly on different schedules. Currently the Nautilus DevOps team is working on developing some scripts that will be executed on different schedules, but for the time being the team is creating some cron jobs in Kubernetes cluster with some dummy commands (which will be replaced by original scripts later). Create a cronjob as per details given below:

Create a cronjob named xfusion.

Set Its schedule to something like */11 * * * *, you set any schedule for now.

Container name should be cron-xfusion.

Use httpd image with latest tag only and remember to mention the tag i.e httpd:latest.

Run a dummy command echo Welcome to xfusioncorp!.

Ensure restart policy is OnFailure.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.
## Solution
Create a yaml file for CronJob.
```sh
thor@jump_host ~$ vi xfusion.yaml
```
```yml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: xfusion
spec:
  schedule: "*/11 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-xfusion
            image: httpd:latest
            command:
            - /bin/sh
            - -c
            - echo Welcome to xfusioncorp!
          restartPolicy: OnFailure
```

Save the file and create CronJob.

```sh
thor@jump_host ~$ kubectl apply -f xfusion.yaml 
cronjob.batch/xfusion created
```
## References

[Running Automated Tasks with a CronJob](https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/)
