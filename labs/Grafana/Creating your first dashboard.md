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
