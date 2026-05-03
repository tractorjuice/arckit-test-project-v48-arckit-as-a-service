# ArcKit as a Service (Managed SaaS) — UK Government AI Playbook Conformance

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:ai-playbook`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-AIP-v1.0 |
| **Document Type** | UK Government AI Playbook Conformance Assessment |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) |
| **Reviewed By** | [PENDING — DPO; AI Ethics reviewer; ARB] |
| **Approved By** | [PENDING — Service Owner; ARB] |
| **Distribution** | ARB, DPO, ICO (on engagement), CDDO/CO AI assurance team, prospective public-sector buyers |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial assessment against UK Government AI Playbook (10 principles + delivery framework). Inputs: ADR-004, DPIA, RISK R-009/R-015. |

---

## 1. Purpose

This document evidences ArcKit as a Service (managed SaaS) conformance with the **UK Government AI Playbook**. It is required because the service uses AI generation as a core feature (FR-004, UC-2). It is paired with `ARC-001-DPIA-v1.0.md` (which addresses UK GDPR data protection) and `ARC-001-RISK-v1.0.md` (R-009 / R-015).

---

## 2. AI Use Description

**What ArcKit's AI does**: AI-assisted generation of artefact drafts (architecture documents, ADRs, diagrams, etc.) based on tenant prompts and the tenant's own existing artefacts.

**What it does not do**: Make decisions about people. There is no automated processing producing legal effects on individuals (UK GDPR Art 22). All AI output is **assistive** to a human author who reviews and approves before publication.

**Risk classification (current)**: **Limited risk** — assistive content generation; human-in-the-loop required for publication; no automated decision-making about people. ATRS (Algorithmic Transparency Recording Standard) is **not currently mandatory** under the published criteria; an ATRS skeleton is maintained and reassessed annually.

---

## 3. AI Playbook Principles — Conformance

### Principle 1 — You know what AI is and what its limitations are

**Status**: Compliant.

**Evidence**: ADR-004 explicitly characterises AI as assistive, not authoritative; UI badges AI-generated content; user training material describes hallucination risk; R-009 names hallucination risk and mitigations.

---

### Principle 2 — You use AI lawfully, ethically and responsibly

**Status**: Compliant with Conditions.

**Evidence**:

- **Lawful**: tenant lawful basis under their own UK GDPR posture; vendor processor obligations satisfied via DPA (DPIA §2).
- **Ethically**: no automated decision-making about people; transparent provenance metadata; human-in-the-loop required for publication.
- **Responsibly**: no-train DPA default (ADR-004); per-tenant AI budget caps (ADR-008); audit log of every generation (ADR-005).

**Gap**: AI Ethics reviewer not yet appointed (separately from DPO).

**Action**: AI Ethics reviewer named pre-public-beta.

---

### Principle 3 — You know how to use AI safely and securely

**Status**: Compliant.

**Evidence**:

- Tenant_id propagation through AIAdaptor (ADR-004).
- No cross-tenant prompt context (per-call tenant scoping).
- AI calls covered by CI isolation suite (ADR-001 / ADR-004).
- Provider DPA reviewed annually.
- AI provider sub-processor inventory disclosed.

---

### Principle 4 — You have meaningful human control at the right stages

**Status**: Compliant.

**Evidence**:

- Generated content is **draft** until a human reviews and approves for publication.
- UI badging makes AI involvement visible.
- Provenance metadata (ADR-004 §6) records model, version, timestamp.
- Tenant admin can disable AI generation per workspace.

---

### Principle 5 — You understand how to manage the AI lifecycle

**Status**: Compliant.

**Evidence**:

- Provider DPA reviewed annually (ADR-004).
- Golden-prompt regression suite detects model drift (ADR-004 / DevOps).
- Tier-aware default model selection (ADR-004); rotation handled via adaptor.
- Decommission path: AI feature degrades gracefully if no provider (ADR-004; project 002 NFR-A-003).

---

### Principle 6 — You use the right tool for the job

**Status**: Compliant.

**Evidence**: AI is one of multiple authoring paths (manual authoring per FR-003 always available); AI selected for the well-defined task of drafting structured artefacts from templates and existing tenant content; provider models chosen per tier capability needs.

---

### Principle 7 — You are open and collaborative

**Status**: Compliant with Conditions.

**Evidence**:

- AI Playbook conformance (this doc), DPIA, sub-processor inventory **published**.
- ArcKit core open-source.
- Generation provenance metadata machine-readable.

**Gap**: ATRS skeleton maintained but not published (current classification: not mandatory).

**Action**: Annual reassessment; publish ATRS the moment classification crosses the threshold.

---

### Principle 8 — You work with commercial colleagues from the start

**Status**: Compliant.

**Evidence**: AI provider DPA reviewed by DPO; commercial terms included in vendor sub-processor inventory; pricing model accounts for AI inference cost (FinOps).

---

### Principle 9 — You have the skills and expertise needed to implement and use AI

**Status**: Compliant with Conditions.

**Evidence**: Lead Architect appointment plan includes AI experience; pen test scope covers AI surface; AI Ethics reviewer to be named.

**Gap**: AI Ethics reviewer pending.

---

### Principle 10 — You use these principles alongside your organisation's policies

**Status**: Compliant.

**Evidence**: This document references and extends:

- Architecture principles (Principle 5 security, Principle 7 sovereignty, Principle 13/AI-ethics implicit).
- Tenant ToS prohibits putting special-category personal data into prompts (DPIA §4).
- Vendor employee policy (PENDING) covers AI prompt-content discipline for staff.

---

## 4. Cross-Cutting Controls Map

| Control | Source | Evidence |
|---------|--------|----------|
| No-train DPA default | ADR-004 | Provider DPA |
| Tenant_id propagation to AI | ADR-001 / ADR-004 | CI isolation suite |
| Per-tenant budget cap | ADR-004 / ADR-008 | Token-bucket; circuit breaker |
| Generation provenance metadata | ADR-004 §6 | Schema published |
| Human-in-the-loop required | ADR-004 / R-009 | UI gate |
| Audit log of every generation | ADR-005 | SIEM; tenant-visible (FR-012) |
| Annual reassessment | This doc | Cadence in §6 |
| ATRS skeleton maintained | This doc | Annual review |

---

## 5. Risks Specific to AI

| Risk | Mitigation | Cross-ref |
|------|-----------|-----------|
| Hallucinated content presented as authoritative | UI badging; human-in-the-loop gate; user training | R-009 |
| Prompt content leak between tenants | Per-tenant scoping; no shared embedding store v1; CI isolation | ADR-001/004 |
| Provider DPA / capability shift | Two-provider strategy; golden-prompt regression | R-004; ADR-004 |
| UK Gov AI Playbook reclassifies use | Annual reassessment; ATRS skeleton ready | R-015 |
| Bias in generated content reinforces inequities | Template-driven generation reduces free-form bias surface; user training | This doc §3 P1 |

---

## 6. Cadence

| Cadence | Activity | Owner |
|---------|----------|-------|
| Per release | Golden-prompt regression suite | Engineering |
| Per release | AI generation provenance correctness | Engineering |
| Quarterly | AI provider DPA review | DPO |
| Quarterly | Pen-test AI surface | Security Lead |
| Annually | AI Playbook conformance refresh (this doc) | Service Owner + AI Ethics |
| Annually | ATRS classification reassessment | Service Owner + AI Ethics |
| On trigger | Any AI Playbook update; any AI-incident; any provider model retirement | Service Owner |

---

## 7. Linked Artefacts

- ADR-004 (AI Provider Abstraction) — primary technical anchor.
- ADR-001, ADR-005, ADR-008 — supporting controls.
- DPIA (`ARC-001-DPIA-v1.0.md`).
- Risk Register (R-009, R-015, R-004).
- TCoP §14.

---

## 8. External References

- UK Government AI Playbook: https://www.gov.uk/government/publications/ai-playbook-for-the-uk-government
- Algorithmic Transparency Recording Standard: https://www.gov.uk/government/collections/algorithmic-transparency-recording-standard-hub
- ICO AI guidance: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/
- NCSC AI guidance: https://www.ncsc.gov.uk/collection/ai-and-cyber-security
- A pro-innovation approach to AI regulation (UK White Paper): https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach

---

**Generated by**: ArcKit `/arckit:ai-playbook` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
