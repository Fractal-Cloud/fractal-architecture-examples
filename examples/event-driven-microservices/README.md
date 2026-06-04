# Fractal Event-Driven Microservices

Synchronous call chains couple services at runtime: one slow downstream call stalls the caller.

Here, services publish and consume on a shared topic instead of calling each other over HTTP. Each service has its own storage. The blueprint includes order, shipping, billing, and inventory workloads, a dead-letter queue, and tracing across the flow.

## What's included

### Ingress

API Gateway routes synchronous client traffic to the Order Service. Further steps run over messaging.

### Runtime

Four workloads on a container platform:

- **Order Service**: uses the shared topic and a relational orders database
- **Shipping Service**: consumer with its own relational shipping database
- **Billing Service**: consumer with its own relational billing database
- **Inventory Service**: consumer with a key-value cache for stock lookups

Service mesh with mTLS between workloads.

### Messaging

Broker with:

- **Orders Topic**: events shared by all four services
- **Dead Letter Queue**: failed messages kept aside for replay and inspection

### Storage

- Relational databases for order, shipping, and billing data
- Key-value cache for inventory

### Observability

Logging, metrics, and tracing on the container platform.

## Design principles

- Services coordinate through the topic, not through synchronous HTTP chains.
- Each bounded context owns its database; there is no shared store across services.
- The DLQ prevents bad messages from blocking the main topic indefinitely.
- Traces should cover gateway entry, handlers, and async consumers.
