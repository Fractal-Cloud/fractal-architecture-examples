# Fractal Production API Stack

This Fractal provisions a complete, production-ready API stack. Developers request an API endpoint; they get a battle-tested infrastructure template — no JIRA ticket required.

## What's included

**Ingress** — An API Gateway handles all inbound traffic, enforcing rate limiting, routing, and protocol termination at the edge.

**Runtime** — A Container-as-a-Service platform hosts the application workload. A service mesh secures all east-west communication with mutual TLS between services.

**Observability** — Three pillars are provisioned from day one: structured logging, metrics monitoring, and distributed tracing. No retrofitting required.

**Storage** — Three complementary backends cover the full data surface:
- Relational database for persistent, structured data
- Key-value store (Redis-compatible) for caching hot responses and session data
- File and blob storage for documents, media, and binary assets

## Design principles

- **Self-service by default** — the entire stack is requested and provisioned through the platform, not through ops tickets.
- **Security built-in** — mTLS for internal traffic and API Gateway policies for external traffic are part of the template, not opt-in additions.
- **Observable from boot** — logs, metrics, and traces are wired before the first deployment.

