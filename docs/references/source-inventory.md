# ProvaAI Portfolio Source Inventory

**Purpose:** Track which existing private-repo and knowledge-base materials feed the public portfolio documentation.

**Audience:** Internal authoring reference only. This file helps keep the portfolio docs accurate and traceable.

**Last reviewed:** 2026-06-22

---

## 1. Source Priority Rules

When there is overlap or inconsistency, use this priority order:

1. **Code and deploy structure** = executable truth
2. **Repo-local technical docs** = implementation truth
3. **Knowledge Graph notes** = historical/contextual truth
4. **Planning docs and review docs** = supporting interpretation, not canonical facts

### Public-safety rule
Only promote information into public portfolio docs when it is:
- architecturally useful
- already safe to describe at a high level
- free of secrets, tokens, private credentials, or sensitive operator detail

---

## 2. Portfolio Deliverables → Source Mapping

| Portfolio doc | Primary sources | Notes |
|---|---|---|
| `README.md` | `prova-ai-api/README.md`, infra refactor knowledge note, widget architecture docs, package manifests | Fast, recruiter-friendly summary only |
| `docs/overview/product-summary.md` | `prova-ai-ui/docs/ai-context/CONTEXTO_PROJETO.md`, widget README, API README | Rewrite in cleaner public English |
| `docs/overview/technology-stack.md` | `prova-ai-ui/package.json`, `prova-ai-widget/prova-ai-widget/package.json`, `prova-ai-api/README.md`, deployment docs | Normalize versions and roles by layer |
| `docs/overview/repository-map.md` | repo READMEs + package manifests + backend service docs | Explain repo boundaries and responsibilities |
| `docs/architecture/system-architecture.md` | infra refactor knowledge note, widget architecture doc, deployment README | Redraw into cleaner portfolio diagrams |
| `docs/architecture/request-and-data-flows.md` | UI context doc, widget architecture, Shopify knowledge notes, backend docs | Prioritize try-on + widget flows |
| `docs/architecture/engineering-decisions.md` | infra refactor knowledge note, architecture review doc, deployment docs | Focus on tradeoffs and reasoning |
| `docs/infrastructure/infrastructure-overview.md` | `prova-ai-api/src/docs/deployment/README.md`, infra refactor knowledge note | Best core infra sources |
| `docs/infrastructure/kubernetes-and-terraform.md` | `prova-ai-api/dply/**`, deployment docs | Use directory structure as source of truth |
| `docs/infrastructure/environments-and-deployment.md` | `prova-ai-api/README.md`, deployment docs, CI/CD references in knowledge note | Explain local/staging/prod and promotion |
| `docs/infrastructure/observability-and-operations.md` | infra refactor knowledge note, monitoring README, deployment docs | Keep public-safe and architectural |
| `docs/repositories/prova-ai-api.md` | API README, deployment docs, service READMEs under `src/srvcs/**` | Strongest technical deep dive |
| `docs/repositories/prova-ai-ui.md` | UI README, UI context doc, code structure under `src/` | Treat old review docs as supporting only |
| `docs/repositories/prova-ai-widget.md` | widget README, `docs/architecture.md`, Shopify knowledge notes | Strong portfolio story for integrations |
| `docs/showcase/notable-engineering-work.md` | infra refactor note, deployment docs, widget architecture, UI architecture notes | Explicitly surface engineering depth |
| `docs/showcase/lessons-learned.md` | infra refactor note, architecture review doc, implementation plans | Reflection doc, not pure inventory |
| `docs/showcase/screenshots.md` | future screenshots from the user | Use placeholders first |

---

## 3. Core Source Files

### A. Product + backend + infra

#### `prova-ai-api/README.md`
Best for:
- backend overview
- deployment model summary
- concise infra positioning

Reusable facts:
- .NET backend identity
- three-layer deployment model
- role of `dply/`

#### `prova-ai-api/src/docs/deployment/README.md`
Best for:
- environment model
- platform/app separation
- deployment commands and conceptual structure
- observability/security sections to summarize safely

Reusable facts:
- Terraform env roots
- platform Helm components
- app Kustomize overlays
- local/staging/prod deployment approach

#### `prova-ai-api/dply/**`
Best for:
- actual infrastructure structure
- what exists vs what is only described

Reusable facts:
- folder topology
- ownership boundaries
- platform components present in the repo

Do **not** copy blindly:
- environment-specific sensitive values
- raw operational snippets that are too implementation-specific for a public portfolio README

---

### B. Knowledge Graph — infrastructure

#### `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Infrastructure/ProvaAI Infrastructure - Phases 10-14 Refactor.md`
Best for:
- strongest current architecture narrative
- Mermaid diagrams to adapt
- refactor story
- observability evolution
- CI/CD and environment decisions

This is the single best source for:
- infra storytelling
- tradeoffs
- notable engineering work

#### `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Infrastructure/ProvaAI Infrastructure MOC.md`
Best for:
- summary and navigation
- identifying supporting notes

#### `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Infrastructure/ProvaAI Infrastructure - Ownership and Environment Model.md`
Best for:
- detailed explanation of environment and ownership decisions

Use when writing:
- `engineering-decisions.md`
- `environments-and-deployment.md`

---

### C. UI sources

#### `prova-ai-ui/README.md`
Best for:
- current UI stack snapshot
- dashboard/front-end role
- local integration notes

