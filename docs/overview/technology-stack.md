# ProvaAI Technology Stack

ProvaAI is split across three main repositories that together deliver a virtual try-on product for fashion e-commerce:

- `prova-ai-api` — backend API, domain services, and infrastructure-as-code
- `prova-ai-ui` — merchant/admin web application
- `prova-ai-widget` — Shopify app plus storefront widget/extension

This page normalizes the stack across those repositories so the rest of the documentation can refer to one shared technical baseline.

---

## 1. Stack at a Glance

| Layer | Primary technologies | Role in the product |
|---|---|---|
| Merchant/admin frontend | Next.js 14, React 18, TypeScript, Tailwind CSS, Zustand, Framer Motion | Merchant-facing dashboard, product management, protected app flows |
| Storefront / Shopify experience | React Router 7, React 18, TypeScript, Shopify App Bridge, Polaris, Theme App Extension, Vite | Embedded Shopify app plus storefront virtual try-on widget |
| Backend application | .NET 10, C# 14, ASP.NET Core, modular class-library architecture | Core business logic, auth, product/store management, fitting-session orchestration |
| AI workflow | Gemini-based image-generation workflow | Generates the virtual try-on result from shopper photo + product image |
| Data and state | PostgreSQL, Redis, Prisma, EF Core | Durable application data, session/state support, caching |
| Object/file storage | Google Cloud Storage | Product images and fitting-session assets |
| Platform and runtime | Kubernetes, Kustomize, Helm, Traefik | App runtime, ingress, environment overlays, platform components |
| Infrastructure as code | Terraform | Cloud foundation and per-environment provisioning |
| Observability | SigNoz, Prometheus, Grafana | Application telemetry plus cluster/workload monitoring |
| CI/CD and developer workflow | GitHub Actions, Taskfile, Tilt, DevBox | Build/test/promotion automation and local environment workflows |

---

## 2. Frontend Stack (`prova-ai-ui`)

### Core technologies

| Technology | Version / evidence | Why it is used |
|---|---|---|
| Next.js | 14.2.5 | App Router-based web application for merchant/admin flows |
| React | 18.2.0 | Component model for the dashboard UI |
| TypeScript | 5.5.4 | Type safety across UI code and API boundaries |
| Tailwind CSS | 3.4.13 | Utility-first styling for the app shell and screens |
| Zustand | 4.5.2 | Lightweight client-side state for auth and permissions flows |
| Framer Motion | 12.x | Interaction polish and motion in the UI |
| TanStack React Query | 5.x | Present as dependency and ready for richer data-fetching patterns |

### Product role

The UI repository powers the authenticated management surface for the product. Based on the repo docs and structure, it covers:

- login and protected navigation
- dashboard and metrics views
- product gallery and fitting-result browsing
- virtual try-on flow from the web app side
- proxy/auth patterns for talking to the backend API

### Architectural style

The UI uses a modern React/Next split with:

- route-based screens under `src/app/`
- shared components under `src/components/`
- HTTP/proxy and domain helpers under `src/lib/`
- state and permission helpers under `src/store/`

---

## 3. Shopify App + Widget Stack (`prova-ai-widget`)

### Core technologies

| Technology | Version / evidence | Why it is used |
|---|---|---|
| React Router | 7.12.x | Shopify app shell and route handling |
| React | 18.3.x | UI foundation for the embedded app and widget tooling |
| TypeScript | 5.9.x | Type safety across app, widget, and services |
| Shopify App Bridge React | 4.2.x | Embedded Shopify app integration |
| Shopify Polaris | 13.9.x | Admin-facing Shopify-consistent UI components |
| Prisma | 6.16.x | App persistence for Shopify/session-related data |
| Vite | 6.x | Fast build pipeline, especially for the storefront widget bundle |
| Tailwind CSS | 4.1.x | Utility-first styling in the widget/application experience |
| Framer Motion | 12.x | Motion and interaction polish in the widget flow |
| Vitest + Testing Library + axe-core | 4.x / 16.x / 4.11.x | Unit, UI, and accessibility-oriented testing |

### Shopify-specific building blocks

The repository combines multiple concerns in one codebase:

1. **Embedded Shopify app**
   - manages app auth/session and merchant-facing admin flows
2. **Theme App Extension**
   - injects the virtual try-on entry point into the product detail page (PDP)
3. **Storefront widget runtime**
   - captures user input, uploads images, polls for results, and renders the try-on experience

### Architectural style

The widget architecture is explicitly layered:

- presentation components
- custom hooks for state and process orchestration
- services for API and validation logic
- utilities for logging, constants, error handling, and motion primitives

That separation is one of the strongest implementation details in the product because it keeps storefront UX concerns separate from business-process orchestration.

---

## 4. Backend and Domain Stack (`prova-ai-api`)

### Core technologies

