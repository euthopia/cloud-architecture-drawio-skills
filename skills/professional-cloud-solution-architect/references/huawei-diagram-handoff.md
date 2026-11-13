# Huawei Diagram Handoff

Pass this contract to `drawio-huawei`. Do not ask the diagram skill to infer
architecture decisions that should have been made by the solution architect.

## Required inputs

- objective, audience, scope, and selected viewpoint;
- facts, assumptions, open questions, and approved ADRs;
- actors, entry points, principal request/data flows, and protocols;
- Cloud, Region, VPC, AZ, Subnet, and on-premises/external boundaries;
- service instances, placement scope, and public/private exposure;
- identity, trust, encryption, secrets, logging, and policy boundaries;
- availability zones, redundancy model, state ownership, and dependencies;
- backup, replication, failover direction, RTO, and RPO;
- ingress, egress, NAT, private endpoints, and cross-boundary connections;
- labels or annotations required to communicate assumptions and risks.

## Acceptance review

After `drawio-huawei` validates and renders the diagram, confirm that:

1. Every service and connection maps to an approved architecture element.
2. Region/VPC/AZ/Subnet containment reflects actual service scope.
3. Trust boundaries and public exposure are visible and unambiguous.
4. HA and DR claims show distinct failure domains and recovery mechanisms.
5. Arrows communicate direction and meaning without crossing containers
   unnecessarily.
6. Official Huawei icons render correctly and remain editable in draw.io.
7. The visual hierarchy supports the intended audience and viewpoint.
8. The diagram, written recommendation, ADRs, and risk register agree.
