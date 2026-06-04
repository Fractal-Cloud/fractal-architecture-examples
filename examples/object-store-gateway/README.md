# Fractal Object Store Gateway

Public object storage without a gateway in front means weak access control and no central place for auth, scanning, or audit.

This Fractal exposes blob storage through an API gateway and a workload on a container platform. Clients talk to the API; the workload enforces policy before reads and writes reach the store. The `FilesAndBlobs` component maps to MinIO on Kubernetes or to S3 / Azure Blob in the cloud, depending on the environment.

## What's included

### Ingress

API Gateway: routing, rate limits, hook for authentication and policy.

### Runtime

Container platform with a custom workload that implements upload/download and authorization in front of storage.

### Storage

`FilesAndBlobs` for durable objects (MinIO, S3, or Azure Blob per target platform).

## Design principles

- Objects are not served from raw storage URLs; traffic goes through the API and gateway.
- The blueprint is the minimal gateway + workload + store pattern; add cache, AV scanning, or audit storage when you need them.
- One component type in the Fractal, multiple backing implementations without changing the blueprint shape.
