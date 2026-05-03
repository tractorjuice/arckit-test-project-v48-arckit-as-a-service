# ArcKit as a Service (Sovereign Deployment) — MOD Secure by Design Assessment

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:mod-secure`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-MODSEC-v1.0 |
| **Document Type** | MOD Secure by Design Assessment (CAAT-aligned) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock — until Sovereign Delivery Lead appointed |
| **Reviewed By** | [PENDING — Vendor Security Lead; Customer Accreditor] |
| **Approved By** | [PENDING — Customer SIRO; ARB] |
| **Distribution** | Customer Accreditor (SD-1); Customer SIRO (SD-2); Customer DSO (SD-3); MOD Defence Digital (SD-7); Vendor Security Lead |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial assessment. MOD Secure by Design (SbD) approach + Continuous Assurance + JSP 440 / JSP 604 alignment for sovereign deployments. |

---

## 1. Purpose

This document evidences ArcKit Sovereign Deployment alignment with **MOD Secure by Design**, the MOD-specific instantiation of the UK Government Secure by Design approach, with continuous assurance via the **Cyber Assurance Audit and Test (CAAT)** mindset and alignment with **JSP 440** (Defence Manual of Security and Resilience) and **JSP 604** (Defence Network Connection Authorisation).

The assessment is companion to:

- `ARC-002-RISK-v1.0.md` — sovereign risk register.
- ADRs 001 (packaging), 002 (update), 003 (identity), 004 (AI).
- Project 002 NFR-SEC-001 (MOD SbD / JSP 440 / JSP 604 alignment).

---

## 2. MOD SbD Outcomes — Conformance

### Outcome 1 — Risk understanding

**Status**: Compliant.

**Evidence**: `ARC-002-RISK-v1.0.md` Orange-Book aligned; SR-* set covers sovereign-specific risks; cross-references project 001 risks.

### Outcome 2 — Continuous risk management

**Status**: Compliant with Conditions.

**Evidence**: Quarterly review; pen-test cadence; LTS patch SLA. Per-engagement risk dialogue with customer SIRO.

**Gap**: Per-customer risk-appetite document.

**Action**: Per-engagement risk-appetite annex pre-install.

### Outcome 3 — Defence in depth

**Status**: Compliant.

**Evidence**: Same defence-in-depth as SaaS (ADR-001 layers); plus customer-controlled identity (ADR-003), customer-controlled KMS (INT-007), customer-controlled observability (INT-004), no outbound by default (NFR-SEC-004).

### Outcome 4 — Secure development

**Status**: Compliant.

**Evidence**: DevOps strategy (project 001) + ADR-001 packaging discipline; signed images; SBOM per release; SLSA L3+ provenance; CI isolation suite covers single-tenant config too.

### Outcome 5 — Supply-chain assurance

**Status**: Compliant.

**Evidence**: ADR-001 packaging — cosign signing, CycloneDX SBOM, SLSA provenance, INTEGRITY procedure for customer verification; sub-processor inventory (vendor side).

### Outcome 6 — Personnel security

**Status**: Compliant.

**Evidence**: Vendor BPSS vetting policy (project 001 SbD §2 Action); cleared-personnel attestation via customer IdP claim mapping (ADR-003); access logging in customer audit (FR-010).

### Outcome 7 — Physical security

**Status**: Customer-side. Vendor-side covered by office security policy.

### Outcome 8 — Logical security

**Status**: Compliant.

**Evidence**: Within-deployment isolation (FR-006 / NFR-SEC-006); encryption at rest (NFR-SEC-003); customer KMS (INT-007); identity (ADR-003).

### Outcome 9 — Detect and respond

**Status**: Compliant.

**Evidence**: Customer-controlled observability (INT-004); audit log (FR-010); incident-response runbook (sovereign instantiation of `/arckit:operationalize`).

### Outcome 10 — Recover

**Status**: Compliant with Conditions.

**Evidence**: Backup/restore runbook (FR-003); roll-back path (ADR-002); DR rehearsal cadence per customer.

**Gap**: First customer DR rehearsal pending.

**Action**: First DR rehearsal during reference-customer engagement (BR-008).

---

## 3. Continuous Assurance (CAAT-style)

| Cadence | Activity | Owner |
|---------|----------|-------|
| Per release | CI: signature; SBOM coverage; SLSA provenance; sovereign profile build + smoke | Engineering |
| Per release | Tenant_id (project) propagation lint; CI isolation suite | Engineering |
| Quarterly | Vendor pen test (rotating scope, sovereign profile) | Vendor Security Lead |
| Per engagement | Customer ITHC / acceptance test | Customer + Vendor |
| Annually | NCSC CAF-style self-assessment for sovereign profile | Vendor Security Lead |
| Annually | DR rehearsal at customer site | Customer Operator |
| Annually | LTS patch SLA review | LTS Engineering Lead |
| On trigger | Any signing-key event; any MOD policy update; any customer-side incident | Vendor Security Lead |

---

## 4. JSP 440 / 604 Alignment Summary

| JSP topic | ArcKit Sovereign approach |
|-----------|---------------------------|
| Information classification handling | Per project 002 NFR-C-001 — bundle integrity verifiable; OFFICIAL → SECRET capability subject to customer accreditation |
| Cryptography | Customer-supplied KMS (INT-007); cryptography appropriate to classification (NFR-SEC-003); FIPS / CESG-evaluated where customer mandates |
| Network connection authorisation | No outbound by default (NFR-SEC-004); customer-controlled egress where opted in (e.g., AI endpoint, ADR-004); JSP 604 evidence package supplied |
| Risk-managed exception | Documented per engagement; risk-appetite annex (§2 Outcome 2 action) |
| Personnel | Cleared-personnel attestation (ADR-003); vendor BPSS for any vendor-side access |

---

## 5. Threat Model (Sovereign-Specific)

```mermaid
flowchart LR
  C[Customer cleared user] --> ING[Customer-controlled ingress]
  ING --> APP[ArcKit application]
  APP --> CDB[(Customer DB)]
  APP --> COBJ[(Customer object store)]
  APP --> CKMS[Customer KMS]
  APP --> CIDP[Customer IdP]
  APP --> CAI[Customer-approved AI endpoint?]
  APP --> COBS[Customer observability]
  M[Vendor (rare; opt-in)] -. signed bundle .-> APP
  M -. opt-in remote support .-> APP
