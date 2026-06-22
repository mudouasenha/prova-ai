# ProvaAI Portfolio Documentation Plan

> **For Hermes:** Use this plan to build a public-facing portfolio repository that works for both recruiters and senior engineers. Keep the intro accessible, then progressively increase technical depth.

**Goal:** Turn this repository into a polished public technical showcase of the ProvaAI product, its architecture, infrastructure, repository landscape, and implementation decisions.

**Audience:** Primary split audience — recruiters/hiring managers first, then senior engineers/tech leads deeper in the docs.

**Documentation mode:** Balanced hybrid — concise showcase README + deep technical handbook under `docs/`.

**Visibility constraint:** Public repo. Reuse only information already present in the existing private repos and knowledge base. Do not introduce secrets, internal-only credentials, or operational details that exceed the current public-safe boundary.

---

## 1. Success Criteria

The final repository should include at minimum:

1. A strong root `README.md` that quickly explains the product and technical scope.
2. A clear **Technology Stack** section.
3. A complete **Infrastructure** section drawing from `prova-ai-api/dply` and deployment docs.
4. A **repository-by-repository breakdown** explaining purpose, tech, and architecture.
5. A **system architecture diagram** for the whole product.
6. A place for **screenshots/prints** to be added later without restructuring the repo.
7. Additional “showcase” material that highlights engineering decisions, tradeoffs, and lessons.

---

## 2. Recommended Repository Structure

```text
README.md
assets/
  diagrams/
  screenshots/
docs/
  overview/
    product-summary.md
    technology-stack.md
    repository-map.md
  architecture/
    system-architecture.md
    request-and-data-flows.md
    engineering-decisions.md
  infrastructure/
    infrastructure-overview.md
    kubernetes-and-terraform.md
    environments-and-deployment.md
    observability-and-operations.md
  repositories/
    prova-ai-api.md
    prova-ai-ui.md
    prova-ai-widget.md
  showcase/
    screenshots.md
    notable-engineering-work.md
    lessons-learned.md
  references/
    source-inventory.md
```

### Structure rationale

- `README.md` handles fast evaluation.
- `docs/overview` orients a non-specialist reader.
- `docs/architecture` explains the system design.
- `docs/infrastructure` is where the most senior technical material lives.
- `docs/repositories` provides repo-level drill-down.
- `docs/showcase` frames the work as portfolio material rather than raw internal documentation.
- `assets/diagrams` and `assets/screenshots` let visuals be added cleanly later.

---

## 3. Recommended README Shape

The root `README.md` should be optimized for a 30-60 second scan.

### Proposed sections

1. **Title + One-line Product Summary**
   - What ProvaAI is
   - What business problem it solves

2. **Why This Project Is Technically Interesting**
   - Multi-repo product
   - AI-powered virtual try-on workflow
   - Shopify integration
   - Kubernetes/Terraform-based infrastructure

3. **High-Level Architecture Diagram**
   - One diagram showing UI, API, widget, infra, and external services

4. **Technology Stack**
   - Short table by layer

5. **Repository Map**
   - `prova-ai-api`
   - `prova-ai-ui`
   - `prova-ai-widget`

6. **Infrastructure Highlights**
   - Environment model
   - K8s + Terraform layering
   - Observability stack
   - CI/CD promotion model

7. **Screenshots / Product Tour**
   - Placeholder section now, actual images later

8. **Deep-Dive Docs Index**
   - Links to `/docs/**`

9. **Key Engineering Contributions / Takeaways**
   - Best place to surface your portfolio value explicitly

---

## 4. Documentation Tone Rules

### README tone
- recruiter-friendly
- plain English
- compact and impressive
- minimal jargon unless immediately useful

### Deep docs tone
- senior-engineer friendly
- precise and structured
- diagram- and table-heavy when useful
- explain decisions, not just components

### Global tone rules
- avoid hype language
- prefer concrete system facts
- distinguish current state vs historical/refactor history
- never include secrets, raw tokens, internal URLs that should not be public, or unsafe operational specifics

---

## 5. Source Material Inventory

Use the existing repos and knowledge base as source-of-truth inputs.

### A. Backend and infrastructure
Primary sources:
- `prova-ai-api/README.md`
- `prova-ai-api/src/docs/deployment/README.md`
- `prova-ai-api/src/docs/deployment/deployment.md`
- `prova-ai-api/dply/**`
- `prova-ai-api/src/srvcs/**/README.md`

Best current infrastructure synthesis source:
- `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Infrastructure/ProvaAI Infrastructure - Phases 10-14 Refactor.md`

### B. Frontend UI
Primary sources:
- `prova-ai-ui/README.md`
- `prova-ai-ui/docs/ai-context/CONTEXTO_PROJETO.md`
- `prova-ai-ui/src/**`

