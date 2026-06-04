# Fractal API with DB, Storage, and Observability

An API needs more than a route and a container. This Fractal provisions ingress, runtime, three storage types, and logging, metrics, and tracing in one blueprint.

## What's included

### Ingress

API Gateway for inbound traffic: rate limiting, routing, TLS termination.

### Runtime

Container platform with a CaaS workload for the service. Service mesh with mTLS on east-west traffic.

### Observability

Logging, metrics, and distributed tracing on the container platform.

### Storage

- Relational database for structured, persistent data
- Key-value store for cache and session state
- File and blob storage for documents and binary assets

## Design principles

- Relational, key-value, and blob storage are declared in the same template as the API.
- Logs, metrics, and traces are part of the initial deployment, not a later add-on.
- External traffic goes through the gateway; internal traffic uses the mesh.