| Technology | Version / evidence | Why it is used |
|---|---|---|
| .NET | 10 | Main runtime for the backend and supporting libraries |
| C# | 14 | Primary application language |
| ASP.NET Core | .NET web application | HTTP API and service host |
| Entity Framework Core | referenced across backend docs | Persistence and database access |
| PostgreSQL | 16 via CloudNativePG | Main relational datastore |
| Redis | Bitnami Helm deployment | Cache and fast-access state |
| Mapster | backend service docs | Object mapping across layers |
| RestSharp / HTTP clients | backend service docs | Integration with external services |

### Architectural style

The backend repo is more than a web API. It acts as the platform center of gravity for the whole product by combining:

- HTTP API surface
- domain services and shared contracts
- infrastructure modules and deployment definitions
- tests and operational docs

At a service level, the repo is organized as modular libraries such as:

- `ProvaAI.API`
- `ProvaAI.Fitting`
- `ProvaAI.Stores`
- `ProvaAI.Users`
- `ProvaAI.Payments`
- `ProvaAI.Integrations.Stripe`
- `ProvaAI.Integrations.Shopify`
- shared libraries under `src/shrd/`

### Notable backend responsibilities

- authentication/session flows consumed by the UI
- store and catalog management
- fitting-session lifecycle management
- AI orchestration for virtual try-on generation
- storage/file handling
- integration surfaces for Shopify and payment-related workflows

---

## 5. AI and Integration Stack

| Integration | Role |
|---|---|
| Gemini-based image generation workflow | Generates virtual try-on outputs from shopper input plus product references |
| Shopify | Merchant integration, storefront widget placement, app auth/webhooks, storefront configuration |
| Stripe | Payment-related integration support in the backend service landscape |
| Google Cloud Storage | File/object storage for product and fitting-session assets |

### Why this matters

The product is not just a CRUD application. Its core experience depends on coordinating:

- a shopper-facing storefront interaction
- a merchant-facing administration surface
- an asynchronous AI/media-processing backend workflow
- external commerce and cloud integrations

---

## 6. Data, Persistence, and Storage

| Concern | Technology | Notes |
|---|---|---|
| Main transactional database | PostgreSQL | Hosted in Kubernetes via CloudNativePG |
| Cache / short-lived access | Redis | Used for fast state and application support patterns |
| Shopify app persistence | Prisma | Used in the widget/app repository |
| File/object storage | Google Cloud Storage | Stores images and generated artifacts |

This split reflects the product’s mixed operational needs: relational business data, cached runtime state, and image-heavy media flows.

---

## 7. Infrastructure and Platform Stack

### Core platform components

| Area | Technology | Role |
|---|---|---|
| Container orchestration | Kubernetes | Runs platform services and product workloads |
| App overlays | Kustomize | Environment-specific app deployment composition |
| Platform packaging | Helm | Installs/manages shared platform services |
| Ingress | Traefik | HTTP ingress and routing |
| Database operator | CloudNativePG | PostgreSQL management inside the cluster |
| Secrets management | External Secrets Operator | Syncs secret material from cloud secret stores |
| Telemetry | SigNoz | Application telemetry collection |
| Metrics | Prometheus + Grafana | Cluster/workload visibility and dashboards |

### Deployment model

The infrastructure follows a clean three-layer split:

1. **Terraform** for cloud foundation
2. **Platform Kubernetes components** for shared services
3. **Application overlays** for environment-specific runtime deployment

That model is central to the technical story of ProvaAI because it shows a clear separation between cloud provisioning, platform operations, and application delivery.

---

## 8. Developer Workflow and Delivery Tooling

| Tooling | Role |
|---|---|
| GitHub Actions | CI/CD, build/test, image promotion |
| Taskfile | Standard task runner for deployment and ops workflows |
| Tilt | Local Kubernetes development loop |
| DevBox | Local toolchain/bootstrap management |
| Docker / container images | Packaging and deployment artifact |

### Delivery pattern

The backend/infrastructure docs describe an environment-aware promotion model where staging and production overlays are updated via CI instead of mutating one shared deployment definition. That is a strong signal of deliberate release engineering rather than ad hoc deployment.

---

## 9. Stack Characteristics Worth Highlighting in the Portfolio

From a portfolio perspective, the most valuable stack characteristics are:

1. **Multi-surface product architecture**
   - merchant/admin UI
   - Shopify app
   - storefront widget
   - backend platform

2. **AI woven into a production-style workflow**
   - image upload
   - asynchronous processing
   - result retrieval
   - storage lifecycle

3. **Infrastructure maturity beyond the app code**
   - Terraform + Kubernetes layering
   - platform components as first-class concerns
   - observability and secret-management patterns

4. **Clear separation of concerns**
   - layered widget architecture
   - modular backend services
   - environment-specific deployment overlays

---

## 10. Notes on Versioning and Scope

This stack summary is based on the current repository manifests and technical docs reviewed on **2026-06-22**.

Where historical notes disagree with live manifests, the package manifests and current deployment structure take precedence.
