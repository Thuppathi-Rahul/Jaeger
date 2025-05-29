# Jaeger

**What is Jaeger?**
>
Jaeger is an open-source, end-to-end distributed tracing system created by Uber Technologies. It’s used for monitoring and troubleshooting the performance of microservices-based architectures.
It is part of the CNCF (Cloud Native Computing Foundation) ecosystem, just like Kubernetes and Prometheus.
>

**Fundamentals of Jaeger**
>
Jaeger implements the OpenTracing standard (now superseded by OpenTelemetry) and is used to:

1.Trace requests across distributed systems

2.Measure service latency

3.Understand application performance bottlenecks

4. Visualize request flows
>

**Key Concepts:**

| Term        | Meaning                                                                   |
| ----------- | ------------------------------------------------------------------------- |
| **Trace**   | A collection of spans representing the journey of a request               |
| **Span**    | A single operation, includes start time, duration, tags, logs, and parent |
| **Context** | Metadata propagated between services                                      |
| **Baggage** | User-defined data that travels with a request                             |



**Jaeger Architecture**
>
Jaeger is composed of several components:

**1. Client Libraries**

Instrumented in your code to create and propagate spans.

Languages: Go, Java, Python, Node.js, etc.

Often integrated via OpenTelemetry SDK now.

**2. Agent**

A network daemon that listens for spans sent over UDP.

Runs as a sidecar or daemonset in Kubernetes.

Batches and sends spans to the collector.

**3. Collector**

Receives spans from agents or directly from apps.

Validates, transforms, and stores them in a backend like Elasticsearch or Cassandra.

**4. Storage Backend**

Where trace data is persisted.

Supported: Elasticsearch, Cassandra, Kafka, Google Cloud Bigtable, etc.

**5. Query Service**

Provides an API for retrieving trace data.

Powers the web UI and exposes APIs for external tools.

**6. UI**

A web frontend to explore traces and visualize performance.

>




**Jaeger Deployment in Kubernetes (AKS or other)**

>
**1. Helm (Recommended for Production)
Install Jaeger via Helm:**

```
helm repo add jaegertracing https://jaegertracing.github.io/helm-charts
helm repo update

helm install jaeger jaegertracing/jaeger \
  --namespace observability \
  --create-namespace \
  --set provisionDataStore.cassandra=false \
  --set provisionDataStore.elasticsearch=true \
  --set storage.type=elasticsearch

```

**Access Jaeger UI (using port-forwarding or Ingress):**

```
kubectl port-forward svc/jaeger-query 16686:16686 -n observability
```
Then open: http://localhost:16686
>




**2. All-in-One (for Dev/Testing)
Quick and easy setup using YAML:**

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jaeger
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jaeger
  template:
    metadata:
      labels:
        app: jaeger
    spec:
      containers:
      - name: jaeger
        image: jaegertracing/all-in-one:latest
        ports:
        - containerPort: 16686  # UI
        - containerPort: 14268  # Collector
```
**Apply using:**
```
kubectl apply -f jaeger-deployment.yaml
```

**Uses of Jaeger**
>
Performance Bottleneck Analysis: Identify slow services and optimize them.

Root Cause Analysis: Trace failures and see where they originate.

Monitoring Request Latency: View how long a request takes across multiple services.

Service Dependency Visualization: Understand how services interact.

Alerting Integration: Works with Prometheus and Grafana for alerts and visualization.
>

**Importance of Jaeger**

| Benefit                    | Description                                                                |
| -------------------------- | -------------------------------------------------------------------------- |
| 🔍 Deep visibility         | See inside requests across multiple services                               |
| ⚡ Performance Optimization | Pinpoint and reduce latency                                                |
| 🧠 DevOps & SRE Friendly   | Helps SREs troubleshoot incidents and perform RCA                          |
| 🔗 Integrates Easily       | With OpenTelemetry, Prometheus, Grafana, and Service Mesh (Istio, Linkerd) |



**Competitors to Jaeger**

>
🔸 **1. Zipkin**
Simpler than Jaeger, but less feature-rich.

Easier setup, especially for Spring Boot apps.

🔸 **2. AWS X-Ray**
Cloud-native to AWS.

Limited to AWS services; vendor lock-in.

🔸 **3. Datadog APM**
Commercial.

Highly integrated with cloud services and metrics.

🔸 **4. New Relic / Dynatrace / AppDynamics**
Full observability suites.

Paid, enterprise-grade solutions.

🔸 5. **Grafana Tempo**
Lightweight, integrates tightly with Prometheus + Loki.


>



🧠 **Summary**

>
| Aspect          | Jaeger                                     |
| --------------- | ------------------------------------------ |
| Type            | Distributed tracing tool                   |
| Use             | Performance monitoring, RCA, observability |
| Architecture    | Agent → Collector → Storage → Query → UI   |
| Deployment      | Helm, Kubernetes YAML, Docker              |
| Storage         | Elasticsearch, Cassandra, Kafka, etc.      |
| Integrates With | OpenTelemetry, Istio, Prometheus, Grafana  |
| Competitors     | Zipkin, X-Ray, Tempo, Datadog, New Relic   |
>



📘 **Questions & Answers**
>
✅ Q1: What is Jaeger used for?
A: For distributed tracing to analyze and monitor performance across microservices.

✅ Q2: What are the core components of Jaeger?
A: Client library, Agent, Collector, Storage, Query Service, and UI.

✅ Q3: How can Jaeger be deployed in Kubernetes?
A: Using Helm charts (recommended) or YAML deployments (for testing).

✅ Q4: What is the role of Jaeger Agent?
A: Collects spans from applications and sends them to the collector.

✅ Q5: Which backends can Jaeger use for storage?
A: Elasticsearch, Cassandra, Kafka, Google Bigtable.

✅ Q6: What are some popular alternatives to Jaeger?
A: Zipkin, AWS X-Ray, Grafana Tempo, Datadog APM, New Relic.
>

