### Solution: Exercise 1

#### Task:
Install the required libraries using the provided commands.

#### Solution:
Execute the following commands in your terminal or command prompt:

```bash
go get github.com/prometheus/client_golang/prometheus
go get github.com/prometheus/client_golang/prometheus/promauto
go get github.com/prometheus/client_golang/prometheus/promhttp
```

---

### Solution: Exercise 2

#### Task:
Create a Go application that exposes Prometheus metrics via an HTTP endpoint and verify its functionality by accessing the metrics endpoint.

#### Solution:
Create a file named `main.go` with the following code:

```go
package main

import (
    "net/http"

    "github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
    http.Handle("/metrics", promhttp.Handler())
    http.ListenAndServe(":2112", nil)
}
```

Run the application using the following command:

```bash
go run main.go
```

Access the metrics endpoint using:

```bash
curl http://localhost:2112/metrics
```

You should see Prometheus metrics output.

---

### Solution: Exercise 3

#### Task:
Modify the existing Go application to include custom Prometheus metrics and verify their presence in the metrics output.

#### Solution:
Update the `main.go` file with the following code to add custom metrics:

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
```

Run the updated application using:

```bash
go run main.go
```

Access the metrics endpoint using:

```bash
curl http://localhost:2112/metrics
```

You should see the custom `myapp_processed_ops_total` metric in the output along with other Prometheus metrics.
```
