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

## Create a New Dashboard

1. Navigate to the Dashboards page and click the New Dashboard button.

   Creating a new dashboard in Grafana

2. A screen appears where you can add new empty panels and rows.

   Starting a new dashboard in Grafana

3. A new screen appears with a single dummy panel.

   A new Grafana dashboard with an empty panel

## Customize the Dashboard Using Prometheus Query Editor

To edit a specific Grafana panel:

1. Click the panel’s title to open a drop-down menu.

2. In the menu, click Edit.

   Accessing the edit section to edit a graph in query editor

3. The edit window appears. Customize panels by introducing new queries or modifying the current ones. The querying is performed using Prometheus query language.

   Editing a graph in query editor in Grafana

4. The following metrics are not featured in Grafana’s premade Prometheus dashboard, but are useful for monitoring Prometheus:

   - `prometheus_local_storage_memory_chunks`: Monitors memory chunks Prometheus stores in memory.
   - `prometheus_local_storage_memory_series`: Monitors memory series Prometheus stores in memory.
   - `prometheus_local_storage_ingested_samples_total`: Measures the ingestion rate for the samples.
   - `prometheus_target_interval_length_seconds`: Measures the amount of time between target scrapes.
   - `prometheus_local_storage_chunk_ops_total`: Monitors the per-second rate of all Prometheus storage chunk operations.

