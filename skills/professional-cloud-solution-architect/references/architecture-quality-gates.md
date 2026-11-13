# Architecture Quality Gates

Use these gates for production designs, formal reviews, migrations, and designs
with material security, availability, regulatory, or cost impact. Tailor depth
to risk; do not pad a small design with irrelevant sections.

## 1. Problem and evidence

- Business outcome, success metric, scope, exclusions, stakeholders, and owner.
- Current-state evidence: topology, traffic, incidents, cost, dependencies, and
  operational pain. Distinguish measured facts from estimates.
- Constraints: provider/Region, residency, compliance, skills, contracts,
  deadlines, legacy integration, and budget.
- Workload archetype: synchronous web/API, event-driven, batch/data, streaming,
  AI training/inference, edge, or mixed.

Gate: each major design decision traces to a requirement, constraint, or risk.

## 2. Quantified non-functional requirements

Capture units, target, measurement window, and owner for:

- availability/SLO and error-budget policy;
- peak and steady throughput, concurrency, payload size, growth, and seasonality;
- latency percentiles at the user boundary, not only component averages;
- durability, consistency, retention, and deletion requirements;
- RTO/RPO by business capability and dependency;
- data classification, residency, recovery geography, and audit retention;
- cost envelope, unit-cost metric, and forecast confidence.

Gate: no "high availability", "low latency", or "scalable" without a measurable target.

## 3. Boundaries and flows

- Show actors, external systems, ownership, trust zones, and data classes.
- Trace ingress, east-west, egress, management, deployment, telemetry, backup,
  replication, and break-glass paths separately.
- Name protocols, authentication, encryption, throttling, retries, timeouts,
  idempotency, ordering, and backpressure where they affect behavior.
- Identify synchronous dependency chains and blast-radius boundaries.

Gate: every arrow has a purpose; every trust-boundary crossing has a control.

## 4. Security and privacy

- Federated identity, least privilege, workload identity, short-lived credentials,
  separation of duties, privileged access, and emergency access.
- Private connectivity and controlled egress by default; explicit public exposure.
- Encryption in transit and at rest, key ownership/rotation, secret lifecycle,
  certificate lifecycle, and sensitive-data discovery/masking.
- Threat model abuse cases: spoofing, tampering, data disclosure, denial of
  service, privilege escalation, supply chain, and tenant isolation.
- Preventive, detective, responsive, and recovery controls with evidence sources.

Gate: security controls have owners and observable evidence, not only product names.

## 5. Reliability and disaster recovery

Build a compact failure-mode table with component/dependency, failure, user
impact, detection, automatic response, manual recovery, RTO/RPO, and test cadence.

Check host, process, node, AZ, Region, network, identity, DNS, quota, deployment,
operator, data corruption, and third-party failure. Verify that redundancy does
not share a hidden dependency. State consistency and split-brain behavior.

Gate: failover and restore are tested procedures with acceptance criteria;
backup existence alone is not recovery readiness.

## 6. Performance and scale

- Capacity model with bottlenecks, quotas, saturation signals, and headroom.
- Horizontal/vertical scaling trigger, stabilization, scale-to-zero, and warm-up.
- Caching policy, invalidation, hot-key/partition handling, and load shedding.
- Performance test shape reflects production traffic and dependency behavior.

Gate: the design identifies the first likely bottleneck and how it is detected.

## 7. Operations and delivery

- Service ownership, on-call, runbooks, escalation, dependency map, and support plan.
- SLI/SLO dashboards, logs, metrics, traces, audit events, alert quality, and cost telemetry.
- Immutable/repeatable deployment, policy as code, artifact provenance, scanning,
  staged rollout, rollback, schema compatibility, and configuration drift control.
- Day-2 procedures: patching, certificate/key rotation, quota management,
  access review, restore, failover, and decommissioning.

Gate: a named team can operate the system without the original architect present.

## 8. FinOps and sustainability

- Cost model by major driver and unit metric; baseline, peak, and growth scenarios.
- Commitment versus elasticity decision, storage lifecycle, data transfer,
  observability volume, licenses, idle capacity, and DR duplication.
- Budgets, anomaly detection, allocation tags/projects, showback/chargeback, and
  rightsizing cadence.

Gate: cost is an observable architecture attribute with an owner and guardrails.

## 9. Decision and delivery readiness

For each material choice record context, options, criteria, decision, consequences,
reversibility, trigger to revisit, and owner. Maintain a risk register with
likelihood, impact, treatment, owner, due date, and residual risk.

Migration phases need entry/exit criteria, dependency order, data migration and
reconciliation, coexistence, rollback, security review, load test, DR exercise,
and decommission plan.

Gate: the recommendation is actionable, testable, reversible where practical,
and explicit about accepted risk.
