Sure, here are the two tutorials rewritten as markdown files:

**Tutorial 1: Grafana 101**

```markdown
# Grafana 101: Monitoring Your Application

## Prerequisites

Before starting, ensure you have the following installed:

- Docker
- Docker Compose (included in Docker for Desktop for macOS and Windows)
- Git

## Set up the Sample Application

1. Clone the repository containing the sample application:

   ```bash
   git clone https://github.com/grafana/tutorial-environment.git
   ```

2. Navigate to the cloned directory:

   ```bash
   cd tutorial-environment
   ```

3. Start the sample application:

   ```bash
   docker-compose up -d
   ```

4. Verify that all services are running:

   ```bash
   docker-compose ps
   ```

5. Access the sample application by browsing to localhost:8081.

## Exploring Metrics and Logs

### Logging in to Grafana

1. Open a web browser and go to localhost:3000.

2. Log in using the default credentials (admin/admin).

3. Change the password when prompted.

### Adding a Metrics Data Source

1. In Grafana, go to "Configuration" > "Data Sources".

2. Click on "Add data source".

3. Select Prometheus and enter the URL: http://prometheus:9090.

4. Save and test the data source.

### Exploring Metrics

1. Navigate to the Explore section in the sidebar.

2. Enter `tns_request_duration_seconds_count` in the query editor.

3. Apply the `rate` function to visualize the rate of requests per second.

4. Group time series by route using the `sum` aggregation operator.

5. Experiment with different grouping labels.

### Adding a Logging Data Source

1. Again in the "Configuration" > "Data sources" section, add a new data source.

2. Select Loki and enter the URL: http://loki:3100.

3. Save and test the data source.

### Exploring Logs

1. Navigate to the Explore section in the sidebar.

2. Select the Loki data source.

3. Enter `{filename="/var/log/tns-app.log"}` in the query editor.

4. Filter logs based on time or specific occurrences.
```

**Tutorial 2: Grafana with Prometheus**

```markdown
# Grafana with Prometheus: Installation and Configuration

## Installing Grafana

1. Create a ConfigMap for Grafana data sources:

   ```bash
   nano grafana-datasource-config.yaml
   ```

   Add the required configurations and save the file.

2. Apply the configuration to your cluster:

   ```bash
   kubectl create -f grafana-datasource-config.yaml
   ```

3. Create a YAML file for Grafana deployment and service configurations.

4. Apply the deployment and service configurations to the cluster.

5. Forward Grafana service to port 3000:

   ```bash
   kubectl port-forward svc/grafana 3000
   ```

6. Access Grafana in a browser at http://localhost:3000/, and log in with the default credentials.

## Adding Prometheus as a Data Source

1. In Grafana, navigate to "Configuration" > "Data Sources".

2. Click "Add data source" and select Prometheus.

3. Enter the Prometheus URL and save & test the data source.

## Importing Prometheus Stats Dashboard

1. Navigate to Data Sources > Prometheus.

2. Open the Settings menu and click "Dashboards".

3. Import the Prometheus dashboard.
```

These markdown files can be used to create separate tutorials for Grafana 101 and Grafana with Prometheus.
