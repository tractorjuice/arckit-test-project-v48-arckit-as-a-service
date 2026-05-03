# ArcKit as a Service (Managed SaaS) — Project Plan

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:plan`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-PLAN-v1.0 |
| **Document Type** | Project Plan |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) |
| **Distribution** | Project Team, ARB, Vendor SLT |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial plan. Phased Discovery → Alpha → Private Beta → Public Beta → GA, with explicit gates and deliverables traced to PRIN/REQ/STKE/RISK/ADRs. |

---

## 1. Phased Approach

ArcKit as a Service follows the GDS Service Standard delivery phases (Discovery → Alpha → Beta → Live). The plan also names a Private Beta sub-phase before Public Beta, because the SaaS unit economics and operator readiness must be tested with a small set of consenting tenants before opening signups.

```mermaid
gantt
    title ArcKit as a Service — Indicative Timeline (months from start)
    dateFormat  YYYY-MM
    axisFormat  %b %Y

    section Discovery
    Discovery (this phase)            :done, d1, 2026-05, 2M
    PRIN, STKE, REQ, ADRs, RISK, TCoP, DPIA, SbD, SOBC :done, d2, 2026-05, 2M

    section Alpha
    Engineering setup & ARB           :a1, after d2, 1M
    Implement ADR-001 / 002 / 006     :a2, after a1, 3M
    Implement ADR-003 / 004 / 005 / 008 :a3, after a1, 3M
    CI isolation suite                :a4, after a1, 2M
    First DR rehearsal                :a5, after a2, 1M
    Alpha service-standard assessment :gate1, milestone, after a5, 0d

    section Private Beta
    First 5–10 SME pilots             :pb1, after gate1, 3M
    First pen test                    :pb2, after gate1, 1M
    Sub-processor inventory published :pb3, after gate1, 1M
    Private-beta gate                 :gate2, milestone, after pb1, 0d

    section Public Beta
    G-Cloud submission                :pubb1, after gate2, 2M
    Pricing page & marketing site live :pubb2, after gate2, 1M
    Service-standard beta assessment  :pubb3, after gate2, 1M
    First paid tenant                 :pubb4, after pubb3, 1M
    Public-beta exit gate             :gate3, milestone, after pubb4, 0d

    section GA / Live
    Cyber Essentials Plus             :ga1, after gate3, 1M
    G-Cloud go-live                   :ga2, after gate3, 2M
    GA launch                         :ga3, milestone, after ga2, 0d
    Cross-subsidy break-even target   :ga4, milestone, after ga3, 18M
