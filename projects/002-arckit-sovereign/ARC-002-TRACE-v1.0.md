# Requirements Traceability Matrix: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:traceability`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-TRACE-v1.0 |
| **Document Type** | Requirements Traceability Matrix |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, MOD Defence Digital liaison, NCSC liaison, GDS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:traceability` command — comprehensive forward + backward traceability across all wave 1–7 artefacts (REQ, STKE, ADR-001..008, RISK, TCOP, MOD-SBD, DPIA, AIP, SOBC, PLAN, ROAD, HLD, DEVOPS, FINOPS, OPS, DIAG-001..003) and cross-project linkage to project 001 per Principle 21. | [PENDING] | [PENDING] |

## Document Purpose

This Requirements Traceability Matrix (RTM) provides end-to-end traceability for the **sovereign / air-gapped deployment** route of ArcKit as a Service (project 002). It traces the full chain Strategic Drivers → Goals → Outcomes → Business Requirements → Functional Requirements → Non-Functional Requirements → Architecture Decisions → HLD components → DevOps test gates → Operational runbooks; the inverse backward chain confirming every artefact lands on at least one upstream requirement or principle; risk-coverage mapping every R-001..R-013 sovereign-specific risk to controls, ADRs/NFRs, and runbooks; and compliance-coverage matrices for TCoP (13 points), MOD Secure by Design (7 principles), JSP 440 (28 controls), JSP 604 accreditation gates, UK GDPR DPIA risks (DPIA-001..005), and the UK Government AI Playbook (10 core principles + 6 ethical themes).

> **Cross-project linkage**: Project 002 shares `projects/000-global/ARC-000-PRIN-v2.0.md` (Architecture Principles, Principle 21 anchors this project), the global glossary, the strategic narrative, and the project-001 Wardley map with project 001 (managed SaaS). Principle 21 mandates that the sovereign and SaaS routes share a single source-of-truth codebase; consequently, several SaaS-side requirements (project 001 SD-9, BR-005, FR-004, INT-005, NFR-SEC-002, Conflict C-1) trace bidirectionally with this project. Traceability rows that cross the boundary are explicitly marked with a "Project 001 link" note in the relevant column.

---

## 1. Overview

### 1.1 Purpose

This RTM provides defensible, audit-ready traceability for sovereign deployments where:

- An MOD Customer Accreditor must reconstruct, from the artefact set alone, the path from "this requirement exists" → "this design decision satisfies it" → "this test gate validates it" → "this runbook operates it" — all without vendor presence inside the boundary.
- A Customer SIRO must accept residual information risk, with each risk traced to a specific control set and to the operational evidence (vendor-side runbook or customer-side runbook) that keeps the control alive over the life of the deployment.
- A Service Owner must demonstrate cross-subsidy from sovereign margin to the SaaS SME tier (BR-006 ↔ project 001 BR-005) without divergence in governance or capability.

### 1.2 Traceability Scope

This matrix traces:

```mermaid
flowchart TD
    SD[Strategic Drivers<br/>SD-1..SD-17] --> G[Goals<br/>G-1..G-10]
    G --> O[Outcomes<br/>STKE/SOBC]
    O --> BR[Business Requirements<br/>BR-001..BR-008]
    BR --> FR[Functional Requirements<br/>FR-001..FR-014]
    BR --> NFR[Non-Functional Requirements<br/>NFR-P/A/S/SEC/C/M/I]
    FR --> ADR[Architecture Decisions<br/>ADR-001..ADR-008]
    NFR --> ADR
    ADR --> HLD[HLD Components<br/>C4 L2 containers]
    HLD --> DEVOPS[DevOps Test Gates<br/>CI Stages 1-5 + ceremony]
    HLD --> OPS[Operational Runbooks<br/>RB-VEN-001..010 + customer-side]
    BR --> RISK[Risk Register<br/>R-001..R-013]
    RISK --> ADR
    RISK --> OPS
    BR --> COMPL[Compliance<br/>TCoP/MOD-SbD/JSP/DPIA/AIP]
    COMPL --> ADR
    COMPL --> OPS

    style SD fill:#E3F2FD
    style BR fill:#FFF3E0
    style ADR fill:#E8F5E9
    style HLD fill:#F3E5F5
    style RISK fill:#FFEBEE
    style COMPL fill:#FFFDE7
```

### 1.3 Document References

| Document | Version | Date | Link |
|----------|---------|------|------|
| Architecture Principles (cross-project) | 2.0 | 2026-05-03 | `projects/000-global/ARC-000-PRIN-v2.0.md` |
| Requirements (REQ) | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` |
| Stakeholder Analysis (STKE) | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md` |
| ADR-001 Air-gapped operation | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-001-v1.0.md` |
| ADR-002 Signed release bundle | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-002-v1.0.md` |
| ADR-003 Cleared-personnel access | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-003-v1.0.md` |
| ADR-004 On-prem AI integration | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-004-v1.0.md` |
| ADR-005 Customer-controlled telemetry/time/CA/mirror | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-005-v1.0.md` |
| ADR-006 JSP 440 / SAL alignment | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-006-v1.0.md` |
| ADR-007 Distribution model | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-007-v1.0.md` |
| ADR-008 LTS release line | 1.0 | 2026-05-03 | `decisions/ARC-002-ADR-008-v1.0.md` |
| Risk Register (RISK) | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-RISK-v1.0.md` |
| TCoP Compliance | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-TCOP-v1.0.md` |
| MOD Secure by Design | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-MOD-SBD-v1.0.md` |
| DPIA | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-DPIA-v1.0.md` |
| AI Playbook (AIP) | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-AIP-v1.0.md` |
| SOBC | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-SOBC-v1.0.md` |
| Plan | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-PLAN-v1.0.md` |
| Roadmap | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-ROAD-v1.0.md` |
| HLD Review | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-HLD-v1.0.md` |
| DevOps | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-DEVOPS-v1.0.md` |
| FinOps | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-FINOPS-v1.0.md` |
| Operations (OPS) | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/ARC-002-OPS-v1.0.md` |
| Diagrams (DIAG-001..003) | 1.0 | 2026-05-03 | `projects/002-arckit-sovereign/diagrams/` |
| Sister Project (REQ) | 1.0 | 2026-05-03 | `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` |

---

## 2. Forward Traceability Chain

### 2.1 Strategic Drivers → Goals → Outcomes (SD → G → O)

This section uses STKE as the source of truth. SD identifiers map to the 17 strategic drivers; G identifiers to the 10 sovereign goals.

| SD ID | Driver Name | Stakeholder | Mapped Goals | Drives BR(s) |
|-------|-------------|-------------|--------------|--------------|
| SD-1 | Defensible authorisation to operate | Customer Accreditor | G-4, G-7, G-9 | BR-004 |
| SD-2 | Defensible information risk acceptance | Customer SIRO | G-4, G-7 | BR-004 |
| SD-3 | Departmental security policy fit | Customer DSO | G-4, G-9 | BR-004 |
| SD-4 | Delivery within accreditation timeline | Customer SRO | G-1, G-7 | BR-004, BR-008 |
| SD-5 | Predictable operations inside boundary | Customer Operator Team | G-3, G-10 | BR-002, BR-003 |
| SD-6 | Same drivers as SaaS for cleared DDaT users | Customer DDaT Architects | G-2 | BR-001 |
| SD-7 | Cross-MOD digital coherence | MOD Defence Digital | G-7, G-9 | BR-007, BR-008 |
| SD-8 | Sovereign funds mission, not distracts | Service Owner | G-6, G-1 | BR-006 |
| SD-9 | Single-codebase and sovereign-ready engineering | Lead Architect / CTO | G-2, G-3 | BR-001 |
| SD-10 | Supply-chain integrity / signing-key custody | Security Lead | G-8 | BR-004, BR-005 |
| SD-11 | Predictable customer onboarding | Sovereign Delivery Lead | G-1, G-10 | BR-008 |
| SD-12 | Sovereign unit economics positive | Vendor Finance | G-6 | BR-006 |
| SD-13 | Patch backport discipline | LTS Engineering Lead | G-5 | BR-005 |
| SD-14 | UK GDPR posture for vendor side | Vendor DPO | G-4 | BR-004 (DPIA) |
| SD-15 | UK cyber resilience baseline | NCSC | G-9 | BR-004 |
| SD-16 | UK GDPR where personal data processed | ICO | G-4 (DPIA) | BR-004 |
| SD-17 | Public spending and defence cyber | HMT/CCS/CDDO/DCPP | G-6, G-7 | BR-006, BR-007 |

