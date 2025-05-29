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
