# Troubleshooting Kubernetes Pod CrashLoopBackOff Error with K8sgpt

**Solution**

#### Error Identification

The issue in the YAML file that causes the `CrashLoopBackOff` error is the incorrect `containerPort` specified for the container. The NGINX default port is 80, but in the YAML file, it's set to `8080`.

#### How to identify the error with K8sGPT
Hands-on Lab: Troubleshooting Kubernetes Pod CrashLoopBackOff Error


1. Authenticate with the k8sgpt tool using the following command:
   ```
   k8sgpt auth 
   ```

2. Analyze the Pod YAML file to identify the issue causing the `CrashLoopBackOff` error:
   ```
   k8sgpt analyze --explain -f crashloop-error.yaml
   ```

3. Review the analysis results to understand the root cause of the error.

4. Edit the Pod YAML file based on the insights gained from the analysis to resolve the issue. Modify the `containerPort` to the correct port (80).
5. Determine the Desired Port:
   - Decide which port the container should listen on.
   - If the container should listen on the default NGINX port (80), remove the `containerPort` field or set it to `80`.

   Modified YAML:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: crashloop-error-2
   spec:
     containers:
       - name: container-1
         image: nginx:latest
   ```

6. Apply the edited YAML file to the Kubernetes cluster to implement the changes:
   ```
   kubectl apply -f modified-crashloop-error.yaml
   ```

7. Verify that the Pod transitions from `CrashLoopBackOff` to a running or ready state:
   ```
   kubectl get pods
   ```

## Conclusion
By analyzing the Pod YAML file with k8sgpt and making the necessary changes to the `containerPort`, you can troubleshoot and resolve the `CrashLoopBackOff` error, ensuring that the Pod functions as intended.
