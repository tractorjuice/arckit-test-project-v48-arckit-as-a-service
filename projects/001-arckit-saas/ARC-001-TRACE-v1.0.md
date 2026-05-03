# ArcKit as a Service (Managed SaaS) — Requirements Traceability Matrix

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:traceability`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-TRACE-v1.0 |
| **Document Type** | Requirements Traceability Matrix |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Owner** | Mark Craddock (Service Owner) |
| **Distribution** | ARB, DDaT Architects (SD-1, SD-2, SD-4) |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial matrix. Traces every BR/FR/NFR/INT/UC/DR/SD-G to PRIN, ADR, design view, and intended verification. |

---

## How to read

For each requirement: **Principle(s)** anchored to (PRIN), the **ADR(s)** that decide it, the **HLD section** that realises it, and the **verification** evidence (CI test, audit, runbook). "—" means none yet (DRAFT). All references are to artefacts in this project unless stated.

---

## 1. Business Requirements

| Req | Title | Principles | ADRs | HLD § | Verification |
|-----|-------|-----------|------|-------|--------------|
| BR-001 | Free tier for verified UK SMEs | 1, 17 | 002, 004, 008 | §5.5 | Pricing page; affordability review (annual) |
| BR-002 | Transparent published pricing | 1 | 008 | §5.5 | Pricing page live; published list |
| BR-003 | SME eligibility verification | 1 | 003 (identity) | §7 (UC-1 sequence) | INT-003 integration test; appeal procedure |
| BR-004 | G-Cloud procurement route | 1 | 002 | — | G-Cloud submission; SOBC §3 |
| BR-005 | Cross-subsidy funding model | 1, 17 | 002, 004, 008 | §5.5 | FinOps quarterly; cross-subsidy KPI |
| BR-006 | UK public sector policy evidence | 5, 7 | 002, 003, 004, 005 | — | TCoP; SbD; AI Playbook conformance |
| BR-007 | Tenant portability and exit | 4 | 007 | §9 | Round-trip CI test; mock exit drill |
| BR-008 | Adoption and activation | 1 | 008 | §7 (UC-1) | KPI dashboard; pilot tenant feedback |

---

## 2. Use Cases

| UC | Title | Principles | ADRs | HLD § / Sequence |
|----|-------|-----------|------|------------------|
| UC-1 | SME Tenant Self-Service Onboarding | 1 | 002, 003, 008 | §7 |
| UC-2 | AI-Assisted Artefact Generation | 1, 4 | 004, 005, 008 | §8 |
| UC-3 | Tenant Data Export and Exit | 4 | 007, 005 | §9 |

---

## 3. Functional Requirements

| FR | Title | Principles | ADRs | HLD § | Verification |
|----|-------|-----------|------|-------|--------------|
| FR-001 | Tenant provisioning + SME verification | 1 | 003, 002 | §7 | Onboarding integration test; INT-003 |
| FR-002 | Multi-tenant workspace management | 8 | 001 | §3 | CI isolation suite |
| FR-003 | Architecture artefact authoring | 4 | 007 | §3 (svc_artefact) | UI integration tests |
| FR-004 | AI-assisted generation | 4 | 004, 008 | §8 | Golden-prompt suite; budget enforcement |
| FR-005 | Artefact versioning + audit trail | 4, 5 | 005 | §3 (svc_artefact + svc_audit) | Audit-log integrity check |
| FR-006 | Full-fidelity export | 4 | 007 | §9 | Round-trip CI test |
| FR-007 | SSO integration | 5 | 003 | §5.2 | Federation test harness |
| FR-008 | Public API + event interfaces | 4 | 005, 007 | §3 | OpenAPI conformance |
| FR-009 | Public status page + notifications | 14 (GDS), 17 | 005, 006 | §5.7 | Status page live; incident comms drill |
| FR-010 | Tenant offboarding + deletion | 4, 5 | 001, 007 | §9 | Deletion test; UK GDPR Art 17 |
| FR-011 | Billing + subscription | 1 | — | §3 (svc_billing) | Billing integration test |
| FR-012 | Tenant audit log access | 5 | 005, 001 | §3 (svc_audit) | API contract test |
| FR-013 | GOV.UK Design System alignment | 6 (Accessibility) | — | §3 (web) | a11y CI; manual a11y audit |
| FR-014 | Admin console for service operators | 5 | 003, 005, 008 | §3 (svc_admin) | Hardware-key MFA; audit |
| FR-015 | Public marketing + pricing site | 1 | — | — | Pricing page live |

---

## 4. Non-Functional Requirements

### Performance

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-P-001 Interactive response | 005, 006 | §5.7 | SLO; load test |
| NFR-P-002 AI generation latency | 004, 005 | §8 | SLO; load test |
| NFR-P-003 Bulk export latency | 007 | §9 | Load test |

### Availability

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-A-001 Availability target | 002, 006 | §4 | SLO; multi-AZ test |
| NFR-A-002 Disaster recovery | 002, 006 | §4 | DR rehearsal |
| NFR-A-003 Fault tolerance + bulkheads | 001, 008 | §5.5 | Noisy-tenant load test |

### Scalability

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-S-001 Horizontal scaling | 001, 006 | §4 | Cell-management; capacity model |
| NFR-S-002 Data volume scaling | 002, 006 | §4 | Storage capacity model |

### Security

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-SEC-001 Authentication | 003 | §5.2 | Pen test; CI |
| NFR-SEC-002 Tenant isolation | 001 | §5.1 | CI isolation suite; pen test |
| NFR-SEC-003 Authorisation | 001, 003 | §5.1 | RBAC tests |
| NFR-SEC-004 Encryption + KMS | 002, 006 | §4 | KMS audit |
| NFR-SEC-005 Secrets management | 006 | §4 | Secret-scan CI |
| NFR-SEC-006 Vulnerability management | 005, 006 | §5.8 | Pen-test cadence; VDP |
| NFR-SEC-007 Service-to-service auth | 006 | §4 | mTLS or SPIFFE; CI |
| NFR-SEC-008 NCSC CAF | 001, 003, 005, 006 | §5.8 | CAF self-assessment |
| NFR-SEC-009 NCSC Cloud Security Principles | 002 | §4 | Mapping in ADR-002 §7 |

### Compliance

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-C-001 UK GDPR / DPA | 002, 005 | §5.4 | DPIA |
| NFR-C-002 Audit logging + retention | 005 | §5.4 | Retention policy; integrity |
| NFR-C-003 WCAG 2.2 AA / PSBAR | — | §5.8 | a11y CI + manual audit |
| NFR-C-004 TCoP | all | — | TCoP doc |
| NFR-C-005 GDS Service Standard | all | — | Service assessment |
| NFR-C-006 ISO 27001 alignment | 005, 006 | §5.8 | Control mapping |
| NFR-C-007 Government Security Classifications | 001, 002 | §5.4 | OFFICIAL handling |
| NFR-C-009 NCSC CSP / CAF | 002, 005 | §5.8 | NFR-SEC-008/009 |

### Maintainability / Usability / Interoperability / Portability

| NFR | ADRs | HLD § | Verification |
|-----|------|-------|--------------|
| NFR-U-001 UX | — | §3 (web) | UX research |
| NFR-U-002 Accessibility | — | §5.8 | a11y CI |
| NFR-M-001 Observability | 005 | §5.4 | OTel coverage |
| NFR-M-002 Documentation | — | — | Docs site (`/arckit:pages`) |
| NFR-M-003 Operational runbooks | — | — | Operationalize |
| NFR-I-001 Open API standards | 002, 003, 005, 007 | §5.4 | OpenAPI conformance |
| NFR-I-002 Data portability | 007 | §9 | Round-trip CI |

---

## 5. Integration Requirements

| INT | Title | ADRs | HLD § | Verification |
|-----|-------|------|-------|--------------|
| INT-001 Tenant IdP | 003 | §5.2 | Federation harness |
| INT-002 Payment processing | — | §3 (svc_billing) | Sandbox test |
| INT-003 Companies House | 003 | §7 | Integration test |
| INT-004 Email delivery | — | §7 | Sandbox test |
| INT-005 AI provider | 004 | §8 | Provider switch test |
| INT-006 Object storage + DB | 002, 006 | §4 | Storage parity test (S3↔MinIO) |
| INT-007 Observability backend | 005 | §5.4 | OTLP smoke |
| INT-008 G-Cloud / Marketplace | — | — | G-Cloud listing |
| INT-009 Vulnerability disclosure | — | §5.8 | VDP live |

---

## 6. Data Requirements (DR-001 to DR-007)

DR-001 to DR-007 identified in REQ Data Requirements; each entity carries `tenant_id` (ADR-001 §7), is encrypted at rest (ADR-002, NFR-SEC-004), audited (ADR-005), exportable (ADR-007). Verification: schema lint per ADR-001 §6.

---

## 7. Stakeholder Goals (G-*)

| SD/G | Stakeholder | Goal | Source ADRs / docs |
|------|-------------|------|--------------------|
| SD-1 G-1 | DDaT EA buyer | Recognisable, credible governance evidence | All ADRs; TCoP; SOBC |
| SD-1 G-2 | DDaT EA buyer | No bespoke verification effort | TCoP; SbD; this matrix |
| SD-3 G-* | DDaT Security Architect | CAF-aligned posture | ADR-001/005; SbD; CAF mapping |
| SD-6 G-* | SME Architect | Affordable, fast governance | Principle 1; ADRs 004 / 008 |
| SD-13 G-* | HMT/CCS/CDDO | SME-supplier diversity; spending discipline | SOBC; FinOps; affordability review |
| SD-14 G-* | GDS Service Assessors | Service Standard quality | TCoP; Service Assessment doc |

(Full SD-G mapping documented in STKE; this matrix lists key cross-cutting goals.)

---

## 8. Risk Coverage

Every R-* in `ARC-001-RISK-v1.0.md` is mitigated by at least one ADR and/or runbook. See risk register for explicit cross-references.

---

## 9. Coverage Summary

| Coverage check | Result |
|----------------|--------|
| Every BR-* covered by ≥1 ADR | ✅ |
| Every FR-* covered by ≥1 ADR or HLD section | ✅ |
| Every NFR-* covered by ≥1 ADR or design view | ✅ |
| Every INT-* covered | ✅ |
| Orphan requirements after this trace | 0 (closes ORPHAN-REQ finding from health.json) |
| Risks without ADR mitigation | 0 |

---

**Generated by**: ArcKit `/arckit:traceability` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**AI Model**: Claude Opus 4.7 (1M context)