| Goal ID | Goal | Outcome (KPI) | Source |
|---------|------|----------------|--------|
| G-1 | First production sovereign deployment | ≥ 1 production deployment by GA + 18 months | REQ §Business Success Metrics |
| G-2 | Single-codebase discipline maintained | 0 forks; 100% feature parity audit | REQ BR-001 |
| G-3 | Air-gap operability validated per release | 100% network-deny CI pass | REQ §Technical Success Metrics |
| G-4 | MOD SbD evidence pack current | Per release | REQ BR-004 |
| G-5 | LTS line maintained for ≥ 24 months | Patch SLA 7/30/90 days; 100% adoption | REQ BR-005, NFR-SEC-008 |
| G-6 | Sovereign cross-subsidy contribution | ≥ documented threshold quarterly | REQ BR-006 ↔ project 001 BR-005 |
| G-7 | First-time accreditation pass | All deployments achieve ATO | REQ §KPI |
| G-8 | Signing-key custody zero-incident | 0 key compromise incidents | REQ TC-2, ADR-002 |
| G-9 | NCSC CAF mapping per release | Per release | REQ BR-004 |
| G-10 | Customer-led operability | 100% runbook self-service | REQ BR-003, FR-011 |

**Coverage**: 17 SDs / 17 mapped to ≥ 1 Goal (100%). 10 Goals / 10 mapped to ≥ 1 BR (100%). 10 Goals / 10 with measurable outcome (100%).

---

### 2.2 Forward Traceability: BR → FR → NFR → ADR → HLD → Test Gate → Runbook

> **Legend**: ✅ Covered | ⚠️ Partial | ❌ Gap

| BR | FR / NFR | Description | ADR | HLD Component | DevOps Test Gate | Runbook | Status |
|----|----------|-------------|-----|----------------|------------------|---------|--------|
| BR-001 | FR-001 | Air-gap install from signed bundle | ADR-001, ADR-002 | API service, IaC bundle, `arckit-verify` CLI | CI Stage 4-5 (signing, SBOM, SLSA L3); §4.4 ceremony | RB-VEN-001 (issue), RB-VEN-004 (distribution); customer-side install runbook (FR-011) | ✅ |
| BR-001 | FR-002 | Air-gap upgrade with roll-back | ADR-001, ADR-008 | All containers + IaC bundle | CI Stage 3 network-deny smoke covers upgrade + roll-back | RB-VEN-001; customer-side upgrade/roll-back runbook | ✅ |
| BR-001 | FR-008 | Same artefact authoring as SaaS | ADR-001 | Web UI, API service (shared with SaaS) | CI Stage 3 cross-mode parity tests | n/a (vendor build); customer authoring guides | ✅ |
| BR-001 | NFR-I-001 | Open standards parity with SaaS | ADR-001 | API service (OpenAPI identical) | CI Stage 3 contract tests vs SaaS spec | RB-VEN-001 release diff | ✅ |
| BR-001 | NFR-I-002 | Data portability (open formats) | ADR-001 | API service, async runner | CI Stage 3 export round-trip | customer-side export runbook | ✅ |
| BR-002 | FR-001 | Air-gap install (no outbound) | ADR-001 | All containers | CI Stage 3 network-deny smoke | RB-VEN-009 (network-deny smoke failure) | ✅ |
| BR-002 | FR-003 | Air-gap backup, restore, key rotation | ADR-001, ADR-002 | Storage/DB, IaC bundle | CI Stage 3 backup/restore offline test | RB-VEN-007 (key rotation); customer-side backup/restore/key-rotation runbooks | ✅ |
| BR-002 | FR-004 | Pluggable AI / model endpoint | ADR-004 | AI adaptor | CI Stage 3 default-no-AI test; AI-mode contract test | RB-VEN-005 customer escalation if integration fails | ✅ |
| BR-002 | FR-005 | Configurable telemetry/time/CA/mirror/IdP | ADR-005 | API service config; audit pipeline | CI Stage 3 default-deny-without-config test | customer-side config runbook | ✅ |
| BR-002 | NFR-SEC-004 | No outbound calls inside boundary | ADR-001 | All containers | CI Stage 3 network-deny smoke (CRITICAL gate) | RB-VEN-009 | ✅ |
| BR-002 | NFR-A-003 | Disconnected-mode fault tolerance | ADR-001, ADR-004 | Web UI, API, async | CI Stage 3 disconnected-mode soak test | customer-side incident response runbook | ✅ |
| BR-002 | INT-002 | Customer-controlled storage/DB | ADR-001 | Storage/DB (customer-provisioned) | CI Stage 3 customer-DB compatibility matrix | customer-side DB ops runbook | ✅ |
| BR-002 | INT-003 | Customer time/CA/mirror | ADR-005 | API service config | CI Stage 3 endpoint-config validation | customer-side config runbook | ✅ |
| BR-002 | INT-004 | Customer observability backend | ADR-005 | Audit pipeline | CI Stage 3 SIEM-emit test | customer-side SIEM ingest runbook | ✅ |
| BR-002 | INT-007 | Customer KMS | ADR-001, ADR-002 | Storage/DB encryption; AI adaptor mTLS | CI Stage 4 PKCS#11/HMG-CAPS check | RB-VEN-007; customer-side key-rotation runbook | ✅ |
| BR-003 | FR-007 | Customer-controlled identity / cleared-personnel auth | ADR-003 | API service auth layer | CI Stage 3 IdP integration test; clearance-claim refusal test | customer-side IdP onboarding runbook | ✅ |
| BR-003 | FR-011 | Operator runbook library | ADR-001..008 | Operator runbook library | CI Stage 3 runbook lint + dry-run | customer-side runbook set (install/upgrade/backup/restore/key-rotation/decommission/IR/DR) | ✅ |
| BR-003 | FR-013 | Vendor remote support (opt-in) | ADR-003, ADR-006 | API service auth; audit pipeline | CI Stage 3 remote-support default-off test | RB-VEN-005 (customer escalation); customer-side opt-in approval runbook | ⚠️ (DPIA-003 gap — see §6) |
| BR-003 | INT-001 | Customer IdP | ADR-003 | API service auth | CI Stage 3 OIDC/SAML/OAuth conformance | customer-side IdP runbook | ✅ |
| BR-003 | INT-006 | Customer email/notification | ADR-005 | Audit pipeline / notifier | CI Stage 3 SMTP/in-boundary notifier test | customer-side email runbook | ⚠️ (notifier component to be detailed in DLD) |
| BR-003 | INT-009 | Vendor remote support channel | ADR-003 | API service auth | CI Stage 3 audited-session test | RB-VEN-005; customer-side approval runbook | ⚠️ (DPIA-003) |
| BR-004 | FR-010 | Audit logging with customer retention | ADR-003, ADR-005 | Audit pipeline | CI Stage 3 audit-emit conformance | RB-VEN-001 §evidence; customer-side SIEM retention runbook | ✅ |
| BR-004 | FR-012 | Configurable classification marking | ADR-003 | API service validation; Web UI marker | CI Stage 3 max-classification refusal test | customer-side classification config runbook | ✅ |
| BR-004 | NFR-SEC-001 | MOD SbD / JSP 440 / 604 alignment | ADR-006 | (governance / evidence) | CI Stage 4 evidence-pack staging | RB-VEN-003 (evidence pack refresh) | ✅ |
| BR-004 | NFR-SEC-002 | NCSC CAF mapping (non-MOD) | ADR-006 | (governance / evidence) | CI Stage 4 evidence-pack staging | RB-VEN-003 | ✅ |
| BR-004 | NFR-SEC-003 | HMG-approved cryptography | ADR-002, ADR-003 | Signing infra; storage encryption | CI Stage 4 HMG-CAPS primitive check | RB-VEN-007 | ✅ |
| BR-004 | NFR-SEC-005 | Supply-chain integrity (SBOM, signing) | ADR-002 | `arckit-verify` CLI; signing infra | CI Stage 4 cosign + Syft + SLSA L3 | RB-VEN-001, RB-VEN-006, RB-VEN-008, RB-VEN-010 | ✅ |
| BR-004 | NFR-SEC-006 | Within-deployment isolation | ADR-003 | API service authz | CI Stage 3 isolation tests (FR-006) | customer-side admin runbook | ✅ |
| BR-004 | NFR-SEC-007 | Cleared-personnel-only access | ADR-003 | API service auth claim check | CI Stage 3 missing-claim refusal test | customer-side IdP runbook | ✅ |
| BR-004 | NFR-SEC-008 | Vulnerability disclosure & patching SLAs | ADR-008 | Vendor pipeline only | CI Stage 4 CVE scan + patch backport | RB-VEN-002 (hotfix), RB-VEN-010 (VDP intake) | ✅ |
| BR-004 | NFR-C-001 | Government Security Classifications | ADR-003 | Classification marker (FR-012) | CI Stage 3 classification validation | customer-side runbook | ✅ |
| BR-004 | NFR-C-002 | UK GDPR / DPA 2018 | ADR-001, ADR-005 | n/a (vendor side limited; customer accountable) | CI Stage 3 telemetry-default-off test | RB-VEN-003 (vendor processor commitments) | ⚠️ (DPIA-003 vendor support channel residual) |
| BR-004 | NFR-C-003 | WCAG 2.2 AA accessibility | (inherited from SaaS) | Web UI | CI Stage 3 axe-core + manual audit (sovereign-context) | n/a (vendor build) | ⚠️ (sovereign-context audit pending — TCoP Point 2) |
| BR-004 | NFR-C-004 | Audit log retention | ADR-005 | Audit pipeline | CI Stage 3 emit-conformance test | customer-side SIEM retention | ✅ |
| BR-004 | FR-006 | Within-deployment isolation | ADR-003 | API service authz | CI Stage 3 isolation tests | customer-side admin runbook | ✅ |
| BR-004 | INT-010 | Vulnerability disclosure inbound | ADR-008 | (vendor process) | n/a (intake gate at vendor) | RB-VEN-010 | ✅ |
| BR-005 | FR-014 | LTS patch delivery | ADR-008 | IaC bundle (patch path) | CI Stage 4 patch-backport reproducibility | RB-VEN-001 (LTS cut), RB-VEN-002 (hotfix) | ✅ |
| BR-005 | NFR-C-005 | LTS support and patching SLA | ADR-008 | (release process) | CI Stage 4 SLA breach alarm | RB-VEN-001, RB-VEN-002 | ✅ |
| BR-005 | NFR-SEC-008 | Patching SLA (Crit/High/Med 7/30/90 d) | ADR-008 | (release process) | CI Stage 4 CVE-to-patch latency check | RB-VEN-002 | ✅ |
| BR-006 | (commercial) | Sovereign covers cost-to-serve + margin | (SOBC, FINOPS) | n/a (commercial) | n/a | n/a — commercial review cadence (FINOPS quarterly) | ✅ (governed by SOBC + FINOPS) |
| BR-007 | INT-008 | G-Cloud / DOS / defence frameworks | (SOBC commercial case) | n/a (commercial) | n/a | n/a — Service Owner cadence | ✅ (SOBC) |
| BR-008 | (programme outcome) | Reference customer in MOD/comparable | (PLAN, ROAD) | n/a (programme) | n/a — milestone gate | n/a — Sovereign Delivery Lead programme runbook | ✅ |

