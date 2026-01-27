# Distributed Failure Replay System (DFRS)

Distributed Failure Replay System (DFRS) is a developer-focused platform that captures real production HTTP request failures across distributed services and enables deterministic local replay for debugging.

The goal of DFRS is to help engineers **reproduce hard-to-debug production issues locally** by reconstructing the exact request timeline across services, replaying the original request in a sandbox environment, and comparing the original vs replayed behavior.

---

## Motivation

Debugging distributed systems is hard.

When an API fails in production:
- Logs are fragmented across services
- Reproducing the exact failure locally is often impossible
- Issues depend on timing, request shape, and downstream interactions

DFRS addresses this by capturing **request-level execution data** (not kernel or memory state), correlating events across services, and making failures replayable in a controlled local environment.

This project intentionally focuses on **practical developer workflows**, not low-level system tracing.

---

## High-Level Architecture

Services
↓
Agent SDK (HTTP middleware)
↓
Kafka (event stream)
↓
Ingestor Service
↓
PostgreSQL (metadata) + MinIO (payloads)
↓
API Server
↓
Web UI (Trace Timeline)
↓
Replay Engine


---

## Core Components

### 1. Agent SDK
- Lightweight HTTP middleware
- Captures request & response metadata
- Generates and propagates `trace_id`
- Emits structured events asynchronously

### 2. Kafka
- Central event stream
- Ensures ordered processing per trace
- Decouples services from ingestion

### 3. Ingestor Service
- Consumes events from Kafka
- Persists trace metadata to PostgreSQL
- Stores request/response bodies in MinIO

### 4. API Server
- Exposes trace and timeline APIs
- Serves replay and diff results

### 5. Web UI
- Lists captured traces
- Visualizes request timelines
- Displays original vs replayed responses

### 6. Replay Engine
- Reconstructs original HTTP requests
- Replays requests in a sandbox environment
- Produces response diffs

---

## MVP Scope

### Included
- HTTP request & response capture
- Cross-service trace correlation
- Timeline persistence
- Trace visualization
- Request replay
- Response diffing

### Explicitly Excluded
- CPU-level replay
- Memory snapshots
- Kernel instrumentation
- Language-agnostic agents
- Full OpenTelemetry compliance

---

## Tech Stack

### Backend
- **Framework:** NestJS (Node.js)
- **Messaging:** Kafka
- **Database:** PostgreSQL
- **Object Storage:** MinIO

### Frontend
- **Framework:** React
- **Language:** TypeScript
- **Visualization:** React Flow

### Infrastructure
- Docker Compose
- Monorepo with multiple services

---

## Repository Structure

dfrs/
├── packages/
│ └── agent-sdk/ # HTTP capture middleware
├── services/
│ ├── ingestor/ # Kafka consumer
│ ├── api-server/ # Trace & replay APIs
│ └── replay-engine/ # Request replay logic
├── ui/ # React frontend
├── infra/ # Docker Compose & infra config
└── contracts/ # Event schemas


---

## Design Principles

- **Request-level, not kernel-level**
- **Simple over perfect**
- **Vertical slice delivery**
- **Production-plausible, MVP-scoped**
- **Clear contracts between components**

---

## Local Development

### Prerequisites
- Docker
- Node.js (18+)

### Start Infrastructure
```bash
cd infra
docker compose up -d
```
### Status

🚧 Work in progress
This project is being developed incrementally with a focus on end-to-end vertical slices.


