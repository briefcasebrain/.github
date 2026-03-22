# Briefcase AI

Open-source decision tracking for AI. Record, replay, and audit every AI decision.

```bash
pip install briefcase-ai
```

## What It Does

Briefcase captures immutable snapshots of every AI decision — the exact inputs, model parameters, outputs, confidence scores, costs, and execution context. You can replay any decision deterministically, detect behavioral drift across model versions, and instrument existing frameworks with 2–3 lines of code.

```python
from briefcase import capture

@capture
def classify(text):
    return model.predict(text)

# Every call is now recorded: inputs, outputs, model, cost, latency.
```

## Core Capabilities

**Decision Recording** — Capture inputs, outputs, model parameters, costs, and metadata for every AI call. Stored as immutable snapshots.

**Deterministic Replay** — Re-run any recorded decision with identical inputs. Compare outputs across model versions, prompt changes, or config updates.

**Drift Detection** — Measure how model behavior changes over time. Track consistency scores, detect outliers, get alerts when outputs shift.

**Cost Tracking** — Per-call cost estimation with built-in pricing for major providers. Set budgets and get alerts.

**PII Sanitization** — Automatically redact sensitive data (SSNs, credit cards, emails, phone numbers, API keys) before snapshots are stored.

**Framework Integrations** — Drop-in instrumentation for LangChain, CrewAI, LlamaIndex, AutoGen, AG2, OpenAI Agents, and lakeFS. Add 2–3 lines, capture everything.

**Storage Adapters** — Pluggable backends: SQLite for local dev, lakeFS for versioned data lakes, plus DVC, Nessie, Pachyderm, and more.

**OpenTelemetry Native** — Standardized AI semantic conventions. Compatible with any OTel backend (Datadog, Grafana, Honeycomb).

## Architecture

```
Your AI Agent → Briefcase SDK → Storage Backend → Replay & Analysis
                    │                │
              @capture decorator   Immutable decision snapshots
              Framework hooks      SQLite / lakeFS / VCS
```

17K lines of Rust core. Python SDK via PyO3. Apache-2.0.

## Get Started

📖 **Docs**: [briefcaseai.io](https://briefcaseai.io)
📦 **PyPI**: [briefcase-ai](https://pypi.org/project/briefcase-ai/)
🚀 **Quick Start**: [briefcaseai.io/getting-started/quickstart](https://briefcaseai.io/getting-started/quickstart)

## Repositories

| Repo | Description |
|------|-------------|
| [briefcase-ai-sdk](https://github.com/briefcasebrain/briefcase-ai-sdk) | Rust core + Python SDK |
| [briefcase-ai-sdk-docs](https://github.com/briefcasebrain/briefcase-ai-sdk-docs) | Documentation site (briefcaseai.io) |