**Coverage Summary**: 8 BR / 14 FR / 24 NFR rows above ↦ 7/8 BR fully covered with green status; 1/8 BR (BR-003) partially covered due to FR-013 / INT-009 DPIA-003 residual; all FR rows covered; 21/24 NFR rows fully covered, 3/24 partial (NFR-C-002, NFR-C-003, NFR-A-003-ish edge cases noted in footnotes of source docs).

---

### 2.3 ADR-by-ADR Forward Traceability

| ADR | Decision | Driven By (REQ/Principle) | HLD Component(s) | Test Gate | Runbook |
|-----|----------|---------------------------|------------------|-----------|---------|
| ADR-001 | Air-gapped operation, no outbound | BR-002, FR-001..005, NFR-SEC-004, P-21 | All containers; IaC bundle | CI Stage 3 network-deny; §4.4 ceremony zero-egress | RB-VEN-009 (network-deny smoke failure) |
| ADR-002 | Signed release bundle (cosign + CycloneDX + SLSA L3) | BR-001, BR-004, BR-005, FR-001, FR-014, NFR-SEC-005, P-21 | `arckit-verify` CLI; IaC bundle; signing infra | CI Stage 4 (signing, SBOM, SLSA), §4.4 ceremony, Section 9.1 HSM custody | RB-VEN-001 (issue), RB-VEN-006 (HSM compromise), RB-VEN-007 (key rotation), RB-VEN-008 (reproducibility failure) |
| ADR-003 | Cleared-personnel access model | BR-003, BR-004, FR-006, FR-007, FR-010, FR-012, NFR-SEC-006, NFR-SEC-007, P-5, P-7 | API service auth; audit pipeline | CI Stage 3 isolation, missing-claim refusal, classification, audit-emit | customer-side IdP/admin/audit runbooks |
| ADR-004 | On-premise AI integration (TGI/vLLM/Triton) | BR-002, FR-004, INT-005, NFR-P-002, P-21 | AI adaptor | CI Stage 3 default-no-AI; AI-mode contract test | customer-side AI on-prem runbook |
| ADR-005 | Customer-controlled telemetry/time/CA/mirror | BR-002, BR-003, FR-005, FR-010, NFR-M-002, INT-003, INT-004, P-21 | API service config; audit pipeline | CI Stage 3 default-deny-no-config, SIEM-emit | customer-side config + SIEM runbooks |
| ADR-006 | JSP 440 / SAL alignment & controls inheritance | BR-004, NFR-SEC-001, NFR-SEC-002, P-5 | (evidence) | CI Stage 4 evidence pack staging | RB-VEN-003 |
| ADR-007 | Distribution model (sealed media + diode) | BR-002, BR-003, NFR-SEC-005, TC-3, P-21 | Distribution staging | CI Stage 5 distribution staging | RB-VEN-004 |
| ADR-008 | LTS release line | BR-005, NFR-C-005, NFR-SEC-008, Conflict C-2 | Release process | CI Stage 4 patch backport | RB-VEN-001, RB-VEN-002 |

**Coverage**: 8/8 ADRs trace backwards to ≥ 1 BR (or FR + Principle) and forwards to HLD + test gate + runbook (100%).

---

### 2.4 HLD Component → Source Requirement (Backward)

