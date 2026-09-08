# AETHER — AI Incident Intelligence Platform

> Evidence-driven incident investigation for engineering teams.

AETHER combines telemetry correlation, retrieval, and LLM reasoning to turn fragmented operational signals into an auditable incident investigation: **symptoms → evidence → root-cause hypothesis → remediation**.

## Why this project

Production incidents rarely live in one data source. Logs explain symptoms, traces explain execution paths, deployments explain change, and runbooks explain known recovery paths. AETHER is designed around the principle that an AI incident assistant should **retrieve and connect evidence before generating an explanation**.

## Architecture

```text
┌──────────────────────┐
│ React + TypeScript   │  Operator UI
└──────────┬───────────┘
           │
┌──────────▼───────────┐
│ FastAPI              │  API / orchestration
└──────────┬───────────┘
           │
┌──────────▼───────────┐
│ Correlation + RAG    │  evidence retrieval
└──────────┬───────────┘
           │
     ┌─────┴─────┐
     ▼           ▼
 PostgreSQL   Claude API
 + pgvector   reasoning
     │           │
     └─────┬─────┘
           ▼
   RCA + evidence + remediation
```

### Evidence flow

`Logs → Traces → Deployments → Commits/PRs → Retrieval → Correlation → LLM synthesis → RCA`

## Core capabilities

- **Telemetry ingestion:** logs, stack traces, deployment metadata, incidents, and OpenTelemetry traces
- **Semantic retrieval:** operational knowledge indexed with PostgreSQL + pgvector
- **Incident correlation:** connects symptoms with services, changes, ownership, and historical incidents
- **Evidence-backed RCA:** distinguishes retrieved evidence from generated synthesis
- **Remediation recommendations:** produces actionable next steps rather than a generic incident summary
- **Safety controls:** confidence thresholds, validation, human review, and audit logging
- **Observability:** metrics and traces for the AI pipeline itself

## Evaluation

The project reports results from an **840-case incident benchmark**:

| Metric | Reported result |
|---|---:|
| Top-1 diagnostic accuracy | **94.2%** |
| Precision | **95.4%** |
| Recall | **91.8%** |
| False-positive rate | **2.18%** |
| Triage-time reduction | **40%** |
| Platform availability | **99.9%** |

These are **project-reported evaluation results**, not independently audited production benchmarks. The implementation and evaluation workflow are the source of truth.

## Technology

**AI:** Claude API · LangChain · RAG  
**Backend:** Python · FastAPI  
**Data:** PostgreSQL · pgvector  
**Frontend:** React · TypeScript  
**Observability:** OpenTelemetry · Prometheus  
**Deployment:** Docker · AWS

## Engineering principles

1. **Evidence before generation** — retrieve the signals needed to support an explanation.
2. **Evaluation before optimization** — define measurable failure modes and track them.
3. **Human control for high-impact actions** — recommendations are not autonomous production changes.
4. **Observability for AI systems** — latency, retrieval quality, errors, and outputs all need visibility.

## How to evaluate the project

When reviewing this repository, focus on four questions:

1. Can the ingestion and retrieval path be reproduced locally?
2. Is the evidence chain inspectable rather than hidden inside a prompt?
3. Can benchmark cases and metrics be rerun independently?
4. Are failure modes, validation, and human-review paths explicit?

## Repository guide

Use the repository tree as the source of truth for the current implementation.

```text
backend/         API, orchestration, retrieval, RCA
frontend/        operator interface
evaluation/      benchmark and evaluation workflows
infrastructure/ deployment configuration
tests/           automated validation
```

## Status

🚧 **Active engineering project**

Current work centers on stronger reproducible evaluation, richer telemetry integrations, and production-grade deployment workflows.

## Author

**Naga Lokesh Sai Alla**  
[GitHub](https://github.com/lokesh8286235) · [LinkedIn](https://linkedin.com/in/naga-lokesh-sai-alla-538242251) · [Portfolio](https://portfolio-r7n2.vercel.app)
