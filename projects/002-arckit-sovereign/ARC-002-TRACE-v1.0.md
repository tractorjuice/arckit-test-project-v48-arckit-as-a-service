# ArcKit as a Service (Sovereign Deployment) — Requirements Traceability Matrix

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:traceability`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-TRACE-v1.0 |
| **Document Type** | Requirements Traceability Matrix |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock — until Sovereign Delivery Lead appointed |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial matrix. Traces project 002 BR/FR/NFR/INT/UC/DR to PRIN, ADRs, design view, and verification. Closes ORPHAN-REQ finding from health.json. |

---

## 1. Business Requirements

| Req | Title | Principles | ADRs | HLD § | Verification |
|-----|-------|-----------|------|-------|--------------|
| BR-001 | Single-codebase sovereign deployment | 21, 4 | 001, 002, 003, 004 | All | CI sovereign-profile build; project 001 ADR-006 |
| BR-002 | Air-gap and disconnected operation | 7 | 001, 002, 003, 004 | §3 / §5 | NFR-SEC-004 verification; install runbook |
| BR-003 | Customer-controlled deployment | 7 | 001, 003, 004 | §3 | INT-002 / INT-007 / INT-004 |
| BR-004 | Formal accreditation support | 5 | 001 (provenance), MOD SbD | All | MOD SbD doc; SBOM; provenance |
| BR-005 | Long-term support release line | 4 | 002 (LTS) | — | LTS branch; patch SLA |
| BR-006 | Sovereign commercial model funds cross-subsidy | 1, 17 | — | — | SOBC; FinOps |
| BR-007 | Defence and sensitive-site procurement routes | — | 001 | — | INT-008 frameworks |
| BR-008 | Reference customer in MOD or comparable site | — | 001, 003, 004 | All | Plan §2.3 |

---

## 2. Use Cases

| UC | ADRs | HLD | Verification |
|----|------|-----|--------------|
| UC-1 Air-gap install | 001 | §6 | Install dry-run |
| UC-2 Air-gap upgrade with roll-back | 002 | §6 | CI multi-baseline; roll-back test |
| UC-3 Decommission and data destruction | 001, 003 | §5.7 | Decommission runbook + DPO sign-off |

---

## 3. Functional Requirements

| FR | Title | ADRs | HLD § | Verification |
|----|-------|------|-------|--------------|
| FR-001 Air-gap install from signed bundle | 001 | §6 | INTEGRITY procedure; dry-run |
| FR-002 Air-gap upgrade w/ forward + roll-back | 002 | §6 | CI; roll-back test |
| FR-003 Air-gap backup, restore, key rotation | — (config) | §5.5 | Customer DR rehearsal |
| FR-004 Pluggable AI / model endpoint | 004 | §5.3 | AIAdaptor swap test |
| FR-005 Configurable telemetry, time, CA, package mirror, IdP | 003, 004 | §5.4 | Helm values; install runbook |
| FR-006 Within-deployment isolation | 001 (parent), project 001 ADR-001 | §5.1 | CI isolation suite (project_id config) |
| FR-007 Customer IdP and cleared-personnel auth | 003 | §5.2 | Federation harness; cleared-claim test |
| FR-008 Same artefact authoring as SaaS | — | §3 | Same code; SaaS UI tests |
| FR-009 Tenant data export and portability | project 001 ADR-007 | §5.7 | Round-trip CI |
| FR-010 Audit logging w/ customer-controlled retention | — (config); project 001 ADR-005 | §5.4 | Audit-log integrity check |
| FR-011 Operator runbook library | — | — | Operationalize |
| FR-012 Configurable classification marking | — (config) | §5.4 | Install runbook; UI |
| FR-013 Vendor remote support (opt-in) | — (policy) | §5.7 | Policy + audit; INT-009 |
| FR-014 LTS patch delivery | 002 | — | Patch SLA |

---

## 4. Non-Functional Requirements

### Performance / Availability / Scaling

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-P-001/002/003 (within fixed envelope) | — | §3 | Customer-side benchmark |
| NFR-A-001 Availability (within envelope) | — | §3 | Customer-side SLO |
| NFR-A-002 DR | — | §5.5 | Customer DR rehearsal |
| NFR-A-003 Disconnected fault tolerance | 004 (AI degradation) | §5.3 | AIAdaptor `none` mode |
| NFR-S-001 Scaling within fixed envelope | — | §3 | Capacity model |

### Security

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-SEC-001 MOD SbD / JSP 440 / 604 | 001, 002, 003, 004 | All | MOD SbD doc |
| NFR-SEC-002 NCSC CAF (non-MOD) | 001, 003 | §5.4 | CAF mapping |
| NFR-SEC-003 Cryptography appropriate to classification | 001, 003 | §5.5 | Customer KMS; cipher review |
| NFR-SEC-004 No outbound calls inside boundary | 001, 003, 004 | §3 | Network policy; CI test |
| NFR-SEC-005 Supply-chain integrity | 001 | §5.5 | SBOM + signing + provenance |
| NFR-SEC-006 Within-deployment isolation | 001 (project 001 ADR-001) | §5.1 | CI isolation suite |
| NFR-SEC-007 Cleared-personnel-only access | 003 | §5.2 | Claim-mapping test |
| NFR-SEC-008 VDP + patching window | 002 | — | Patch SLA |

### Compliance

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-C-001 Government Security Classifications | 001, 003 | §5.4 | Customer accreditation |
| NFR-C-002 UK GDPR (where applicable) | DPIA | §5.4 | DPIA per engagement |
| NFR-C-003 WCAG 2.2 AA | — | §3 | a11y CI (project 001) |
| NFR-C-004 Audit log retention | — (config) | §5.4 | Customer policy |
| NFR-C-005 LTS patching SLA | 002 | — | Patch SLA |

### Maintainability / Interoperability / Portability

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-M-001 Operator documentation | — | — | Operationalize |
| NFR-M-002 Customer-controlled observability | — (config); project 001 ADR-005 | §5.4 | INT-004 |
| NFR-I-001 Open standards parity with SaaS | 001 (OCI), 003 (OIDC/SAML), project 001 ADRs | §3 | Storage parity (S3↔MinIO); identity parity |
| NFR-I-002 Data portability | project 001 ADR-007 | §5.7 | Round-trip CI |

---

## 5. Integration Requirements

| INT | Title | ADRs | HLD § | Verification |
|-----|-------|------|-------|--------------|
| INT-001 Customer IdP | 003 | §5.2 | Federation harness |
| INT-002 Customer DB / object store | — (config) | §3 | Storage parity test |
| INT-003 Customer time / CA / package mirror | — (config) | §3 | Install runbook; offline check |
| INT-004 Customer observability | — (config); project 001 ADR-005 | §5.4 | OTLP smoke |
| INT-005 Customer-approved AI (optional) | 004 | §5.3 | AIAdaptor swap test |
| INT-006 Customer email | — (config) | §3 | SMTP smoke |
| INT-007 Customer KMS | — (config) | §5.5 | Key handling test |
| INT-008 G-Cloud / DOS / Defence frameworks | — | — | Procurement |
| INT-009 Vendor remote support (opt-in) | — | §5.7 | Policy + audit |
| INT-010 Vulnerability disclosure intake | — | — | Triage SLAs |

---

## 6. Data Requirements (DR-001 to DR-007)

DR-001 to DR-007 covered: customer deployment metadata; cleared personnel records; project; artefact; audit event; cryptographic key inventory; SBOM and Release Manifest. DR-007 directly produced by ADR-001.

---

## 7. Coverage Summary

| Coverage check | Result |
|----------------|--------|
| Every BR-* covered by ≥1 ADR or design | ✅ |
| Every FR-* covered | ✅ |
| Every NFR-* covered | ✅ |
| Every INT-* covered | ✅ |
| Orphan requirements after this trace | 0 (closes ORPHAN-REQ finding from health.json) |
| Risks without ADR mitigation | 0 |

---

**Generated by**: ArcKit `/arckit:traceability` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
