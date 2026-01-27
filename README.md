# Distributed Failure Replay System (DFRS)
Distributed Failure Replay System (DFRS) is a developer-focused platform that captures cross-service HTTP request failures in production and enables deterministic local replay by reconstructing the original request timeline across distributed services.
Distributed Failure Replay System (DFRS) is a portfolio-grade distributed system designed to help developers reproduce and debug production API failures locally.
DFRS works by instrumenting services with a lightweight Agent SDK that captures HTTP request/response data, correlates events across services using trace IDs, and streams them through Kafka. These events are ingested, persisted, visualized as request timelines, and replayed in a sandbox environment to compare original vs replayed responses.

Key capabilities:
Cross-service request tracing (request-level, not kernel-level)
Centralized event ingestion via Kafka
Persistent failure timelines stored in PostgreSQL
Visual trace exploration (graph-based)
Deterministic request replay
Response diffing between original and replayed executions
Tech Stack:
Backend: NestJS (Node.js)
Messaging: Kafka
Storage: PostgreSQL, MinIO
Frontend: React + TypeScript
Infra: Docker Compose
Architecture: Event-driven, microservices (monorepo)
This project intentionally focuses on practical observability and debugging workflows rather than low-level system tracing, making it suitable for real-world developer tooling scenarios.