```

---

## 2. Phase Detail

### 2.1 Discovery (in progress; nominal +2 months)

**Goal**: Establish the strategic, requirements, security, privacy, and commercial baseline.

**Deliverables (status as of 2026-05-03)**:

- ✅ Architecture Principles v1.0 / v2.0 (`projects/000-global/ARC-000-PRIN-v2.0.md`).
- ✅ Stakeholder analysis (`ARC-001-STKE-v1.0.md`).
- ✅ Requirements (`ARC-001-REQ-v1.0.md`).
- ✅ ADR-001 Tenant Isolation.
- ✅ ADR-002–008 Cloud / Identity / AI / Observability / Deployment / Export / Quotas.
- ✅ Risk Register.
- ✅ TCoP Assessment.
- ✅ Secure by Design Assessment.
- ✅ DPIA (DRAFT).
- ✅ SOBC.
- 🔲 HLD draft (this phase end).
- 🔲 Diagram pack (C4).
- 🔲 AI Playbook conformance (DRAFT).
- 🔲 DevOps strategy.
- 🔲 FinOps strategy.

**Gate to Alpha**: SOBC approved by ARB; ARB constituted; key roles named; CI isolation suite design ready; HLD signed off.

### 2.2 Alpha (~ +3 months)

**Goal**: Stand up cell #1 in production-equivalent environment; pass first DR rehearsal; book Service Standard alpha assessment.

**Workstreams**:

- **Engineering**: implement ADR-001/002/006 (cell, region, deployment), then ADR-003/004/005/008 (identity, AI, observability, quotas).
- **Security**: CI isolation suite live; vulnerability disclosure programme live; vetting policy in force.
- **Operations**: First cell provisioned; first DR rehearsal; runbook v1.
- **Product**: Onboarding journey (UC-1) testable; AI generation testable.
- **Compliance**: Service Standard alpha assessment booked.

**Gate to Private Beta**: Alpha assessment passed; CI isolation suite green; DR rehearsal RPO/RTO met; risk residuals all ≤ ARB threshold.

### 2.3 Private Beta (~ +3 months)

**Goal**: 5–10 SME pilots in production with full instrumentation; first pen test; sub-processor inventory published.

**Workstreams**:

- **Pilot tenants**: 5–10 SMEs selected; per-tenant feedback log.
- **Security**: First external pen test; remediation plan executed.
- **Compliance**: DPIA approved; sub-processor inventory published; Service Standard beta evidence pack drafted.
- **Engineering**: Iterate on pilot feedback; cell-management automation matured.

**Gate to Public Beta**: Pen test findings remediated within SLA; DPIA APPROVED; pilot tenants successfully exporting (FR-006); cross-subsidy economics tracking on plan.

### 2.4 Public Beta (~ +2–3 months)

**Goal**: Open signups for verified UK SMEs; first paid tenant onboarded; G-Cloud listing process under way.

**Workstreams**:

- **Procurement**: G-Cloud submission filed; pricing page live; DPA template ratified.
- **Compliance**: Service Standard beta assessment booked.
- **Engineering**: Edge cases from broader signups handled; admin console (FR-014) hardened.
- **Marketing**: Public marketing site live (FR-015).

**Gate to GA**: Service Standard beta passed; first paid tenants successfully onboarded and operating; sub-processor inventory current; risk register reviewed and ARB-acceptable.

### 2.5 GA / Live (ongoing)

**Goal**: Cyber Essentials Plus achieved; cross-subsidy economics on plan; GA launch.

**Workstreams**:

- **Compliance**: Cyber Essentials Plus; first annual NCSC CAF self-assessment; first annual DPIA refresh.
- **Operations**: First annual DR rehearsal; first incident-response tabletop.
- **Commercial**: G-Cloud go-live; enterprise tier sales; sovereign route engagement (project 002).
- **Continuous improvement**: ADR review cadence; risk register quarterly; observability tuning.

**Long-running gate (BR-005)**: Cross-subsidy break-even by GA + 18 months.

---

## 3. Workstream Map (RACI Sketch)

| Workstream | A | R | C | I |
|------------|---|---|---|---|
| Architecture & ADRs | Lead Architect | Engineering | ARB; Security | Tenants |
| Tenant isolation | Security Lead | Engineering | Lead Architect | DPO |
| Identity (ADR-003) | Security Lead | Engineering | Lead Architect | Tenants |
| AI (ADR-004) | Service Owner | Engineering; AI Ethics | DPO; Lead Architect | ICO; AI Playbook reviewer |
| Observability / SIEM | Security Lead | SRE | Lead Architect | Tenants (FR-012) |
| Cells / deployment | Lead Architect | SRE; Engineering | ARB | — |
| FinOps | FinOps | Service Owner | Lead Architect | Vendor SLT |
| Compliance (TCoP / CAF / DPIA / SbD) | Service Owner / DPO | DPO; Security Lead | ARB | CCS / GDS / ICO |
| Procurement (G-Cloud) | Service Owner | — | Legal | CCS |
| Marketing / pricing | Service Owner | — | — | — |
| Sovereign track (project 002) | Sovereign Delivery Lead | Engineering | Lead Architect | MOD; SD-15 |

---

## 4. Dependencies

| Dependency | Type | Owner | Mitigation |
|------------|------|-------|------------|
| Hyperscaler region availability (UK) | External | — | ADR-002 multi-AZ; documented exit |
| AI provider DPA terms acceptable | External | DPO | ADR-004 two-provider strategy |
| GOV.UK Design System updates | External | — | FR-013; track changes |
| GOV.UK One Login readiness | External | — | ADR-003 — supported as one option, not the only option |
| G-Cloud framework cycle | External | Service Owner | Calendar tracked; alternatives ready |
| Project 002 (sovereign) co-engineering | Internal | Sovereign Delivery Lead | Single-codebase mandate; phased after SaaS alpha |

---

## 5. Quality Gates

| Gate | Criteria | Reference |
|------|----------|-----------|
| Pre-alpha | ARB constituted; key roles named; CI isolation suite live; first DR rehearsal pass; HLD signed off | RISK; SbD; ADR set |
| Pre-public-beta | Pen test green; DPIA APPROVED; sub-processor inventory live; service-standard beta evidence pack | TCoP §16; DPIA §7 |
| Pre-GA | Cyber Essentials Plus; service-standard beta passed; cross-subsidy on plan | TCoP §16; SOBC §6 |
| 18 months post-GA | Cross-subsidy break-even | BR-005 |

---

## 6. Risks Affecting Plan

Top plan risks (full register: `ARC-001-RISK-v1.0.md`):

- R-006 key-person dependency (largest delivery risk).
- R-012 engineering velocity.
- R-016 sovereign-route bifurcation.
- R-018 first DR rehearsal fails.

---

## 7. Linked Artefacts

- Principles, REQ, STKE, RISK, TCoP, SbD, DPIA, SOBC, ADRs (001–008).
- Roadmap: `ARC-001-ROADMAP-v1.0.md`.
- DevOps: `ARC-001-DEVOPS-v1.0.md`.
- FinOps: `ARC-001-FINOPS-v1.0.md`.
- AI Playbook: `ARC-001-AIP-v1.0.md`.
- HLD: `ARC-001-HLD-v1.0.md`.
- Operational Readiness: `ARC-001-OPS-v1.0.md`.

---

**Generated by**: ArcKit `/arckit:plan` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
