# Cloud Architecture Draw.io Skills

> A pair of production-grade **Agent Skills** for designing **Huawei Cloud** solutions and rendering them as **editable draw.io architecture diagrams** — built on the cross-tool **Agent Skills** open standard (`SKILL.md`), so the same skill folders work in Claude Code, OpenAI Codex, Huawei CodeArts Agent, Cursor, GitHub Copilot, Gemini CLI and any other Agent Skills-compatible AI IDE.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Skills](https://img.shields.io/badge/skills-2-6a5acd)
![Format](https://img.shields.io/badge/format-SKILL.md-success)
![Platform](https://img.shields.io/badge/cloud-Huawei%20Cloud-C7000B)

---

## Table of contents

- [What is in this repository](#what-is-in-this-repository)
- [The two skills](#the-two-skills)
- [How the two skills work together](#how-the-two-skills-work-together)
- [Repository layout](#repository-layout)
- [Requirements & prerequisites](#requirements--prerequisites)
- [Installation](#installation)
  - [Option A — Universal one-liner (skills CLI)](#option-a--universal-one-liner-skills-cli)
  - [Option B — Manual copy (universal, any tool)](#option-b--manual-copy-universal-any-tool)
- [AI IDE integration guides](#ai-ide-integration-guides)
  - [Claude Code](#claude-code)
  - [OpenAI Codex (CLI / IDE extension / desktop)](#openai-codex-cli--ide-extension--desktop)
  - [Huawei CodeArts Agent](#huawei-codearts-agent)
  - [Cursor](#cursor)
  - [GitHub Copilot](#github-copilot)
  - [Gemini CLI and other Agent Skills tools](#gemini-cli-and-other-agent-skills-tools)
  - [Any other AI IDE (AGENTS.md / rules / MCP fallback)](#any-other-ai-ide-agentsmd--rules--mcp-fallback)
- [Using the skills](#using-the-skills)
- [Verifying the toolchain](#verifying-the-toolchain)
- [Troubleshooting](#troubleshooting)
- [Design principles baked into the skills](#design-principles-baked-into-the-skills)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## What is in this repository

This repository distributes **two complementary Agent Skills** for professional Huawei Cloud solution architecture:

| Skill | Role | Primary output |
| --- | --- | --- |
| [`professional-cloud-solution-architect`](skills/professional-cloud-solution-architect/SKILL.md) | The **architect**. Owns requirements discovery, target architecture, service selection, reviews, ADRs, security/resilience/operations/FinOps/migration. | A defensible, operable architecture (prose, decision tables, ADRs, views) — and, on request, an editable Huawei Cloud diagram. |
| [`drawio-huawei`](skills/drawio-huawei/SKILL.md) | The **diagram renderer**. Builds and validates editable Huawei Cloud `.drawio` files with official color service icons and correct Region/VPC/AZ/Subnet containment. | A validated, editable `.drawio` file (plus a rendered PNG self-check). |

Both skills use the **Agent Skills open standard** — a folder containing a `SKILL.md` with YAML front-matter (`name`, `description`) plus optional supporting files (`references/`, `assets/`). Because the format is portable, you install the *same* folders into whichever AI IDE your team uses.

---

## The two skills

### 1. `professional-cloud-solution-architect`

> Professional cloud, AI, and Huawei Cloud solution architecture for production systems.

**Use it for:** requirements discovery, target architecture, architecture review, service selection, security, resilience, operations, FinOps, migration, ADRs, or editable Huawei Cloud architecture diagrams.

**Highlights:**
- Turns ambiguous business goals into **defensible, operable architecture** — optimized for fitness to requirements, not service count.
- Explicitly separates **facts, assumptions, decisions, risks, and open questions**.
- Produces **at least two viable options** for material trade-offs, compared against the same criteria.
- Owns **view selection** (context, logical, deployment/network, data/AI, security, operations/DR).
- Bundled references for deep work:
  - [`references/architecture-quality-gates.md`](skills/professional-cloud-solution-architect/references/architecture-quality-gates.md) — quality gates for production designs and formal reviews.
  - [`references/ai-platform-review.md`](skills/professional-cloud-solution-architect/references/ai-platform-review.md) — AI/ML, RAG, agentic and inference review.
  - [`references/huawei-diagram-handoff.md`](skills/professional-cloud-solution-architect/references/huawei-diagram-handoff.md) — the handoff contract it passes to `drawio-huawei`.

### 2. `drawio-huawei`

> Create professional, editable Huawei Cloud architecture diagrams with official color service icons.

**Use it for:** Huawei topology, landing-zone, CCE, data/AI, security, hybrid, and DR diagrams. **Not** for text-only architecture advice.

**Highlights:**
- Uses the **official Huawei color service icons** (bundled Huawei color libraries under [`assets/color/`](skills/drawio-huawei/assets/color/)).
- Enforces correct **`Huawei Cloud → Region → VPC → AZ → Subnet → Security Group → resource`** containment.
- **Deterministic layout** via semantic containers — no hand-placed coordinates.
- **Semantic + geometric validation** and an optional **render self-check** using the `drawio-ai` CLI.
- Never recolors official Huawei icons and never substitutes AWS/Azure/GCP stencils.

---

## How the two skills work together

The skills are designed as a **two-stage pipeline**:

```
Business goal
   │
   ▼
professional-cloud-solution-architect        ← owns the architecture
   • requirements & NFRs
   • options + recommendation
   • views, flows, security, resilience, DR
   • ADRs, risks, migration plan
   │  (huawei-diagram-handoff contract)
   ▼
drawio-huawei                                ← owns rendering + validation
   • select official Huawei icons
   • place Region/VPC/AZ/Subnet/SG
   • validate geometry + semantics
   • render PNG self-check
   ▼
editable .drawio + reviewed PNG
```

- **Advisory / review work** → handled entirely by `professional-cloud-solution-architect`.
- **Architecture + editable Huawei diagram** → the architect decides, then invokes `drawio-huawei` to build and validate.
- **Diagram-only request** → sanity-check topology first, then render with `drawio-huawei`.

The skills reference each other by name, so when both are installed the routing happens automatically.

---

## Repository layout

```
cloud-architecture-drawio-skills/
├── README.md                      ← this file
├── LICENSE                        ← MIT (c) 2026 euthopia
└── skills/
    ├── drawio-huawei/
    │   ├── SKILL.md               ← skill definition (front-matter + workflow)
    │   └── assets/
    │       └── color/             ← 16 official Huawei color stencil libraries (.xml)
    │           ├── HWC Compute and Containers (color).xml
    │           ├── HWC Networking (color).xml
    │           └── ...
    └── professional-cloud-solution-architect/
        ├── SKILL.md
        └── references/
            ├── architecture-quality-gates.md
            ├── ai-platform-review.md
            └── huawei-diagram-handoff.md
```

Skills live under the top-level **`skills/`** directory using the conventional `skills/<skill-name>/SKILL.md` layout, which is what the Agent Skills tooling (Claude Code, Codex skill-installer, the `skills` CLI) expects.

---

## Requirements & prerequisites

The `professional-cloud-solution-architect` skill is **pure instructions** — no runtime needed beyond an AI agent that can read `SKILL.md`.

The `drawio-huawei` skill **drives the `drawio-ai` CLI** to search icons, validate and render diagrams. It requires:

| Requirement | Needed for | Notes |
| --- | --- | --- |
| **Node.js ≥ 18** | `drawio-ai` CLI | The CLI is a zero-dependency Node package. |
| **`drawio-ai` CLI (with Huawei catalog)** | icon search, `validate`, `suggest-layout`, `render` | Ships a `catalog/huawei.json` (260 Huawei icons + 8 Huawei group containers, `huawei_*` / `group_huawei_*` names). The skill also bundles the raw official Huawei color libraries in `assets/color/`. |
| *(Optional)* **draw.io desktop app** | `drawio-ai render --check` PNG self-check | Enables the visual review step; otherwise rendering is skipped and disclosed. |
| *(Optional)* **Graphviz** | large-graph auto-layout | Only for very large topologies. |

Install the `drawio-ai` kit globally:

```bash
npm install -g github:sparklabx/drawio-ai-kit
drawio-ai root          # prints the package root (contains catalog/huawei.json)
```

> **Why the Huawei catalog matters:** the upstream kit ships AWS/Azure/GCP/Databricks/BPMN catalogs plus a **Huawei** catalog. `drawio-huawei` expects Huawei service placement rules and `huawei_*` icon names. If your CLI does not yet expose `--mode huawei` for `principles`, point any command at the bundled catalog explicitly, e.g. `drawio-ai search "ECS" --catalog "$(drawio-ai root)/catalog/huawei.json"`, and use the placement invariants written in `skills/drawio-huawei/SKILL.md`. See [Troubleshooting](#troubleshooting).

---

## Installation

There are two general approaches. Pick the one that matches your team's workflow, then follow the per-IDE guide below for the exact folder.

### Option A — Universal one-liner (skills CLI)

The `skills` CLI (run via `npx skills`, no global install needed) auto-detects installed agents (Claude Code, Codex, Gemini CLI, …) and installs `SKILL.md`-based skills into the right place:

```bash
# Install both skills from this repo (auto-detects local AI agents)
npx skills add euthopia/cloud-architecture-drawio-skills

# Or pick skill(s) explicitly
npx skills add euthopia/cloud-architecture-drawio-skills --skill drawio-huawei
npx skills add euthopia/cloud-architecture-drawio-skills --skill professional-cloud-solution-architect

# Preview without installing
npx skills list euthopia/cloud-architecture-drawio-skills
```

Restart your agent afterwards, then ask it to *"design a Huawei Cloud 3-tier web app and produce an editable draw.io diagram."*

### Option B — Manual copy (universal, any tool)

```bash
git clone https://github.com/euthopia/cloud-architecture-drawio-skills.git
cd cloud-architecture-drawio-skills
```

Then copy each `skills/<name>` folder into the skills directory of your AI IDE (see the per-IDE guides). The skills are fully self-contained — copying the folder is enough; the agent reads `SKILL.md` and the supporting files.

---

## AI IDE integration guides

> All tools below consume the **same** `skills/<name>/SKILL.md` folders. The only thing that changes is *where* each tool looks for skills and *how* it is told about them.

### Claude Code

Claude Code supports Agent Skills natively — project and personal scopes.

**Install (project — shared with the repo / team):**
```bash
mkdir -p .claude/skills
cp -R skills/drawio-huawei .claude/skills/
cp -R skills/professional-cloud-solution-architect .claude/skills/
```

**Install (personal — your user only):**
```bash
mkdir -p ~/.claude/skills
cp -R skills/drawio-huawei ~/.claude/skills/
cp -R skills/professional-cloud-solution-architect ~/.claude/skills/
```

**Use:** Claude auto-loads a skill when relevant, or invoke it directly with `/drawio-huawei` or `/professional-cloud-solution-architect`. Supporting files (`references/`, `assets/`) are available to the skill on demand.

> Docs: <https://code.claude.com/docs/en/skills>

### OpenAI Codex (CLI / IDE extension / desktop)

Codex discovers skills under `$CODEX_HOME/skills/<name>` (default `~/.codex/skills`) and can install them straight from a GitHub repo with its bundled **skill-installer**.

**Install with the skill-installer (recommended):**
```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo euthopia/cloud-architecture-drawio-skills \
  --path skills/drawio-huawei skills/professional-cloud-solution-architect
```

**Or install manually:**
```bash
mkdir -p ~/.codex/skills
cp -R skills/drawio-huawei ~/.codex/skills/
cp -R skills/professional-cloud-solution-architect ~/.codex/skills/
```

**Use:** skills become available on the next turn. Codex also reads `AGENTS.md`; see the [generic fallback](#any-other-ai-ide-agentsmd--rules--mcp-fallback) if you prefer to reference the skills from `AGENTS.md` instead of installing them.

> Skills installed into `$CODEX_HOME/skills` are picked up automatically; private repos can use `GITHUB_TOKEN`/`GH_TOKEN`.

### Huawei CodeArts Agent

Huawei **CodeArts Agent** is enterprise-first with multi-surface delivery (IDE + VS Code/JetBrains plugins + CLI/TUI + Agent Space), **spec-driven development with reusable skills**, **MCP tool integration**, and project **rules / `AGENTS.md`** support. Use the standard `SKILL.md` folders:

**Steps:**
1. **Get the skill folders** into your CodeArts Agent workspace — clone this repo next to your project and keep the `skills/` directory:
   ```bash
   git clone https://github.com/euthopia/cloud-architecture-drawio-skills.git
   ```
2. **Register the skills** in your CodeArts Agent configuration / Agent Space using your version's "custom skills" or "skills repository" mechanism. Point it at the `skills/drawio-huawei` and `skills/professional-cloud-solution-architect` folders (or your team's shared skills repo). Because the folders follow the Agent Skills open standard, a build that supports `SKILL.md` skills can consume them as-is.
3. **Expose the toolchain** — for `drawio-huawei`, make sure the agent's execution sandbox has **Node ≥ 18** and the **`drawio-ai` CLI** on `PATH`. You can also register `drawio-ai` as an **MCP tool** so the agent can call icon search / validate / render directly.
4. **Fallback** — if your CodeArts Agent build only supports project rules, add a short pointer in its rules/`AGENTS.md` (see [generic fallback](#any-other-ai-ide-agentsmd--rules--mcp-fallback)).

> Menu names differ across CodeArts Agent versions; if a specific panel isn't obvious, use the rules/`AGENTS.md` pointer — it works on every build that reads project instructions.

### Cursor

Cursor reads project rules from `.cursor/rules` and supports `AGENTS.md`. It does not use a `skills/` directory natively, so use the rules pointer:

**Option 1 — thin rules file** `.cursor/rules/cloud-architecture-skills.mdc`:
```markdown
---
description: Huawei Cloud architecture + draw.io diagram skills
globs: ["**/*"]
---
When the task involves cloud/AI/Huawei Cloud architecture or editable Huawei
Cloud diagrams, read and follow:
- skills/professional-cloud-solution-architect/SKILL.md
- skills/drawio-huawei/SKILL.md   (requires the drawio-ai CLI on PATH)
```

**Option 2 — `AGENTS.md`** at the repo root with the same pointer (see below).

### GitHub Copilot

Copilot supports custom instructions via `.github/copilot-instructions.md`, scoped `*.instructions.md` files, and MCP. Use an instructions file that points to the skills:

`.github/copilot-instructions.md`:
```markdown
## Huawei Cloud architecture & diagrams
- Architecture: follow skills/professional-cloud-solution-architect/SKILL.md
- Editable Huawei Cloud diagrams: follow skills/drawio-huawei/SKILL.md
  (requires the drawio-ai CLI; register it as an MCP/CLI tool if available)
```

You can additionally register `drawio-ai` as an MCP server so the coding agent can run `search` / `validate` / `render`.

### Gemini CLI and other Agent Skills tools

Any tool that implements the **Agent Skills open standard** can load these folders directly. For Gemini CLI and similar CLIs that read a `SKILL.md`-based skills directory, copy the folders into that tool's skills path (often `~/.gemini/skills/` or a project `skills/` directory) or use the universal installer:

```bash
npx skills add euthopia/cloud-architecture-drawio-skills
```

If a particular tool exposes skills through a plugins/marketplace mechanism, publish or import this repo as a skill source.

### Any other AI IDE (AGENTS.md / rules / MCP fallback)

The lowest-common-denominator integration works in **every** tool that reads project instructions (`AGENTS.md`, rules files, or a system-prompt file). Add a short pointer so the agent knows the skills exist and where their instructions live:

```markdown
## Cloud architecture skills

This repository ships two Agent Skills. Read the relevant SKILL.md before acting.

- Huawei Cloud solution architecture (requirements, reviews, ADRs, service selection,
  security, resilience, FinOps, migration): read
  `skills/professional-cloud-solution-architect/SKILL.md`
- Editable Huawei Cloud draw.io diagrams (official icons, Region/VPC/AZ/Subnet
  containment, validation, render check): read `skills/drawio-huawei/SKILL.md`.
  Requires the `drawio-ai` CLI (Node >= 18) on PATH.
```

**If your tool supports MCP**, you can also wrap the `drawio-ai` CLI as an MCP tool so the agent invokes icon search, validation and rendering as first-class tool calls.

---

## Using the skills

Once installed, drive the skills with natural-language prompts. Good starting prompts:

**Architecture (uses `professional-cloud-solution-architect`)**
- *"Design a production-grade 3-tier web application on Huawei Cloud in `cn-north-4`. Give me the target architecture, at least two options for the compute tier, NFRs, a risk register, and an ADR for the chosen option."*
- *"Review this Huawei Cloud landing-zone design for availability, security and cost gaps, and list the failure domains and shared single points of failure."*
- *"Plan a migration from an on-prem VMware estate to Huawei Cloud with phases, rollback and exit criteria."*

**Diagram (uses `drawio-huawei`, often invoked by the architect)**
- *"Produce an editable Huawei Cloud draw.io diagram for that architecture, showing Region → VPC → AZ → Subnet → Security Group placement, with public/private ingress, a NAT gateway and an OBS bucket outside the workload subnets."*
- *"Draw a Huawei Cloud CCE reference architecture with independent AZs, an ELB ingress, RDS primary/standby, and a DR Region. Validate it and render a PNG self-check."*

**Combined (architect → diagram handoff)**
- *"Architect a 2-region active/standby DR solution for Huawei Cloud, then render it as a validated editable `.drawio` file."*

The architect emits a structured **handoff contract** (`references/huawei-diagram-handoff.md`) so the renderer receives objective, scope, boundaries, flows, RTO/RPO and service placement — not guesses.

---

## Verifying the toolchain

After installing the skill and the CLI, confirm the `drawio-huawei` toolchain is healthy before relying on it:

```bash
# 1. CLI present and locatable
command -v drawio-ai
drawio-ai root

# 2. Huawei catalog is reachable and queryable
drawio-ai categories | head
drawio-ai search "ECS Elastic Cloud Server" --catalog "$(drawio-ai root)/catalog/huawei.json" --limit 3

# 3. Full diagram quality gate (run against a generated file)
drawio-ai validate output.drawio
drawio-ai suggest-layout output.drawio
drawio-ai render output.drawio --check -o output.png   # needs draw.io desktop for PNG
```

If `search` returns `huawei_*` / `group_huawei_*` entries, the Huawei catalog is wired up correctly.

---

## Troubleshooting

| Symptom | Cause | Fix |
| --- | --- | --- |
| `drawio-ai: command not found` | CLI not installed / not on `PATH` | `npm install -g github:sparklabx/drawio-ai-kit`; ensure the global npm bin dir is on `PATH`. |
| `Unknown --mode "huawei". Valid modes: aws, azure, gcp, databricks, bpmn` | Your `drawio-ai` build does not yet expose Huawei as a first-class `principles` mode. | Use the bundled catalog: `drawio-ai search "<service>" --catalog "$(drawio-ai root)/catalog/huawei.json"`, and follow the placement invariants in `skills/drawio-huawei/SKILL.md`. Older/newer kit versions differ here. |
| Icon search returns nothing | Wrong/absent catalog | Confirm `$(drawio-ai root)/catalog/huawei.json` exists; pass it with `--catalog`. |
| `render` fails or produces no PNG | draw.io desktop app not installed | Install the draw.io desktop app to enable `render --check`, or skip rendering and disclose that visual review was not performed. |
| Garbled CJK/Huawei labels in a diagram | Terminal/locale encoding | Work in a UTF-8 environment; keep labels UTF-8. |
| Skill never triggers in the agent | Skill not in the tool's skills path, or no rules pointer | Verify the folder is under the tool's skills directory (see per-IDE guide) or add the `AGENTS.md`/rules pointer. |
| Agent "invents" icons | `drawio-ai` not available to the agent's sandbox | Ensure Node ≥ 18 + `drawio-ai` are available **inside** the agent runtime, or register `drawio-ai` as an MCP tool. |

---

## Design principles baked into the skills

These rules are enforced by the skill instructions themselves:

- **Fitness over decoration** — architecture is optimized for requirements, not service count or visual complexity.
- **Facts vs. assumptions** — uncertainty is made explicit; assumptions are labelled.
- **Options, not a single answer** — material trade-offs get at least two viable options compared on the same criteria.
- **Correct containment** — `Huawei Cloud → Region → VPC → AZ → Subnet → Security Group → resource`; a VPC belongs to exactly one Region.
- **Managed control planes stay outside workload subnets** — IAM, CTS, CES/AOM/LTS, CDN, DNS, KMS/DEW, OBS buckets and managed control planes are placed outside workload subnets unless private connectivity is being modeled.
- **Failure domains, not marketing** — a design is never called "highly available" merely because it uses managed services; actual failure domains, dependencies, health signals and recovery mechanisms must be identified.
- **Official icon integrity** — Huawei SVGs use percent-encoded `data:image/svg+xml,...` (never base64, which mxGraph splits at `;`), with `catalogName=huawei_*` preserved for semantic validation.
- **Evidence discipline** — a cloud service capability is never asserted from memory when it affects correctness; it is marked for verification.

See each skill's `SKILL.md` for the full workflow and invariants.

---

## Contributing

Issues and pull requests are welcome.

- Keep each skill self-contained under `skills/<skill-name>/` with a valid `SKILL.md` front-matter (`name`, `description`).
- Preserve structure and naming in `drawio-huawei/assets/color/` — these are the official Huawei color libraries.
- When updating a skill, keep the `professional-cloud-solution-architect` ↔ `drawio-huawei` handoff contract (`references/huawei-diagram-handoff.md`) consistent.
- Validate any generated `.drawio` with `drawio-ai validate` before proposing diagram changes.

---

## License

Released under the **MIT License** — see [LICENSE](LICENSE). Copyright © 2026 euthopia.

---

## Acknowledgements

- Huawei Cloud **official color service icon libraries**, bundled under `drawio-huawei/assets/color/`.
- The **`drawio-ai` / `drawio-ai-kit`** project (sparklabx) — the zero-dependency CLI for ground-truth stencil catalogs, layout principles and structural validation.
- The **Agent Skills open standard** (`SKILL.md`), which makes these skills portable across Claude Code, OpenAI Codex, Huawei CodeArts Agent and other AI IDEs.
