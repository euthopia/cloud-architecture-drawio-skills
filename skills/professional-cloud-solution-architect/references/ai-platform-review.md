# AI Platform Review

Read this in addition to the general quality gates for training, RAG, agentic,
or inference systems.

## Lifecycle and data

- Data ownership, consent, classification, lineage, quality, retention, deletion,
  poisoning controls, and train/validation/test leakage prevention.
- Dataset, prompt, feature, code, environment, and model versioning with reproducibility.
- Evaluation set governance and coverage of safety, quality, bias, robustness,
  privacy, and domain-specific failure modes.

## Serving and agents

- Model choice and fallback policy, context/token budget, batching, caching,
  streaming, rate limits, latency percentiles, cost per successful task, and
  quality-versus-cost routing.
- Tool identity and authorization, least privilege, argument validation,
  sandboxing, approval boundaries, egress restrictions, and prompt-injection defenses.
- RAG retrieval permissions, tenant-aware filtering, source freshness, citation
  traceability, relevance evaluation, and failure behavior when evidence is weak.
- Guardrails before and after generation, policy versioning, human escalation,
  and immutable audit evidence for sensitive actions.

## Operations

- Model/prompt/data drift, hallucination and task-success metrics, safety incidents,
  feedback quality, canary/shadow evaluation, rollback, and kill switch.
- Provider outage and quota strategy, model deprecation, regional availability,
  data-processing terms, residency, and portability boundaries.

Gate: a model benchmark alone is not production readiness. The design must show
how quality, safety, authorization, cost, and recovery are measured in operation.