Use carefully:
- `prova-ai-ui/docs/ai-context/ARCHITECTURE_REVIEW.md`
  - useful for tradeoffs, cleanup insights, and architecture commentary
  - not ideal as canonical portfolio copy without reframing

### C. Shopify widget
Primary sources:
- `prova-ai-widget/prova-ai-widget/README.md`
- `prova-ai-widget/prova-ai-widget/docs/architecture.md`
- `prova-ai-widget/prova-ai-widget/docs/WIDGET_ARCHITECTURE.md`
- `knowledge/Knowledge Graph/04 Product Development/ProvaAI/Shopify/**`

### D. Visual assets
Existing likely reusable brand assets:
- `prova-ai-ui/public/brand/provaai-mark.png`
- `prova-ai-widget/prova-ai-widget/assets/ProvaAILogo-removebg-preview.png`

### E. Existing plans already in this portfolio repo
- `docs/plans/2026-04-21-shopify-studio-fittingsession-flow.md`

---

## 6. Proposed Documentation Content by File

### `docs/overview/product-summary.md`
Purpose:
- explain the product in product + technical terms

Include:
- product goal
- primary user journeys
- major system actors (shopper, merchant/admin, backend services)
- how AI is used in the workflow

### `docs/overview/technology-stack.md`
Purpose:
- present a single normalized stack table across repos

Include tables for:
- frontend
- backend
- widget/shopify
- infrastructure/platform
- observability
- external integrations

### `docs/overview/repository-map.md`
Purpose:
- explain how the product is split into repositories

Include per repo:
- purpose
- audience/users
- primary technologies
- responsibilities
- dependencies on other repos/services

### `docs/architecture/system-architecture.md`
Purpose:
- explain the whole system composition

Include:
- high-level product diagram
- main runtime boundaries
- where each repo fits
- external dependencies (Shopify, Stripe, Gemini, GCS, etc.)

### `docs/architecture/request-and-data-flows.md`
Purpose:
- explain important flows

Prioritize:
1. user virtual try-on flow
2. merchant/admin dashboard flow
3. Shopify widget flow
4. media/storage flow
5. deployment/promote flow (optional)

### `docs/architecture/engineering-decisions.md`
Purpose:
- show technical judgment, not just inventory

Include:
- why multi-repo
- why Kustomize overlays + Terraform env roots
- why widget architecture is layered
- how observability evolved
- tradeoffs and compromises

### `docs/infrastructure/infrastructure-overview.md`
Purpose:
- provide the readable infrastructure story

Include:
- GCP/GKE context
- three-layer infra model
- environment strategy
- platform services
- ingress, storage, secrets, observability

### `docs/infrastructure/kubernetes-and-terraform.md`
Purpose:
- detail `dply`-driven structure

Include:
- Terraform module/env split
- K8s platform vs app split
- overlays
- what is Helm-managed vs Kustomize-managed

### `docs/infrastructure/environments-and-deployment.md`
Purpose:
- explain local/staging/prod and promotion flow

Include:
- environment comparison table
- local dev path
- staging/prod promotion model
- CI/CD summary

### `docs/infrastructure/observability-and-operations.md`
Purpose:
- demonstrate production-minded engineering

Include:
- SigNoz role
- Prometheus/Grafana role
- current observability boundaries
- secret management model
- operational lessons learned

### `docs/repositories/prova-ai-api.md`
Purpose:
- deep dive on the backend and infrastructure repo

Include:
- repo role
- stack
- domain modules/services
- deployment ownership
- why this repo is the platform center of gravity

### `docs/repositories/prova-ai-ui.md`
Purpose:
- deep dive on the dashboard/front-end repo

Include:
- role in product
- auth/proxy model
- key UI areas
- architecture notes and tradeoffs

### `docs/repositories/prova-ai-widget.md`
Purpose:
- deep dive on the Shopify/widget repo

Include:
- Shopify app + extension role
- layered widget architecture
- merchant/shopper flow
- relationship to backend APIs

### `docs/showcase/screenshots.md`
Purpose:
- stable place to attach screenshots later

Use a fixed layout such as:
- Landing / intro
- Admin dashboard
- Product gallery
- Virtual try-on experience
- Shopify storefront widget
- Infra / architecture visuals

### `docs/showcase/notable-engineering-work.md`
Purpose:
- explicitly frame your contribution and technical depth

Possible sections:
- infra refactor and environment separation
- deployment standardization
- Shopify/widget integration design
- AI workflow integration
- observability and ops maturity

### `docs/showcase/lessons-learned.md`
Purpose:
- show senior reflection

Include:
- what worked
- what was hard
- what you would improve next
- what this project taught about product/infra boundaries

### `docs/references/source-inventory.md`
Purpose:
- track which existing source docs feed the new portfolio docs
- useful while authoring and updating

---

## 7. Diagram Strategy

Use a two-level diagram strategy.

### Level 1: README diagram
One clean, simplified diagram for fast understanding.

