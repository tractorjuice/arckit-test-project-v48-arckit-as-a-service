# ArcKit as a Service (Managed SaaS) — Data Protection Impact Assessment (DPIA)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:dpia`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DPIA-v1.0 |
| **Document Type** | Data Protection Impact Assessment (UK GDPR Article 35) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Owner** | Data Protection Officer (PENDING — Service Owner is interim accountable owner) |
| **Reviewed By** | [PENDING — DPO; Security Lead] |
| **Approved By** | [PENDING — Service Owner; ARB] |
| **Distribution** | DPO, Security Lead, ARB, Buying-authority DPOs (on request), ICO (if engaged) |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial DPIA. Inputs: PRIN, REQ, STKE, RISK, ADRs 001–008. UK ICO DPIA template structure. |

---

## 1. Step 1 — Identify the need for a DPIA

A DPIA is required because ArcKit as a Service:

- Processes personal data of a large number of data subjects (tenant users — potentially thousands of UK Government and SME-supplier staff).
- Uses **AI-assisted generation** that processes prompt content which **may contain personal data** in tenant-generated artefacts (FR-004; ADR-004) — meets ICO criterion of "innovative use of technology".
- Operates a **multi-tenant** architecture where isolation failure would cause data leakage (NFR-SEC-002; ADR-001) — meets ICO criterion of "matching or combining datasets".
- Will process data of **tenant employees**, who under the contract are data subjects of the **tenant** (controller), with ArcKit as **processor** (UK GDPR Article 28).
- Provides services to **public-sector buying authorities** with public-interest obligations.

DPIA is therefore both a UK GDPR Article 35 obligation and an ICO best-practice expectation.

---

## 2. Step 2 — Describe the processing

### Nature of processing

ArcKit is a multi-tenant SaaS for enterprise architecture governance. Each tenant authors, edits, versions, exports, and shares architecture artefacts (Markdown documents, diagrams, structured metadata). Vendor-side processing comprises:

- Identity / authentication (per ADR-003).
- Storage and retrieval of tenant content (per ADR-002, ADR-006).
- AI-assisted generation of artefact drafts based on tenant prompts (per ADR-004).
- Audit logging and observability (per ADR-005).
- Billing for paid tiers (FR-011).

### Scope

**Data categories** (per data flow):

| Data category | Source | Location | Vendor role | Lawful basis (vendor as processor for tenant content; vendor as controller for service-account data) |
|---------------|--------|----------|-------------|-------------------------------------------------------------------------------------------------|
| Tenant user identity (name, email, organisation, role) | Tenant; IdP | UK region (ADR-002) | Processor for tenant; Controller for service-account record | Tenant lawful basis (typically legitimate interest / contract); vendor: contract performance |
| Tenant content (artefacts) | Tenant | UK region | Processor | Tenant lawful basis |
| Tenant content fed into AI prompts | Tenant | UK region; transmitted to AI provider (UK / EU / approved) | Processor | Tenant lawful basis; vendor processor under DPA |
| Audit log entries | Vendor system | UK region | Controller (security purposes) | Legitimate interest (Art 32 security obligation) |
| Billing data (paid tier) | Tenant admin | UK region; payment processor | Joint controller for billing | Contract performance |
| Sub-processor data flow (e.g., email send) | Vendor system | Sub-processor location (UK preferred) | Processor (delegated) | As above |

**Data subjects**: tenant employees (predominantly); tenant admin contacts; service operators (vendor staff); incident-response contacts.

**Volume**: at scale (NFR-S-001), ~5,000 tenants × ~10 average users = ~50,000 data subjects.

**Geography**: UK residency for storage and primary compute (Principle 7; ADR-002). Sub-processor flows may transit EU under IDTA / UK Adequacy (DPA detail).

### Context

- Tenants self-select to use the service; explicit Terms of Service plus per-tenant DPA accepted at onboarding (FR-001).
- Buying authorities have additional contractual frameworks (G-Cloud terms supersede some service ToS).
- Special-category data is **out of scope** by default; tenants are contractually prohibited from putting special-category personal data into artefacts (FR-002 onboarding warning; ToS clause).

### Purposes

