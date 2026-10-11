# Microservice Anomaly and Performance Testbed Dataset

This repository hosts a collection of time-series datasets capturing operational baselines and fault-injection scenarios within a microservice architecture. The metrics were collected using **Prometheus** and visualized via **Grafana**.

## Dataset Catalog

The testbed datasets are organized by the specific system state or fault type injected during the metrics collection:

### 1. Baselines & Normal Operation
*   `normal_baseline.csv`: Standard operational metrics under expected workloads without injected faults. Used as the ground truth for healthy behavior.
*   `inter_service_normal.csv`: Baseline network communication and response patterns between dependent microservices under optimal conditions.

### 2. Resource Stress Scenarios
*   `cpu_stress.csv`: Metrics recorded during heavy CPU utilization or compute-resource starvation experiments.
*   `memory_stress.csv` & `memory_stress_test.csv`: System behavior under simulated memory leaks or high RAM consumption, leading to potential Out-Of-Memory (OOM) risks.

### 3. Traffic & Network Anomalies
*   `high_traffic.csv`: Metrics capturing sudden traffic spikes, flash crowds, or load testing beyond standard microservice capacity.
*   `slow_response.csv`: Scenarios where service dependencies exhibit processing degradation, causing delayed application responses.
*   `inter_service_slow.csv`: Explicitly captures high network latency or delayed round-trip times (RTT) between internal microservice communication pathways.

### 4. Failure & Error Scenarios
*   `error_rate.csv`: Data capturing a high volume of HTTP 5xx errors or application-level exceptions.
*   `service_failure.csv`: Total collapse, crash, or downtime of a critical microservice component.
*   `inter_service_error.csv`: Network, gRPC, or HTTP protocol-level communication failures between dependent internal services.

## Prometheus Data Schema
The CSV files represent exported Prometheus time-series metrics sampled at regular scrape intervals. Key features typically include:
*   `timestamp`: The Unix timestamp or RFC3339 formatted time of metric collection.
*   `instance` / `job`: The target microservice instance identifier.
*   `node_cpu_seconds_total` / `container_cpu_usage_seconds_total`: CPU consumption counters.
*   `container_memory_working_set_bytes`: Active RAM footprint of the microservice container.
*   `http_requests_total`: Request counters tracked by HTTP status codes (2xx, 4xx, 5xx) and routing methods.
*   `http_request_duration_seconds_bucket`: Latency distribution histograms for calculating p50, p90, and p99 response times.

## Public Access via GitHub Pages
Because these files are hosted publicly on GitHub Pages, you can pull them directly into Python data science or machine learning pipelines (e.g., for training anomaly detection models) without cloning the repo:

```python
import pandas as pd

# Replace [username] and [repo-name] with your actual GitHub details
url = "https://[username].github.io/[repo-name]/cpu_stress.csv"
df = pd.read_csv(url)

print(df.head())
```
