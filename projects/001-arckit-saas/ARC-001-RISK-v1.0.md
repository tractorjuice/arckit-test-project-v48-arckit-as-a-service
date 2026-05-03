# ArcKit as a Service (Managed SaaS) — Risk Register

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RISK-v1.0 |
| **Document Type** | Risk Register (HM Treasury Orange Book aligned) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Monthly (DRAFT/Alpha); Quarterly (Beta/GA); on-trigger always |
| **Next Review Date** | 2026-06-03 |
| **Owner** | Mark Craddock (Service Owner — risk owner of last resort) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, ARB, Audit Committee, Vendor Senior Leadership, DPO, Security Lead, FinOps |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation. Aligned with HM Treasury Orange Book (Management of Risk in Government); risk categories from Orange Book §3 plus ArcKit-specific overlays. Inputs: PRIN v2.0, REQ, STKE, ADRs 001–008. |

---

## 1. Purpose and Approach

This register identifies, scores, and assigns ownership for the risks to delivering and operating ArcKit as a Service (managed SaaS, Project 001). It follows HM Treasury **Orange Book** principles:

- Risk owners named (single accountable person per risk).
- Risks scored on **likelihood × impact** (1–5 scale each); residual risk shown after mitigation.
- Inherent vs residual risk distinguished.
- Mitigation actions tracked to closure.
- Escalation thresholds defined.

Risk categories used (Orange Book §3 + ArcKit overlay):

- **Strategic** — risks to mission, market position, stakeholder trust.
- **Operational** — risks to service delivery and incident response.
- **Financial** — risks to commercial sustainability and unit economics.
- **Compliance** — risks to regulatory, contractual, or policy obligations.
- **Security** — risks to confidentiality, integrity, availability of tenant data.
- **Technology** — risks to engineering deliverability and technical debt.
- **Reputation** — risks to public trust, particularly with UK Government and SME communities.
- **People** — risks to capability, capacity, and key-person dependency.

### Scoring scale

| Score | Likelihood | Impact (descriptor) |
|-------|------------|----------------------|
| 1 | Rare (< 5% in horizon) | Negligible — no material effect |
| 2 | Unlikely (5–25%) | Minor — recoverable; localised |
| 3 | Possible (25–60%) | Moderate — significant remediation; some tenants affected |
| 4 | Likely (60–90%) | Major — service-impacting; multiple tenants; regulator interest |
| 5 | Almost certain (>90%) | Severe — existential / multi-tenant data loss / mission failure |

**Risk score** = likelihood × impact, on 1–25 scale. **Escalation thresholds**: ≥ 12 to ARB; ≥ 16 to Vendor SLT and (where Government interest) buying-authority SRO.

---

## 2. Top Risks (Heat Map)