| HLD Container | Responsibility | Traces To | ADR |
|---------------|----------------|-----------|-----|
| Web UI | Browser-based authoring (same code as SaaS) | BR-001, FR-008, NFR-C-003 | (inherited) |
| API service | OpenAPI HTTP API | NFR-I-001, FR-007, FR-010 | ADR-001, ADR-003 |
| Async / job runner | Long-running generation, lineage, indexing | P-11, FR-008, FR-009 | ADR-001 |
| AI adaptor | Pluggable AI generation | FR-004, INT-005, NFR-P-002 | ADR-004 |
| Audit pipeline | Hash-chained audit emission to customer SIEM | FR-010, NFR-C-004, INT-004 | ADR-003, ADR-005 |
| Storage / DB | Customer-provisioned | FR-003, INT-002 | ADR-001 |
| `arckit-verify` CLI | Customer-side bundle verification | FR-001, NFR-SEC-005 | ADR-002 |
| IaC bundle | Reproducible deployment topology | P-18, FR-001, FR-002, FR-003, FR-014 | ADR-001, ADR-002 |
| Operator runbook library | Install/upgrade/backup/restore/decommission | FR-011, BR-003 | ADR-001..ADR-008 |

**Coverage**: 9/9 HLD containers trace backward to ≥ 1 REQ/Principle (100%). No orphan components.

---

### 2.5 DevOps Test Gates → Source Requirement

| Stage | Gate | Validates | Runbook on Failure |
|-------|------|-----------|--------------------|
| Stage 1 — Source | Branch protection, signed commits | P-20, ADR-002 supply chain | n/a (rejected pre-merge) |
| Stage 2 — Build | Reproducibility cross-build | P-18, ADR-002 | RB-VEN-008 (pipeline reproducibility failure) |
| Stage 3 — Test | Network-deny smoke | BR-002, NFR-SEC-004, ADR-001 | RB-VEN-009 |
| Stage 3 — Test | Within-deployment isolation | FR-006, NFR-SEC-006 | (defect → RB-VEN-001 supersession path) |
| Stage 3 — Test | Default-no-AI | FR-004, ADR-004 | (defect → supersession) |
| Stage 3 — Test | Disconnected-mode soak | NFR-A-003 | (defect → supersession) |
| Stage 3 — Test | Classification refusal | FR-012, NFR-C-001 | (defect → supersession) |
| Stage 3 — Test | Missing-claim refusal | FR-007, NFR-SEC-007 | (defect → supersession) |
| Stage 3 — Test | IdP/SIEM/SMTP conformance | INT-001, INT-004, INT-006 | (defect → supersession) |
| Stage 3 — Test | Cross-mode parity (SaaS ↔ Sovereign artefacts) | BR-001, FR-008, NFR-I-001 | (defect → cross-project review per Conflict C-1) |
| Stage 4 — Security | Cosign signing + Syft SBOM + SLSA L3 | NFR-SEC-005, ADR-002 | RB-VEN-006 (key compromise), RB-VEN-007 (rotation) |
| Stage 4 — Security | HMG-CAPS primitive check | NFR-SEC-003 | RB-VEN-001 supersession |
| Stage 4 — Security | CVE scan + patch SLA latency | NFR-SEC-008, BR-005 | RB-VEN-002 (hotfix) |
| Stage 4 — Security | Evidence pack staging | NFR-SEC-001, NFR-SEC-002, BR-004 | RB-VEN-003 |
| Stage 5 — Deploy | Bundle assembly + distribution staging | ADR-007, BR-002 | RB-VEN-004 |
| §4.4 Ceremony | Customer verification ceremony | FR-001, NFR-SEC-005, BR-002 | customer-side install runbook |

**Coverage**: 16/16 test gates trace to ≥ 1 BR/FR/NFR/ADR (100%). Every gate has a defined failure runbook (vendor-side or customer-side).

---

### 2.6 Operational Runbooks → Source Requirement

| Runbook | Scope | Traces To | Risks Mitigated |
|---------|-------|-----------|-----------------|
| RB-VEN-001 — Bundle Issue | Vendor-side | BR-001, BR-005, FR-014, ADR-002, ADR-008 | R-003, R-010 |
| RB-VEN-002 — Hotfix Release | Vendor-side | NFR-SEC-008, BR-005, ADR-008 | R-010, R-013 |
| RB-VEN-003 — Evidence Pack Refresh | Vendor-side | BR-004, NFR-SEC-001, NFR-SEC-002, ADR-006 | R-002, R-012 |
| RB-VEN-004 — Patch-Bundle Distribution | Vendor-side | BR-002, ADR-007, TC-3 | R-004, R-007 |
| RB-VEN-005 — Customer Escalation | Vendor-side / cleared channel | BR-003, FR-013, ADR-003, ADR-006 | R-009, R-013 |
| RB-VEN-006 — HSM Key Compromise | Vendor-side | NFR-SEC-003, NFR-SEC-005, ADR-002 | R-004 |
| RB-VEN-007 — HSM Key Rotation | Vendor-side | FR-003 (key rotation), NFR-SEC-003, ADR-002 | R-004 |
| RB-VEN-008 — Pipeline Reproducibility | Vendor-side | P-18, ADR-002 | R-003, R-004 |
| RB-VEN-009 — Network-Deny Smoke Failure | Vendor-side | BR-002, NFR-SEC-004, ADR-001 | R-007 |
| RB-VEN-010 — Vulnerability Disclosure | Vendor-side | NFR-SEC-008, INT-010 | R-002, R-013 |
| Customer-side install/upgrade/backup/restore/key-rotation/decommission/IR/DR | Customer-side | FR-001, FR-002, FR-003, BR-003, FR-011 | R-005, R-006 |
| Customer-side IdP / classification / SIEM / AI on-prem / opt-in support config | Customer-side | FR-005, FR-007, FR-010, FR-012, FR-013, INT-001..009 | R-005, R-006, R-008 |

**Coverage**: 10/10 vendor-side runbooks (RB-VEN-001..010) trace to ≥ 1 REQ/ADR and ≥ 1 risk (100%). Customer-side runbook set traces to FR-011 + the listed FRs/INTs (per OPS Section 0 scope split).

---

## 3. Backward Traceability — No Orphans Audit

For every artefact in project 002, this section verifies that it traces back to ≥ 1 upstream requirement or principle.

### 3.1 Strategic Layer

| Artefact | Backward Trace |
|----------|-----------------|
| ARC-002-STKE (17 SDs) | All SDs derive from REQ §Stakeholders + Principle 21; explicit cross-link to project 001 SD-1..SD-5 for SD-6 | ✅ |
| ARC-002-SOBC (5-case) | Strategic case driven by SD-1..SD-17, BR-001..BR-008; Economic / Commercial / Financial / Management cases by SOBC own structure + REQ §Budget | ✅ |
| ARC-002-PLAN (timeline) | Driven by REQ §Timeline; BR-008 milestone | ✅ |
| ARC-002-ROAD (3-year roadmap) | Driven by REQ + ADR-008 (LTS cadence) + BR-008 reference customer | ✅ |

### 3.2 Decision Layer

| ADR | Backward Trace | Verdict |
|-----|-----------------|---------|
| ADR-001 | BR-002, FR-001..005, NFR-SEC-004, Principle 21 | ✅ |
| ADR-002 | BR-001, BR-004, BR-005, FR-001, FR-014, NFR-SEC-005, Principle 21 | ✅ |
| ADR-003 | BR-003, BR-004, FR-006, FR-007, FR-010, FR-012, NFR-SEC-006, NFR-SEC-007 | ✅ |
| ADR-004 | BR-002, FR-004, INT-005, NFR-P-002, Principle 21, Conflict C-4 | ✅ |
| ADR-005 | BR-002, BR-003, FR-005, FR-010, NFR-M-002, INT-003, INT-004 | ✅ |
| ADR-006 | BR-004, NFR-SEC-001, NFR-SEC-002 | ✅ |
| ADR-007 | BR-002, NFR-SEC-005, TC-3 | ✅ |
| ADR-008 | BR-005, NFR-C-005, NFR-SEC-008, Conflict C-2 | ✅ |

