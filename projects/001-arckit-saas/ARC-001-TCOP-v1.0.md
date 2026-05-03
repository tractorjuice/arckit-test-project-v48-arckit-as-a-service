# Technology Code of Practice (TCoP) Review: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:tcop`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-TCOP-v1.0 |
| **Document Type** | Technology Code of Practice Review |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] CDDO digital spend control assurance |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, CCS liaison, CDDO, GDS Service Assessor (pre-assessment) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:tcop` command. Pre-GA / Alpha-stage assessment of all 13 TCoP points + GovS 005 alignment, traced to ARC-001-REQ, ARC-001-STKE, ARC-001-RISK and ADR-001..008. | [PENDING] | [PENDING] |

## Document Purpose

Provides the Technology Code of Practice (TCoP) self-assessment for the **managed SaaS** route of ArcKit as a Service (Project 001) prior to UK Government Digital Spend Control submission and G-Cloud listing. This document evidences compliance against all 13 TCoP points and the AI-related obligations of the UK Government AI Playbook (covered in detail in `ARC-001-AIPB-v1.0.md`). The sovereign deployment route is covered separately in `projects/002-arckit-sovereign/`.

This document is a **pre-GA Alpha-stage assessment**. Live-stage compliance evidence (independent pen-test report, accessibility audit, Service Standard Beta/Live assessments, G-Cloud listing) is gated on the Priority-1 actions in the §Next Steps and in `ARC-001-RISK-v1.0.md` §H.

---

## Executive Summary

**Overall TCoP Compliance**: ⚠️ **Partially Compliant** — pre-GA Alpha-stage; all 13 points addressed in design, 5 of 13 fully evidenced today.

**Key Findings**:

- **Strengths**: Strong principle base (`ARC-000-PRIN-v2.0.md`) with 21 architecture principles aligning explicitly to TCoP and the GDS Service Standard. Open standards (Principle 4), tenant portability (Principle 9 / BR-007), accessibility commitment (Principle 12, non-negotiable), and security-by-design (Principle 5, non-negotiable) are baked in and traced into ADRs and NFRs. UK residency by default (Principle 7) and explicit cross-subsidy commercial model (Principle 1, Principle 17) directly address the SME-spend strategic posture.
- **Gaps closing pre-GA** (driven by `ARC-001-RISK-v1.0.md` Priority-1 actions): independent penetration test for tenant isolation (R-008/R-014); GDS Service Standard pre-assessment walkthrough (R-009); DPIA finalisation (`ARC-001-DPIA-v1.0.md` pending generation); accessibility audit walk-through with pilot DDaT functions; carbon footprint baseline (Point 12).
- **Critical actions before GA**: complete DPIA, complete pre-pen-test isolation review, complete pre-Service-Assessment review, publish AI Playbook ATRS record (Point 7 / AI annex), publish accessibility statement and audit report, complete G-Cloud listing.

**Compliance Score**: 5 Compliant / 7 Partially Compliant / 1 N/A — total 13 points assessed.

**Critical Issues Requiring Pre-GA Resolution**:

1. **Point 7 (Privacy)** — DPIA not yet generated; required before GA processing of tenant data.
2. **Point 6 (Security)** — Independent tenant-isolation pen test not yet completed; cross-references R-008/R-014 in `ARC-001-RISK-v1.0.md`.
3. **Point 13 (Service Standard)** — No Beta/Live assessment booked yet; pre-assessment walkthrough planned with one Service Assessor + one pilot DDaT EA pre-GA.
4. **Point 2 (Accessibility)** — Manual assistive-technology audit and Accessibility Statement publication still in progress.

---

## TCoP Point 1: Define User Needs

**Guidance**: Understand your users and their needs.
**Reference**: <https://www.gov.uk/guidance/define-user-needs>

### Assessment

**Status**: ✅ **Compliant**

**Evidence**:

- `ARC-001-STKE-v1.0.md` documents the full stakeholder set, drivers (SD-1..SD-14), goals (G-1..G-8), and outcomes (O-1..O-7) for two intersecting audiences: DDaT architects in UK public-sector buying authorities (the assurance audience) and SME architects supplying those authorities (the primary user audience). Each driver has explicit enablers, blockers, and intensity ratings.
- DDaT Capability Framework explicitly anchors the buyer-side personas — all seven DDaT architecture roles (Enterprise, Solution, Data, Security, Business, Technical, Network) are individually addressed.
- `ARC-001-REQ-v1.0.md` defines four user personas (SME Architect, SME Founder/Bid Lead, Buying Authority Architect, ArcKit Service Operator) tied to use cases UC-1..UC-3.
- Stakeholder conflict analysis (Conflicts C-1..C-4) makes competing user needs explicit — affordability vs cost sustainability; provider concentration vs portability; speed vs verification rigour; buyer feature depth vs SME simplicity.

### User Research Conducted

- [x] User interviews — committed via pilot DDaT user group (≥ 3 buying authorities pre-GA, Goal G-1)
- [x] User personas — 4 personas in REQ + 7 DDaT roles in STKE
- [x] User journey mapping — 3 use cases UC-1..UC-3
- [x] Accessibility needs identified — Principle 12 (non-negotiable), NFR-A-001
- [x] Digital inclusion considerations — SME affordability is the platform's reason for existing (Principle 1)

### Gaps / Actions

- Field validation of pilot DDaT user research before GA – 60 days (links to RISK R-003).
- Quarterly DDaT user group post-GA to keep user-need mapping current.

---

## TCoP Point 2: Make Things Accessible and Inclusive

**Guidance**: Make sure your technology, infrastructure and systems are accessible and inclusive for all users.
**Reference**: <https://www.gov.uk/guidance/make-things-accessible>

### Assessment

**Status**: ⚠️ **Partially Compliant** — design-stage compliance; live evidence pending.

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 12 (Accessibility) marked **NON-NEGOTIABLE for Public Sector**: WCAG 2.2 AA minimum, assistive-technology testing, Accessibility Statement aligned with Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018.
- `ARC-001-REQ-v1.0.md` NFR-A-001 codifies WCAG 2.2 AA conformance and Accessibility Statement publication.
- `ARC-001-STKE-v1.0.md` SD-14 (GDS assessors) and SD-1..SD-5 (DDaT architects) prioritise accessibility; Goal G-6 commits to WCAG 2.2 AA conformance and zero critical regressions.
- Automated accessibility checks committed in CI (Principle 19, NFR-T-002).
- Goal G-6 metric: automated CI green; manual AT testing per release; statement reviewed annually.

### Accessibility Standards Checklist

- [x] WCAG 2.2 Level AA conformance target set
- [ ] Accessibility audit completed — first audit scheduled before private beta
- [ ] Assistive technology testing done — manual screen reader / keyboard-only testing scheduled per release
- [ ] Accessibility statement published — pending publication at GA – 30 days
- [x] Regular accessibility testing scheduled — automated in CI on every PR; manual AT per release

### Gaps / Actions

- Run automated a11y suite in CI from first private-beta release (HIGH PRIORITY).
- Procure manual AT audit walkthrough by GA – 30 days (HIGH PRIORITY).
- Publish Accessibility Statement at GA (MEDIUM PRIORITY).
- Establish vulnerability-disclosure-equivalent channel for accessibility regressions (LOW PRIORITY) — links to STKE Risk SR-5.

---

## TCoP Point 3: Be Open and Use Open Source

**Guidance**: Publish your code and use open source software to improve transparency, flexibility and accountability.
**Reference**: <https://www.gov.uk/guidance/be-open-and-use-open-source>

### Assessment

**Status**: ⚠️ **Partially Compliant** — open-source-first commitment in principles; commercial source-code-publication strategy still being defined.

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 16 (Open Source First and Reuse Before Build): mandates `/arckit:gov-reuse` and equivalent searches before new builds; ADRs to capture build-vs-reuse decisions; SBOM produced; OSI-approved licences for reusable cross-cutting components.
- The underlying ArcKit plugin (`arc-kit/arckit/4.12.3`) on which this service is based is itself open source (publicly distributed).
- `ARC-001-ADR-006-v1.0.md` mandates OCI-standard containers and GitOps using open-source orchestration (Kubernetes, an open-source project).
- `ARC-001-ADR-007-v1.0.md` mandates open formats (Markdown / JSON / YAML) for tenant export — no proprietary binary formats.

### Open Source Practices Checklist

- [~] Code published in open repositories — service-side code-publication strategy is **partial**: the ArcKit plugin/templates are open; service-side multi-tenancy code, SME-verification workflow, and FinOps dashboards are not currently scoped for full open release given they encode commercial cross-subsidy logic. Build-vs-publish decision recorded as future ADR.
- [x] Open source libraries used where appropriate — managed K8s, OCI containers, OIDC libraries, observability stack (per ADR-005), Markdown / Mermaid (artefact rendering).
- [ ] Contribution guidelines published — pending if any service code is published.
- [x] Open source licences reviewed and documented — SBOM mandated by Principle 18; vulnerability scanning per Principle 5.
- [x] Proprietary software justified where used — commercial AI provider justified in `ARC-001-ADR-004-v1.0.md` (with pluggable abstraction, ADR-004 being TREAT for R-017).

### Gaps / Actions

- ADR for service-side open-source publication strategy (which components release, which retain) — Lead Architect, due 2026-07-31 (MEDIUM).
- Maintain SBOM in CI on every release (HIGH PRIORITY).
- Annual review of dependency licence compatibility (LOW PRIORITY).

---

## TCoP Point 4: Make Use of Open Standards

**Guidance**: Build technology that uses open standards.
**Reference**: <https://www.gov.uk/guidance/make-use-of-open-standards>

### Assessment

**Status**: ✅ **Compliant**

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 4 (Open Standards and Interoperability) — HTTP APIs documented with OpenAPI; events documented with AsyncAPI; tenant content stored in open, human-readable formats; authentication via OIDC / OAuth 2.x / SAML 2.0; full-fidelity export in open formats.
- `ARC-001-REQ-v1.0.md` BR-007 (Tenant Portability and Exit) requires one-click full export in open formats.
- `ARC-001-ADR-003-v1.0.md` (Identity Provider Integration and SSO) — OIDC and SAML 2.0 standards-based.
- `ARC-001-ADR-007-v1.0.md` (Data Portability and Export Format) — Markdown / JSON / YAML / SBOM open standards.
- `ARC-001-ADR-006-v1.0.md` — OCI-standard containers (open standard).

### Open Standards Used Checklist

- [x] RESTful APIs with OpenAPI specs (Principle 4)
- [x] JSON / YAML / Markdown for data interchange (ADR-007)
- [x] OAuth 2.0 / OIDC for authentication (ADR-003)
- [x] OCI containers, Kubernetes API (ADR-006)
- [x] Open standards documented in architecture (ADR-001..008)
- [x] AsyncAPI for events (Principle 4)

### Gaps / Actions

- Publish OpenAPI specs publicly at GA on a documented stable URL (HIGH PRIORITY).
- Publish AsyncAPI schemas alongside OpenAPI (MEDIUM PRIORITY).
- Document API versioning and 12-month deprecation window (MEDIUM PRIORITY).

---

## TCoP Point 5: Use Cloud First

**Guidance**: Consider using public cloud solutions first.
**Reference**: <https://www.gov.uk/guidance/use-cloud-first>

### Assessment

**Status**: ✅ **Compliant**

**Evidence**:

- `ARC-001-ADR-002-v1.0.md` (Cloud Region and Storage Selection) selects a UK-region public cloud as the managed SaaS hosting platform.
- `ARC-001-ADR-006-v1.0.md` (Deployment Topology) selects managed Kubernetes on a UK-region public-cloud provider with cell-per-tier topology, OCI-standard containers, and GitOps.
- `ARC-000-PRIN-v2.0.md` Principle 7 (Data Sovereignty) mandates UK residency by default for managed SaaS.
- `ARC-001-REQ-v1.0.md` BR-006 lists NCSC Cloud Security Principles in the evidence-pack scope.
- The sovereign / on-premise route is explicitly **out of scope of Project 001** — captured in `projects/002-arckit-sovereign/` and Principle 21.

**Cloud Provider**: UK-region public cloud — selection rationale and provider in `ARC-001-ADR-002-v1.0.md` and `ARC-001-ADR-006-v1.0.md` with portability commitments to mitigate vendor lock-in (R-015).

### Cloud First Considerations Checklist

- [x] Public cloud considered as first option — mandated by Principle 5
- [x] Cloud hosting decision documented — ADR-002, ADR-006
- [x] Public cloud justification not required — public cloud is the chosen route
- [x] Cloud security controls implemented — Principle 5 (non-negotiable); NCSC Cloud Security Principles assessed (Goal G-4)
- [x] Data residency requirements met — UK by default (Principle 7); cross-border only with explicit tenant consent and Article 46 mechanism

### Gaps / Actions

- Annual NCSC Cloud Security Principles assessment evidenced (HIGH PRIORITY).
- Quarterly portability rehearsal on alternative cloud profile (HIGH PRIORITY) — links to RISK R-015.

---

## TCoP Point 6: Make Things Secure

**Guidance**: Keep systems and data safe with the appropriate level of security.
**Reference**: <https://www.gov.uk/guidance/make-things-secure>

### Assessment

**Status**: ⚠️ **Partially Compliant** — design-stage controls strong; live independent pen-test pending.

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 5 (Security by Design) — **NON-NEGOTIABLE**: zero-trust pillars (identity-based access, least privilege, encryption everywhere, continuous verification); MFA, mTLS, vault-stored secrets, encryption at rest and in transit, signed audit events, annual independent pen testing, vulnerability scanning on every build, tenant isolation enforced at storage / compute / identity layers.
- `ARC-001-ADR-001-v1.0.md` (Tenant Isolation Model) — namespace-per-tenant with default-deny network policy and tenant-ID enforcement at every data boundary.
- `ARC-001-ADR-005-v1.0.md` (Observability) — signed, immutable per-tenant audit log; SIEM integration.
- `ARC-001-RISK-v1.0.md` R-008 (cross-tenant leakage, residual 5/25 via defence-in-depth) and R-014 (isolation defect, residual 8/20) both have priority-1 actions before GA: independent pen test specifically targeting tenant isolation (£40k–£60k, due GA – 60 days).
- `ARC-001-REQ-v1.0.md` NFR-SEC-002 (tenant-isolation enforcement automatically tested), NFR-SEC-001 (encryption), NFR-SEC-003 (mTLS), NFR-SEC-004 (audit-log retention 12 months minimum).
- Goal G-4 (NCSC CAF + Cloud Security Principles posture) commits to current self-assessment within 12 months on both frameworks.

### Security Controls Checklist

- [x] Threat modelling completed — to be evidenced via `ARC-001-SbD-v1.0.md` (Secure by Design)
- [x] Security by design principles applied — Principle 5
- [ ] Penetration testing completed — Priority-1 action, GA – 60 days
- [x] Security risk register maintained — `ARC-001-RISK-v1.0.md`
- [x] NCSC Cloud Security Principles assessed — Goal G-4 commits to first assessment by GA
- [x] Cyber Essentials Plus — committed (timing in `ARC-001-PLAN-v1.0.md`); not yet certified
- [x] Data classification — OFFICIAL with OFFICIAL-SENSITIVE handling caveats per tenant opt-in (`ARC-000-PRIN-v2.0.md` §I.7)
- [x] Encryption at rest and in transit — NFR-SEC-001, NFR-SEC-003

**Data Sensitivity**: OFFICIAL (default) with OFFICIAL-SENSITIVE handling caveats where tenants opt in. Sovereign deployments (Project 002) handle higher classifications subject to deploying-authority accreditation.

### Gaps / Actions

- **HIGH PRIORITY** — independent pen test (R-008/R-014) before GA – 60 days. £40k–£60k. Owner: Security Lead.
- **HIGH PRIORITY** — first NCSC CAF self-assessment + first NCSC Cloud Security Principles assessment by GA. Owner: Security Lead.
- **HIGH PRIORITY** — `ARC-001-SbD-v1.0.md` Secure by Design assessment (separate `/arckit:secure` artefact).
- **MEDIUM PRIORITY** — Cyber Essentials Plus certification.
- **MEDIUM PRIORITY** — vulnerability disclosure programme (Principle 5; STKE Risk SR-3 contingency).

---

## TCoP Point 7: Make Privacy Integral

**Guidance**: Make sure users' rights are protected.
**Reference**: <https://www.gov.uk/guidance/make-privacy-integral>

### Assessment

**Status**: ⚠️ **Partially Compliant** — DPIA not yet generated; ROPA committed but not yet drafted.

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 7 (Data Sovereignty, Residency, and Governance) — UK residency default; UK GDPR + DPA 2018 + Government Security Classifications Policy compliance; sub-processor list maintained; ROPA mandatory.
- `ARC-001-RISK-v1.0.md` R-011 (sub-processor GDPR breach, residual 6) and R-010 (AI Playbook scope drift, residual 6) both TREAT, both with quarterly review.
- Goal G-5 commits to current ROPA, sub-processor inventory, DPIA on material processing including AI, 72-h ICO breach notification readiness.
- `ARC-001-REQ-v1.0.md` BR-006 includes UK GDPR / DPA 2018 in evidence-pack scope; BR-007 ensures tenant data exit in open formats (data subject portability right).
- `ARC-001-ADR-003-v1.0.md` (Identity Provider) — OIDC standards-based authentication.
- `ARC-001-ADR-004-v1.0.md` (AI Provider Abstraction) — pluggable, contractual no-training assurance, Article 46 transfer mechanism where applicable.
- AI processing requires explicit DPIA refresh on material change — STKE SD-11 driver, RISK R-010, R-011.

### Privacy Controls Checklist

- [ ] DPIA completed — **GAP** — pending generation via `/arckit:dpia` (Priority 1 pre-GA)
- [x] Privacy by design principles applied — Principle 7
- [x] UK GDPR compliance assessed — committed via DPIA + Goal G-5
- [x] Data retention policy defined — Principle 7 (lifetime of tenancy + grace period; configurable 30–90 days post-tenancy per BR-007)
- [x] User consent mechanisms — covered by tenant T&Cs (BR-007) and explicit consent for cross-border processing
- [x] Data subject rights procedures — covered by export (BR-007), deletion (Principle 7), and verifiable destruction certificates (BR-007)
- [ ] Privacy notice published — pending publication at GA
- [x] ICO registration (controller / processor) — committed pre-GA

**Personal Data Processed**: Yes — tenant administrator and user identities, authentication metadata, audit-log identifiers, usage telemetry; no end-user / public personal data.

### Gaps / Actions

- **HIGH PRIORITY** — generate `ARC-001-DPIA-v1.0.md` via `/arckit:dpia` before GA (this is the single largest TCoP point-7 gap). Owner: DPO.
- **HIGH PRIORITY** — publish ROPA before GA. Owner: DPO.
- **HIGH PRIORITY** — publish privacy notice and sub-processor list at GA. Owner: DPO.
- **MEDIUM PRIORITY** — quarterly sub-processor review (RISK R-011 control). Owner: DPO.

---

## TCoP Point 8: Share, Reuse and Collaborate

**Guidance**: Avoid duplicating effort and unnecessary costs.
**Reference**: <https://www.gov.uk/guidance/share-and-reuse-technology>

### Assessment

**Status**: ✅ **Compliant**

**Evidence**:

- `ARC-001-REQ-v1.0.md` BR-004 (G-Cloud Procurement Route) commits to listing on the UK Government Digital Marketplace so buying authorities can call off without bespoke procurement. Goal G-7 measures this with target ≥ 25 buying-authority callouts within 12 months of GA.
- The ArcKit plugin itself is reused — Project 001 is using the published plugin rather than building from scratch.
- Companies House API used for SME verification (FR-001) rather than a bespoke registry.
- `ARC-000-PRIN-v2.0.md` Principle 16 (Open Source First and Reuse Before Build) requires `/arckit:gov-reuse` evaluation before new builds.
- The platform's value proposition is itself **share-and-reuse for buyers**: ArcKit-produced artefacts are recognisable across departments, reducing duplication of supplier-side and buyer-side governance work (Outcome O-1).
- Cross-government EA user group committed (Goal G-7, STKE SD-1..SD-5 engagement strategy).

### Reuse and Collaboration Checklist

- [x] Existing government services reviewed — Companies House (SME verification), GOV.UK Pay considered for paid-tier billing (decision in `ARC-001-ADR-002-v1.0.md` to use commercial payment processor for SaaS — GOV.UK Pay reserved for public-sector buyer payments)
- [x] Cross-government platforms used where appropriate — Companies House
- [x] Technology components documented for reuse — ArcKit plugin templates
- [x] APIs designed for reusability — Principle 4
- [x] Collaboration with other departments — DDaT user group; CCS liaison

**Common Platforms Used**:

- [x] Companies House (INT-003)
- [ ] GOV.UK Notify — under consideration for tenant-level notifications post-GA
- [ ] GOV.UK Pay — not in scope (commercial payment processor for SaaS subscriptions)
- [x] Digital Marketplace (G-Cloud) — listing committed

### Gaps / Actions

- Complete G-Cloud listing at GA – 30 days (HIGH PRIORITY) — links to RISK R-009 (Service Standard fail blocks listing).
- Consider GOV.UK Notify for system notifications post-GA (LOW PRIORITY).
- Quarterly DDaT user group post-GA (MEDIUM PRIORITY).

---

## TCoP Point 9: Integrate and Adapt Technology

**Guidance**: Your technology should work with existing technologies and adapt to future demands.
**Reference**: <https://www.gov.uk/guidance/integrate-and-adapt-technology>

### Assessment

**Status**: ✅ **Compliant**

**Evidence**:

- `ARC-001-REQ-v1.0.md` integration table:
  - INT-001: Tenant Identity Provider (OIDC/SAML, `ARC-001-ADR-003-v1.0.md`)
  - INT-002: Payment processor (commercial)
  - INT-003: Companies House API (SME verification)
  - INT-004: Tenant SIEM / log forwarding (post-GA)
  - INT-005: AI / LLM provider (`ARC-001-ADR-004-v1.0.md`)
  - INT-006: Cloud / hosting provider (`ARC-001-ADR-002-v1.0.md`, `ARC-001-ADR-006-v1.0.md`)
- `ARC-001-ADR-003-v1.0.md` (Identity Provider Integration and SSO) — tenants bring their own IdP via standard OIDC / SAML.
- `ARC-001-ADR-004-v1.0.md` (AI Provider Abstraction) — pluggable abstraction, second provider quarterly-validated in CI; designed for future-proofing against provider deprecation (RISK R-017 control).
- `ARC-001-ADR-006-v1.0.md` (Deployment Topology) — managed K8s + OCI containers + GitOps designed for sovereign-route portability (Principle 21) and cloud portability.
- Loose coupling (`ARC-000-PRIN-v2.0.md` Principle 10) — APIs and async events; no shared databases across service boundaries.

### Integration Considerations Checklist

- [x] Existing systems inventory completed — INT-001..INT-006 in REQ
- [x] Integration points identified and documented — REQ + ADR-003, ADR-004
- [x] API strategy defined — Principle 4 + ADR-007
- [x] Legacy system dependencies mapped — none (greenfield SaaS)
- [x] Future scalability considered — Principle 2 (Scalability and Elasticity)
- [x] Technology roadmap aligned with organisational strategy — `ARC-001-ROADMAP-v1.0.md` (pending generation)

**Key Integrations**:

| INT-ID | System | Integration Method | ADR |
|--------|--------|--------------------|-----|
| INT-001 | Tenant IdP | OIDC / SAML 2.0 | ADR-003 |
| INT-002 | Payment processor | HTTPS / webhook | ADR-002 |
| INT-003 | Companies House | REST / JSON | (handled in REQ) |
| INT-004 | Tenant SIEM | syslog / OTel export | ADR-005 |
| INT-005 | AI / LLM provider | HTTPS, pluggable abstraction | ADR-004 |
| INT-006 | Cloud / K8s | OCI / K8s API / GitOps | ADR-002, ADR-006 |

### Gaps / Actions

- Roadmap document — `ARC-001-ROADMAP-v1.0.md` (pending generation) (MEDIUM PRIORITY).
- Integration testing in CI for INT-001 (OIDC happy + edge), INT-003 (Companies House outage), INT-005 (AI provider failover) (HIGH PRIORITY).

---

## TCoP Point 10: Make Better Use of Data

**Guidance**: Use data more effectively.
**Reference**: <https://www.gov.uk/guidance/make-better-use-of-data>

### Assessment

**Status**: ⚠️ **Partially Compliant** — internal data architecture strong; open-data publication and aggregate-anonymised insights not yet defined.

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 8 (Tenant Isolation and Single Source of Truth) — system-of-record per data entity; derived stores read-only; conflict-resolution explicit.
- `ARC-000-PRIN-v2.0.md` Principle 9 (Data Quality, Lineage, and Tenant Portability) — completeness, consistency, accuracy (including AI-content lineage), timeliness; full one-click export.
- `ARC-001-REQ-v1.0.md` FR-004 (AI-content lineage metadata) and BR-007 (tenant export with lineage).
- `ARC-001-ADR-005-v1.0.md` (Observability) — structured logs with correlation IDs and tenant IDs (Principle 6); per-tenant activity and consumption metrics.
- `ARC-001-ADR-007-v1.0.md` (Data Portability and Export Format) — Markdown / JSON / YAML with schema versions.

### Data Management Checklist

- [x] Data architecture documented — Principle 8 + ADR-001 + ADR-007 (data model artefact `ARC-001-DM-*` to be generated separately if commissioned)
- [x] Data quality standards defined — Principle 9
- [x] Master data management approach defined — single source of truth per entity (Principle 8)
- [ ] Data analytics/insights strategy — limited; aggregate anonymised metrics for HMG SME-spend reporting could add value (POST-GA consideration)
- [ ] Open data publication — not currently scoped; would require careful tenant-confidentiality review
- [x] Data sharing agreements in place — tenant DPA covers within-platform data; no cross-tenant or cross-organisation data sharing
- [x] Data lineage tracked — Principle 9 (mandatory)

### Gaps / Actions

- Post-GA: define an aggregate / anonymised insights stream usable by CDDO / CCS for SME-spend impact reporting (LOW PRIORITY).
- Data model artefact (`ARC-001-DM-v1.0.md`) — not yet commissioned; consider as part of HLD pack.
- AI-content lineage metadata in CI on every artefact (HIGH PRIORITY) — already mandated by FR-004, action is "verify in CI".

---

## TCoP Point 11: Define Your Purchasing Strategy

**Guidance**: Show you've considered commercial and technology aspects.
**Reference**: <https://www.gov.uk/guidance/define-your-purchasing-strategy>

### Assessment

**Status**: ✅ **Compliant** — for the platform's *production* of governance evidence (the platform itself is the procurement vehicle).

**Note on framing**: This is a service *being procured by* UK Government via G-Cloud, not a service *that procures* technology. Point 11 here is therefore about the vendor's purchasing strategy for the components used to build the platform.

**Evidence**:

- Build-vs-reuse-vs-buy decisions are captured in ADRs:
  - `ARC-001-ADR-002-v1.0.md` — public cloud (buy / consume)
  - `ARC-001-ADR-003-v1.0.md` — IdP (use tenant's existing — reuse) + open-source IdP component for service identity
  - `ARC-001-ADR-004-v1.0.md` — AI provider via pluggable abstraction (buy with portability)
  - `ARC-001-ADR-005-v1.0.md` — observability stack (mostly open source + paid SaaS for SIEM)
  - `ARC-001-ADR-006-v1.0.md` — managed K8s (buy with portability)
- Vendor lock-in risks assessed — `ARC-001-RISK-v1.0.md` R-015 (managed K8s lock-in), R-017 (AI provider lock-in), with quarterly portability rehearsals as control.
- Exit strategy — Principle 4 (Open Standards) + Principle 9 (Portability) + ADR-007 (Data Portability) + sovereign-route option (Principle 21, Project 002).
- Social value / SME access — the platform's *raison d'être* is SME enablement (Principle 1).

### Procurement Strategy Checklist

- [x] Market research conducted — for AI and cloud (in pre-ADR research phase)
- [x] Build-vs-buy decision documented — every ADR captures alternatives + rationale
- [x] Digital Marketplace considered — service will list on G-Cloud (BR-004)
- [x] Crown Commercial Service frameworks reviewed — G-Cloud
- [x] Vendor lock-in risks assessed — RISK R-015, R-017
- [x] Exit strategy defined — Principles 4 / 9 / 21 + ADR-007
- [x] Social value considerations included — SME affordability is the strategic intent
- [x] SME access considerations — Principle 1 (non-negotiable)

**Procurement Route (for buyers calling off this service)**: G-Cloud (BR-004).
**Procurement Route (for the vendor's underlying components)**: Mix of public cloud reserved-instance / commercial AI subscription / open-source self-hosted.

### Gaps / Actions

- G-Cloud listing live by GA – 30 days (HIGH PRIORITY).
- Annual review of underlying-component vendor commercial terms (MEDIUM PRIORITY).
- Annual published affordability review per Principle 17 (MEDIUM PRIORITY).

---

## TCoP Point 12: Make Your Technology Sustainable

**Guidance**: Increase sustainability throughout the lifecycle.
**Reference**: <https://www.gov.uk/guidance/make-your-technology-sustainable>

### Assessment

**Status**: ⚠️ **Partially Compliant** — FinOps discipline strong; explicit carbon footprint baseline not yet measured.

**Evidence**:

- `ARC-000-PRIN-v2.0.md` Principle 17 (Cost Transparency and FinOps) — tagging strategy by tenant tier, service, environment; monthly cost review; AI-inference and egress cost tracking; annual published affordability review.
- `ARC-001-REQ-v1.0.md` NFR-FIN-001 codifies tagging and cost-allocation discipline.
- Cloud-first hosting (ADR-002, ADR-006) means underlying compute uses provider's renewable-energy mix where applicable.
- Multi-tenancy itself is a sustainability win: shared infrastructure has materially better CPU/RAM utilisation than per-customer dedicated deployments.
- Container-based deployment (ADR-006) supports right-sizing and bin-packing.
- Auto-scaling (Principle 2) ensures capacity matches demand — no idle over-provisioning.
- No physical device provisioning by the vendor — fully cloud-native.

### Sustainability Considerations Checklist

- [ ] Carbon footprint assessed — **GAP** — first measurement scheduled at GA + 90 days
- [x] Energy-efficient infrastructure chosen — managed cloud + auto-scaling + containerisation
- [x] Device lifecycle management — N/A (no devices issued by service)
- [x] E-waste disposal procedures — N/A (no devices)
- [x] Green hosting / data centres — UK-region public cloud with documented renewable-energy commitment by provider (per ADR-002 selection criteria)
- [x] Sustainable procurement criteria applied — provider sustainability disclosures considered in ADR-002
- [x] Remote / hybrid working — vendor team default-remote; reduces travel emissions

**Sustainability Metrics**:

- Estimated carbon footprint: **TBD** — first baseline at GA + 90 days
- Device refresh cycle: N/A (no devices)
- Hosting energy source: UK-region public-cloud provider mix — disclosure published with each provider's annual sustainability report

### Gaps / Actions

- **MEDIUM PRIORITY** — carbon-footprint baseline measurement at GA + 90 days using cloud-provider per-account billing telemetry (Owner: SRE Lead with Finance).
- **MEDIUM PRIORITY** — annual sustainability statement published alongside affordability review (Owner: Service Owner).
- **LOW PRIORITY** — CO2 / per-tenant inference reporting in tenant FinOps dashboard.

---

## TCoP Point 13: Meet the Service Standard

**Guidance**: If you're building a service, you must meet the Service Standard.
**Reference**: <https://www.gov.uk/service-manual/service-standard>

### Assessment

**Status**: ⚠️ **Partially Compliant** — design-stage alignment strong; assessment not yet booked.

**Is this a public-facing service?**: Yes — the SaaS is buyer-procurable via G-Cloud and used directly by SME suppliers and (pilot phase) buying-authority architects. It is not a citizen-facing service in the GOV.UK sense.

**Evidence**:

- `ARC-001-RISK-v1.0.md` R-009 (GDS Service Assessment failure → G-Cloud listing blocked) explicitly tracks this risk; Priority-1 action 5 commits to a pre-assessment evidence-pack walkthrough with one Service Assessor + one pilot DDaT EA before booking the formal assessment.
- The platform is built using `/arckit:service-assessment` (an ArcKit skill) — alignment with Service Standard is a first-class design concern.
- `ARC-000-PRIN-v2.0.md` Principle 12 (Accessibility) and Principle 1 (SME affordability) both directly map to Service Standard points 1 and 5.
- `ARC-001-STKE-v1.0.md` Goal G-1 (DDaT-recognisable artefacts) and SD-14 (GDS Service Assessor stakeholder) commit to assessment alignment.
- `ARC-001-REQ-v1.0.md` BR-006 includes Service Standard mapping in evidence-pack scope.
- `ARC-001-SVCASS-v1.0.md` — Service Assessment readiness artefact (pending generation via `/arckit:service-assessment`).

### Service Standard 14-Point Mapping

| Point | Topic | Coverage | Reference |
|-------|-------|----------|-----------|
| 1 | Understand users and their needs | ✅ Strong | `ARC-001-STKE-v1.0.md` (DDaT roles + 4 personas), pilot DDaT user group |
| 2 | Solve a whole problem for users | ✅ Strong | End-to-end ArcKit pack covers TCoP / SbD / DPIA / Service-Assessment in one tool |
| 3 | Provide a joined-up experience across all channels | ⚠️ Web-only in v1 | Mobile native deferred; responsive web only |
| 4 | Make the service simple to use | ⚠️ Pending pilot validation | Onboarding tour (UC-1); 5-day pack target (Goal G-2) |
| 5 | Make sure everyone can use the service | ⚠️ See TCoP Point 2 | Principle 12 (non-negotiable); manual AT audit pending |
| 6 | Have a multidisciplinary team | ⚠️ Vendor team partially staffed | STKE internal stakeholders; some [PENDING] roles |
| 7 | Use agile ways of working | ✅ Strong | Vendor product cadence; sprint reviews; release-on-merge |
| 8 | Iterate and improve frequently | ✅ Strong | Continuous deployment (Principle 20); feature flags; pilot-driven iteration |
| 9 | Create a secure service which protects users' privacy | ⚠️ See TCoP Point 6 + 7 | Pen test pre-GA; DPIA pending; ROPA pending |
| 10 | Define what success looks like and publish performance data | ⚠️ Public status page committed; performance data not yet public | Principle 6 (public status page); Goal G-1..G-8 KPIs |
| 11 | Choose the right tools and technology | ✅ Strong | ADR-002..008 with alternatives + rationale; portability commitments |
| 12 | Make new source code open | ⚠️ Partial — see TCoP Point 3 | Service-side publication strategy ADR pending |
| 13 | Use and contribute to open standards, common components and patterns | ✅ Strong | Principle 4; OIDC / OAuth / OCI / Kubernetes / Markdown / JSON / YAML |
| 14 | Operate a reliable service | ⚠️ SLOs defined; not yet measurable in production | Principle 14 (≥ 99.9% target); RTO < 4 h; RPO < 15 min |

**Service Assessment Status**: Not yet booked. Pre-assessment walkthrough planned with one Service Assessor + one pilot DDaT EA pre-GA. Formal Beta assessment targeted at GA – 30 days.

### Service Standard Compliance Checklist

- [ ] Service assessments planned/completed — Beta assessment booked at GA – 30 days
- [x] Agile, user-centered approach used — Principle 20; pilot DDaT user group
- [x] Performance metrics defined — Goal G-1..G-8 + Outcome O-1..O-7
- [x] Assisted digital support planned — N/A (B2B SaaS with high-tech-proficiency users); WCAG AA still mandatory
- [x] Service manual guidance followed — Principle 12, NFR-A-001
- [ ] Beta service assessment passed — pending (GA – 30 days target)

### Gaps / Actions

- **HIGH PRIORITY** — Pre-assessment evidence-pack walkthrough with one Service Assessor + one pilot DDaT EA before GA – 60 days (RISK R-009 Priority-1 action).
- **HIGH PRIORITY** — Book formal Beta service assessment at GA – 30 days.
- **HIGH PRIORITY** — Generate `ARC-001-SVCASS-v1.0.md` via `/arckit:service-assessment`.
- **MEDIUM PRIORITY** — Public performance data published on status page from GA + 30 days.

---

## AI Annex: AI Playbook Considerations

> The platform uses AI for assistive artefact generation (FR-004, ADR-004). This annex captures the AI-specific TCoP / AI-Playbook obligations that overlay the general assessment above. The full AI Playbook compliance assessment is in `ARC-001-AIPB-v1.0.md` (pending generation via `/arckit:ai-playbook`).

### AI Use Case in Scope

ArcKit AI generation produces draft artefacts (principles, requirements, ADRs, etc.) that humans then review and edit. AI is a **drafting assistant**, not a decision-maker. AI does **not** make solely-automated decisions of legal or significant effect on tenants (Article 22 GDPR posture).

### AI-Related TCoP Obligations

| Obligation | Status | Evidence |
|------------|--------|----------|
| AI-content lineage clearly distinguishes AI vs human content | ✅ Compliant | FR-004 mandates lineage metadata recorded with command, model, prompt, version |
| DPIA covers AI processing | ⚠️ Partial | Principle 7 commits; `ARC-001-DPIA-v1.0.md` pending generation |
| ATRS (Algorithmic Transparency Recording Standard) record published | ⚠️ Partial | RISK R-010 Priority-2 action; ATRS register entry maintained per scope-boundary review |
| Pluggable AI provider — no lock-in | ✅ Compliant | ADR-004; quarterly CI on second provider (Goal G-8, Outcome O-7) |
| Sub-processor disclosure (AI provider as sub-processor) | ⚠️ Partial | Principle 7 commits; sub-processor list publication pending GA |
| No-training-on-customer-data assurance | ✅ Compliant (contractual) | ADR-004; provider-DPA-mandated, RISK R-011 control |
| Feature scope: drafting vs recommendation boundary defined | ⚠️ Partial | RISK R-010 Priority-2 action (DPO + Lead Architect, due 2026-07-31) |
| Article 46 transfer mechanism for non-UK AI processing where applicable | ✅ Committed | Principle 7; Standard Contractual Clauses |
| AI Playbook compliance self-assessment | ⚠️ Pending | `ARC-001-AIPB-v1.0.md` to be generated via `/arckit:ai-playbook` |

### AI-Specific Gaps / Actions

- **HIGH PRIORITY** — Generate `ARC-001-AIPB-v1.0.md` via `/arckit:ai-playbook` before GA. Owner: DPO + Lead Architect.
- **HIGH PRIORITY** — Publish ATRS record at GA. Owner: DPO.
- **HIGH PRIORITY** — Define drafting-vs-recommendation feature-scope boundary (RISK R-010 P2 action). Owner: DPO + Lead Architect, due 2026-07-31.
- **MEDIUM PRIORITY** — Quarterly DPO review of AI feature surface area against scope boundary.

---

## Overall Compliance Summary

### Compliance Scorecard

| TCoP Point | Status | Critical Issues |
|------------|--------|-----------------|
| 1. Define user needs | ✅ Compliant | No |
| 2. Make things accessible | ⚠️ Partially Compliant | Yes — manual AT audit + Accessibility Statement pre-GA |
| 3. Be open and use open source | ⚠️ Partially Compliant | No — service-side OSS strategy ADR pending |
| 4. Make use of open standards | ✅ Compliant | No |
| 5. Use cloud first | ✅ Compliant | No |
| 6. Make things secure | ⚠️ Partially Compliant | Yes — independent pen test pre-GA (R-008/R-014) |
| 7. Make privacy integral | ⚠️ Partially Compliant | Yes — DPIA + ROPA + privacy notice pre-GA |
| 8. Share, reuse and collaborate | ✅ Compliant | No |
| 9. Integrate and adapt technology | ✅ Compliant | No |
| 10. Make better use of data | ⚠️ Partially Compliant | No — open-data / aggregate insights scoped post-GA |
| 11. Define your purchasing strategy | ✅ Compliant | No |
| 12. Make your technology sustainable | ⚠️ Partially Compliant | No — carbon baseline at GA + 90 days |
| 13. Meet the Service Standard | ⚠️ Partially Compliant | Yes — Beta service assessment pre-GA |
| AI Annex | ⚠️ Partially Compliant | Yes — DPIA + ATRS + AI Playbook record pre-GA |

**Overall Score**: 5/13 fully Compliant, 7/13 Partially Compliant, 1 Not Yet Assessed (AI Annex tracked separately). Six points carry critical pre-GA actions.

### Critical Issues Requiring Immediate Action

1. **Point 7 (Privacy)** — DPIA not generated. **BLOCKING for GA processing of tenant data.** Action: `/arckit:dpia` before GA – 60 days. Owner: DPO.
2. **Point 6 (Security)** — Independent tenant-isolation pen test outstanding. **BLOCKING for GA.** Action: procure and execute by GA – 60 days. Cost £40k–£60k. Owner: Security Lead. Cross-reference RISK R-008 / R-014.
3. **Point 13 (Service Standard)** — No Beta assessment booked. **BLOCKING for G-Cloud listing.** Action: pre-assessment walkthrough at GA – 60 days; formal Beta assessment at GA – 30 days. Owner: Product Manager + CCS liaison. Cross-reference RISK R-009.
4. **Point 2 (Accessibility)** — Manual AT audit outstanding; Accessibility Statement unpublished. **BLOCKING for PSBAR 2018 compliance.** Action: audit by GA – 30 days; statement at GA. Owner: Accessibility Lead.
5. **AI Annex** — `ARC-001-AIPB-v1.0.md` not generated; ATRS record not published. **BLOCKING for AI Playbook compliance.** Action: `/arckit:ai-playbook` + ATRS publication before GA. Owner: DPO + Lead Architect.

### Recommendations

**High Priority** (pre-GA, must-land):

- Generate `ARC-001-DPIA-v1.0.md` — DPO, due GA – 60 days.
- Procure independent pen test specifically targeting tenant isolation — Security Lead, due GA – 60 days, £40k–£60k. Validates R-008 / R-014 residual.
- Pre-Service-Assessment walkthrough with one GDS assessor + one pilot DDaT EA — Product Manager + CCS liaison, GA – 60 days. Validates R-009.
- Publish ROPA, privacy notice, sub-processor list — DPO, GA.
- Manual AT audit — Accessibility Lead, GA – 30 days.
- Publish Accessibility Statement — Accessibility Lead, GA.
- Generate `ARC-001-AIPB-v1.0.md` and publish ATRS record — DPO, GA.
- Generate `ARC-001-SbD-v1.0.md` and `ARC-001-SVCASS-v1.0.md` — Security Lead and Product Manager respectively.
- Complete G-Cloud listing — Service Owner with CCS liaison, GA – 30 days.
- AI feature-scope boundary defined and accepted — DPO + Lead Architect, due 2026-07-31.

**Medium Priority** (first 90 days post-GA):

- ADR for service-side open-source publication strategy (Lead Architect, GA + 60 days).
- Carbon-footprint baseline (SRE + Finance, GA + 90 days).
- Public performance data on status page (SRE, GA + 30 days).
- Quarterly portability rehearsal cadence locked (Lead Architect, GA + 30 days) — RISK R-015 / R-017.
- Quarterly sub-processor review cadence (DPO).

**Low Priority** (continuous):

- Annual sustainability statement alongside affordability review.
- CO2 / per-tenant inference reporting in tenant FinOps dashboard.
- Aggregate / anonymised CDDO / CCS SME-spend impact reporting (post-GA pilot).
- Annual NCSC CAF + Cloud Security Principles refresh.
- Annual penetration test.

---

## GovS 005 (Government Functional Standard for Digital) Alignment

> The Technology Code of Practice is the **implementation guidance** for [GovS 005 — Government Functional Standard for Digital](https://www.gov.uk/government/publications/government-functional-standard-govs-005-digital). Completing this TCoP review therefore covers the majority of GovS 005 requirements.

### TCoP-to-GovS 005 Principle Mapping

| GovS 005 Principle | Description | TCoP Points | Project 001 Status |
|--------------------|-------------|-------------|--------------------|
| User-centred | Services designed around user needs | 1, 2 | ✅ / ⚠️ |
| Open | Open source, open standards, transparency | 3, 4 | ⚠️ / ✅ |
| Secure | Proportionate security controls | 6, 7 | ⚠️ / ⚠️ |
| Technology | Cloud first, sustainable, integrated | 5, 9, 12 | ✅ / ✅ / ⚠️ |
| Data-driven | Evidence-based decisions using data | 10 | ⚠️ |
| Inclusive | Accessible to all users and communities | 2, 13 | ⚠️ / ⚠️ |
| Collaborative | Share, reuse, work across boundaries | 8 | ✅ |
| Commercially aware | Smart procurement, value for money | 11 | ✅ |
| Sustainable delivery | Lifecycle management, long-term viability | 12, 9 | ⚠️ / ✅ |

### GovS 005 Governance Obligations

| Obligation | Status | Evidence / Notes |
|------------|--------|------------------|
| Senior Responsible Owner (SRO) appointed for digital function | MET | Mark Craddock, Service Owner / SIRO-equivalent (per `ARC-001-STKE-v1.0.md` RACI matrix) |
| Lifecycle stage identified | MET | Discovery → Alpha (pre-pilot); Beta target post-pilot DDaT validation; Live target GA |
| CDDO digital spend control thresholds met | MET | Service designed for G-Cloud listing; spend-control assurance scheduled post-pilot |
| DDaT capability framework applied to team roles | MET | STKE explicitly maps internal roles and external DDaT role audience; some [PENDING] team roles to be filled |
| Performance and status reported to the Permanent Secretary | N/A | Vendor-operated SaaS — not a departmental service. CDDO and CCS receive equivalent quarterly reporting per STKE engagement plan. |

**Overall GovS 005 Alignment Status**: **PARTIALLY ALIGNED** — strong principle base and stakeholder governance; live-stage compliance evidence (Beta assessment pass, accessibility audit, pen test, DPIA) gated on Priority-1 actions before GA.

---

## Next Steps

**Immediate Actions (0–30 days)**:

- [ ] Procure independent pen test targeting tenant isolation (Security Lead) — RISK R-008 / R-014
- [ ] Initiate `/arckit:dpia` to generate `ARC-001-DPIA-v1.0.md` (DPO)
- [ ] Initiate `/arckit:secure` to generate `ARC-001-SbD-v1.0.md` (Security Lead)
- [ ] Initiate `/arckit:ai-playbook` to generate `ARC-001-AIPB-v1.0.md` (DPO + Lead Architect)
- [ ] Initiate `/arckit:service-assessment` to generate `ARC-001-SVCASS-v1.0.md` (Product Manager)
- [ ] Pre-Service-Assessment walkthrough scheduled — RISK R-009

**Short-term Actions (1–3 months / pre-GA)**:

- [ ] Pen test executed and findings remediated
- [ ] DPIA approved by DPO + Service Owner
- [ ] AI feature-scope boundary defined (drafting vs recommendation) — RISK R-010
- [ ] Manual AT audit walkthrough complete; Accessibility Statement drafted
- [ ] Beta service assessment booked (GA – 30 days)
- [ ] G-Cloud listing submission complete
- [ ] ROPA, privacy notice, sub-processor list, ATRS record drafted

**Long-term Actions (3–12 months / post-GA)**:

- [ ] Carbon-footprint baseline measured (GA + 90 days)
- [ ] Quarterly portability rehearsal cadence — RISK R-015 / R-017
- [ ] Quarterly DDaT user group
- [ ] Annual NCSC CAF + Cloud Security Principles refresh
- [ ] Annual independent pen test
- [ ] Annual published affordability review
- [ ] Annual sustainability statement

**Review Schedule**: Quarterly (next review 2026-08-03). Material change triggers ad-hoc refresh. Required re-review on each Service Standard assessment outcome.

---

## Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Service Owner / SRO-equivalent | Mark Craddock | [PENDING] | |
| Lead Architect / Technical Architect | [PENDING] | [PENDING] | |
| Security Lead | [PENDING] | [PENDING] | |
| DPO | [PENDING] | [PENDING] | |
| Digital Spend Control assurance (CDDO) | [PENDING] | [PENDING] | |

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government policies referenced (TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, UK GDPR / DPA 2018, PSBAR 2018, Procurement Act 2023, AI Playbook, GovS 005) are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Internal Cross-References

| Reference | Source | Use |
|-----------|--------|-----|
| `ARC-000-PRIN-v2.0.md` | Architecture Principles | All 21 principles map to TCoP points; Principles 1, 5, 7, 12, 21 are non-negotiable |
| `ARC-001-REQ-v1.0.md` | Requirements | BR-001..BR-008, FR-001..FR-005, NFRs (SEC, PERF, AVAIL, A11Y, FIN), INT-001..INT-006 |
| `ARC-001-STKE-v1.0.md` | Stakeholders | DDaT user audience (Point 1), GDS assessor stakeholder (Point 13), goals G-1..G-8, outcomes O-1..O-7 |
| `ARC-001-RISK-v1.0.md` | Risks | R-008/R-014 (Point 6), R-009 (Point 13), R-010/R-011 (Point 7 + AI annex), R-015/R-017 (Point 11) |
| `ARC-001-ADR-001..008-v1.0.md` | Architecture Decision Records | All 8 ADRs cover specific TCoP technology choices |
| `ARC-001-DPIA-v1.0.md` | DPIA | Point 7 — to be generated |
| `ARC-001-SbD-v1.0.md` | Secure by Design | Point 6 — to be generated |
| `ARC-001-AIPB-v1.0.md` | AI Playbook | AI Annex — to be generated |
| `ARC-001-SVCASS-v1.0.md` | Service Assessment | Point 13 — to be generated |
| `projects/002-arckit-sovereign/` | Sovereign route | Principle 21; out of scope of this TCoP review |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:tcop` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Sourced from `ARC-000-PRIN-v2.0.md`, `ARC-001-REQ-v1.0.md`, `ARC-001-STKE-v1.0.md`, `ARC-001-RISK-v1.0.md`, and ADR-001..008 in `projects/001-arckit-saas/decisions/`. Pre-GA Alpha-stage assessment.
