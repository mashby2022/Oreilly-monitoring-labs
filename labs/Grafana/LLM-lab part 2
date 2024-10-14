## Lab 2: Visualizing Triton Metrics with Grafana

**Introduction:**

This lab builds upon the Prometheus setup from Lab 1 and focuses on visualizing the collected Triton Inference Server metrics using Grafana, aligning with the original instructions. You'll learn how to install Grafana, configure it to use Prometheus as a data source, and import a pre-built dashboard to gain insights into Triton's performance.

**Learning Objectives:**

* Install and configure Grafana on a GKE cluster.
* Configure Grafana to use Prometheus as a data source.
* Import a pre-built Grafana dashboard for Triton Inference Server.
* Analyze and interpret the visualized metrics.

**Prerequisites:**

* Completion of Lab 1 (Prometheus should be running).
* `kubectl` CLI installed.
* Helm CLI installed.

**Original Instructions (Grafana):**

**Initialize GMP settings:**

* Run the following command:
  ```bash
  gcloud container clusters get-credentials triton-inference --location us-central1
  kubectl edit operatorconfig -n gmp-public
  ```
* Add the following section right above line start with metadata:
  ```yaml
  features:
    targetStatus:
      enabled: true
  ```
* Then run the following command to create GMP PodMonitoring resource targeting deployed triton inference server:
  ```bash
  gcloud container clusters get-credentials triton-inference --location us-central1
  kubectl -n triton apply -f vllm-podmonitoring.yaml
  ```

**Use cloud monitoring metric explorer to display Model inference metrics:**

* Go to Monitoring/Metric Explorer, switch to PromQL on the right side of the console.
* In the query window, type `nv_`, you will see a list of Nvidia triton metrics available.
* Choose one of `NV_` metric, and Click "Run Query" button on the right side, you will see the chart of this metric.

**Use Grafana to visualize Model inference monitoring metrics:**

**Lab Steps (Grafana):**

1. **Install Grafana using Helm:**

   * Add the Grafana Helm repository:
     ```bash
     helm repo add grafana https://grafana.github.io/helm-charts
     helm repo update
c

