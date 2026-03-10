# Enterprise AI Architecture on Snowflake Cortex

**Experience with enterprise data engineering — now building production AI natively in Snowflake.**

[![Portfolio](https://img.shields.io/badge/Portfolio-shrikantlambe.github.io-29B5E8)](https://shrikantlambe.github.io) [![LinkedIn](https://img.shields.io/badge/LinkedIn-shrikantlambe-0077B5)](https://linkedin.com/in/shrikantlambe) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## What This Is

A **production-grade enterprise AI reference architecture** built natively on the Snowflake Data Cloud using Cortex AI. Three working demos, fully deployable in a Snowflake trial account in under 3 hours.

## Architecture Overview

```
Source Systems → Kafka/Snowpipe → Bronze (RAW) → Silver (dbt) → Gold (Governed)
                                                                      ↓
                                                             Cortex AI Layer
                                              ┌───────────────────────────────┐
                                              │  COMPLETE   │  SENTIMENT      │
                                              │  CLASSIFY   │  Cortex Analyst │
                                              │  ML FORECAST│  Cortex Search  │
                                              └───────────────────────────────┘
                                                                      ↓
                                              Sigma / Streamlit / API Consumers
```

## The Three Demos

### Demo 1 — Executive Summary Engine
| Attribute | Detail |
|---|---|
| **Cortex function** | `SNOWFLAKE.CORTEX.COMPLETE` |
| **Pattern** | Structured metrics → Prompt template → LLM → Governed summary |
| **Business value** | Board-ready executive summaries in <30 seconds from Gold layer |
| **Inspired by** | Production Workday Marketing AI project |

### Demo 2 — Customer Intelligence Pipeline
| Attribute | Detail |
|---|---|
| **Cortex functions** | `CORTEX.SENTIMENT` + `CORTEX.CLASSIFY_TEXT` |
| **Pattern** | Batch classification in Silver → materialized Gold → Streamlit dashboard |
| **Business value** | Automatic ticket triage, churn signal detection, recommended actions |

### Demo 3 — Conversational Analytics (Cortex Analyst)
| Attribute | Detail |
|---|---|
| **Cortex feature** | Cortex Analyst REST API + Semantic Model YAML |
| **Pattern** | Natural language → governed SQL → live results in chat UI |
| **Business value** | Self-service analytics for non-SQL users, with RBAC passthrough |

## Repository Structure

```
snowflake-cortex-architecture/
├── README.md
├── setup/
│   └── 00_master_setup.sql          # Full environment setup
├── demo1_executive_summary/
│   ├── 01_create_tables.sql
│   ├── 02_test_cortex_complete.sql
│   └── streamlit_app.py
├── demo2_ticket_intelligence/
│   ├── 01_create_tables.sql
│   ├── 02_classification_view.sql
│   ├── 03_gold_table.sql
│   └── streamlit_app.py
├── demo3_cortex_analyst/
│   ├── 01_star_schema.sql
│   ├── 02_semantic_model_setup.sql
│   ├── sales_analytics.yaml         # Corrected semantic model
│   └── streamlit_chat_app.py
└── architecture/
    └── index.html                   # Interactive architecture explorer
```

## Quick Start

1. **Create a Snowflake trial account** at [app.snowflake.com](https://app.snowflake.com) (select AWS us-east-1)
2. **Run the setup script**: Open Snowsight → New SQL Worksheet → paste `setup/00_master_setup.sql`
3. **Pick a demo** and follow the numbered SQL files in order
4. **Deploy the Streamlit app**: Snowsight → Projects → Streamlit → + New App → paste the Python file

## Key Architecture Decisions

**Why native Cortex over external LLM APIs?**
Data never leaves Snowflake's governance boundary. RBAC, row-level security, and column masking apply to AI outputs automatically. No separate API keys, no token budget tracking, no data movement audit trail.

**Why Medallion architecture?**
Bronze → Silver → Gold enforces quality contracts at each tier. AI functions run against Gold only — ensuring LLM inputs are validated, deduplicated, and typed before inference.

**Production additions (not in this demo):**
- Row-access policies per persona
- Column masking for PII
- TASK-scheduled batch inference
- AI output audit log table
- dbt tests on Gold before AI consumption

## About

Built by **Shrikant Lambe** — Extensive experience in enterprise data & AI at Workday, Lyft, Intuitive Surgical, and ServiceNow. Stanford AI-Driven Leadership · Cornell Data Analytics · BITS Pilani M.S.

- Portfolio: [shrikantlambe.github.io](https://shrikantlambe.github.io)
- LinkedIn: [linkedin.com/in/shrikantlambe](https://linkedin.com/in/shrikantlambe)
- Medium: [medium.com/@shrikantlambe](https://medium.com/@shrikantlambe)
