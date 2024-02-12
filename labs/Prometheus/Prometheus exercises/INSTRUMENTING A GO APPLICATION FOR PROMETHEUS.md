# Monitoring a Go App with Prometheus 
### Prerequisites:
Before starting these exercises, ensure you have the following installed:

1. Go programming language installed on your system.
2. Basic knowledge of Go programming.
3. Access to a terminal or command prompt.

---

### Exercise 1: Installation

#### Instructions:
Follow the steps below to install the necessary libraries for Prometheus monitoring in Go applications:

1. Open your terminal or command prompt.
2. Execute the following commands:

```bash
go mod init main
go get github.com/prometheus/client_golang/prometheus
go install github.com/prometheus/client_golang/prometheus
```

#### Task:
Install the required libraries using the provided commands.

---

### Exercise 2: Exposing Prometheus Metrics

#### Instructions:
Create a Go application that exposes Prometheus metrics via an HTTP endpoint. Follow the steps outlined below:

1. Set up a new Go file (`main.go`).
2. Write the necessary code to import the required libraries and expose the `/metrics` endpoint.

  ```go
package main

import (
    "net/http"
    "time"

    "github.com/prometheus/client_golang/prometheus"
    "github.com/prometheus/client_golang/prometheus/promauto"
    "github.com/prometheus/client_golang/prometheus/promhttp"
)

func recordMetrics() {
    go func() {
        for {
            opsProcessed.Inc()
            time.Sleep(2 * time.Second)
        }
    }()
}

var (
    opsProcessed = promauto.NewCounter(prometheus.CounterOpts{
        Name: "myapp_processed_ops_total",
        Help: "The total number of processed events",
    })
)

func main() {
    recordMetrics()

    http.Handle("/metrics", promhttp.Handler())
    http.ListenAndServe(":2112", nil)
}

4. Implement the HTTP server to listen on port `:2112`.
5. Run the application using `go run main.go`.
6. Access the metrics endpoint using `curl http://localhost:2112/metrics`.

#### Task:
Create a Go application that exposes Prometheus metrics via an HTTP endpoint and verify its functionality by accessing the metrics endpoint.

---

### Exercise 3: Adding Custom Metrics

#### Instructions:
Enhance the previous Go application by adding custom Prometheus metrics. Follow the steps below:

1. Modify the existing `main.go` file to include custom metrics registration.
2. Implement a custom metric named `myapp_processed_ops_total` that counts the number of processed events.
3. Run the updated application using `go run main.go`.
4. Access the metrics endpoint using `curl http://localhost:2112/metrics` and observe the output.

#### Task:
Modify the existing Go application to include custom Prometheus metrics and verify their presence in the metrics output.
```