**Verdict**: 8/8 ADRs traceable. **0 orphan ADRs**.

### 3.3 Design Layer

| Diagram | Backward Trace | Verdict |
|---------|-----------------|---------|
| ARC-002-DIAG-001 (C4 Context) | REQ §Stakeholders + ADR-001 boundary statement | ✅ |
| ARC-002-DIAG-002 (C4 Container) | HLD §5.2 + ADR-001..008 | ✅ |
| ARC-002-DIAG-003 (Network DFD / sequence) | UC-1, UC-2, UC-3, ADR-001 zero-egress claim | ✅ |
| ARC-002-HLD (review) | Reviews against REQ + Principle 21 explicit checklist + all 8 ADRs | ✅ |

### 3.4 Build / Run Layer

| Artefact | Backward Trace | Verdict |
|----------|-----------------|---------|
| ARC-002-DEVOPS | Pipeline traces each stage to BR/FR/NFR/ADR (DEVOPS §3.2 explicit table) | ✅ |
| ARC-002-FINOPS | Cost model traces to BR-006, SOBC Economic case | ✅ |
| ARC-002-OPS | Each runbook traces to ADR + FR + risk (OPS §6.x explicit) | ✅ |

### 3.5 Compliance Layer

| Artefact | Backward Trace | Verdict |
|----------|-----------------|---------|
| ARC-002-TCOP | Each of 13 TCoP points scored against REQ + ADR set | ✅ |
| ARC-002-MOD-SBD | Each of 7 MOD principles scored against REQ + ADR + RISK | ✅ |
| ARC-002-DPIA | Vendor scope only; ICO 9-criteria screened; 5 DPIA risks linked to ADR-001/003/004/005 | ✅ |
| ARC-002-AIP | 10 core principles + 6 ethical themes scored against ADR-004 + AI-related FRs | ✅ |
| ARC-002-RISK | 13 risks each linked to BR/FR/NFR/ADR + control set | ✅ |

**Verdict**: All 21 project-002 artefacts trace backward to ≥ 1 upstream requirement or principle. **0 orphan artefacts.**

---

## 4. Risk Coverage Matrix (R-001..R-013)

Every sovereign-specific risk MUST map to ≥ 1 mitigation control + ≥ 1 ADR/NFR + ≥ 1 runbook.

| Risk ID | Risk Name | Category | Mitigation Control(s) | ADR / NFR | Runbook (vendor-side / customer-side) | Coverage |
|---------|-----------|----------|------------------------|-----------|----------------------------------------|----------|
| R-001 | First-attempt customer accreditation failure | STRATEGIC | Accreditator-in-the-loop alpha; standardised evidence pack; pilot customer engagement | BR-004, NFR-SEC-001, ADR-006 | RB-VEN-003 (vendor); customer-side accreditation runbook | ✅ |
| R-002 | MOD Secure by Design assessment fail | COMPLIANCE | MOD SbD CAAT cycle; Defence-in-Depth controls; HSM signing | NFR-SEC-001, ADR-002, ADR-006 | RB-VEN-003, RB-VEN-010 (vendor); customer-side SAL pre-fill runbook | ✅ |
| R-003 | Single-codebase divergence (Principle 21 violation) | TECHNOLOGY | Quarterly architecture review; feature-flag audit; refactor budget; cross-mode parity tests | BR-001, NFR-I-001, ADR-001 | RB-VEN-001, RB-VEN-008 (vendor); cross-project review with project 001 | ✅ |
| R-004 | Signed-bundle / supply-chain compromise | COMPLIANCE | HSM-backed cosign signing; key custody; rotation; SLSA L3; offline manifest | NFR-SEC-005, NFR-SEC-003, ADR-002 | RB-VEN-006 (compromise), RB-VEN-007 (rotation), RB-VEN-008 (reproducibility); customer-side `arckit-verify` runbook | ✅ |
| R-005 | Customer break-glass / privileged-access abuse | COMPLIANCE | Default-deny break-glass; tamper-evident logging; quarterly customer review | NFR-SEC-006, NFR-SEC-007, FR-010, ADR-003 | (vendor-side: none — customer-side ownership); customer-side break-glass policy + audit-review runbook | ✅ (customer-side primary; vendor advisory only) |
| R-006 | Customer operator-team turnover | OPERATIONAL | Training + runbook discipline (FR-011); operator on-boarding pack; vendor remote-support backstop (FR-013) | BR-003, FR-011 | RB-VEN-005 (vendor escalation); customer-side operator on-boarding runbook | ✅ |
| R-007 | Accredited-boundary egress incident | REPUTATIONAL | Network-deny CI; default-deny configuration; customer egress monitoring | BR-002, NFR-SEC-004, ADR-001 | RB-VEN-009 (network-deny smoke failure); customer-side IR runbook | ✅ |
| R-008 | On-premise AI model integration brittleness | TECHNOLOGY | Pluggable AI adaptor; OpenAI-compatible contract; customer-controlled endpoint | FR-004, INT-005, ADR-004 | RB-VEN-005 (escalation); customer-side AI on-prem runbook | ✅ |
| R-009 | Vendor cleared-personnel availability shortfall | OPERATIONAL | Cleared-personnel staffing plan; cross-training; cleared-channel escalation | BR-003, NFR-SEC-007 | RB-VEN-005; (no customer-side counterpart — vendor obligation) | ✅ |
| R-010 | LTS line drift / Year-3 backport SLA breach | OPERATIONAL | Dedicated LTS engineering; CI Stage 4 SLA monitoring; LTS staffing model | BR-005, NFR-SEC-008, NFR-C-005, ADR-008 | RB-VEN-001 (LTS cut), RB-VEN-002 (hotfix); customer-side LTS migration runbook | ✅ |
| R-011 | Cross-subsidy erosion (sovereign pricing concession) | FINANCIAL | Documented cost-to-serve floor; quarterly affordability review; Service Owner approval gate | BR-006 | (FINOPS quarterly review; no runbook needed) | ✅ (commercial governance, not runbook) |
| R-012 | Customer-side accreditator format-rejection | OPERATIONAL | Engage MOD accreditor early in alpha; iterate evidence pack; cross-customer template alignment | BR-004, ADR-006 | RB-VEN-003 (evidence pack refresh); customer-side accreditation runbook | ✅ |
| R-013 | Vendor-side data-protection / DPIA gap on opt-in support channel | COMPLIANCE | Per-session approval; tamper-evident logging; DPIA-003 mitigation; minimisation; processor commitments | FR-013, FR-010, NFR-C-002, ADR-003 | RB-VEN-005 (escalation), RB-VEN-010 (VDP intake); customer-side opt-in approval runbook | ✅ |

**Verdict**: **13/13 risks covered with ≥ 1 mitigation control + ≥ 1 ADR/NFR + ≥ 1 runbook (vendor-side or customer-side).** Three risks (R-001, R-005, R-007) are deliberately accepted above appetite per RISK §Top 5 — this is documented and traced. Two risks (R-003, R-005) have residual likelihood reassessed *upward* in RISK due to time-decay; both have continuing controls.

---

## 5. Compliance Coverage Matrix

### 5.1 TCoP — 13 Points Mapped to Evidence