#### `prova-ai-ui/package.json`
Best for:
- exact current frontend stack versions

#### `prova-ai-ui/docs/ai-context/CONTEXTO_PROJETO.md`
Best for:
- product flow summary
- route/function overview
- frontend/backend interaction hints

Use carefully:
- content may be partially historical
- rewrite and verify against code where needed

#### `prova-ai-ui/docs/ai-context/ARCHITECTURE_REVIEW.md`
Best for:
- architectural tradeoffs
- refactor observations
- examples of complexity and cleanup opportunities

Use as:
- commentary source
- lessons-learned source
- not canonical truth by itself

---

### D. Shopify / widget sources

#### `prova-ai-widget/prova-ai-widget/README.md`
Best for:
- public-friendly explanation of the widget
- shopper flow
- merchant activation concept

#### `prova-ai-widget/prova-ai-widget/docs/architecture.md`
Best for:
- layered widget architecture
- component/service/hook breakdown
- initialization and try-on flows

#### `prova-ai-widget/prova-ai-widget/package.json`
Best for:
- exact widget/app stack
- framework and testing toolchain

#### `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Shopify/ProvaAI - Shopify Integration MOC.md`
Best for:
- map of Shopify-related knowledge
- locating deeper contract notes

#### `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Shopify/**`
Best for:
- Shopify auth/session context
- storefront/widget deployment context
- contract and workflow details

---

## 4. Supporting Source Files by Use Case

### For repository deep dives
Use these backend service docs where helpful:
- `prova-ai-api/src/srvcs/ProvaAI.API/README.md`
- `prova-ai-api/src/srvcs/ProvaAI.Fitting/README.md`
- `prova-ai-api/src/srvcs/ProvaAI.Stores/README.md`
- `prova-ai-api/src/srvcs/ProvaAI.Users/README.md`
- `prova-ai-api/src/srvcs/ProvaAI.Payments/README.md`
- `prova-ai-api/src/srvcs/ProvaAI.Integrations.Stripe/README.md`

### For observability/infrastructure operations
Use these selectively:
- `prova-ai-api/dply/k8s/platform/monitoring/README.md`
- `prova-ai-api/dply/k8s/platform/tailscale/README.md`
- `prova-ai-api/src/docs/deployment/monitoring-setup.md`
- `prova-ai-api/src/docs/deployment/cicd-setup.md`

### For flow-level explanations
Potentially useful:
- `docs/plans/2026-04-21-shopify-studio-fittingsession-flow.md`
- widget architecture docs
- Shopify contract notes in the knowledge graph

---

## 5. Facts Already Strong Enough to Reuse

These are already strongly supported across sources and can be promoted into portfolio docs after wording cleanup:

1. ProvaAI is a **virtual try-on product** for apparel/e-commerce use cases.
2. The product is split across at least three main repos:
   - `prova-ai-api`
   - `prova-ai-ui`
   - `prova-ai-widget`
3. The backend/infra repo uses a **three-layer deployment model**:
   - Terraform cloud foundation
   - Kubernetes platform components
   - application overlays
4. The platform includes or references:
   - GKE
   - Traefik
   - PostgreSQL via CloudNativePG
   - Redis
   - SigNoz
   - Prometheus/Grafana
   - External Secrets
5. The widget has a **layered React architecture** with components, hooks, services, and utilities.
6. The product involves integrations such as:
   - Shopify
   - Stripe
   - Gemini / AI image-generation workflow
   - GCS/storage

---

## 6. Facts That Need Careful Framing or Re-Verification

Before promoting these to public docs, re-check wording and sensitivity:

1. Exact runtime versions that differ across historical docs
2. Specific GCP project identifiers if they are unnecessary for the public story
3. Internal URLs, tunnels, or operator access paths
4. Credentials, rotation notes, or exposed-secret history details
5. Historical architecture-review opinions that may no longer reflect the current system
6. Cost numbers if they are presented as current rather than point-in-time estimates

---

## 7. Diagram Reuse Candidates

Adapt, don’t copy raw, from these sources:

1. `ProvaAI Infrastructure - Phases 10-14 Refactor.md`
   - architecture overview Mermaid
   - deployment structure Mermaid
   - CI/CD Mermaid

2. `prova-ai-widget/prova-ai-widget/docs/architecture.md`
   - widget layered architecture
   - initialization flow
   - try-on flow

Recommended adaptation strategy:
- README gets one simplified diagram
- deep docs get cleaner, purpose-specific diagrams
- portfolio versions should be visually lighter than the internal engineering originals

---

## 8. Screenshot Placeholders to Prepare For

Expected future images from the user:
- overview / landing screenshot
- dashboard screenshot
- product gallery screenshot
- virtual try-on flow screenshot
- Shopify widget screenshot
- infra/diagram screenshot if desired

Store under:
- `assets/screenshots/`

Reference from:
- `docs/showcase/screenshots.md`
- optionally `README.md`

---

## 9. Recommended Next Authoring Targets

Write next, in order:

1. `docs/overview/technology-stack.md`
2. `docs/overview/repository-map.md`
3. `docs/architecture/system-architecture.md`
4. `docs/infrastructure/infrastructure-overview.md`
5. `README.md`

This order stabilizes facts before the public-facing narrative.
