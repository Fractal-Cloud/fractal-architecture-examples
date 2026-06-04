# Fractal FaaS Serverless Stack

Sporadic workloads should not pay for idle clusters. With FaaS you pay per invocation when the function runs, not for always-on nodes.

This Fractal puts serverless functions behind an API gateway and connects them to a document database, a key-value cache, and blob storage. It uses `CustomWorkloads.FaaS.Workload` only: no container platform and no Kubernetes cluster in the blueprint.

## What's included

### Ingress

API Gateway in front of the serverless tier (routing, rate limits, TLS).

### Runtime

Three FaaS workloads, each tied to a storage role:

- **Serverless Key-Value**: logic for cache and hot state
- **Serverless Storage**: logic for files and blobs
- **Serverless Document**: logic for document persistence

### Storage

- Document database for records and JSON documents
- Key-value store for cache and short-lived state
- File and blob storage for media and large objects

## Design principles

- Functions scale to zero; there is no standing cluster cost between invocations.
- The blueprint omits `ContainerPlatform` and service mesh; runtime is FaaS.
- Client calls hit the gateway first, then the function that owns the right store.
- One function per storage concern keeps boundaries clear; add topic-driven functions separately if you need async jobs.