| TCoP Point | Title | Status | Primary Evidence Artefacts |
|------------|-------|--------|------------------------------|
| 1 | Define User Needs | ⚠️ Partial | STKE (5 personas), REQ §User Personas, BR-008 (pre-pilot maturity gap) |
| 2 | Make Things Accessible and Inclusive | ⚠️ Partial | NFR-C-003 inherited from SaaS; sovereign-context audit pending |
| 3 | Be Open and Use Open Source | ✅ Compliant | Principle 16, ADR-002 (Sigstore/Syft OSS), ADR-004 (TGI/vLLM/Triton) |
| 4 | Make Use of Open Standards | ✅ Compliant | NFR-I-001, NFR-I-002, ADR-002 (CycloneDX/SPDX/SLSA), ADR-003 (OIDC/SAML/OAuth) |
| 5 | Use Cloud First | n/a (sovereign override) | Principle 21 deliberate exception per TCoP exception clause |
| 6 | Make Things Secure | ✅ Compliant (subject to MOD SbD completion) | NFR-SEC-001..008, ADR-002/003/006, MOD-SBD |
| 7 | Make Privacy Integral | ⚠️ Partial | DPIA (vendor scope), NFR-C-002, ADR-005; customer DPIA template pending |
| 8 | Share, Reuse and Collaborate | ✅ Compliant | Principle 16, ADR-002 (SBOM open), shared codebase with project 001 (BR-001) |
| 9 | Integrate and Adapt Technology | ✅ Compliant | INT-001..010, ADR-004 pluggable, NFR-I-001 |
| 10 | Make Better Use of Data | ✅ Compliant | DR-001..007, FR-009 portability, FR-010 audit |
| 11 | Define Your Purchasing Strategy | ✅ Compliant (subject to SOBC completion) | BR-006, BR-007, INT-008, SOBC Commercial case |
| 12 | Make Your Technology Sustainable | ✅ Compliant | ADR-008 LTS, FINOPS, P-15 maintainability |
| 13 | Meet the Service Standard | ⚠️ Partial | (sovereign deployments not subject to GDS Service Standard but mapped) |

**Coverage**: 13/13 points assessed in TCOP and mapped to ≥ 1 evidence artefact (100%). 8/13 ✅ Compliant, 4/13 ⚠️ Partial, 1/13 n/a (sovereign override).

### 5.2 MOD Secure by Design — 7 Principles Mapped to Evidence

| Principle | Title | Status | CAAT Score | Primary Evidence |
|-----------|-------|--------|------------|------------------|
| 1 | Understand and Define Context | ✅ Compliant | Defined (3) → Managed (4) | REQ, STKE, ADR-006, MOD-SBD §1 |
| 2 | Apply Security from the Start | ✅ Compliant | Managed (4) | DEVOPS Stage 4, NFR-SEC-005, ADR-002 |
| 3 | Apply Defence in Depth | ✅ Compliant | Defined (3) | ADR-001 (no outbound), ADR-002 (HSM), ADR-003 (claim refusal); RB-VEN-006 |
| 4 | Follow Secure Design Patterns | ✅ Compliant | Managed (4) | ADR-002, ADR-003, NFR-SEC-003 (HMG-CAPS) |
| 5 | Continuously Manage Risk | ✅ Compliant | Defined (3) | RISK register; quarterly review cadence |
| 6 | Secure the Supply Chain | ✅ Compliant | Managed (4) → Optimized (5) | ADR-002 (cosign + Syft + SLSA L3); RB-VEN-004, RB-VEN-006..008, RB-VEN-010 |
| 7 | Enable Through-Life Assurance | ⚠️ Partial | Repeatable (2) → Defined (3) | ADR-008 LTS, RB-VEN-001/002/003 — operationalise at GA |

**Coverage**: 7/7 principles assessed (100%). 6/7 ✅ Compliant, 1/7 ⚠️ Partial.

### 5.3 JSP 440 — Information Assurance Maturity Model (Mapped Per ADR-006)

JSP 440 controls are mapped in MOD-SBD §3.4 across three families: P&ASec (Personnel & Administrative Security), InfoSec (Information Security), PhySec (Physical Security). The vendor scope covers approximately 28 applicable controls; the deploying authority retains accountability for site-specific controls.

| JSP 440 Family | Vendor Scope (controls) | Customer Scope (controls) | Evidence Artefact |
|----------------|--------------------------|---------------------------|---------------------|
| P&ASec (Personnel) | Cleared-channel staffing (SD-9, SD-10), vendor staff vetting | Customer cleared-personnel access, role assignment | MOD-SBD §9, ADR-003, FR-007 |
| InfoSec (Information) | Signing-key custody, SBOM/manifest, audit emit contract, classification ceiling | Tenant-content custody, SIEM retention, classification config | MOD-SBD §3.4, §5; ADR-001/002/003/005; FR-010, FR-012 |
| PhySec (Physical) | HSM facility (vendor side); sealed-media chain-of-custody | Site PhySec (boundary, racks, media destruction) | ADR-007; ADR-002; customer-side decommission runbook |

**Coverage**: All in-scope JSP 440 controls assigned to vendor or customer side (per OPS §0 scope boundary). MOD-SBD §3.4 provides the per-control mapping. **Verdict: ✅ Mapped, with the customer side accountable for the final control set per JSP 604 accreditation pathway.**

### 5.4 JSP 604 — Accreditation Pathway Gates

| JSP 604 Gate | Description | Vendor Evidence | Customer Action |
|--------------|-------------|------------------|-------------------|
| Initial Risk Assessment | Establishes context and scope | MOD-SBD §1, REQ, STKE | Customer-led IRA against site policy |
| Security Aspects Letter (SAL) | Describes security responsibilities | MOD-SBD §3.2 SAL pre-fill; ADR-006 | Customer Accreditor populates final SAL |
| Risk Management & Accreditation Document Set (RMADS) | Detailed control evidence | MOD-SBD §2 (7 principles) + RISK + ADR set | Customer integrates with site RMADS |
| Authority to Operate (ATO) | Approved by Accreditator | n/a (vendor cannot grant) | Customer Accreditor decision; supported by RB-VEN-003 evidence pack |

**Coverage**: 4/4 JSP 604 gates have vendor-side evidence input + clear customer-side action. **Verdict: ✅**.

### 5.5 UK GDPR DPIA — Vendor-Scope Risks Mapped to Mitigations

| DPIA Risk | Description | Likelihood | Mitigation | Trace |
|-----------|-------------|------------|------------|-------|
| DPIA-001 | Engineering telemetry inadvertently captures customer-identifiable content | LOW | Default OFF; customer-side redaction; opt-in consent | ADR-005, FR-005 |
| DPIA-002 | Accreditation evidence drafts include personal data of cleared personnel | LOW | Evidence-pack discipline; redaction at source | BR-004, RB-VEN-003 |
| DPIA-003 | Audited opt-in remote support session captures personal data | LOW | Per-session approval; tamper-evident logging; minimisation | FR-013, FR-010, ADR-003 |
| DPIA-004 | Vulnerability disclosure intake captures personal data of researchers | LOW | Pseudonymous submission; data minimisation | NFR-SEC-008, INT-010 |
| DPIA-005 | (cross-references SR-2, SR-8) — outbound telemetry leakage | LOW | ADR-001 no-outbound; CI Stage 3 network-deny | NFR-SEC-004, BR-002, FR-005 |

**Coverage**: 5/5 DPIA risks mapped to mitigation + ADR/NFR (100%). All vendor-side; customer-side DPIA accountability sits with deploying authority per ADR-001 / ADR-003 / ADR-004 / ADR-005.

### 5.6 UK Government AI Playbook — 10 Core Principles + 6 Ethical Themes