- Deliver the contracted SaaS.
- Verify SME eligibility (BR-003; INT-003 — Companies House lookup of company registration data; not personal data of individuals beyond what Companies House publishes).
- Provide AI assistance (FR-004) consistent with tenant-set policy.
- Operate, secure, and audit the service (NFR-SEC, NFR-C-001/002).
- Bill paid-tier tenants.

---

## 3. Step 3 — Consultation

| Stakeholder | Consulted? | Method | Outcome |
|-------------|------------|--------|---------|
| ArcKit DPO (PENDING appointment) | [PENDING] | DPIA review | [PENDING] |
| Vendor Security Lead | Authoring input | Review of ADRs and risk register | Inputs incorporated |
| Pilot SME tenants | Planned | Pre-alpha consultation | [PENDING] |
| Pilot buying-authority DPOs | Planned | Pre-public-beta consultation | [PENDING] |
| ICO | Not required at this stage | — | Engagement only if high residual risk identified |

---

## 4. Step 4 — Necessity and proportionality

| Question | Answer |
|----------|--------|
| Is the processing **lawful**? | Yes — controller (tenant) sets lawful basis; vendor processes under Art 28 DPA. |
| Is it **fair**? | Yes — published terms; transparent sub-processor inventory; tenant-visible audit log (FR-012). |
| Is it **transparent**? | Yes — privacy notice; pricing page; sub-processor list; AI provenance metadata (ADR-004). |
| Is the data **adequate, relevant, limited**? | Yes — only data needed to operate the service; PII redaction in logs (ADR-005). |
| Is the data **accurate**? | Tenant-controlled; tenant has self-service edit / delete; UK GDPR Art 16 honoured. |
| Storage **limitation**? | Audit log retention policy (ADR-005); per-tenant retention overrides; offboarding deletion (FR-010). |
| **Integrity and confidentiality** (Art 32)? | ADR-001 isolation; ADR-002 encryption / KMS; ADR-005 audit; SbD assessment. |
| **Accountability**? | This DPIA; record of processing activities; sub-processor inventory; DPA. |

### Proportionality of AI processing (Article 22 / ICO AI guidance)

- AI generation is **assistive**, not automated decision-making (no Article 22 issue).
- Output is reviewed by a human before publication (ADR-004; R-009 mitigation).
- Provenance metadata makes AI involvement transparent.
- DPA with AI provider includes no-train default; tenant opt-in for data sharing for model improvement (off by default).

---

## 5. Step 5 — Identify and assess risks

### High-level risk view (residual)

| Risk | UK GDPR principle / harm | Likelihood | Severity | Residual after mitigations | Cross-ref |
|------|--------------------------|------------|----------|----------------------------|-----------|
| Cross-tenant content leak via isolation defect | Confidentiality (Art 5(1)(f), Art 32) | Low | High | Low × High = **Medium-Low** | RISK R-001; ADR-001 |
| AI prompt content visible to provider / persisted / used to train | Purpose limitation; processor obligations (Art 28); fairness | Low | Medium | Low × Medium = **Low** | ADR-004 (no-train default; UK/EU residency); annual DPA review |
| Sub-processor breach (hyperscaler / IdP / email) | Confidentiality | Low | High | Low × High = **Medium-Low** | Sub-processor inventory; DPA review; incident-notification clauses |
| Audit log tamper / unavailable | Accountability (Art 5(2)); breach detection | Low | Medium | **Low** | ADR-005 hash chain; integrity check monthly |
| Data subject rights (access / erasure) request not honoured in time | Art 12 timeline; rights | Low | Medium | **Low** | DSAR / erasure runbook in `/arckit:operationalize`; 30-day SLA |
| Personal data exposed in logs | Confidentiality | Medium | Medium | Low × Medium = **Low** | PII redaction filter (ADR-005); CI lint; weekly red-team scan |
| Cross-border transfer occurs without safeguard | Art 44 | Low | High | **Low** | UK-residency by default; sub-processor inventory enumerates any transfer + IDTA in place |
| Tenant uses service to process special-category data despite prohibition | Art 9 | Medium | Medium | Medium × Medium = **Medium** | ToS prohibition; UI warning; DPA requires tenant warranty |
| Operator account compromise leads to broad access | Confidentiality | Low | High | **Medium-Low** | ADR-003 hardware-key MFA; step-up; audit; session limits |
| AI-generated content presented as authoritative (Art 22-adjacent harm) | Fairness; Art 5(1)(d) accuracy | Medium | Medium | Low × Medium = **Low** | UI badging; human-in-the-loop; AI Playbook compliance |