Suggested nodes:
- User / Shopper
- Merchant / Admin
- Prova AI UI
- Prova AI Widget (Shopify)
- Prova AI API
- PostgreSQL / Redis / GCS
- Shopify / Stripe / Gemini
- GKE / ingress boundary

### Level 2: Deep-dive diagrams in `docs/`
Create separate diagrams for:
1. full product architecture
2. infrastructure layering
3. deployment/environment model
4. widget request flow
5. try-on flow end-to-end

### Diagram source approach
- Reuse repo- and knowledge-based Mermaid material where possible
- Redraw for readability instead of copying large internal diagrams verbatim
- Keep portfolio diagrams cleaner and more presentation-oriented than internal engineering diagrams

---

## 8. Screenshot Strategy

Do not block documentation authoring on screenshots.

### Phase 1
- create `assets/screenshots/`
- create `docs/showcase/screenshots.md`
- use placeholders and a naming convention

### Naming convention
```text
assets/screenshots/
  01-home-or-overview.png
  02-dashboard.png
  03-product-gallery.png
  04-virtual-try-on-flow.png
  05-shopify-widget.png
  06-infra-diagram.png
```

### Embed style
Each screenshot entry should include:
- title
- what the screen demonstrates
- why it matters technically or from a product perspective

---

## 9. Public-Safety Rules

Before publishing any section, verify:

- no secrets
- no raw access tokens
- no private cluster/internal-only details that should not be exposed
- no credentials copied from historic docs
- no operational steps that reveal sensitive environment specifics beyond what is safe for a public portfolio

When in doubt:
- abstract exact values
- keep topology and architectural decisions
- remove sensitive identifiers if they are not essential to the story

---

## 10. Execution Phases

### Phase 1 — Foundation
Create:
- `README.md`
- `assets/diagrams/`
- `assets/screenshots/`
- docs directory skeleton
- `docs/references/source-inventory.md`

### Phase 2 — Core narrative
Write:
- `docs/overview/product-summary.md`
- `docs/overview/technology-stack.md`
- `docs/overview/repository-map.md`

### Phase 3 — Architecture
Write:
- `docs/architecture/system-architecture.md`
- `docs/architecture/request-and-data-flows.md`
- `docs/architecture/engineering-decisions.md`

### Phase 4 — Infrastructure
Write:
- `docs/infrastructure/infrastructure-overview.md`
- `docs/infrastructure/kubernetes-and-terraform.md`
- `docs/infrastructure/environments-and-deployment.md`
- `docs/infrastructure/observability-and-operations.md`

### Phase 5 — Repository deep dives
Write:
- `docs/repositories/prova-ai-api.md`
- `docs/repositories/prova-ai-ui.md`
- `docs/repositories/prova-ai-widget.md`

### Phase 6 — Showcase layer
Write:
- `docs/showcase/notable-engineering-work.md`
- `docs/showcase/lessons-learned.md`
- `docs/showcase/screenshots.md`

### Phase 7 — Polish
- tighten README
- improve diagrams
- add screenshots
- cross-link docs
- final public-safety review

---

## 11. Suggested Authoring Order

Author in this order:

1. `docs/references/source-inventory.md`
2. `docs/overview/technology-stack.md`
3. `docs/overview/repository-map.md`
4. `docs/architecture/system-architecture.md`
5. `docs/infrastructure/infrastructure-overview.md`
6. `README.md`
7. remaining deep docs

Rationale:
- normalize facts first
- define architecture second
- write the public README after the core facts are stable

---

## 12. Specific Guidance for This Portfolio

Emphasize these strengths because they are portfolio-relevant:

1. **Multi-repo system thinking**
   - product split across API, UI, and Shopify widget

2. **Infrastructure maturity**
   - Terraform + K8s environment model
   - platform/app separation
   - CI/CD promotion model

3. **AI product integration**
   - virtual try-on flow
   - external AI dependency in a productized workflow

4. **Shopify integration complexity**
   - storefront widget + merchant/admin + backend coordination

5. **Operational awareness**
   - observability stack
   - secrets model
   - deployment ergonomics

6. **Engineering judgment**
   - tradeoffs, evolution, and lessons learned

Do not over-emphasize low-value details like exhaustive file trees or incidental setup commands in the README. Those belong deeper in docs only if they help explain architecture.

---

## 13. Next Recommended Task

The next best task is:

**Create the documentation skeleton and source inventory first**, then draft the README and core architecture docs from the strongest existing sources (`prova-ai-api` deployment docs, the infra refactor knowledge note, and the widget architecture doc).

---

## 14. Approval Gate

Before implementation, confirm these defaults:

- language: English
- diagrams: Mermaid in Markdown
- screenshots: added later by filename placeholders first
- audience split: recruiter-friendly README, technical deep dives in `docs/`

If approved, execute Phase 1 next.
