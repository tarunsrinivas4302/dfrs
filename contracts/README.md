- [DFRS Event Contracts](#dfrs-event-contracts)
  - [Purpose](#purpose)
  - [Rules](#rules)
  - [Scope](#scope)

# DFRS Event Contracts

This directory contains the canonical event schemas used across the Distributed Failure Replay System (DFRS).

## Purpose

Event contracts define the data exchanged between:

- Agent SDKs
- Kafka
- Ingestor service
- API server
- Replay engine
- UI

All components rely on these schemas to ensure consistent capture, storage, visualization, and replay of failures.

## Rules

- Agent SDKs MUST emit events that conform to the schema
- The ingestor validates and persists events based on these contracts
- Schema changes must be backward-compatible whenever possible
- Breaking changes require explicit versioning

## Scope

The current schema focuses on:

- HTTP request/response capture
- Trace-level correlation
- Replay-oriented data (not low-level system state)

<!-- Kernel-level tracing, memory snapshots, and language-agnostic capture are intentionally out of scope. -->
