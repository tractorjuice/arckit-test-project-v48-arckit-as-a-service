# ArcKit as a Service (Managed SaaS) — Technology Code of Practice (TCoP) Assessment

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:tcop`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-TCOP-v1.0 |
| **Document Type** | Technology Code of Practice Assessment |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) |
| **Distribution** | ARB, GDS, CDDO, Buying-authority TDA reviewers |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial assessment against TCoP 14 points; evidences from PRIN, REQ, STKE and ADRs 001–008. |

---

## Purpose

This document evidences ArcKit as a Service (managed SaaS) compliance with the UK Government **Technology Code of Practice (TCoP)** — the cross-government standard against which technology spend over £100k must be assessed and which buying authorities expect suppliers to evidence at procurement and Service Standard assessment.

For each TCoP point, this assessment records: **Status** (Compliant / Compliant with Conditions / Not Yet Compliant / Not Applicable), **Evidence** (linked artefacts), **Gaps** (if any), and **Action** (with owner and target date).

---

## Summary

| Point | Title | Status |
|-------|-------|--------|
| 1 | Define user needs | Compliant |
| 2 | Make things accessible and inclusive | Compliant with Conditions (CI a11y test required) |
| 3 | Be open and use open source | Compliant |
| 4 | Make use of open standards | Compliant |
| 5 | Use cloud first | Compliant |
| 6 | Make things secure | Compliant with Conditions (CI isolation suite + first pen test) |
| 7 | Make privacy integral | Compliant with Conditions (DPIA finalisation) |
| 8 | Share, reuse and collaborate | Compliant |
| 9 | Integrate and adapt technology | Compliant |
| 10 | Make better use of data | Compliant |
| 11 | Define your purchasing strategy | Compliant with Conditions (G-Cloud listing pending) |
| 12 | Make your technology sustainable | Compliant |
| 13 | Meet the Service Standard | Compliant with Conditions (alpha assessment pending) |
| 14 | Use AI ethically | Compliant with Conditions (AI Playbook conformance doc pending) |

**Overall**: Compliant with Conditions — clear path to full compliance via the Action register at §16.

---

## 1 — Define user needs

**Status**: Compliant.

**Evidence**:

- `ARC-001-STKE-v1.0.md` defines 14 stakeholder cohorts (SD-1 to SD-14) with explicit drivers, goals (G-*), and measurable outcomes. Stakeholder analysis is DDaT-aligned (buyers, SMEs, vendor, government).
- `ARC-001-REQ-v1.0.md` includes user personas, three core use cases (UC-1 self-service onboarding, UC-2 AI-assisted generation, UC-3 export-and-exit), and 15 functional requirements traced to those personas.
- Principle 1 establishes the SME-supplying-government population as the primary user need.

**Gaps / Action**: User research (continuous discovery) is committed for alpha and beta; outputs feed back into REQ revisions.

---

## 2 — Make things accessible and inclusive

**Status**: Compliant with Conditions.

**Evidence**:

- NFR-C-003 (Accessibility — PSBAR 2018 / WCAG 2.2 AA) and NFR-U-002 in REQ.
- FR-013 (GOV.UK Design System alignment) — adopt rather than reinvent.
- Principle 6 (Accessibility) in PRIN v2.0.

**Gaps**: Automated a11y test in CI not yet implemented; first manual a11y audit scheduled for alpha.

**Action**: A1 — Implement axe-core + pa11y in CI before alpha (Owner: Vendor Lead Architect). A2 — First manual audit by certified a11y consultant before public beta.

---

## 3 — Be open and use open source

**Status**: Compliant.

**Evidence**:

- Principle 4 (Open standards / portability) and Principle 12 (Reproducible by IaC) in PRIN.
- ArcKit core is open-source (`https://github.com/...` — pending publication policy review).
- Source code commit signing required (NFR-SEC-005 implication).
- Sovereign deployment route (project 002) explicitly relies on the open codebase.
- Open standards enumerated in ADR-007 (export format), ADR-005 (OpenTelemetry), ADR-006 (OCI / Kubernetes), ADR-003 (OIDC / SAML).

**Gaps**: Public publication of pricing-tier source-code-vs-managed-service split awaiting governance sign-off (target: pre-GA).

---

## 4 — Make use of open standards

**Status**: Compliant.

**Evidence**:

