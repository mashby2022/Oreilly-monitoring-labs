# Troubleshooting Kubernetes Pod CrashLoopBackOff Error with K8sgpt

**Problem Description**

In this scenario, we have a Kubernetes Pod definition with the following details:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crashloop-error-2
spec:
  containers:
    - name: container-1
      image: nginx:latest
      ports:
        - containerPort: 8080 # Incorrect port, NGINX default is 80
```

When attempting to create this Pod, it enters a `CrashLoopBackOff` state. Your task is to identify and resolve the `CrashLoopBackOff` error by analyzing the Pod YAML file using k8sgpt.

### Task

Identify and resolve the `CrashLoopBackOff` error in the Kubernetes Pod by analyzing the Pod YAML file using k8sgpt.
