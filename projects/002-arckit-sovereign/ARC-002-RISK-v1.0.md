# ArcKit as a Service (Sovereign Deployment) — Risk Register

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-RISK-v1.0 |
| **Document Type** | Risk Register (HM Treasury Orange Book aligned) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) — until Sovereign Delivery Lead appointed |
| **Distribution** | ARB; MOD Defence Digital liaison; Customer SIROs (per engagement) |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation. Sovereign-route-specific risks; cross-references project 001 risks where shared. |

---

## 1. Approach

Same Orange Book approach and scoring scale as `projects/001-arckit-saas/ARC-001-RISK-v1.0.md` §1. Risk codes prefixed `SR-*` to disambiguate from project 001 `R-*`.

---

## 2. Top Sovereign Risks

| Code | Title | Category | Inherent | Residual | Owner |
|------|-------|----------|----------|----------|-------|
| SR-001 | Vendor signing-key compromise → tampered bundle reaches customer | Security / Supply chain | 2×5=10 | 1×5=5 | Vendor Security Lead |
| SR-002 | Codebase bifurcation: sovereign profile silently diverges from `main` | Strategic / Technology | 4×4=16 | 2×4=8 | Vendor Lead Architect |
| SR-003 | Within-deployment cross-project leak (sovereign single-tenant w/ project isolation) | Security | 3×4=12 | 1×4=4 | Vendor Security Lead |
| SR-004 | LTS patch SLA missed (Critical CVE not delivered in 7 days) | Compliance / Operational | 3×4=12 | 2×4=8 | LTS Engineering Lead |
| SR-005 | Customer accreditation slips → procurement stalls | Strategic | 3×4=12 | 2×3=6 | Sovereign Delivery Lead |
| SR-006 | Customer-side install fails to verify signature (operator error) | Operational | 3×3=9 | 2×3=6 | Sovereign Delivery Lead |
| SR-007 | Customer-approved AI endpoint exfiltrates prompt content | Security / Privacy | 2×4=8 | 1×4=4 | Customer (with vendor advisory) |
| SR-008 | On-prem GPU outage degrades AI feature in customer eyes | Operational / Reputation | 4×2=8 | 3×2=6 | Customer Operator |
| SR-009 | Sovereign unit economics fail (per-engagement cost exceeds revenue) | Financial | 3×3=9 | 2×3=6 | Service Owner |
| SR-010 | MOD policy / Secure by Design framework change | Compliance | 2×3=6 | 1×3=3 | Service Owner |
| SR-011 | Reference-customer slot delays (BR-008) | Strategic | 3×3=9 | 2×3=6 | Sovereign Delivery Lead |
| SR-012 | Air-gap install runbook gaps cause first-install delay | Operational | 4×3=12 | 2×3=6 | Sovereign Delivery Lead |
| SR-013 | Vendor remote support (INT-009) misconfigured → ad-hoc outbound channel | Security | 2×4=8 | 1×4=4 | Vendor Security Lead |
| SR-014 | Backup / restore at customer site fails when needed | Operational / Security | 3×4=12 | 2×4=8 | Customer + Vendor (advisory) |
| SR-015 | UK GDPR personal-data residue at decommission (FR-009; UC-3) | Compliance | 2×4=8 | 1×4=4 | Vendor + Customer DPO |
| SR-016 | Engineering effort drawn from SaaS to sovereign (cross-ref project 001 R-016) | Technology / People | 4×3=12 | 2×3=6 | Vendor Lead Architect |
| SR-017 | LTS branch security backports drift from `main` | Technology | 3×3=9 | 2×3=6 | LTS Engineering Lead |
| SR-018 | Cleared-personnel access mis-attestation (claim mapping) | Security / Compliance | 2×4=8 | 1×4=4 | Customer + Vendor (advisory) |
| SR-019 | Cyber-insurance for sovereign customer engagement unattainable | Financial | 3×3=9 | 2×3=6 | Service Owner |
| SR-020 | Cross-project (001) R-006 key-person dependency affects sovereign delivery | People | 4×4=16 | 3×4=12 | Vendor SLT |

(Cross-cutting risks shared with project 001 R-001 / R-005 / R-009 / R-013 / R-014 are referenced rather than duplicated.)

---

## 3. Detailed Risk Records (Sovereign-Specific)

### SR-001 — Vendor signing-key compromise

| Field | Value |
|-------|-------|
| **Description** | Vendor cosign key compromise allows an attacker to sign a tampered bundle that customer accepts. |
| **Mitigations** | HSM custody (ADR-001); dual control; key-rotation runbook (RB-09); revocation procedure; key continuity. |
| **Residual** | 1 × 5 = 5 |
| **Owner** | Vendor Security Lead |

### SR-002 — Codebase bifurcation