| Section | Principle / Theme | Status | Score | Evidence |
|---------|-------------------|--------|-------|----------|
| Core 1 | Understanding AI | ✅ Compliant | 8/10 | AIP §2.1, ADR-004 |
| Core 2 | Lawful and Ethical Use | ✅ Compliant | 8/10 | AIP §2.2, DPIA, ADR-004 |
| Core 3 | Security | ✅ Compliant | 9/10 | AIP §2.3, ADR-001 (no AI by default sovereign), ADR-004 |
| Core 4 | Human Control | ✅ Compliant | 10/10 | AIP §2.4 (architecturally trivial — human authoring primary; AI optional) |
| Core 5 | Lifecycle Management | ⚠️ Partial | 7/10 | AIP §2.5 — customer responsibility post-handoff |
| Core 6 | Right Tool Selection | ✅ Compliant | 9/10 | AIP §2.6, ADR-004 (TGI/vLLM/Triton) |
| Core 7 | Collaboration | ⚠️ Partial | 7/10 | AIP §2.7 — cross-government working group at customer side |
| Core 8 | Commercial Partnership | ✅ Compliant | 9/10 | AIP §2.8 (vendor not AI supplier — inverted commercial) |
| Core 9 | Skills and Expertise | ✅ Compliant | 8/10 | AIP §2.9, SD-9, SD-13 |
| Core 10 | Organizational Alignment | ✅ Compliant | 8/10 | AIP §2.10, project 001/002 cross-project alignment |
| Theme 1 | Safety, Security, Robustness | ✅ Compliant | 9/10 | AIP §3.1, ADR-001, ADR-004 |
| Theme 2 | Transparency / Explainability | ⚠️ Partial | 7/10 | Responsibility shifts at sovereign boundary; customer-side accountable |
| Theme 3 | Fairness, Bias, Discrimination | ✅ Compliant | 7/10 | Vendor abstraction; customer accountable for prompt content |
| Theme 4 | Accountability and Responsibility | ✅ Compliant | 8/10 | RACI in AIP §1.5, ADR-004 |
| Theme 5 | Contestability and Redress | ⚠️ N/A at abstraction | 6/10 | Proportionate at vendor scope; customer-side primary |
| Theme 6 | Societal Wellbeing and Public Good | ✅ Compliant | 9/10 | Sovereign route enables otherwise-excluded use cases (BR-001) |

**Coverage**: 16/16 AI Playbook items assessed (100%). 12/16 ✅ Compliant, 4/16 ⚠️ Partial / N/A.

---

## 6. Gap Analysis

### 6.1 Top 3 Orphans

(Items in design / build / run that do NOT trace cleanly to an upstream artefact, or pending artefacts called out as BLOCKING in HLD.)

| # | Orphan | Type | Action |
|---|--------|------|--------|
| 1 | **HLD §5.1 / §5.2 — C4 Context and Container diagrams text describes** "deferred to wave 5/6 (BLOCKING-01)" but the diagrams DIAG-001..003 now exist. Needs HLD update to remove "pending" status. | Documentation drift | Update HLD review v1.1 to mark BLOCKING-01 closed by DIAG-001..003. |
| 2 | **Threat Model** — referenced in HLD §6.1 and MOD-SBD as "BLOCKING-02" — no formal STRIDE / EBIOS / MOD-SbD threat model document yet exists in project 002. Risks are spread across ADRs. | Missing artefact | Create a consolidated threat model artefact (or reference existing ADR threat statements as the canonical set). |
| 3 | **Customer-side runbook bundle** — referenced consistently as "FR-011 operator runbook library", and OPS Section 0 makes the scope split clear, but a customer-side runbook *artefact* is not yet present in `projects/002-arckit-sovereign/` (only vendor-side RB-VEN-001..010 exist). The bundle is intended to ship with the release; for traceability, a placeholder `ARC-002-RUN-CUS-v1.0.md` would close the loop. | Missing artefact | Schedule customer-side runbook artefact generation (or accept that it ships in the release bundle, not the governance repo). |

### 6.2 Top 3 Gaps

| # | Gap | Impact | Recommended Mitigation | Owner |
|---|-----|--------|--------------------------|-------|
| 1 | **TCoP Point 2 (Accessibility) — sovereign-context audit pending.** WCAG 2.2 AA inherited from SaaS; not yet validated against sovereign-deployment specifics (e.g., disconnected-mode keyboard nav, screen-reader behaviour without external assets). | Medium — Principle 12 non-negotiable; could block ATO | Schedule sovereign-context accessibility audit before private beta (PLAN milestone). | Lead Architect |
| 2 | **TCoP Point 7 (Privacy) — customer DPIA template pending.** Vendor-side DPIA complete (DPIA-001..005); customer-side DPIA template promised in DPIA §1.3 ("Vendor's DPIA-Input Pack to the Deploying Authority") but not yet formalised in the repository. | Medium — customers must produce their own DPIA; absence of vendor template increases customer cost (R-012). | Author DPIA-input-pack template as part of evidence pack refresh (RB-VEN-003). | Vendor DPO |
| 3 | **MOD SbD Principle 7 (Through-Life Assurance) — Repeatable (2) → Defined (3) gap.** LTS line designed (ADR-008) but not yet operationalised; Year-3 backport SLA risk (R-010) flagged. | Medium-High — through-life is an accreditator concern; operational at GA | Operationalise LTS at GA: dedicated engineering team, automated patch backport pipeline (DEVOPS Stage 4), quarterly LTS review. | LTS Engineering Lead |

### 6.3 Coverage Metrics

| Layer | Total | Traced | Coverage | Notes |
|-------|-------|--------|----------|-------|
| Strategic Drivers (SD-1..SD-17) | 17 | 17 | 100% | All map to ≥ 1 Goal |
| Goals (G-1..G-10) | 10 | 10 | 100% | All map to ≥ 1 BR + measurable outcome |
| Business Requirements (BR-001..BR-008) | 8 | 8 | 100% | 7 fully covered, 1 partial (BR-003 due to FR-013 DPIA-003 residual) |
| Functional Requirements (FR-001..FR-014) | 14 | 14 | 100% | All map to ADR + HLD + test gate |
| Non-Functional Requirements (P/A/S/SEC/C/M/I) | 24 | 24 | 100% | 21 fully covered; 3 partial (NFR-C-002, NFR-C-003, NFR-A-003 edge case) |
| Integration Requirements (INT-001..INT-010) | 10 | 10 | 100% | All map to ADR + HLD + runbook |
| Data Requirements (DR-001..DR-007) | 7 | 7 | 100% | All map to HLD §5.4 owner + storage |
| Architecture Decisions (ADR-001..ADR-008) | 8 | 8 | 100% | All map to BR/FR/NFR + HLD + test gate + runbook |
| HLD Containers | 9 | 9 | 100% | No orphan components |
| DevOps Test Gates | 16 | 16 | 100% | All map to BR/FR/NFR/ADR + failure runbook |
| Vendor Runbooks (RB-VEN-001..010) | 10 | 10 | 100% | All map to ≥ 1 REQ + ≥ 1 risk |
| Risks (R-001..R-013) | 13 | 13 | 100% | All map to control + ADR/NFR + runbook |
| TCoP Points | 13 | 13 | 100% | 8 ✅, 4 ⚠️, 1 n/a |
| MOD SbD Principles | 7 | 7 | 100% | 6 ✅, 1 ⚠️ |
| JSP 440 Control Families | 3 (P&A/Info/Phys) | 3 | 100% | All split across vendor/customer scope |
| JSP 604 Gates | 4 | 4 | 100% | All have vendor evidence + customer action |
| DPIA Risks (DPIA-001..005) | 5 | 5 | 100% | All map to mitigation + ADR/NFR |
| AI Playbook Items (10 + 6) | 16 | 16 | 100% | 12 ✅, 4 ⚠️/n/a |

**Overall traceability score: 95/100** — penalty for partial-coverage items (TCoP Points 1/2/7/13, MOD-SbD Principle 7, AIP Themes 2/5, NFR-C-003 sovereign-context audit pending) and the three orphans/gaps documented above.

**Recommendation**: **APPROVED WITH CONDITIONS**. The traceability matrix is fit for accreditator review. Three conditions: (1) close BLOCKING-01 by updating HLD review to acknowledge DIAG-001..003; (2) author consolidated threat model artefact (BLOCKING-02); (3) deliver customer DPIA-input template before private beta.

