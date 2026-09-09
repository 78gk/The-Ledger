# The Ledger

An event-sourced loan decision platform that models a real-world underwriting workflow end to end: document intake, credit analysis, fraud screening, compliance checks, human review, and final decision traceability.

## Why this project matters

Traditional lending workflows often struggle with auditability and reproducibility.  
The Ledger addresses this by treating every domain action as an immutable event, making decisions replayable, explainable, and compliance-ready.

## What it demonstrates

- Event Sourcing + CQRS style architecture for financial decision systems
- Immutable event streams with optimistic concurrency control
- Projection daemon pattern for operational read models
- Upcasting strategy for schema evolution across event versions
- MCP tools/resources for lifecycle operations and observability
- Realistic synthetic dataset generation (profiles, financial docs, events)

## Architecture overview

- **Streams**: application lifecycle, agent telemetry, compliance outcomes, audit trail
- **Storage**: PostgreSQL-backed event store + projection checkpoints + outbox
- **Agents**: document/credit/fraud/compliance/decision flow modeling
- **Read Models**: application summary, agent performance, compliance audit views
- **Interfaces**: MCP server tools/resources for controlled interaction

![The Ledger Architecture](assets/mermaid-diagram-2026-03-22-010058.png)

## Tech stack

- Python (async-first patterns where needed)
- PostgreSQL + `asyncpg`
- Pydantic for typed event contracts
- FastMCP for MCP server integration
- Pytest + pytest-asyncio for validation

## Project structure

```text
ledger/
  agents/         # Agent behavior and orchestration primitives
  domain/         # Aggregates and domain logic
  schema/         # Typed event schemas and registry
  projections/    # Read-model builders and daemon
  mcp/            # MCP server, tools, and resources
datagen/          # Synthetic companies, documents, and event history generator
tests/            # Concurrency, projections, lifecycle, schema, and upcasting tests
```

## Quick start

```bash
# 1) Install dependencies
pip install -r requirements.txt

# 2) Start PostgreSQL
docker run -d --name the-ledger-db \
  -e POSTGRES_PASSWORD=apex \
  -e POSTGRES_DB=apex_ledger \
  -p 5432:5432 postgres:16

# 3) Generate realistic seed data + events
python datagen/generate_all.py --db-url postgresql://localhost/apex_ledger

# 4) Run tests
pytest -q
```

## Recruiter-ready highlights

- Models a high-stakes, compliance-sensitive business domain
- Applies production-grade backend patterns (event sourcing, OCC, projections, outbox)
- Includes deterministic simulation data for repeatable testing and demos
- Covers concurrency, lifecycle integrity, and schema evolution via tests
- Built to explain both **technical rigor** and **business impact** in interviews
