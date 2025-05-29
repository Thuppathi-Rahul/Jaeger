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
