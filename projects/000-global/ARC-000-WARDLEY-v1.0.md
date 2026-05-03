# ArcKit as a Service — Wardley Map (Strategic Positioning)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:wardley`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-WARDLEY-v1.0 |
| **Document Type** | Wardley Map (strategic) |
| **Project** | Cross-project (000-global) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) |
| **Distribution** | ARB; Vendor SLT; ARB-equivalent strategy advisers |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial Wardley map for ArcKit (SaaS + sovereign), with components, evolution stages, dependencies, and strategic gameplay (build/buy/host) decisions. |

---

## 1. User Need at the Top of the Map

The anchor user need: **a verified UK SME or government-cleared user can produce defensible architecture governance evidence quickly enough that the procurement / accreditation barrier is no longer disqualifying**.

Two related anchor needs:

- **SME supplier** (project 001 SD-7, SD-6): "I want to win Government work without bidding-against-incumbents-with-EA-teams handicap."
- **Customer Accreditor** (project 002 SD-1): "I want defensible evidence that my deployment of ArcKit is supply-chain-trustworthy and safe to operate inside my boundary."

---

## 2. Map (Conceptual)

```mermaid
flowchart LR
  classDef genesis fill:#fbb,stroke:#900;
  classDef custom fill:#fdb,stroke:#a60;
  classDef product fill:#fffaa0,stroke:#aa8;
  classDef commodity fill:#cfc,stroke:#080;

  U[User Need: defensible EA evidence on demand]:::genesis

  ARC[ArcKit application — domain logic, AI prompts, governance templates]:::custom
  ADP[AI Adaptor — provider-agnostic]:::custom
  CELL[Cell-management automation]:::custom
  BUNDLE[Sovereign bundle pipeline + signing]:::custom
  AUDIT[Tenant-visible audit log]:::custom
  EXPORT[Deterministic export + round-trip test]:::custom
  TENISO[Tenant isolation discipline / CI suite]:::custom

  GOVTPL[GOV.UK Design System]:::product
  OIDC[OIDC / SAML federation]:::product
  K8S[Managed Kubernetes]:::product
  PG[Postgres + S3-compatible storage]:::commodity
  KMS[KMS / HSM]:::product
  OBS[OpenTelemetry + managed backend]:::product
  AI[Frontier AI providers]:::product
  COSIGN[Sigstore / cosign / SBOM tooling]:::product
  HYP[UK hyperscaler region]:::commodity
  CO[Customer-supplied identity / KMS / observability (sovereign)]:::commodity
  IDP[GOV.UK One Login]:::product

  U --> ARC
  ARC --> ADP
  ARC --> CELL
  ARC --> AUDIT
  ARC --> EXPORT
  ARC --> TENISO
  ARC --> GOVTPL
  ARC --> OIDC
  OIDC --> IDP
  ARC --> K8S
  ARC --> PG
  ARC --> KMS
  ARC --> OBS
  ADP --> AI
  ARC --> BUNDLE
  BUNDLE --> COSIGN
  K8S --> HYP
  PG --> HYP
  KMS --> HYP
  OBS --> HYP
  ARC -.sovereign profile.-> CO
```

(Stages: Genesis → Custom-built → Product → Commodity, left to right.)

---

## 3. Component Evolution Posture