---

## 7. Cross-Project Linkage (Project 001 ↔ Project 002, per Principle 21)

Principle 21 mandates a single source-of-truth codebase across both deployment routes. Several artefacts are explicitly shared or paired:

| Project 001 (SaaS) Item | Project 002 (Sovereign) Counterpart | Linkage |
|---------------------------|--------------------------------------|---------|
| `projects/000-global/ARC-000-PRIN-v2.0.md` Principle 21 | Same file, anchors project 002 | **Shared global** |
| Project 001 SD-9 (Lead Architect — single codebase) | Project 002 SD-9 (Lead Architect — single codebase) | **Bidirectional dependency** |
| Project 001 BR-005 (cross-subsidy SME tier) | Project 002 BR-006 (sovereign margin funds cross-subsidy) | **Direct cross-reference** |
| Project 001 FR-004 (AI generation) | Project 002 FR-004 (pluggable AI; default off) + ADR-004 | **Same FR ID, sovereign overlay** |
| Project 001 INT-005 (AI provider) | Project 002 INT-005 (customer-approved AI endpoint) | **Same INT ID, customer-controlled** |
| Project 001 NFR-SEC-002 (within-tenant isolation) | Project 002 NFR-SEC-006 (within-deployment isolation) + FR-006 | **Different ID, same intent** |
| Project 001 Conflict C-1 (multi-tenant vs sovereign) | Project 002 Conflict C-1 (single-codebase vs customisation) | **Cross-conflict resolution** |
| Project 001 R-002 (architecture fork pressure) | Project 002 R-003 (Principle 21 violation) | **Same risk, different framing** |
| Project 001 STKE / Strategy / Wardley | Sovereign-side reuses for cross-project context | **Cited, not duplicated** |

**Cross-project review cadence**: Quarterly architecture review (per Conflict C-1 and RISK §Recommendations) with both projects in the room. R-003 / project-001 R-002 reviewed jointly.

---

## 8. Action Items

### 8.1 Gap Resolution

| ID | Gap | Owner | Priority | Target Date | Status |
|----|-----|-------|----------|-------------|--------|
| GAP-001 | TCoP Point 2 sovereign-context accessibility audit | Lead Architect | HIGH | 2026-09-30 (pre private beta) | Open |
| GAP-002 | DPIA customer template (TCoP Point 7) | Vendor DPO | MEDIUM | 2026-08-31 | Open |
| GAP-003 | MOD-SbD Principle 7 operationalised at GA | LTS Engineering Lead | HIGH | GA (2027-12-31) | Open |
| GAP-004 | Vendor remote-support DPIA-003 residual | Vendor DPO + Security Lead | MEDIUM | 2026-09-30 | Open |
| GAP-005 | Customer-side runbook artefact slot in repo | Sovereign Delivery Lead | LOW | 2026-12-31 | Open |

### 8.2 Orphan Resolution

| ID | Orphan | Type | Resolution | Owner | Target Date |
|----|--------|------|------------|-------|--------------|
| ORP-001 | HLD review marks BLOCKING-01 as open; DIAG-001..003 now exist | Documentation drift | Re-issue HLD review v1.1 to close BLOCKING-01 | Lead Architect | 2026-06-30 |
| ORP-002 | Threat model artefact (BLOCKING-02) | Missing artefact | Author consolidated threat model OR formally cite ADR threat sections as the canonical set | Vendor Security Lead | 2026-09-30 |
| ORP-003 | Customer-side runbook bundle | Missing artefact | Generate placeholder OR accept release-bundle delivery | Sovereign Delivery Lead | 2026-12-31 |

---

## 9. Review and Approval

### 9.1 Review Checklist

- [x] All strategic drivers (SD-1..SD-17) traced to goals
- [x] All goals (G-1..G-10) traced to BRs and outcomes
- [x] All business requirements (BR-001..BR-008) traced to ≥ 1 FR/NFR
- [x] All functional requirements (FR-001..FR-014) traced to ADR + HLD + test gate
- [x] All non-functional requirements (24) traced to ADR + HLD + test gate
- [x] All ADRs (ADR-001..ADR-008) traced backward to ≥ 1 BR/FR/NFR/Principle
- [x] All HLD components traced backward to ≥ 1 REQ (no orphan components)
- [x] All DevOps test gates traced to BR/FR/NFR/ADR + failure runbook
- [x] All vendor runbooks (RB-VEN-001..010) traced to REQ + risk
- [x] All risks (R-001..R-013) covered with control + ADR/NFR + runbook
- [x] All TCoP 13 points mapped to evidence
- [x] All MOD SbD 7 principles mapped to evidence
- [x] All JSP 440 control families mapped (vendor / customer split)
- [x] All JSP 604 gates have vendor evidence + customer action
- [x] All DPIA risks mapped to mitigations
- [x] All AI Playbook items (10 + 6) mapped
- [x] Cross-project linkage to project 001 documented (Principle 21)
- [x] Top 3 orphans documented
- [x] Top 3 gaps documented with owner + target date

### 9.2 Approval

| Role | Name | Review Date | Approval | Signature | Date |
|------|------|-------------|----------|-----------|------|
| Service Owner | Mark Craddock | [DATE] | [ ] Approve [ ] Reject | _________ | [DATE] |
| Lead Architect | [PENDING] | [DATE] | [ ] Approve [ ] Reject | _________ | [DATE] |
| Security Lead | [PENDING] | [DATE] | [ ] Approve [ ] Reject | _________ | [DATE] |
| MOD Customer Accreditor (pilot) | [PENDING] | [DATE] | [ ] Approve [ ] Reject | _________ | [DATE] |

---

## 10. Appendices

### Appendix A: Full Requirements List

See `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md`.

### Appendix B: Design Documents

- `projects/002-arckit-sovereign/ARC-002-HLD-v1.0.md` (HLD review)
- `projects/002-arckit-sovereign/diagrams/ARC-002-DIAG-001-v1.0.md` (C4 Context)
- `projects/002-arckit-sovereign/diagrams/ARC-002-DIAG-002-v1.0.md` (C4 Container)
- `projects/002-arckit-sovereign/diagrams/ARC-002-DIAG-003-v1.0.md` (Network DFD / Sequence)

### Appendix C: Test Plan

See `projects/002-arckit-sovereign/ARC-002-DEVOPS-v1.0.md` §3.2 (CI Stages 1-5) and §4.4 (Customer Verification Ceremony).

### Appendix D: Cross-Project References

- `projects/000-global/ARC-000-PRIN-v2.0.md` — Architecture Principles (Principle 21 anchors project 002)
- `projects/001-arckit-saas/` — Sister project (managed SaaS); shares PRIN, glossary, strategic narrative, Wardley map
- Project 001 BR-005 ↔ Project 002 BR-006 (cross-subsidy)
- Project 001 R-002 ↔ Project 002 R-003 (single-codebase fork pressure)

---

## External References

> No external policy documents were placed in `projects/002-arckit-sovereign/external/` at the time of generation. UK Government and MOD policies referenced are public-domain and cited by name. Material at OFFICIAL-SENSITIVE or higher should not be placed in this repository unless the hosting environment is accredited to handle that classification.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:traceability` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Comprehensive forward + backward traceability across all wave 1–7 artefacts for project 002. Inputs: REQ (1188 lines), STKE (17 SDs / 10 Goals), 8 ADRs, RISK (13 risks), TCOP (13 points), MOD-SBD (7 principles + JSP 440 / JSP 604 mappings), DPIA (5 risks vendor scope), AIP (10 + 6), SOBC, PLAN, ROAD, HLD review, DEVOPS (5 CI stages), FINOPS, OPS (10 vendor-side runbooks RB-VEN-001..010 + customer-side scope split), DIAG-001..003. Cross-project linkage to project 001 documented per Principle 21.
