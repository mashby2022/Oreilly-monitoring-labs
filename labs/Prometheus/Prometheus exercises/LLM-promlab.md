## Lab 1: Monitoring Triton Inference Server with Prometheus

**Introduction:**

This lab focuses on setting up Prometheus to monitor a Triton Inference Server deployed on a Google Kubernetes Engine (GKE) cluster, following the original instructions provided. You'll learn how to install Prometheus, configure it to scrape metrics from Triton, and verify the collection of key performance indicators.

**Learning Objectives:**

* Install and configure Prometheus on a GKE cluster.
* Configure Prometheus to scrape metrics from Triton Inference Server.
* Access the Prometheus UI and explore the collected metrics.

**Prerequisites:**

* A Google Cloud Project with billing enabled.
* A GKE cluster with Triton Inference Server deployed (Follow the deployment steps in the "Original Instructions" section below).
* `kubectl` CLI installed.
* Helm CLI installed.


**Original Instructions:**

**Summary:**

This tutorial walks through how to set up Llama 2 and other Hugging Face based LLM models through Nvidia Inference Server based on GKE and GPU (Nvidia T4, L4, etc).

**Tutorial steps:**

**Prerequisites:**

* Hugging Face account settings with HF API Token. You also need to have access permission granted for Llama 2 LLM models.
* GCP project and access. You may need to raise GPU quota for L4.
* Download the github repo:

```bash
git clone https://github.com/llm-on-gke/triton-vllm-gke
cd $PWD/triton-vllm-gke
chmod +x create-cluster.sh
```

**Create the GKE cluster:**

* Update the `create-cluster.sh` script, to replace proper values for `PROJECT_ID` and `HF_TOKEN`.
* `./create-cluster.sh`

**Run the following commands to upload model repository, replace your-bucket-name:**

```bash
gsutil mb gs://your-bucket-name
gsutil cp -r model_repository gs://your-bucket-name/model_repository
```

**Deploy Kubernetes resources into GKE cluster:**

* Update the `vllm-gke-deploy.yaml` file if necessary:
    * Right model name env:
      ```yaml
      env:
      - name: model_name
        value: meta-llama/Llama-2-7b-chat-hf
      ```
    * Update model repository URI in cloud storage:
      ```yaml
      args: ["tritonserver", "--model-store=gs://your-bucket-name/model_repository"]
      ```
* Execute the command to deploy inference deployment in GKE, update the `HF_TOKEN` values:
  ```bash
  kubectl apply -f vllm-gke-deploy.yaml -n triton
  ```

**Test out the batch inference:**

* Run cloud build to create testing container images:
* Run the following command to build testing client container to test llama 2 batch inference:
  ```bash
  cd client
  gcloud builds submit .
  ```
* Test GRPC client:
  ```bash
  kubectl run -it -n triton --image us-east1-docker.pkg.dev/your-project/gke-llm/triton-client --env="triton_ip=$TRITON_IP" triton-client 
  kubectl exec -it -n triton triton-client -- bash
  ```
* Once you are in the container, update the `grpc-client.py` with the endpoint with the Service IP generated. Then run the following command inside the testing container:
  ```bash
  curl $TRITON_INFERENCE_SERVER_SERVICE_HOST:8000/v2
  curl $TRITON_INFERENCE_SERVER_SERVICE_HOST:8002/metrics
  python3 grpc-client.py
  ```
* If everything runs smoothly, there will be a `results.txt` file generated, you may check the contents of it.

**Retrieve metrics from Triton Inference server port 8002:**

* Check the metrics exposed by Triton Inference Server:
  ```bash
  kubectl exec -it -n triton bash -- bash
  curl SERVICEIP:8002/metrics
  ```
  You should see a list of metrics starting with `nv_XXX`.

**Lab Steps (Prometheus):**

1. **Install Prometheus using Helm:**

   * Add the Prometheus Helm repository:
     ```bash
     helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
     ```
   * Update Helm repositories:
     ```bash
     helm repo update
     ```
   * Create a namespace for Prometheus:
     ```bash
     kubectl create namespace monitoring
     ```
   * Install Prometheus:
     ```bash
     helm install prometheus prometheus-community/prometheus \
       --namespace monitoring \
       --set server.service.type=LoadBalancer \
       --set alertmanager.enabled=false \
       --set pushgateway.enabled=false \
       --set server.persistentVolume.enabled=false
     ```

2. **Configure Prometheus to Scrape Triton Metrics:**

   * Obtain the Triton Inference Server service IP:
     ```bash
     TRITON_IP=$(kubectl get service triton-inference-server -n triton -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
     ```
   * Create a `prometheus-config.yaml` file:
     ```yaml
     global:
       scrape_interval:     15s
       evaluation_interval: 15s

     scrape_configs:
       - job_name: 'triton'
         static_configs:
           - targets: ['${TRITON_IP}:8002']
     ```
   * Create a ConfigMap in Kubernetes:
     ```bash
     kubectl create configmap prometheus-config -n monitoring --from-file=prometheus-config.yaml
     ```
   * Update the Prometheus deployment to use the ConfigMap:
     ```bash
     kubectl patch deployment prometheus-server -n monitoring -p '{"spec":{"template":{"spec":{"volumes":[{"name":"config-volume","configMap":{"name":"prometheus-config"}}]}},"containers":[{"name":"prometheus-server","volumeMounts":[{"name":"config-volume","mountPath":"/etc/prometheus/prometheus.yml","subPath":"prometheus-config.yaml"}]}]}}'
     ```

3. **Access Prometheus and Verify Metric Collection:**

   * Obtain the Prometheus UI URL:
     ```bash
     kubectl get service prometheus-server -n monitoring
     ```
   * Open the Prometheus UI in your browser using the external IP.
   * In the Prometheus expression browser, enter `nv_inference_request_duration_us` and click "Execute" to see the inference request duration metric collected from Triton.
   * Explore other relevant metrics exposed by Triton.

**Cleanup:**

   * You can keep the Prometheus deployment running for Lab 2. If you wish to clean up, you can uninstall Prometheus using Helm:
     ```bash
     helm uninstall prometheus -n monitoring
     ```

