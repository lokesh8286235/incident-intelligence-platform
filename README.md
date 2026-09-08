# AETHER — AI Incident Intelligence Platform

> Evidence-driven incident investigation for engineering teams.

AETHER combines **telemetry correlation, retrieval, and LLM reasoning** to turn fragmented operational signals into an auditable investigation:

**symptoms → evidence → root-cause hypothesis → remediation**

## Why this project matters

Production incidents rarely live in one data source. Logs explain symptoms, traces explain execution paths, deployments explain change, and runbooks explain known recovery paths.

AETHER is built around a simple engineering principle:

> **Retrieve and connect evidence before generating an explanation.**

The system is designed to make the evidence chain inspectable and to keep generated synthesis distinct from retrieved operational facts.

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

| Capability | Purpose |
|---|---|
| **Telemetry ingestion** | Logs, stack traces, deployments, incidents, and OpenTelemetry traces |
| **Semantic retrieval** | Operational knowledge indexed with PostgreSQL + pgvector |
| **Incident correlation** | Connect symptoms with services, changes, ownership, and historical incidents |
| **Evidence-backed RCA** | Separate retrieved evidence from generated synthesis |
| **Remediation recommendations** | Produce actionable next steps rather than generic summaries |
| **Safety controls** | Confidence thresholds, validation, human review, and audit logging |
| **AI observability** | Metrics and traces for the pipeline itself |

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

## How the system is evaluated

```text
Incident case
     │
     ▼
Telemetry + change context
     │
     ▼
Retrieve candidate evidence
     │
     ▼
Correlate services / changes / history
     │
     ▼
Generate RCA hypothesis
     │
     ▼
Validate against benchmark
     │
     ▼
Measure accuracy / precision / recall / false positives
```

The goal is not merely to produce plausible incident summaries; it is to measure whether the proposed diagnosis is supported by the available evidence.

## Safety model

AETHER intentionally keeps high-impact actions under human control:

- Generated recommendations are not autonomous production changes.
- Confidence thresholds can gate uncertain diagnoses.
- Audit logging preserves the investigation trail.
- Evidence is presented separately from model-generated synthesis.

## Technology

**AI:** Claude API · LangChain · RAG  
**Backend:** Python · FastAPI  
**Data:** PostgreSQL · pgvector  
**Frontend:** React · TypeScript  
**Observability:** OpenTelemetry · Prometheus  
**Deployment:** Docker · AWS

## Repository guide

```text
backend/         # API, orchestration, retrieval, RCA
frontend/        # operator interface
evaluation/      # benchmark and evaluation workflows
infrastructure/  # deployment configuration
tests/           # automated validation
```

## Questions a reviewer should be able to answer

1. Can the ingestion and retrieval path be reproduced locally?
2. Is the evidence chain inspectable rather than hidden inside a prompt?
3. Can benchmark cases and metrics be rerun independently?
4. Are validation, failure modes, and human-review paths explicit?

## Status

🚧 **Active engineering project**

Current work centers on reproducible evaluation, richer telemetry integrations, and production-grade deployment workflows.

## Author

**Naga Lokesh Sai Alla**  
[GitHub](https://github.com/lokesh8286235) · [LinkedIn](https://linkedin.com/in/naga-lokesh-sai-alla-538242251) · [Portfolio](https://portfolio-r7n2.vercel.app)
