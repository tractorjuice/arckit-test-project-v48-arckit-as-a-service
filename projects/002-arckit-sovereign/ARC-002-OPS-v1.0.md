# ArcKit as a Service (Sovereign Deployment) — Operational Readiness Pack

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:operationalize`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-OPS-v1.0 |
| **Document Type** | Operational Readiness Pack (Sovereign — vendor-side + customer-side) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock — until Sovereign Delivery Lead appointed |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial sovereign ops pack. Vendor-side delivery model; customer-side runbook library; LTS support model. |

---

## 1. Two-Sided Service Model

Sovereign ops splits into two sides:

- **Vendor-side**: build the bundle, sign, deliver, support LTS, remote support (opt-in).
- **Customer-side**: install, operate, monitor, back up, patch, decommission.

The boundary is the **customer trust boundary**: vendor never reaches inside without explicit customer-controlled (signed, logged, time-limited) opt-in via INT-009.

---

## 2. Vendor-Side RACI

| Domain | A | R | C | I |
|--------|---|---|---|---|
| Bundle build + signing | Vendor Security Lead | Engineering | Lead Architect | ARB |
| Bundle distribution | Sovereign Delivery Lead | — | Customer | — |
| LTS patch development | LTS Engineering Lead | Engineering | Security | Customers |
| Vendor remote support session (opt-in) | Sovereign Delivery Lead | Engineering / Security | Customer | DPO |
| Vulnerability disclosure intake | Vendor Security Lead | Security | Engineering | Customers |

## 3. Customer-Side RACI (per engagement)

| Domain | A | R | C | I |
|--------|---|---|---|---|
| Install | Customer Operator | — | Sovereign Delivery Lead (advisory) | Customer SIRO |
| Day-2 operations | Customer Operator | — | Vendor (advisory) | Customer SIRO |
| Backup / DR | Customer Operator | — | Vendor (advisory) | Customer SIRO |
| Patching | Customer Operator | — | LTS Engineering Lead (advisory) | Customer SIRO |
| Decommission | Customer Operator + Customer DPO | — | Vendor (advisory) | Customer SIRO |

---

## 4. Sovereign Runbook Library (customer-side)

| Runbook | Purpose | Owner | Cadence |
|---------|---------|-------|---------|
| RB-S01 INTEGRITY procedure | Verify signed bundle on receipt | Customer Operator | Per delivery |
| RB-S02 Air-gap install | UC-1 / FR-001 | Customer Operator | Per install |
| RB-S03 Configuration: IdP claim mapping | ADR-003 | Customer Operator | Install + change |
| RB-S04 Configuration: KMS / observability / time / CA | FR-005 | Customer Operator | Install + change |
| RB-S05 Configuration: AI provider (opt-in) | ADR-004 | Customer Operator | Install + change |
| RB-S06 Patch apply (LTS) | UC-2 / FR-002 / FR-014 | Customer Operator | Per patch |
| RB-S07 Patch roll-back | FR-002 | Customer Operator | Per failed patch |
| RB-S08 Backup / restore | FR-003 | Customer Operator | Daily backup; quarterly restore test |
| RB-S09 Cross-AZ / single-host failure | NFR-A-003 | Customer Operator | Per event; rehearsal annual |
| RB-S10 KMS key rotation | NFR-SEC-003 | Customer Operator | Per customer policy |
| RB-S11 Cleared-personnel role grant / revoke | NFR-SEC-007 | Customer Operator | Per change |
| RB-S12 Audit log integrity check | FR-010 | Customer Operator | Monthly |
| RB-S13 Vendor remote support session (opt-in) | INT-009 | Customer Operator + Vendor | Per request |
| RB-S14 Vulnerability disclosure handling | INT-010 | Vendor Security + Customer | Per disclosure |
| RB-S15 Decommission and erasure | UC-3 / FR-009 / FR-010 | Customer Operator + DPO | Per decommission |
| RB-S16 Annual customer DR rehearsal | NFR-A-002 | Customer Operator | Annual |

---

## 5. Vendor-Side Runbooks

| Runbook | Purpose | Owner |
|---------|---------|-------|
| RB-V01 Bundle build + sign + ship | Per release | Engineering + Security |
| RB-V02 HSM key ceremony | Initial; rotation | Security |
| RB-V03 LTS backport | Per CVE / patch | LTS Engineering Lead |
| RB-V04 Customer engagement intake | Pre-install | Sovereign Delivery Lead |
| RB-V05 Vendor remote support invocation | Opt-in only; signed; logged | Sovereign Delivery Lead + Security |
| RB-V06 Signing-key compromise response | Per SR-001 | Vendor Security Lead |

---

## 6. SLAs

| SLA | Target |
|-----|--------|
| LTS patch (Critical CVE) delivery | ≤ 7 days from public disclosure |
| LTS patch (High) delivery | ≤ 30 days |
| LTS patch (Medium) delivery | ≤ 90 days |
| Customer support response (working hours) | ≤ 1 business day |
| Vendor remote-support session approval | ≤ 1 business day; only with customer-signed request |

---

## 7. Communications and Reporting

- **Per release**: release notes; manifest; SBOM; provenance; security-relevant change list.
- **Per CVE**: vulnerability advisory + patch availability ETA.
- **Quarterly**: customer touchpoint (LTS health, upcoming releases, advisory items).
- **Per customer**: incident comms via customer-defined channel.

---

## 8. Linked Artefacts

- ADRs 001 / 002 / 003 / 004 (project 002).
- REQ, STKE, RISK, MOD-SbD, DPIA, SOBC, Plan, HLD (project 002).
- Project 001 Operationalize (parent).

---

**Generated by**: ArcKit `/arckit:operationalize` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
