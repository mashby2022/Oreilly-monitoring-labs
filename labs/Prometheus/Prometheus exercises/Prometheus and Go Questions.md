# Prometheus Monitoring in Go Applications - Practice Questions

### Practice Question 1:

**What is the purpose of the following code snippet in a Go application?**

```go
http.Handle("/metrics", promhttp.Handler())
http.ListenAndServe(":2112", nil)
```

a) Exposing custom metrics to Prometheus  
b) Initializing the HTTP server  
c) Registering Prometheus metrics handler  
d) Defining the Prometheus endpoint  

---

### Practice Question 2:

**Which function is responsible for incrementing the `myapp_processed_ops_total` counter in the following Go code snippet?**

```go
func recordMetrics() {
    go func() {
        for {
            opsProcessed.Inc()
            time.Sleep(2 * time.Second)
        }
    }()
}
```

a) `recordMetrics()`  
b) `main()`  
c) `opsProcessed.Inc()`  
d) Anonymous goroutine  
