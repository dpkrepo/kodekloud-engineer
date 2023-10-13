## Task
The Nautilus DevOps team is working on to setup some pre-requisites for an application that will send the greetings to different users. There is a sample deployment, that needs to be tested. Below is a scenario which needs to be configured on Kubernetes cluster. Please find below more details about it.

Create a pod named print-envars-greeting.

Configure spec as, the container name should be print-env-container and use bash image.

Create three environment variables:

a. GREETING and its value should be Welcome to

b. COMPANY and its value should be Stratos

c. GROUP and its value should be Industries

Use command to echo ["$(GREETING) $(COMPANY) $(GROUP)"] message.

You can check the output using kubectl logs -f print-envars-greeting command.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

## Solution
Create a yaml file.

```sh
thor@jump_host ~$ vi print-envars-greeting.yaml
```

Specify pod properties.
```yml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  containers:
    - name: print-env-container
      image: bash:latest
      env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "Stratos"
        - name: GROUP
          value: "Industries"
      command: ["bin/sh"]
      args: ["-c", "echo $(GREETING) $(COMPANY) $(GROUP)"]
```

Create the pod.

```sh
thor@jump_host ~$ kubectl apply -f print-envars-greeting.yaml 
pod/print-envars-greeting created
```

Check if this pod works correctly.

```sh
thor@jump_host ~$ kubectl logs -f print-envars-greeting
Welcome to Stratos Industries
```
## References

[Define Environment Variables for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)