| Component | Stage | Posture (build / buy / host / use) | Source |
|-----------|-------|-------------------------------------|--------|
| ArcKit application (domain + templates) | Custom | **Build** (sustained core capability) | Principle 4; SOBC §1 |
| AI Adaptor | Custom | Build (thin abstraction) | ADR-004 |
| Cell-management automation | Custom | Build (no off-the-shelf fits the cell pattern at sovereign-reuse standard) | ADR-006 |
| Sovereign bundle pipeline + signing | Custom | Build atop cosign / SBOM tooling | Project 002 ADR-001 |
| Tenant isolation discipline | Custom | Build + sustain via CI | ADR-001 |
| GOV.UK Design System | Product | **Use** (FR-013) | TCoP §13 |
| OIDC / SAML federation | Product | **Use** (vendor IdP + customer-IdP adaptor) | ADR-003 |
| Managed Kubernetes | Product | **Buy / host on chosen hyperscaler** | ADR-006 |
| Postgres / S3-compatible storage | Commodity | **Use open-API** (portable to project 002 MinIO) | ADR-002 |
| KMS / HSM | Product | **Use** (vendor KMS + CMK) | ADR-002; project 002 INT-007 |
| OpenTelemetry + backend | Product | **Use** (open-standard + managed backend) | ADR-005 |
| Frontier AI providers | Product | **Use** behind adaptor (two providers) | ADR-004 |
| Sigstore / cosign / SBOM | Product | **Use** | Project 002 ADR-001 |
| UK hyperscaler region | Commodity | **Use** (UK residency) | ADR-002 |
| Customer-supplied IdP / KMS / observability (sovereign) | Commodity (from customer side) | **Integrate** | Project 002 ADRs |
| GOV.UK One Login | Product | **Optional integrator** | ADR-003 |

---

## 4. Strategic Gameplay (Wardley plays applied)

| Play | Where applied | Source |
|------|---------------|--------|
| **Open source the codebase** | ArcKit core open-source; sovereign route is the open codebase + bundle + LTS | TCoP §3, §12 |
| **Use ecosystem standards** | OpenAPI, OIDC/SAML, OpenTelemetry, OCI, CycloneDX, SLSA | Principle 4 |
| **Defensible commodity below, differentiated custom above** | Hyperscaler / Postgres / S3 commodity below; ArcKit application + cell pattern + AI Adaptor custom above | Wardley doctrine |
| **Two providers for any genesis-adjacent dependency** | AI providers (×2); hyperscaler open-API alternative; IdP options (vendor + federation + One Login) | ADR-002, 003, 004 |
| **Cross-subsidy** — paid funds free | Enterprise + sovereign tiers fund SME free tier | BR-005 |
| **Pioneer / Settler / Town Planner** | Pioneer = ArcKit application; Settler = cell + bundle pipelines; Town Planner = SRE / LTS line | Vendor team org |

---

## 5. Inertia Risks

- **Hyperscaler concentration** — open-standard primitives reduce inertia, but real switching cost remains. Mitigation: documented exit-plan rehearsal annually.
- **AI provider behaviour drift** — golden-prompt regression suite catches; two-provider posture creates real switching capability.
- **Customer IdP heterogeneity** (sovereign) — mitigated by sticking to OIDC/SAML 2.0; no vendor-specific calls.

---

## 6. Climatic Patterns Considered

- **Punctuated equilibrium in AI capability** — adaptor + golden-prompt suite absorb provider-side discontinuities.
- **Standardisation of supply-chain provenance** (SLSA / SBOM) — embraced early (ADR-001 / ADR-002 of project 002).
- **Government policy maturation on AI** (UK AI Bill / EU AI Act in EU jurisdictions) — annual reassessment baked into AI Playbook conformance doc.

---

## 7. Doctrine Posture

| Wardley doctrine | Applied? | Evidence |
|------------------|----------|----------|
| Use a common language | Yes | ArcKit's documents in this very project demonstrate it |
| Focus on user needs | Yes | STKE; UC-1/2/3; affordability commitment |
| Use appropriate methods | Yes | Phased Discovery → Alpha → Beta → GA |
| Be transparent | Yes | Open source; published pricing; sub-processor inventory |
| Manage inertia | Yes | Two-provider posture; open standards |
| Bias to action | Yes | Phased GA with clear gates |
| Optimise flow | Yes | Trunk-based; cell-by-cell rollout |
| Strategy is iterative | Yes | Annual reviews; ADR superseding chain |

---

## 8. Linked Artefacts

- Principles, REQ, STKE (both projects).
- ADRs across both projects (the maps' "decisions" content).
- SOBC, Roadmap, Plan (both projects).
- Strategy synthesis: `ARC-000-STRATEGY-v1.0.md`.

---

**Generated by**: ArcKit `/arckit:wardley` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