| Code | Title | Category | Inherent (L×I=S) | Residual (L×I=S) | Owner |
|------|-------|----------|------------------|-------------------|-------|
| R-001 | Cross-tenant data leak via isolation defect | Security | 3×5=15 | 1×5=5 | Vendor Security Lead |
| R-002 | SME free-tier economics fail (cross-subsidy doesn't fund) | Financial / Strategic | 3×4=12 | 2×4=8 | Service Owner |
| R-003 | Hyperscaler concentration / DPA term change | Operational / Compliance | 2×4=8 | 2×3=6 | Lead Architect |
| R-004 | AI provider DPA, capability or pricing shift | Operational / Strategic | 4×3=12 | 2×3=6 | Lead Architect |
| R-005 | UK GDPR enforcement event (sub-processor transparency / consent) | Compliance | 2×5=10 | 1×4=4 | DPO |
| R-006 | Key-person dependency on Service Owner | People | 4×4=16 | 3×4=12 | Vendor SLT |
| R-007 | G-Cloud listing delayed / CCS framework change | Strategic / Compliance | 3×3=9 | 2×3=6 | Service Owner |
| R-008 | NCSC CAF outcome cannot be evidenced at alpha | Compliance / Security | 3×4=12 | 2×3=6 | Vendor Security Lead |
| R-009 | AI-generated content presented as authoritative without human review | Strategic / Reputation | 4×4=16 | 2×3=6 | Service Owner |
| R-010 | Cell-management automation immature; manual ops at GA | Operational | 3×3=9 | 2×3=6 | SRE Lead (PENDING) |
| R-011 | Pricing-model misalignment with SME definition / verification gaps | Financial / Compliance | 3×3=9 | 2×3=6 | Service Owner |
| R-012 | Engineering velocity insufficient to hit GA gate | Technology / People | 3×4=12 | 3×3=9 | Vendor Lead Architect |
| R-013 | Public availability incident damages early-adopter trust | Reputation / Operational | 3×4=12 | 2×3=6 | SRE Lead |
| R-014 | Vulnerability disclosure programme overwhelms small team | Operational / Security | 3×3=9 | 2×3=6 | Vendor Security Lead |
| R-015 | UK Gov AI Playbook reclassifies use case | Compliance | 2×3=6 | 1×3=3 | Service Owner |
| R-016 | Sovereign route (project 002) bifurcates engineering effort | Strategic / Technology | 4×3=12 | 2×3=6 | Vendor Lead Architect |
| R-017 | Accessibility (WCAG 2.2 AA) regression at release cadence | Compliance | 3×3=9 | 2×3=6 | Vendor Lead Architect |
| R-018 | Backup / DR rehearsal fails on first execution | Operational / Security | 3×4=12 | 2×4=8 | SRE Lead |
| R-019 | Cyber-insurance unobtainable or unaffordable for SaaS pre-revenue | Financial | 3×3=9 | 2×3=6 | Service Owner |
| R-020 | Procurement Act 2023 transparency obligation interpretation drift | Compliance | 2×3=6 | 1×3=3 | Service Owner |

(Continued risks R-021+ tracked operationally in tooling; this register lists material risks only.)

---

## 3. Detailed Risk Records

### R-001 — Cross-tenant data leak via isolation defect

| Field | Value |
|-------|-------|
| **Category** | Security |
| **Description** | A defect in tenant_id propagation, authorisation logic, or persistence policy allows tenant A to read, write, or infer tenant B's data. A single such event is reputationally and contractually catastrophic. |
| **Trigger / Cause** | Engineering change misses tenant context; missing CI isolation test for new surface; library update changes authorisation behaviour. |
| **Inherent likelihood × impact** | 3 × 5 = **15** |
| **Mitigating controls** | ADR-001 (Pool + Cell + tenant_id + defence in depth + CI isolation suite); NFR-SEC-002 acceptance criteria; quarterly external pen test; bug-bounty programme (NFR-SEC-006, INT-009); per-tenant logging + SIEM alerts; cell blast-radius cap. |
| **Residual likelihood × impact** | 1 × 5 = **5** |
| **Owner** | Vendor Security Lead |
| **Action(s)** | A1 Stand up CI isolation suite before alpha; A2 Bug-bounty live before public beta; A3 First pen test report filed before GA. |
| **Review trigger** | Any cross-tenant scenario surfaced in test, pen test, or production; any new public surface added. |
| **Linked artefacts** | ADR-001, NFR-SEC-002, project 002 STKE SR-3 |

### R-002 — SME free-tier economics fail

| Field | Value |
|-------|-------|
| **Category** | Financial / Strategic |
| **Description** | Cross-subsidy from enterprise tenants and sovereign route does not fund the free SME tier; service runs at a structural loss; pricing must change in a way that breaks Principle 1 commitment. |
| **Trigger / Cause** | Inference / infrastructure cost higher than forecast; enterprise / sovereign uptake slower than forecast; SME cost-per-tenant exceeds budget. |
| **Inherent L×I** | 3 × 4 = **12** |
| **Mitigating controls** | ADR-008 (free-tier quotas conservative and capped); ADR-004 (per-tenant AI budget); Principle 17 FinOps quarterly review; cell-fill discipline; published affordability review (Principle 1 validation gate). |
| **Residual L×I** | 2 × 4 = **8** |
| **Owner** | Service Owner |
| **Action(s)** | A1 Quarterly affordability review starting GA-3 months; A2 Free-tier cost telemetry per ADR-005 from alpha; A3 Annual published affordability review (Principle 1). |
| **Review trigger** | Any cost-per-tenant deviation > 15% from forecast; any tier-change request from FinOps. |
| **Linked artefacts** | Principle 1, BR-001, BR-005, ADR-008, ADR-004 |

### R-003 — Hyperscaler concentration / DPA change

| Field | Value |
|-------|-------|
| **Category** | Operational / Compliance |
| **Description** | Chosen hyperscaler changes UK contracting entity, DPA terms, or pricing in a way that materially harms ArcKit's posture; or experiences a region-wide outage affecting NFR-A-001. |
| **Trigger / Cause** | Provider commercial decision; M&A; regulator action; provider outage. |
| **Inherent L×I** | 2 × 4 = **8** |
| **Mitigating controls** | ADR-002 (open-standard primitives — S3 API, Postgres wire); ADR-006 (OCI containers, Kubernetes-portable); annual exit-plan rehearsal; sub-processor annual DPA review; multi-AZ + cross-region DR. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Lead Architect |
| **Action(s)** | A1 Open-standard primitive portability test in CI; A2 Annual exit-plan rehearsal; A3 Sub-processor DPA annual review log. |
| **Review trigger** | Any provider DPA notice; any region outage; any cost regression > 25%. |

### R-004 — AI provider DPA / capability / pricing shift

| Field | Value |
|-------|-------|
| **Category** | Operational / Strategic |
| **Description** | AI provider changes DPA terms (e.g., training defaults), retires a model, or changes pricing in a way that affects free-tier cost or acceptability. |
| **Trigger / Cause** | Provider product decision; regulator action; market change. |
| **Inherent L×I** | 4 × 3 = **12** |
| **Mitigating controls** | ADR-004 (provider-agnostic adaptor + two providers from day one + golden-prompt regression suite + DPA annual review). |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Lead Architect |
| **Action(s)** | A1 Two providers proven in production by GA; A2 Golden-prompt regression suite green per release; A3 DPA log maintained. |
| **Review trigger** | Any provider DPA change; any model retirement notice; any regression-suite divergence. |

### R-005 — UK GDPR enforcement event

| Field | Value |
|-------|-------|
| **Category** | Compliance |
| **Description** | ICO action against ArcKit or a sub-processor — sub-processor transparency, lawful basis, retention, or cross-border transfer issue. |
| **Inherent L×I** | 2 × 5 = **10** |
| **Mitigating controls** | DPIA (per `/arckit:dpia`); sub-processor inventory published; UK residency (ADR-002); IDTA where applicable; audit trail (ADR-005); incident response runbook with ICO 72-hour notification path. |
| **Residual L×I** | 1 × 4 = **4** |
| **Owner** | DPO |
| **Action(s)** | A1 Sub-processor inventory published before first paid tenant; A2 ICO breach-notification runbook tested annually; A3 Annual DPIA refresh. |
| **Review trigger** | Any ICO guidance update; any sub-processor change; any incident with personal-data dimension. |

### R-006 — Key-person dependency on Service Owner

| Field | Value |
|-------|-------|
| **Category** | People |
| **Description** | Service Owner (Mark Craddock) is currently the single point of accountability for product, commercial, regulatory, and architecture roles until further hires. Loss of availability would stall the service. |
| **Inherent L×I** | 4 × 4 = **16** |
| **Mitigating controls** | Documentation discipline (ArcKit eats its own dog-food); Lead Architect appointment plan; ARB constituted from external advisers. |
| **Residual L×I** | 3 × 4 = **12** (HIGH — escalated to ARB) |
| **Owner** | Vendor SLT (when constituted; currently Service Owner self-mitigated) |
| **Action(s)** | A1 Lead Architect appointed before alpha; A2 ARB constituted before alpha; A3 Operational runbook coverage (NFR-M-003) before GA; A4 Succession plan documented. |
| **Review trigger** | Any change in Service Owner availability; alpha gate. |

### R-007 — G-Cloud listing delayed / CCS framework change

| Field | Value |
|-------|-------|
| **Category** | Strategic / Compliance |
| **Description** | G-Cloud listing process slips, or CCS framework change requires resubmission, delaying tenant onboarding via the framework path. |
| **Inherent L×I** | 3 × 3 = **9** |
| **Mitigating controls** | Early CCS engagement; framework cycle tracked; alternative DOS / direct procurement available for early adopters. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Service Owner |
| **Action(s)** | A1 G-Cloud submission targeted 6 months before GA; A2 DOS pack ready as alternative; A3 CCS framework cycle calendared. |

### R-008 — NCSC CAF outcome cannot be evidenced at alpha

| Field | Value |
|-------|-------|
| **Category** | Compliance / Security |
| **Description** | At alpha, evidence for one or more CAF objectives (most likely C1 monitoring or D1 incident management) is incomplete; buying authorities will not pilot. |
| **Inherent L×I** | 3 × 4 = **12** |
| **Mitigating controls** | ADR-005 (observability), ADR-006 (deployment), Operational Readiness pack (`/arckit:operationalize`); CAF mapping maintained alongside artefacts; pre-alpha self-assessment. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Vendor Security Lead |

### R-009 — AI-generated content presented as authoritative without human review

| Field | Value |
|-------|-------|
| **Category** | Strategic / Reputation |
| **Description** | Tenants accept AI-generated artefacts as published without human review; an artefact contains a hallucination or harmful bias; the failure is attributed to ArcKit publicly. |
| **Inherent L×I** | 4 × 4 = **16** |
| **Mitigating controls** | ADR-004 (provenance metadata); UI badging of AI-generated content; "human-in-the-loop required for publication" hard gate; AI Playbook conformance doc; user training material. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Service Owner |

### R-010 — Cell-management automation immature

| Field | Value |
|-------|-------|
| **Category** | Operational |
| **Description** | At GA, cell creation/scaling/migration is partly manual; first incident overwhelms small ops team. |
| **Inherent L×I** | 3 × 3 = **9** |
| **Mitigating controls** | ADR-006 implementation plan; alpha includes cell-management drill; runbooks (NFR-M-003); SRE Lead appointment. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | SRE Lead (PENDING) |

### R-011 — Pricing-model / SME-verification gaps

| Field | Value |
|-------|-------|
| **Category** | Financial / Compliance |
| **Description** | SME verification (BR-003) misclassifies tenants; either SMEs blocked from free tier (mission-failure) or non-SMEs gain free tier (cost-impact). |
| **Inherent L×I** | 3 × 3 = **9** |
| **Mitigating controls** | INT-003 Companies House integration; published SME definition; appeal process; periodic verification refresh. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Service Owner |

### R-012 — Engineering velocity insufficient

| Field | Value |
|-------|-------|
| **Category** | Technology / People |
| **Description** | Hiring slow; scope of ADR-001 / 002 / 003 / 004 / 006 demands more engineering than available before GA. |
| **Inherent L×I** | 3 × 4 = **12** |
| **Mitigating controls** | Phased GA; alpha with subset; contracting capacity for cell-management automation; ADR scope discipline. |
| **Residual L×I** | 3 × 3 = **9** (kept under monthly review) |
| **Owner** | Vendor Lead Architect |

### R-013 — Public availability incident damages early trust

| Field | Value |
|-------|-------|
| **Category** | Reputation / Operational |
| **Description** | Visible incident in the early public-beta or GA period creates a "founders' SaaS / not-ready" perception; SME pilots stall. |
| **Inherent L×I** | 3 × 4 = **12** |
| **Mitigating controls** | NFR-A-001/002/003; status page (FR-009); transparent incident communication; pre-GA chaos / DR drills; cell blast-radius cap. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | SRE Lead |

### R-014 — Vulnerability disclosure overwhelms small team

| Field | Value |
|-------|-------|
| **Category** | Operational / Security |
| **Description** | Bug bounty / VDP submissions exceed triage capacity; high-severity item misses SLA. |
| **Inherent L×I** | 3 × 3 = **9** |
| **Mitigating controls** | NFR-SEC-006; triage SLAs; out-of-hours rotation; managed bounty platform. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Vendor Security Lead |

### R-015 — UK Gov AI Playbook reclassifies use case

| Field | Value |
|-------|-------|
| **Category** | Compliance |
| **Description** | UK AI policy update reclassifies ArcKit's use as higher-risk; ATRS becomes mandatory; additional controls needed. |
| **Inherent L×I** | 2 × 3 = **6** |
| **Mitigating controls** | Annual reassessment; ATRS skeleton maintained; AI Playbook conformance doc reviewed every release. |
| **Residual L×I** | 1 × 3 = **3** |
| **Owner** | Service Owner |

### R-016 — Sovereign route bifurcates engineering effort

| Field | Value |
|-------|-------|
| **Category** | Strategic / Technology |
| **Description** | Project 002 sovereign requirements pull engineering effort away from SaaS GA; or design fork creates two codebases instead of one. |
| **Inherent L×I** | 4 × 3 = **12** |
| **Mitigating controls** | Principle 21 single-codebase mandate; ADR-001/006 sovereign-reuse design; ARB enforces single-codebase test in CI; project 002 plan sequenced after SaaS alpha. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Vendor Lead Architect |

### R-017 — Accessibility regression

| Field | Value |
|-------|-------|
| **Category** | Compliance |
| **Description** | WCAG 2.2 AA / PSBAR 2018 regression slips into release. |
| **Inherent L×I** | 3 × 3 = **9** |
| **Mitigating controls** | NFR-C-003; automated a11y tests in CI; manual a11y audit before each release; GOV.UK Design System adoption (FR-013). |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Vendor Lead Architect |

### R-018 — Backup / DR rehearsal fails on first execution

| Field | Value |
|-------|-------|
| **Category** | Operational / Security |
| **Description** | First DR rehearsal exposes a gap; RPO / RTO not met. |
| **Inherent L×I** | 3 × 4 = **12** |
| **Mitigating controls** | NFR-A-002; pre-alpha DR rehearsal; cross-region backup (ADR-002); per-cell isolation (ADR-001/006). |
| **Residual L×I** | 2 × 4 = **8** (kept HIGH until first rehearsal passes) |
| **Owner** | SRE Lead |

### R-019 — Cyber-insurance unobtainable / unaffordable

| Field | Value |
|-------|-------|
| **Category** | Financial |
| **Description** | Cyber-insurance market for early-stage SaaS handling government data is tightening; cover may be unaffordable or unavailable at launch. |
| **Inherent L×I** | 3 × 3 = **9** |
| **Mitigating controls** | Broker engaged early; Cyber Essentials Plus baseline as proof-point; staged risk-acceptance with ARB; commercial reserve. |
| **Residual L×I** | 2 × 3 = **6** |
| **Owner** | Service Owner |

### R-020 — Procurement Act 2023 transparency obligations

| Field | Value |
|-------|-------|
| **Category** | Compliance |
| **Description** | Vendor's interpretation of contract / KPI publication obligations under Procurement Act 2023 differs from a buying authority's. |
| **Inherent L×I** | 2 × 3 = **6** |
| **Mitigating controls** | Legal review; transparent published list pricing (BR-002); buyer engagement pre-contract. |
| **Residual L×I** | 1 × 3 = **3** |
| **Owner** | Service Owner |

---

## 4. Risk Appetite Statement

For ArcKit as a Service:

- **Tenant data isolation** — appetite is **zero**. No residual likelihood above 1 is acceptable for cross-tenant defects.
- **UK GDPR / regulatory compliance** — appetite is **very low**. Any residual likelihood above 1 requires ARB review.
- **Availability** — appetite is **low** for material downtime (NFR-A-001 99.9%); higher for short, communicated maintenance windows.
- **Cost / unit economics** — appetite is **moderate** during pre-revenue phase; tightens toward break-even (BR-005).
- **Reputation with UK Government** — appetite is **very low**; one prominent incident sets the SME-affordable narrative back years.
- **Engineering velocity vs scope** — appetite is **moderate**; phased delivery acceptable, GA scope reductions discussable.

---

## 5. Governance and Reporting

- **Monthly** during DRAFT/Alpha phase: Service Owner + ARB review of all risks ≥ 9.
- **Quarterly** in Beta/GA: full register review; trend analysis.
- **On-trigger** always: any incident ≥ Severity 2; any DPA change; any regulatory event; any change in residual score ≥ 12.
- **Reported to**: Vendor SLT (when constituted); ARB; Audit Committee (when constituted).
- **Tooling**: this register is the canonical source; operational tracking in shared issue tracker labelled `risk-register`.

---

## 6. Linked Artefacts

- Principles: `projects/000-global/ARC-000-PRIN-v2.0.md` (esp. 1, 5, 7, 8, 17, 21).
- Requirements: `ARC-001-REQ-v1.0.md`.
- Stakeholders: `ARC-001-STKE-v1.0.md` (risk owners trace to stakeholder roles).
- ADRs: `ARC-001-ADR-001..008-v1.0.md`.
- Project 002 cross-references: STKE SR-3 (cross-tenant data leak), R-002 (sovereign-route bifurcation).
- HM Treasury Orange Book: https://www.gov.uk/government/publications/orange-book

---

**Generated by**: ArcKit `/arckit:risk` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
