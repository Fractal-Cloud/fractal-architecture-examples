# Fractal CQRS Stack

Reads and writes rarely want the same schema, latency, or consistency guarantees. One model for both often overloads the write path or starves readers.

CQRS splits command and query. This Fractal wires a write side (authoritative store + outbox + events), a projector that updates read models, and a query side that reads document store, search index, and cache only.

## What's included

### Ingress

API Gateway with two entry workloads:

- **Command Service**: mutations, delegates to the domain write model
- **Query Service**: reads from materialized views only

### Write path

On the container platform:

- **Domain Model**: business rules, **Write Database** (relational store of record)
- **Outbox Entity**: outbox on the broker so DB commit and event intent stay aligned
- **Outbox Relay**: publishes outbox rows to the **Event Topic** after commit

### Read path

- **Projector**: consumes the event topic, updates **Read Database** (document) and **Search Index**
- **Query Service**: serves from read database, search index, and **Cache** (key-value)

### Messaging

- **Event Topic**: domain events from outbox relay to projector
- **Dead Letter Topic**: failed messages for inspection and replay
- **Reprocessor**: replays from the dead-letter path into the pipeline

### Storage

- Relational write database (source of truth for commands)
- Document read database (views built by the projector)
- Search index (lookup and filter on read models)
- Key-value cache (frequent read paths)

## Design principles

- Queries do not read the write database; commands do not depend on read-store layout.
- Read models lag the write side by design; the projector closes that gap over the topic.
- Outbox avoids writing to the DB and publishing to the broker in two separate, racy steps.
- Scale reads with cache, documents, and search without pushing that load onto the write store.
- DLQ plus reprocessor make projection failures visible and recoverable.