- ADR-002 selects open-standard primitives (S3 API, Postgres wire, OIDC/SAML).
- ADR-003 — OIDC + SAML 2.0 federation; OpenAPI for the public API (FR-008, NFR-I-001).
- ADR-005 — OpenTelemetry for instrumentation.
- ADR-007 — Markdown + JSON + OpenAPI for export.
- NFR-I-001 (Open API standards) and NFR-I-002 (Data portability) in REQ.

---

## 5 — Use cloud first

**Status**: Compliant.

**Evidence**:

- ADR-002 selects UK-resident hyperscaler region with managed primitives.
- ADR-006 selects managed Kubernetes per cell.
- Principle 7 (UK sovereignty within cloud-first frame) explicitly endorses cloud-first with UK residency.
- No on-prem build is contemplated for the SaaS route.

---

## 6 — Make things secure

**Status**: Compliant with Conditions.

**Evidence**:

- Principles 5 (Security by design — non-negotiable) and 8 (Tenant isolation — non-negotiable).
- ADR-001 (Tenant Isolation), ADR-003 (Identity), ADR-005 (Observability + SIEM).
- NFR-SEC-001 to 009 (full security NFR family).
- Risk Register R-001, R-008 with named mitigations.
- NCSC Cloud Security Principles mapping documented; CAF mapping explicit (NFR-SEC-008/009).

**Gaps**: CI isolation suite live by alpha; first external pen test by alpha; Cyber Essentials Plus certification pre-GA.

**Action**: A1 — CI isolation suite (Owner: Security Lead, before alpha). A2 — First pen test (Owner: Security Lead, alpha). A3 — Cyber Essentials Plus (pre-GA).

---

## 7 — Make privacy integral

**Status**: Compliant with Conditions.

**Evidence**:

- Principle 7 (Data sovereignty) and PRIN coverage of UK GDPR.
- NFR-C-001 (UK GDPR / DPA 2018) explicit.
- DPIA scheduled (`/arckit:dpia` — see `ARC-001-DPIA-v1.0.md`).
- ADR-001 (tenant isolation = controller separation), ADR-002 (UK residency), ADR-005 (PII redaction at source, audit log retention).
- Sub-processor inventory drafted (ADR-002 Appendix B).

**Gaps**: DPIA finalised at v1.0 status (not yet APPROVED); sub-processor inventory needs final hyperscaler / AI selections (ADR-006 finalisation).

**Action**: A1 — DPIA approved (Owner: DPO, before public beta). A2 — Sub-processor inventory published (before first paid tenant).

---

## 8 — Share, reuse and collaborate

**Status**: Compliant.

**Evidence**:

- ArcKit's mission is itself a sharing and reuse platform for UK Government / SME architecture.
- Single codebase serves multi-tenant SaaS and sovereign deployment (Principle 21; ADRs 001/004/006).
- `/arckit:gov-reuse` engaged at requirements stage to check for existing public-sector code; collaboration record in `external/`.
- Open-source licensing supports cross-government reuse.

---

## 9 — Integrate and adapt technology

**Status**: Compliant.

**Evidence**:

- Public API and event interfaces (FR-008; NFR-I-001).
- OIDC/SAML federation (FR-007; ADR-003).
- Companies House integration (INT-003).
- GOV.UK One Login as an external IdP option (ADR-003).
- Webhook / event interface for tenant integrations (FR-008).

---

## 10 — Make better use of data

**Status**: Compliant.

**Evidence**:

- Principle 9 (Data quality, lineage, portability).
- ADR-007 (Full-fidelity data portability).
- Per-tenant audit log access (FR-012; ADR-005).
- Per-tenant cost telemetry feeding FinOps (Principle 17).
- Generation provenance metadata (ADR-004) supports decision auditability.

---

## 11 — Define your purchasing strategy

**Status**: Compliant with Conditions.

**Evidence**:

- BR-002 (Transparent published pricing).
- BR-004 (G-Cloud procurement route).
- Principle 1 commitment to SME affordability and transparent pricing.
- Sovereign route (project 002) procurement frameworks identified (G-Cloud / DOS / Defence frameworks per project 002 INT-008).

**Gaps**: G-Cloud listing not yet submitted; pricing page not yet published.

**Action**: A1 — G-Cloud submission (Owner: Service Owner, target: 6 months pre-GA). A2 — Pricing page live (before public beta).

---

## 12 — Make your technology sustainable

**Status**: Compliant.

**Evidence**:

- Principle 17 (FinOps — includes carbon-aware region preference).
- ADR-002 carbon-aware region preference (where cost-equivalent).
- ADR-006 right-sizing + spot/preemptible workloads.
- ADR-008 quotas prevent unbounded resource consumption.
- Annual sustainability report committed in PRIN.