No residual risk is currently assessed as **High**; therefore Article 36 prior consultation with the ICO is **not** triggered. This will be re-assessed if any residual increases to High at a future review.

---

## 6. Step 6 — Identify measures to reduce risk

### Technical measures

| Measure | Source / Cross-ref |
|---------|--------------------|
| Tenant_id propagation enforced default-deny | ADR-001; NFR-SEC-002 |
| CI isolation suite per change | ADR-001 |
| Encryption at rest (CMK on paid tier) and in transit (TLS 1.2+) | ADR-002; NFR-SEC-004 |
| Phishing-resistant operator MFA | ADR-003; NFR-SEC-001 |
| OIDC/SAML federation; no plaintext password handling for federated tenants | ADR-003 |
| AI: tenant_id propagation; no-train DPA; per-tenant prompt context | ADR-004 |
| Observability: PII redaction at source; tamper-evident audit log | ADR-005 |
| Per-tenant quotas / abuse prevention | ADR-008 |
| WAF + bot detection | ADR-006 |
| Backup / DR per RPO 15 min, RTO 4 h | NFR-A-002 |

### Organisational measures

| Measure | Source / Cross-ref |
|---------|--------------------|
| DPA with all sub-processors; annual review | NFR-C-001; SbD §5 |
| Sub-processor inventory published | TCoP §7 |
| BPSS vetting for production access | SbD Action 3 |
| Engineering training on tenant-context | ADR-001 §6 Neutral |
| Incident-response runbook with ICO 72-hour notification path | `/arckit:operationalize` |
| DSAR / erasure runbook with 30-day SLA | This DPIA action |
| Vulnerability disclosure programme | NFR-SEC-006 |
| Annual DPIA refresh | This document §7 |
| Pen testing quarterly | NFR-SEC-006 |

---

## 7. Step 7 — Sign off and record outcomes

| Decision | Status | Owner |
|----------|--------|-------|
| Residual risk acceptable to proceed to alpha | Pending DPO sign-off | DPO + Service Owner |
| ICO Article 36 prior consultation needed | No (no residual High risks identified) | DPO |
| DPIA review cadence | Annual + on material change | DPO |
| Sign-off | [PENDING — DPO appointment] | DPO |

### Action register (DPIA-specific)

| ID | Action | Owner | Target |
|----|--------|-------|--------|
| D1 | DPO appointed | Service Owner | Pre-alpha |
| D2 | DPIA APPROVED status | DPO | Pre-public-beta |
| D3 | Sub-processor inventory published | DPO | Pre-first-paid-tenant |
| D4 | DSAR / erasure runbook live | DPO + Engineering | Pre-public-beta |
| D5 | Pilot tenant DPA template ratified | DPO + Service Owner | Pre-alpha |
| D6 | ToS clause prohibiting special-category data live | Legal + Service Owner | Pre-alpha |
| D7 | First annual DPIA refresh | DPO | 2027-05-03 |

---

## 8. Linked Artefacts

- Principles: `projects/000-global/ARC-000-PRIN-v2.0.md` (esp. 7).
- Requirements: `ARC-001-REQ-v1.0.md` (esp. NFR-C-001, NFR-SEC-*, NFR-I-002).
- Risk: `ARC-001-RISK-v1.0.md` (R-001, R-005, R-009).
- ADRs: 001, 002, 003, 004, 005, 006, 007, 008.
- TCoP: `ARC-001-TCOP-v1.0.md` §7.
- Secure by Design: `ARC-001-SECURE-v1.0.md`.
- AI Playbook: `ARC-001-AIP-v1.0.md`.
- Operational Readiness: `ARC-001-OPS-v1.0.md` (DSAR / erasure runbooks).

---

## 9. External References

- ICO DPIA template: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-impact-assessments-dpias/
- ICO AI guidance: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/
- UK GDPR / DPA 2018: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/
- UK IDTA: https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/international-data-transfer-agreement-and-guidance/

---

**Generated by**: ArcKit `/arckit:dpia` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