```

### STRIDE summary (sovereign deltas)

| Boundary | Sovereign-specific threat | Mitigation |
|----------|---------------------------|-----------|
| Vendor → Customer (bundle) | Tampered bundle | ADR-001 signing + INTEGRITY verification |
| Customer cleared user → App | Spoofed clearance attestation | ADR-003 default-deny on missing claim |
| App ↔ Customer KMS | Key misuse | Customer policy; audit log |
| App → Customer-approved AI | Prompt content exfiltration | Customer policy; vendor warns; audit logged |
| Vendor remote support (INT-009) | Out-of-band channel becomes ad-hoc backdoor | Strict policy; signed and logged; opt-in only |

---

## 6. Action Register

| ID | Action | Owner | Target |
|----|--------|-------|--------|
| M-1 | Per-engagement risk-appetite annex template | Sovereign Delivery Lead | Pre-first-install |
| M-2 | INTEGRITY verification gate in install runbook | Sovereign Delivery Lead | Pre-first-install |
| M-3 | First customer DR rehearsal | Customer Operator + Vendor advisory | First engagement |
| M-4 | LTS patch SLA published | LTS Engineering Lead | Pre-GA (project 002) |
| M-5 | JSP 604 evidence pack | Vendor Security Lead | Per engagement |
| M-6 | Customer-side audit-log integrity check | Vendor Security Lead | Pre-first-install |

---

## 7. Linked Artefacts

- Principles: `projects/000-global/ARC-000-PRIN-v2.0.md` (esp. 5, 7, 21).
- REQ, STKE, RISK (project 002).
- ADRs 001 / 002 / 003 / 004 (project 002).
- DPIA (`ARC-002-DPIA-v1.0.md`).
- Operational Readiness (`ARC-002-OPS-v1.0.md`).
- Cross-project: project 001 SbD; project 001 ADR set.

---

## 8. External References

- MOD Secure by Design: https://www.security.gov.uk/policy-and-guidance/secure-by-design/
- JSP 440 (overview): MOD internal — referenced via customer engagement
- JSP 604 (overview): MOD internal — referenced via customer engagement
- NCSC supply-chain security: https://www.ncsc.gov.uk/collection/supply-chain-security
- NCSC CAF: https://www.ncsc.gov.uk/collection/cyber-assessment-framework

---

**Generated by**: ArcKit `/arckit:mod-secure` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