---

## 13 — Meet the Service Standard

**Status**: Compliant with Conditions.

**Evidence**:

- NFR-C-005 (GDS Service Standard) explicit.
- Service Standard readiness assessment (`/arckit:service-assessment` — see `ARC-001-SVCASS-v1.0.md`).
- 14-point alignment evidenced in REQ NFR family and ADR set.

**Gaps**: Alpha assessment not yet booked; readiness against Points 4 (multidisciplinary team), 6 (multidisciplinary), and 14 (operate a reliable service) needs evidencing at alpha.

**Action**: A1 — Service assessment readiness review pre-alpha (Owner: Service Owner). A2 — Book alpha assessment (CDDO). A3 — Address gaps surfaced in `ARC-001-SVCASS-v1.0.md`.

---

## 14 — Use AI ethically

**Status**: Compliant with Conditions.

**Evidence**:

- ADR-004 (AI Provider Abstraction) — provenance, no-train default, human-in-the-loop required.
- AI Playbook conformance doc (`/arckit:ai-playbook` — see `ARC-001-AIP-v1.0.md`).
- ATRS skeleton maintained; current assessment classifies use as "limited risk" (ATRS not yet mandatory).
- DPIA covers AI processing.
- R-009 in risk register names hallucination / unwarranted-authority risk and mitigations.

**Gaps**: AI Playbook conformance doc still v1.0 DRAFT; ATRS reassessment annual.

**Action**: A1 — AI Playbook conformance doc to APPROVED state pre-public beta (Owner: Service Owner + AI Ethics reviewer).

---

## 15 — Cross-cutting Compliance Mapping (NCSC, GDS, ICO)

| Standard | Mapped through | Evidence anchor |
|----------|----------------|-----------------|
| NCSC Cloud Security Principles | NFR-C-009; ADRs 001–008 | ADR-002 §7, ADR-001 §7 |
| NCSC CAF | NFR-SEC-008; ADR-005 | Risk R-008 |
| GDS Service Standard | NFR-C-005; `/arckit:service-assessment` | TCoP §13 |
| UK GDPR / DPA 2018 | NFR-C-001; DPIA | TCoP §7; ADR-002 |
| Cyber Essentials / CE+ | NFR-C-009; ADR-006 | Action 6.A3 |
| WCAG 2.2 AA / PSBAR 2018 | NFR-C-003 | TCoP §2 |
| HMT Green Book | SOBC | `ARC-001-SOBC-v1.0.md` |
| Procurement Act 2023 | BR-002, BR-004 | Risk R-020 |

---

## 16 — Action Register (Conditions to Reach Full Compliance)

| ID | TCoP | Action | Owner | Target |
|----|------|--------|-------|--------|
| 2.A1 | 2 | CI a11y tests live | Lead Architect | Alpha |
| 2.A2 | 2 | Manual a11y audit | Service Owner | Public beta |
| 6.A1 | 6 | CI isolation suite | Security Lead | Alpha |
| 6.A2 | 6 | First pen test | Security Lead | Alpha |
| 6.A3 | 6 | Cyber Essentials Plus | Service Owner | Pre-GA |
| 7.A1 | 7 | DPIA APPROVED | DPO | Public beta |
| 7.A2 | 7 | Sub-processor inventory published | DPO | Pre first paid tenant |
| 11.A1 | 11 | G-Cloud submission | Service Owner | 6 months pre-GA |
| 11.A2 | 11 | Pricing page live | Service Owner | Public beta |
| 13.A1 | 13 | Service assessment readiness | Service Owner | Pre-alpha |
| 13.A2 | 13 | Alpha assessment booked | Service Owner | Alpha |
| 14.A1 | 14 | AI Playbook conformance APPROVED | Service Owner + AI Ethics | Public beta |

---

**External References**

- Technology Code of Practice: https://www.gov.uk/guidance/the-technology-code-of-practice
- GDS Service Standard: https://www.gov.uk/service-manual/service-standard
- NCSC Cloud Security Principles: https://www.ncsc.gov.uk/collection/cloud/the-cloud-security-principles
- NCSC CAF: https://www.ncsc.gov.uk/collection/cyber-assessment-framework
- UK Government AI Playbook: https://www.gov.uk/government/publications/ai-playbook-for-the-uk-government

---

**Generated by**: ArcKit `/arckit:tcop` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
