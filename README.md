# Fractal Architecture Examples

Repository of **Fractal** blueprints for **Fractal Cloud**: reusable infrastructure templates you import and deploy as a unit.

Each example is a JSON file (`fractal-*.json`) with components, dependencies, and links. Import it in Fractal Cloud, then request a deployment from your catalog.

## Examples

| Example | Description |
|---------|-------------|
| [API, DB, Storage & Observability](examples/api-db-storage-observability/) | API with gateway, container workload, service mesh, relational DB, cache, blob storage, logging, metrics, and tracing. |
| [FaaS Serverless Stack](examples/faas-serverless-stack/) | API gateway and FaaS functions over document DB, cache, and blobs; no container platform. |
| [Event-Driven Microservices](examples/event-driven-microservices/) | Microservices on a shared topic, storage per service, distributed tracing. |
| [CQRS Stack](examples/cqrs-stack/) | Separate write and read models via events and projection. |
| [Object Store Gateway](examples/object-store-gateway/) | Object storage behind an API gateway and workload instead of public bucket URLs. |

## Repository layout

```
examples/
├── api-db-storage-observability/
│   ├── fractal-api-db-storage-observability.json
│   └── README.md
├── faas-serverless-stack/
│   ├── fractal-faas-serverless-stack.json
│   └── README.md
├── event-driven-microservices/
│   ├── fractal-event-driven-microservices.json
│   └── README.md
├── cqrs-stack/
│   ├── fractal-cqrs-stack.json
│   └── README.md
└── object-store-gateway/
    ├── fractal-object-store-gateway.json
    └── README.md
```

## Using a blueprint

1. Open the example folder and read `README.md`.
2. Import the `fractal-*.json` file into Fractal Cloud.
3. Deploy through your platform catalog.

## About Fractals

A **Fractal** is a versioned infrastructure template. The blueprint lists components (gateway, runtime, databases, messaging, and so on) with explicit dependencies. Platform teams publish Fractals to a catalog; product teams pick one and deploy the linked stack.