| Field | Value |
|-------|-------|
| **Description** | Sovereign-specific code drifts from `main` so that the sovereign profile becomes a fork in practice. |
| **Mitigations** | Single-codebase mandate (Principle 21); CI builds sovereign profile per release; ARB enforces; project 001 ADR-006 compatibility. |
| **Residual** | 2 × 4 = 8 (kept HIGH; reviewed monthly) |
| **Owner** | Vendor Lead Architect |

### SR-003 — Within-deployment cross-project leak

| Field | Value |
|-------|-------|
| **Description** | Sovereign single-tenant has internal isolation between projects / communities of interest (project 002 FR-006). A defect could allow cross-project access. |
| **Mitigations** | Same ADR-001 enforcement (project 001) — single-tenant with project-scoped row-level security; CI isolation suite covers project boundary too. |
| **Residual** | 1 × 4 = 4 |
| **Owner** | Vendor Security Lead |

### SR-004 — LTS patch SLA missed

| Field | Value |
|-------|-------|
| **Description** | Critical CVE not delivered to customer within published SLA. |
| **Mitigations** | LTS branch tooling (ADR-002); CI multi-baseline; on-call backport rota; customer comms. |
| **Residual** | 2 × 4 = 8 |
| **Owner** | LTS Engineering Lead |

### SR-005 — Customer accreditation slips

| Field | Value |
|-------|-------|
| **Description** | Customer-side accreditation (e.g., MOD Authority to Operate) takes longer than commercial plan accommodates. |
| **Mitigations** | Early customer engagement; provenance / SBOM evidence ready (ADR-001); MOD SbD doc; customer-facing INTEGRITY procedure. |
| **Residual** | 2 × 3 = 6 |
| **Owner** | Sovereign Delivery Lead |

### SR-006 — Customer install fails to verify signature

| Field | Value |
|-------|-------|
| **Description** | Customer operator skips or mis-runs verification step at install. |
| **Mitigations** | INTEGRITY runbook (ADR-001); install script gates verification; vendor support requires verification before troubleshooting. |
| **Residual** | 2 × 3 = 6 |
| **Owner** | Sovereign Delivery Lead |

### SR-012 — Air-gap install runbook gaps

| Field | Value |
|-------|-------|
| **Description** | First-install runbook missing edge cases delays go-live. |
| **Mitigations** | Pre-publish customer dry-run; runbook iterates per customer feedback; reference customer first (BR-008). |
| **Residual** | 2 × 3 = 6 |
| **Owner** | Sovereign Delivery Lead |

### SR-014 — Backup / restore at customer site fails

| Field | Value |
|-------|-------|
| **Description** | Customer's local backup/restore process (FR-003) fails during DR test or real incident. |
| **Mitigations** | Documented backup/restore runbook; quarterly DR rehearsal; vendor support advisory model. |
| **Residual** | 2 × 4 = 8 (kept HIGH until first DR rehearsal passes) |
| **Owner** | Customer Operator (vendor advisory) |

### SR-015 — UK GDPR personal-data residue at decommission

| Field | Value |
|-------|-------|
| **Description** | Decommission (UC-3) leaves residual personal data on customer media. |
| **Mitigations** | Decommission runbook; cryptographic erasure where supported; customer DPO sign-off. |
| **Residual** | 1 × 4 = 4 |
| **Owner** | Customer DPO + Vendor advisory |

### SR-020 — Key-person dependency affects sovereign delivery

| Field | Value |
|-------|-------|
| **Description** | Project 001 R-006 affects ability to staff sovereign engagements. |
| **Mitigations** | Sovereign Delivery Lead appointment; runbook coverage; succession plan. |
| **Residual** | 3 × 4 = 12 (kept HIGH; ARB-tracked) |
| **Owner** | Vendor SLT |

---

## 4. Risk Appetite (sovereign-specific)

- **Customer accreditation evidence integrity** — appetite **zero**.
- **Air-gap safety** — appetite **zero** for outbound calls in the default profile.
- **Codebase bifurcation** — appetite **very low**.
- **Engagement unit economics** — appetite **moderate** in initial year; tightens by year 2.

---

## 5. Governance

Same cadence as project 001 (monthly DRAFT/Alpha; quarterly Beta/Live; on-trigger always). Reports to ARB, Vendor SLT, and (per engagement) Customer SIRO.

---

## 6. Linked Artefacts

- Principles: `projects/000-global/ARC-000-PRIN-v2.0.md` (esp. 4, 5, 7, 21).
- Requirements: `ARC-002-REQ-v1.0.md`.
- Stakeholders: `ARC-002-STKE-v1.0.md`.
- ADRs: 001 (packaging), 002 (update), 003 (identity), 004 (AI).
- Cross-project: project 001 RISK (R-001 / R-006 / R-016 directly cross-relevant).

---

**Generated by**: ArcKit `/arckit:risk` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
