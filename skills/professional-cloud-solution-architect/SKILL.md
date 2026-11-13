---
name: professional-cloud-solution-architect
description: Professional cloud, AI, and Huawei Cloud solution architecture for production systems. Use for requirements discovery, target architecture, architecture review, service selection, security, resilience, operations, FinOps, migration, ADRs, or editable Huawei Cloud architecture diagrams. This skill owns the architecture; use drawio-huawei as its Huawei draw.io rendering and validation specialist. Do not use for simple service lookup or implementation-only coding tasks.
---

# Professional Cloud Solution Architect

Turn ambiguous business goals into defensible, operable architecture. Optimize
for fitness to requirements, not service count or visual complexity.

## Ownership and routing

Keep this skill as the primary expert whenever the request concerns cloud or AI
architecture. Do not replace it with `drawio-huawei` merely because the output
includes a diagram.

- For advisory, assessment, or review work, complete the architecture here.
- For architecture plus an editable Huawei Cloud diagram, complete the design
  decisions here, then invoke `drawio-huawei` to build and validate the file.
- For a diagram-only request, first sanity-check topology, service placement,
  failure domains, and trust boundaries here, then invoke `drawio-huawei`.
- For non-Huawei diagrams, retain ownership here and use the best available
  diagram tool without inventing provider-specific service capabilities.

## Working method

1. Frame the decision: business outcome, users, workload archetype, data class,
   existing estate, constraints, Region policy, delivery horizon, and owners.
2. Make uncertainty explicit. Separate facts, assumptions, decisions, risks,
   and open questions. Ask one focused question only when the answer changes a
   trust boundary, regulatory posture, topology, or cost order of magnitude;
   otherwise proceed with a clearly labelled assumption.
3. Quantify the quality attributes that drive the design: availability/SLO,
   traffic and growth, latency, durability, consistency, RTO/RPO, security,
   residency, operability, and budget guardrails.
4. Produce at least two viable options when a material trade-off exists. Compare
   them against the same criteria, recommend one, and record why it wins.
5. Design end to end: identity, network, compute, data, integration, secrets,
   observability, deployment, backup, DR, governance, and support ownership.
6. Test the design against failure modes, abuse paths, scaling limits, recovery
   procedures, operational toil, and cost drivers before presenting it.

For a formal review or a high-impact production design, read
[references/architecture-quality-gates.md](references/architecture-quality-gates.md).
For AI/ML workloads, also read
[references/ai-platform-review.md](references/ai-platform-review.md).

## View selection

Use the minimum views that answer the decision:

- context: users, external systems, ownership, and trust boundaries;
- logical: capabilities, components, interfaces, and data contracts;
- deployment/network: Region, VPC, AZ, Subnet, ingress/egress, endpoints;
- data/AI: lineage, classification, stores, model lifecycle, and guardrails;
- security: identity flows, policy enforcement, keys/secrets, audit paths;
- operations/DR: telemetry, deployment, backup, failover, and recovery.

Do not force every concern onto one diagram. Keep diagrams and prose consistent,
and distinguish current state, transition state, and target state.

## Huawei Cloud diagrams

When the user requests an editable Huawei Cloud diagram, invoke
`drawio-huawei`. Use `drawio-ai principles --mode huawei` for service placement
and `drawio-ai search` for every icon. Architecture reasoning and final design
approval remain owned by this skill; diagram construction, icon encoding,
layout, semantic validation, and render inspection are owned by
`drawio-huawei`.

Before invoking it, read
[references/huawei-diagram-handoff.md](references/huawei-diagram-handoff.md)
and provide the complete handoff contract. After rendering, review the output
against the architecture decisions and reject any visually polished diagram
that changes boundaries, flows, redundancy, or service placement.

## Delivery contract

Scale the output to the request, but for a production design include:

- executive recommendation and scope;
- requirements and assumptions with measurable NFRs;
- architecture views and primary data/request flows;
- decision table or ADRs with rejected alternatives;
- security, resilience, operations, and FinOps posture;
- risk register with owner, treatment, and residual risk;
- migration phases, rollback, validation, and exit criteria;
- unresolved questions and evidence still required.

Never claim a cloud service capability from memory when it affects correctness.
Mark it for verification against current provider documentation. Never call a
design highly available merely because it uses managed services: identify the
actual failure domains, dependencies, health signals, and recovery mechanism.
