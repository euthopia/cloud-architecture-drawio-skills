---
name: drawio-huawei
description: Create professional, editable Huawei Cloud architecture diagrams with official color service icons, correct Region/VPC/AZ/Subnet containment, deterministic layout, semantic validation, and visual review. Use for Huawei topology, landing-zone, CCE, data/AI, security, hybrid, and DR diagrams. Do not use for text-only architecture advice.
---

# Draw.io Huawei Cloud

Use the locally installed `drawio-ai` Huawei extension. It compiles Huawei's
maintained color libraries into a searchable catalog and validates both diagram
geometry and Huawei-specific architecture semantics.

## Workflow

1. Confirm the correct kit:

   ```bash
   command -v drawio-ai
   drawio-ai root
   drawio-ai principles --mode huawei
   ```

   If Huawei mode is unavailable, stop instead of inventing service icons.

2. Reduce the request to actors, trust boundaries, primary flows, Region/VPC/AZ/
   Subnet placement, availability and RTO/RPO, security, operations, and explicit
   assumptions. For complex systems, use separate context, deployment/network,
   data/AI, security, and DR viewpoints as needed.

3. Run `drawio-ai scaffold --list` and copy the closest Huawei template. Resolve
   every service with one batched `drawio-ai search` query. Use returned
   `huawei_*` and `group_huawei_*` names exactly.

4. Build with `group`/`frame`/`grid`/`icon`/`box` and `renderTree`. Do not use
   hand-written topology coordinates. Prefer semantic containers:
   `group_huawei_cloud`, `group_huawei_region`, `group_huawei_vpc`,
   `group_huawei_availability_zone`, `group_huawei_subnet`, and
   `group_huawei_security_group`.

5. Keep one main reading direction. Use solid edges for primary request/data
   flow and dashed edges for policy, replication, telemetry, and audit.

## Architecture invariants

- Nest `Huawei Cloud → Region → VPC → AZ → Subnet → Security Group → resource`.
  A VPC belongs to one Region; multi-region systems use sibling VPCs.
- Keep IAM, CTS, CES/AOM/LTS, CDN, DNS, KMS/DEW, OBS buckets, and managed
  control planes outside workload Subnets. Put VPCEP or ENI-bound resources
  inside only when private connectivity is being modeled.
- Show VPN, Direct Connect, Cloud Connect, Enterprise Router, and VPCEP as
  nodes, not vague link labels.
- Show independent AZ placement and disclose shared failure points. One NAT
  Gateway across several AZs requires an explicit decision.
- Do not substitute AWS/Azure/GCP terminology or stencil IDs and do not recolor
  official Huawei icons.

Use `drawio-ai principles --mode huawei` as the detailed service-placement source.

## Icon integrity and delivery

Huawei SVG styles must use percent-encoded
`data:image/svg+xml,%3Csvg...`, never `data:image/svg+xml;base64,...` because
mxGraph splits style strings at semicolons. Preserve `catalogName=huawei_*` for
semantic validation.

Run the complete gate:

```bash
node build.mjs
drawio-ai validate output.drawio
drawio-ai suggest-layout output.drawio
drawio-ai render output.drawio --check -o output.png
```

Deliver the editable `.drawio` under the user's project only when validation is
clean and the rendered PNG confirms icons, labels, arrows, and boundaries. State
scope and assumptions; include Region, availability posture, and RTO/RPO when
relevant. If rendering is unavailable, disclose that limitation.
