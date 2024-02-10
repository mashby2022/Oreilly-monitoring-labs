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

