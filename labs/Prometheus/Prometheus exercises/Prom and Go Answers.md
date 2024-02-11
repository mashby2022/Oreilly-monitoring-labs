# Prometheus Monitoring in Go Applications - Answers with Explanation

### Practice Question 1:

**Correct Answer:** c) Registering Prometheus metrics handler

**Explanation:**
The purpose of the given code snippet in a Go application is to register a Prometheus metrics handler. In this code, `http.Handle("/metrics", promhttp.Handler())` registers the `/metrics` endpoint with Prometheus metrics handler, and `http.ListenAndServe(":2112", nil)` starts an HTTP server to serve these metrics on port 2112. This is a common pattern used in Go applications to expose Prometheus metrics to be scraped by Prometheus server.

[Source: Prometheus Go Client Documentation](https://pkg.go.dev/github.com/prometheus/client_golang/prometheus/promhttp#Handler)

---

### Practice Question 2:

**Correct Answer:** d) Anonymous goroutine

**Explanation:**
In the given Go code snippet, the function `recordMetrics()` starts an anonymous goroutine using the `go func() {...}()` syntax. Inside this goroutine, the `opsProcessed.Inc()` function is responsible for incrementing the `myapp_processed_ops_total` counter. This counter is incremented every 2 seconds according to the provided code, indicating the total number of processed events in the application.

[Source: Prometheus Go Client Documentation](https://pkg.go.dev/github.com/prometheus/client_golang/prometheus#Counter)
``` 
