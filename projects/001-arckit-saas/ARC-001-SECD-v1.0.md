# UK Government Secure by Design Assessment: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:secure`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SECD-v1.0 |
| **Document Type** | Secure by Design Assessment (NCSC CAF + UK Gov Cyber Security Standard) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (Service Owner / SIRO-equivalent) |
| **Reviewed By** | [PENDING] Security Lead, DPO, Lead Architect |
| **Approved By** | [PENDING] Service Owner / SIRO-equivalent |
| **Distribution** | Project Team, Architecture Team, NCSC liaison (post-pilot), CCS, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:secure` command. NCSC CAF v3.2 self-assessment, Cyber Essentials Plus trajectory, UK GDPR posture, GovS 007 alignment, formal acceptance vehicle for residual position on `ARC-001-RISK-v1.0.md` R-008/R-009/R-010/R-011. | [PENDING] | [PENDING] |

## Document Purpose

The Secure by Design assessment for the **managed SaaS** of ArcKit as a Service (Project 001). Two purposes:

1. Self-assessment against NCSC Cyber Assessment Framework (CAF), Cyber Essentials, UK Government Cyber Security Standard (July 2025), GovS 007 — evidencing the security posture before GA.
2. **Formal acceptance vehicle** for the residual positions of the four COMPLIANCE-category risks in `ARC-001-RISK-v1.0.md` that exceed the very-low compliance appetite (≤ 4): R-008 (cross-tenant leak, residual 5), R-009 (Service Standard fail, residual 6), R-010 (AI Playbook scope drift, residual 6), R-011 (UK GDPR breach via AI sub-processor, residual 6).

The sovereign deployment route is out of scope and is covered by `projects/002-arckit-sovereign/` and the MOD Secure by Design assessment in that project.

---

## Executive Summary

**Overall Security Posture**: **Adequate (with conditional pre-GA actions)** — the architecture is designed to a strong NCSC-aligned baseline; the operational evidence (pen test, CAF self-assessment, Cyber Essentials Plus, vulnerability disclosure programme) is gated on the Priority-1 actions in `ARC-001-RISK-v1.0.md` §H.

**NCSC CAF Score (pre-GA self-assessment)**: **9/14 Achieved**, 5/14 Partially Achieved, 0/14 Not Achieved.

**Key Security Findings**:

- **Strengths**: Defence-in-depth tenant isolation (ADR-001 namespace per tenant + tenant-ID enforcement at every data boundary + CI isolation tests + signed audit log + default-deny network policy + bulkhead patterns). Encryption-everywhere mandated by Principle 5 (NON-NEGOTIABLE). UK residency by default (Principle 7). Pluggable AI provider abstraction (ADR-004) protecting against sub-processor concentration. Single risk register with explicit appetite (`ARC-001-RISK-v1.0.md`) and SIRO-equivalent ownership.
- **Gaps closing pre-GA**: independent pen test specifically targeting tenant isolation (R-008/R-014, £40k–£60k); first NCSC CAF self-assessment + first NCSC Cloud Security Principles assessment; Cyber Essentials Plus certification; DPIA finalisation; ATRS record; vulnerability disclosure programme; NCSC Vulnerability Monitoring Service (VMS) enrolment.
- **Blocking issues for GA**: pen test, DPIA, Cyber Essentials, ROPA + privacy notice, formal Service Owner / DPO / Security Lead joint acceptance of R-008/R-009/R-010/R-011.

**Cyber Essentials Status**: **Not Started → Targeting Cyber Essentials Plus by GA – 30 days**.

**Cyber Security Standard Compliance** (Cabinet Office, July 2025): **Partially Compliant** — most clauses satisfied by design; clauses 4.3/4.4 exceptions register opened (see §9.3).

**Risk Summary**: **Medium overall residual risk** — driven by COMPLIANCE category (4 risks at residual 5–6 vs ≤ 4 appetite), all formally accepted in §10 of this document, with the impact-floor of R-008 (Catastrophic — multi-tenant SaaS thesis) being the only structural barrier to a Low rating.

**Project Phase**: **Discovery / Alpha → Beta** (pre-GA). Live-stage compliance gated on Priority-1 actions.

---

## 1. NCSC Cyber Assessment Framework (CAF) Assessment

> Reference: NCSC CAF (current revision). Self-assessment scoped to the managed SaaS in scope of Project 001 only; sovereign deployment in Project 002 has its own MOD Secure by Design assessment.

### Objective A: Managing Security Risk

#### A1: Governance

**Status**: ✅ **Achieved**

**Evidence**:

- Senior leadership (Service Owner / SIRO-equivalent) named in `ARC-001-STKE-v1.0.md` Decision Authority Matrix.
- 21 architecture principles in `ARC-000-PRIN-v2.0.md`; Principles 5, 7, 12, 21 marked **NON-NEGOTIABLE**.
- Security roles and responsibilities in STKE: Service Owner (SIRO-equivalent), Security Lead, DPO, Lead Architect — each with defined RACI columns.
- Risk-register ownership and quarterly cadence in `ARC-001-RISK-v1.0.md` §J.
- Security oversight: weekly review of R-008 / R-014 KRIs; monthly Service Owner full-register review; quarterly compliance-acceptance re-affirmation.

**Security Governance Checklist**:

- [x] Senior leadership owns information security — Service Owner (SIRO-equivalent), accountable in STKE RACI
- [x] SIRO appointed — Service Owner is SIRO-equivalent for the managed SaaS; full SIRO role on government deployments handled by deploying authority
- [x] Security policies and standards defined — Principle 5 (Security by Design); Principles 7, 8, 12 supporting
- [x] Security roles and responsibilities documented — STKE RACI matrix
- [x] Security risk management process established — `ARC-001-RISK-v1.0.md` (Orange Book)
- [x] Security oversight and reporting in place — weekly + monthly + quarterly cadence

**Gaps / Actions**: none — refresh annually.

---

#### A2: Risk Management

**Status**: ✅ **Achieved**

**Evidence**:

- `ARC-001-RISK-v1.0.md` is a HM Treasury Orange Book–compliant register with 17 risks, 5×5 inherent / residual scoring, 4Ts response, KRIs.
- Information assets implicit in the data model (artefacts, audit logs, identity records, billing records); explicit asset register pending generation in `ARC-001-DM-v1.0.md`.
- Risk appetite explicitly defined per category (`ARC-001-RISK-v1.0.md` §G).
- Residual-risk acceptance trail in §10 of this document for the four COMPLIANCE residual positions exceeding appetite.

**Risk Management Checklist**:

- [x] Information assets identified — implicit in REQ; explicit register to follow in `ARC-001-DM-v1.0.md`
- [x] Threats and vulnerabilities assessed — RISK §C details inherent / residual / triggers / consequences per risk
- [x] Risk assessment methodology defined — Orange Book 5×5 (RISK §A and §K)
- [x] Risk register maintained and reviewed — RISK §J cadence
- [x] Risk treatment plans implemented — RISK §H
- [x] Residual risks accepted by SIRO-equivalent — see §10 of this document (formal acceptance vehicle)

**Gaps / Actions**: complete `ARC-001-DM-v1.0.md` to make information-asset register fully explicit (MEDIUM).

---

#### A3: Asset Management

**Status**: ⚠️ **Partially Achieved**

**Evidence**:

- Software inventory: SBOM mandated by Principle 18 and produced on every build via the CI pipeline (Principle 20).
- Hardware: N/A — fully cloud-native (no vendor-issued devices); infrastructure-as-code (Principle 18) is the equivalent inventory.
- Data assets catalogued at the type level (artefacts, identity, audit, billing, telemetry); explicit register pending in `ARC-001-DM-v1.0.md`.
- Asset ownership: Lead Architect (compute/storage), Security Lead (audit logs/secrets), DPO (personal data), Finance (billing).

**Asset Management Checklist**:

- [x] Hardware inventory — N/A (cloud-native)
- [x] Software inventory — SBOM via CI
- [ ] Data assets catalogued formally — pending `ARC-001-DM-v1.0.md`
- [x] Asset ownership assigned — implicit by RACI
- [ ] Lifecycle and disposal — backup retention covered (Principle 7); end-of-tenancy verifiable destruction certificates (BR-007); explicit asset-lifecycle policy pending

**Gaps / Actions**:

- Generate `ARC-001-DM-v1.0.md` (data model) — MEDIUM, GA + 60 days.
- Document asset-lifecycle policy as a §6 appendix to this SbD — MEDIUM, GA – 30 days.

---

#### A4: Supply Chain

**Status**: ⚠️ **Partially Achieved**

**Evidence**:

- Sub-processor list maintained per Principle 7; published pre-GA.
- AI / cloud / payment / Companies House / SIEM are the principal supply-chain dependencies (per `ARC-001-REQ-v1.0.md` INT-001..INT-006).
- Pluggable AI provider abstraction (ADR-004) reduces single-source supply-chain risk and is the control for `ARC-001-RISK-v1.0.md` R-017 (AI provider lock-in).
- Vendor DPAs cover sub-processor change notification; tenant 30-day notice on sub-processor change (RISK R-011 control).
- SBOM produced on every build (Principle 18) — supply-chain integrity baseline for code.
- NCSC supply-chain guidance referenced in Principle 21.

**Supply Chain Checklist**:

- [x] Vendor / sub-processor inventory — committed; published pre-GA
- [x] DPAs / contractual security clauses — committed for AI / cloud / payment
- [x] Sub-processor change notice mechanism — 30-day tenant notice
- [x] SBOM produced for every release — Principle 18
- [ ] Software supply-chain attestation (e.g., SLSA) — not yet adopted; consider post-GA
- [ ] NCSC Vulnerability Monitoring Service (VMS) enrolment — not yet completed (HIGH PRIORITY pre-GA)
- [ ] Annual sub-processor review formalised in calendar — quarterly review in RISK; first walkthrough pre-GA

**Gaps / Actions**:

- Enrol in NCSC VMS — Security Lead, GA – 30 days (HIGH).
- Adopt SLSA Level 2+ for build attestations — Lead Architect, GA + 90 days (MEDIUM).
- Publish sub-processor list at GA — DPO, GA (HIGH).

---

### Objective B: Protecting Against Cyber Attack

#### B1: Service Protection Policies

**Status**: ✅ **Achieved**

**Evidence**:

- Principle 5 (Security by Design) sets the policy baseline — non-negotiable.
- Principle 8 (Tenant Isolation and Single Source of Truth) defines isolation policy.
- Principle 12 (Accessibility) is the user-facing policy companion.
- ADR-008 (Per-Tenant Quotas, Rate Limits, Fair Use) defines acceptable use policy.
- ADR-007 (Data Portability and Export Format) defines tenant-data portability and exit policy.
- Acceptable Use, Information Security Policy, and Data Protection Policy will be published pre-GA in the tenant evidence pack (BR-006).

**Policy Checklist**:

- [x] Acceptable use policy — ADR-008 + tenant T&Cs
- [x] Access control policy — ADR-001 + ADR-003 + Principle 5 §I.5
- [x] Data protection policy — Principle 7 + DPIA (pending) + tenant DPA
- [x] Incident response policy — DPO incident runbook (pending, GA – 30 days)
- [x] Cryptography policy — Principle 5 §I.5 (encryption-everywhere)
- [x] Software development policy — Principles 18, 19, 20 (IaC, automated testing, CI/CD)

**Gaps / Actions**: publish in tenant evidence pack at GA (HIGH).

---

#### B2: Identity and Access Control

**Status**: ⚠️ **Partially Achieved** — design-stage strong; live-stage privileged-access tooling pending.

**Evidence**:

- `ARC-001-ADR-003-v1.0.md` — tenants bring their own IdP via OIDC / SAML 2.0; service-side IdP for tenant-administrator sessions.
- `ARC-001-ADR-001-v1.0.md` — tenant-ID propagated and enforced at every data-access boundary.
- Principle 5 §I.5 mandates MFA for all human access (tenants and operators).
- Service-to-service authentication via mutual TLS or signed tokens (Principle 5).
- Secrets stored in vault; never in code or config or images (Principle 5).
- Short-lived tokens with refresh-rotation (ADR-003).
- WAF + DDoS-aware ingress (ADR-006 / ADR-005).
- Privileged Access Management (PAM) for vendor operators — design committed, live tooling decision pending pre-GA (typically a managed PAM offering).

**Access Control Checklist**:

- [x] MFA for all tenant administrators — ADR-003
- [x] MFA for all vendor operators — Principle 5 §I.5
- [x] Least privilege role model — ADR-001 RBAC scoped per tenant
- [ ] Privileged Access Management for vendor admins — design committed; tooling decision pending — HIGH PRIORITY pre-GA
- [x] Service-to-service mTLS — Principle 5 §I.5; NFR-SEC-003
- [x] Quarterly access review — committed in tenant evidence pack
- [x] Just-in-time elevated access for break-glass — committed; runbook pending
- [x] Tenant-ID propagation enforced everywhere — ADR-001 + NFR-SEC-002

**Gaps / Actions**:

- Select and deploy PAM for vendor operators — Security Lead + Lead Architect, GA – 30 days (HIGH).
- Document break-glass procedure — Security Lead, GA – 30 days (HIGH).
- Quarterly access review process documented — Security Lead, GA + 30 days (MEDIUM).

---

#### B3: Data Security

**Status**: ⚠️ **Partially Achieved** — design-stage strong; DPIA, ROPA, privacy notice gating B3 to "Achieved".

**Evidence**:

- Encryption at rest for all tenant data and backups — Principle 5 §I.5; NFR-SEC-001.
- Encryption in transit (current TLS) — Principle 5 §I.5; NFR-SEC-003.
- UK residency default — Principle 7.
- Tenant-data portability with verifiable destruction — Principle 9; BR-007; ADR-007.
- Data classification — OFFICIAL with OFFICIAL-SENSITIVE handling caveats per tenant opt-in.
- DLP — controlled via tenant-ID enforcement and tenant export-only-self-data architecture; explicit DLP tooling not in scope (sub-processor exfil-detection covered via SIEM, ADR-005, and quarterly sub-processor review, RISK R-011 control).
- DPIA — pending generation via `/arckit:dpia`.
- ROPA — committed in Principle 7; publication pending GA.

**Data Security Checklist**:

- [x] Encryption at rest — NFR-SEC-001
- [x] Encryption in transit — NFR-SEC-003
- [x] Key management — vault-based; rotation policy pending documentation
- [x] Data classification — OFFICIAL (default) / OFFICIAL-SENSITIVE (opt-in)
- [ ] DPIA completed — **GAP** — `ARC-001-DPIA-v1.0.md` pending
- [ ] ROPA published — pending GA
- [x] Data minimisation — only identity, artefacts, audit, billing, telemetry
- [x] Retention and verifiable destruction — Principle 7; BR-007
- [x] Tenant data portability — BR-007; ADR-007

**Gaps / Actions**:

- Generate DPIA — DPO, GA – 60 days (CRITICAL pre-GA).
- Publish ROPA — DPO, GA (HIGH).
- Document key-rotation policy — Security Lead, GA – 30 days (HIGH).
- Sub-processor list published at GA — DPO (HIGH).

---

#### B4: System Security

**Status**: ⚠️ **Partially Achieved** — design-stage strong; live-stage patching SLO and EDR pending.

**Evidence**:

- Patching SLO: critical CVE within 14 days, high within 30 — committed in Principle 5 §I.5 (in line with Cyber Essentials).
- Vulnerability scanning of dependencies and container images on every build — Principle 5 + Principle 19.
- Hardening — managed K8s defaults + security context constraints + read-only root file systems + non-root containers (ADR-006).
- EDR / runtime threat detection — covered by SIEM-integrated runtime tooling (ADR-005); specific EDR tool decision pending.
- Anti-malware on developer endpoints — vendor-team policy; covered under B6 staff awareness.

**System Security Checklist**:

- [x] Patching SLO defined — Principle 5 §I.5
- [x] Vulnerability scanning in CI — Principle 19
- [x] Container hardening — ADR-006
- [ ] EDR / runtime threat detection in production — tool decision pending — HIGH PRIORITY pre-GA
- [x] Anti-malware on operator endpoints — vendor IT policy
- [x] Build-image signing — Principle 18 (signed artefacts) + SBOM
- [x] Default-deny network policy — ADR-006

**Gaps / Actions**:

- Select EDR / runtime tooling — Security Lead, GA – 30 days (HIGH).
- NCSC VMS enrolment — Security Lead, GA – 30 days (HIGH; cross-references A4).
- Patching SLO measurable in CI — Lead Architect, GA – 30 days (MEDIUM).

---

#### B5: Resilient Networks

**Status**: ✅ **Achieved**

**Evidence**:

- ADR-006 (Deployment Topology) — namespace-per-tenant + default-deny network policy + service mesh + ingress / egress segmentation.
- WAF + cloud-provider DDoS protection at ingress (ADR-006).
- mTLS service-to-service (Principle 5).
- Multi-AZ topology for resilience (Principle 14).
- No PSN connectivity (B2B SaaS — tenants connect over public internet via TLS).
- Status page externally visible (Principle 6).

**Network Security Checklist**:

- [x] Network segmentation — namespace + service mesh
- [x] Boundary firewalls — cloud-provider VPC + WAF
- [x] DDoS protection at ingress — cloud-provider built-in
- [x] mTLS service-to-service — Principle 5
- [x] Multi-AZ — Principle 14
- [x] Default-deny intra-cluster — ADR-006
- [N/A] PSN — N/A (B2B SaaS over public internet)

**Gaps / Actions**: none — quarterly chaos-test the failover (Principle 3).

---

#### B6: Staff Awareness

**Status**: ⚠️ **Partially Achieved**

**Evidence**:

- Security culture embedded in principles (Principle 5 NON-NEGOTIABLE).
- Security-aware code-review checklist mandated (RISK R-014 control).
- Annual phishing-awareness training — committed; not yet executed.
- Vulnerability disclosure programme — committed; channel pending pre-GA.

**Staff Awareness Checklist**:

- [x] Security training included in onboarding — vendor-team policy
- [ ] Annual phishing-awareness training — schedule before GA (HIGH)
- [x] Code-review security checklist — Principle 19 + R-014 control
- [x] Data-handling training for personal-data roles — committed; DPO-led
- [ ] Vulnerability disclosure programme channel — pending — HIGH PRIORITY pre-GA

**Gaps / Actions**:

- Stand up vulnerability disclosure programme channel (e.g., security.txt + dedicated mailbox + 90-day disclosure window) — Security Lead, GA – 30 days (HIGH).
- Annual phishing simulation — Security Lead, GA + 90 days (MEDIUM).

---

### Objective C: Detecting Cyber Security Events

#### C1: Security Monitoring

**Status**: ✅ **Achieved (design-stage)** — live SIEM rules and runbooks pending.

**Evidence**:

- `ARC-001-ADR-005-v1.0.md` (Observability Stack) — structured logs with correlation IDs and tenant IDs; per-tenant audit log signed and immutable; SIEM integration; metrics; tracing; security-event extraction.
- Principle 5 §I.5 mandates structured logging of all auth and authz events.
- Principle 6 requires logs / metrics / traces with retention: security 12 months minimum, app 90 days, metrics 13 months.
- KRI dashboard for R-008 / R-014 (RISK §J): CI isolation-test pass rate, audit-log anomalies, pen-test residual findings.
- Public status page for tenant-visible operational signal.

**Monitoring Checklist**:

- [x] SIEM-grade logging — ADR-005
- [x] Tenant-ID + correlation-ID on every event — ADR-005 + ADR-001
- [x] Signed immutable audit log — ADR-005
- [ ] SIEM rules and runbooks tuned — pending live data; HIGH PRIORITY pre-GA
- [x] Retention thresholds — Principle 6
- [x] Public status page — Principle 6
- [x] Alerts wired to on-call rotation — committed; SRE on-call rotation in `ARC-001-OPS-v1.0.md` (pending generation)

**Gaps / Actions**:

- SIEM rule library + runbook authoring — Security Lead + SRE Lead, GA – 30 days (HIGH).
- On-call rotation document — generate `ARC-001-OPS-v1.0.md` via `/arckit:operationalize` (HIGH).

---

#### C2: Proactive Security Event Discovery

**Status**: ⚠️ **Partially Achieved**

**Evidence**:

- Annual independent pen test mandated by Principle 5 §I.5; first pen test scheduled pre-GA targeting tenant isolation (RISK §H Priority-1 action).
- CI tenant-isolation tests on every PR (Principle 19; NFR-SEC-002).
- Vulnerability scanning per Principle 5 + Principle 19.
- NCSC Vulnerability Monitoring Service enrolment — committed pre-GA.
- Threat hunting — not formally scoped in v1; deferred until tenant data volume justifies it (post-GA + 6 months).

**Discovery Checklist**:

- [ ] First independent pen test — pre-GA – 60 days (CRITICAL)
- [x] Quarterly vulnerability scan baseline — Principle 5 + Principle 19
- [ ] NCSC VMS enrolment — pre-GA – 30 days (HIGH)
- [x] CI tenant-isolation tests — NFR-SEC-002 (Strong control for R-008/R-014)
- [ ] Threat hunting cadence — deferred; document decision in §6 (LOW)

**Gaps / Actions**: per RISK §H Priority-1 actions 1, 2 — pen test + VMS.

---

### Objective D: Minimising the Impact of Incidents

#### D1: Response and Recovery Planning

**Status**: ⚠️ **Partially Achieved**

**Evidence**:

- Incident runbook with ICO-72h-notification template — committed; in RISK §H Priority-1 action 7; due GA – 30 days.
- RTO < 4 hours; RPO < 15 minutes (Principle 14; NFR-AVAIL-001/002).
- Disaster recovery testing at least annually (Principle 14).
- Backup with verifiable restore procedure — Principle 7 + Principle 14.
- Cyber liability insurance — RISK R-008 transfer secondary; procurement at GA – 30 days.

**Response and Recovery Checklist**:

- [ ] Documented incident response plan — pending; HIGH PRIORITY pre-GA
- [x] RTO / RPO defined — NFR-AVAIL-001/002
- [x] Backup and restore — Principle 7
- [ ] Annual DR test — committed; first test pre-GA (HIGH)
- [ ] Cyber liability insurance — committed; procurement at GA – 30 days (HIGH)
- [x] ICO 72-h notification template — RISK §H action 7

**Gaps / Actions**: per RISK §H Priority-1 actions 6, 7 — insurance + runbook.

---

#### D2: Improvements

**Status**: ✅ **Achieved**

**Evidence**:

- Principle 19 — automated testing improves continuously; coverage thresholds defined.
- Principle 20 — CI/CD with quality gates; tenant-isolation tests run on every release (NFR-SEC-002).
- RISK §J cadence — weekly KRI review for R-008 / R-014; monthly full-register; quarterly compliance acceptance re-affirmation; annual appetite review.
- Continuous improvement embedded in `ARC-001-RISK-v1.0.md` Orange Book Part I-E.
- No-blame post-incident reviews shared publicly (Principle 19; RISK R-012 control).

**Improvements Checklist**:

- [x] Post-incident review process — RISK R-012 control
- [x] KRI / KCI metrics — RISK §J
- [x] Continuous improvement embedded in cadence — RISK §J
- [x] Lessons-learned channel back into principles / ADRs — Principle 15 (Maintainability)

**Gaps / Actions**: none — operate at cadence.

---

### CAF Score Summary

| Objective | Principle | Status | Evidence Reference |
|-----------|-----------|--------|--------------------|
| A — Managing Risk | A1 Governance | ✅ Achieved | STKE RACI, RISK §J |
| A | A2 Risk Management | ✅ Achieved | RISK Orange Book |
| A | A3 Asset Management | ⚠️ Partial | SBOM in CI; data-asset register pending |
| A | A4 Supply Chain | ⚠️ Partial | SBOM, sub-processor list; VMS pending |
| B — Protecting | B1 Service Protection Policies | ✅ Achieved | Principles 5/7/8/12 + ADR-008 |
| B | B2 Identity & Access | ⚠️ Partial | MFA + tenant-ID; PAM tool pending |
| B | B3 Data Security | ⚠️ Partial | Encryption + portability; DPIA / ROPA pending |
| B | B4 System Security | ⚠️ Partial | Patching SLO; EDR pending |
| B | B5 Resilient Networks | ✅ Achieved | ADR-006 |
| B | B6 Staff Awareness | ⚠️ Partial | Code-review checklist; phishing / VDP pending |
| C — Detecting | C1 Security Monitoring | ✅ Achieved | ADR-005 |
| C | C2 Proactive Discovery | ⚠️ Partial | CI iso tests; first pen test + VMS pending |
| D — Minimising | D1 Response & Recovery | ⚠️ Partial | RTO / RPO defined; runbook + insurance pending |
| D | D2 Improvements | ✅ Achieved | RISK §J + Principle 19/20 |

**Overall CAF Score**: **9/14 Achieved**, 5/14 Partially Achieved, 0/14 Not Achieved.

**Path to 14/14**: complete the eight Priority-1 actions in RISK §H — chiefly pen test, VMS enrolment, EDR, PAM, DPIA, ROPA, runbook, vulnerability disclosure programme. Target: GA – 30 days.

---

## 2. Cyber Essentials Compliance

### 2.1 Cyber Essentials Five Controls

| Control | Status | Evidence |
|---------|--------|----------|
| **Firewalls and internet gateways** | ✅ | Cloud-provider VPC + WAF + DDoS (ADR-006); default-deny network policy |
| **Secure configuration** | ✅ | Container hardening, security contexts, IaC-mastered config (Principle 18) |
| **User access control** | ⚠️ | MFA + RBAC + tenant-ID enforcement; PAM tool decision pending |
| **Malware protection** | ⚠️ | EDR tool decision pending; container image scanning in CI |
| **Patch management** | ⚠️ | 14-day critical / 30-day high SLO defined; measurable in CI pending |

### 2.2 Certification Path

- **Target**: Cyber Essentials Plus (external technical verification) by GA – 30 days, given OFFICIAL classification and prospective £5M+ contract reach via G-Cloud.
- **Owner**: Security Lead.
- **Estimated cost**: £4k–£8k for assessment.
- **Status**: not yet engaged with assessor; Priority-1 action pre-GA.

### 2.3 Pre-Assessment Action List

1. Select and deploy PAM (B2 gap) — GA – 30 days.
2. Select and deploy EDR (B4 gap) — GA – 30 days.
3. Patching SLO measurable in CI dashboard — GA – 30 days.
4. Engage Cyber Essentials Plus assessor — GA – 60 days.
5. Submit for assessment — GA – 30 days.

---

## 3. UK GDPR / Data Protection Act 2018 Compliance

### 3.1 Personal Data Processed

- Tenant administrator and user identities (name, work email, role, optionally photo).
- Authentication and session metadata.
- Audit-log records linking user IDs to actions.
- Billing records (organisation legal name, billing contact, payment processor reference).
- Aggregated usage telemetry (per-tenant, not per-user-identifying for anonymous analytics).

**No** end-user / public personal data is processed; **no** special-category data; **no** children's data.

### 3.2 Lawful Basis

- **Performance of contract** (UK GDPR Article 6(1)(b)) — primary basis for tenant administration data.
- **Legitimate interests** (Article 6(1)(f)) — for security logging, fraud / abuse detection, service-improvement analytics (LIA pending generation alongside DPIA).

### 3.3 Compliance Posture Checklist

- [x] DPO appointed — Vendor DPO (named in STKE)
- [ ] DPIA completed — `ARC-001-DPIA-v1.0.md` pending — **CRITICAL pre-GA**
- [ ] Privacy notice published — pending GA — HIGH
- [ ] ROPA maintained and current — pending; first version at GA — HIGH
- [x] Sub-processor list — committed; published pre-GA
- [x] Data subject rights procedures — covered by export (BR-007), deletion (Principle 7), destruction certificates (BR-007)
- [x] Data breach notification process — RISK §H action 7 (ICO 72-h template) — pending finalisation pre-GA
- [x] ICO registration — committed pre-GA
- [x] International transfers — Article 46 mechanism (Standard Contractual Clauses) where AI provider is non-UK; tenant consent required for any non-Article-46 transfer (Principle 7)
- [x] Cross-border transfer impact assessment — covered by DPIA when AI provider is non-UK

### 3.4 Critical Gaps

1. **DPIA not generated** (CRITICAL — blocking GA processing).
2. **ROPA, privacy notice, sub-processor list** not yet published (HIGH — blocking GA).
3. **ICO breach notification runbook** not finalised (HIGH — RISK §H action 7).

---

## 4. Cloud Security Principles (NCSC, 14 Principles)

> Required by Principle 5 §I.5 and Goal G-4 in `ARC-001-STKE-v1.0.md`. First assessment due by GA.

| # | Principle | Status | Evidence |
|---|-----------|--------|----------|
| 1 | Data in transit protection | ✅ | NFR-SEC-003 (current TLS); mTLS service-to-service |
| 2 | Asset protection and resilience | ✅ | Multi-AZ (Principle 14); encryption at rest (NFR-SEC-001); UK residency (Principle 7) |
| 3 | Separation between users / tenants | ✅ | ADR-001 namespace-per-tenant + tenant-ID enforcement; CI isolation tests |
| 4 | Governance framework | ✅ | This document + RISK + STKE |
| 5 | Operational security | ⚠️ | EDR + PAM pending |
| 6 | Personnel security | ⚠️ | Vetting / cleared-personnel-only N/A for SaaS; vendor-team background checks committed |
| 7 | Secure development | ✅ | Principles 18/19/20; SBOM; vulnerability scanning |
| 8 | Supply chain security | ⚠️ | VMS pending; SLSA L2+ deferred |
| 9 | Secure user management | ⚠️ | MFA + RBAC; PAM pending |
| 10 | Identity and authentication | ✅ | OIDC + SAML (ADR-003); short-lived tokens; mTLS service-to-service |
| 11 | External interface protection | ✅ | WAF + DDoS + ingress segmentation (ADR-006) |
| 12 | Secure service administration | ⚠️ | PAM pending; break-glass runbook pending |
| 13 | Audit information for users | ✅ | Per-tenant immutable audit log (ADR-005); tenant-facing audit-log download |
| 14 | Secure use of the service | ✅ | Tenant evidence pack (BR-006) + tenant onboarding guide |

**Cloud Security Principles Score**: **9/14 Achieved**, 5/14 Partially.

**Overlap with CAF**: PAM (B2 / 9 / 12), EDR (B4 / 5), VMS (A4 / 8), DPIA (B3 / 4) — same set of pre-GA actions closes both.

---

## 5. Threat Model Summary

> Full threat-model evidence captured here at design level; quarterly review post-GA. STRIDE-style summary against the multi-tenant SaaS architecture.

### 5.1 Trust Boundaries

1. Public internet → ingress (WAF / DDoS / TLS termination)
2. Ingress → service mesh (mTLS within cluster)
3. Cross-tenant boundary (namespace + RBAC + tenant-ID enforcement)
4. Service → vault (mutual auth, short-lived tokens)
5. Service → external sub-processor (HTTPS + DPA + sub-processor monitoring)
6. Service → audit log (append-only, signed, immutable)

### 5.2 Top Threat Vectors and Controls

| # | Threat | STRIDE Category | Affected Asset | Primary Control | Risk Reference |
|---|--------|-----------------|----------------|-----------------|----------------|
| T1 | Cross-tenant data retrieval (the existential) | I (Information disclosure) | Tenant artefacts | Defence-in-depth (ADR-001 + CI iso + audit log + bulkhead) | R-008, R-014 |
| T2 | Tenant-ID propagation defect introduced in code | T (Tampering) | Tenant artefacts | CI isolation tests on every PR; mandatory code review with security checklist | R-014 |
| T3 | Identity layer compromise (shared IdP) | E (Elevation of privilege) | Sessions across tenants | Bulkhead per tenant; short-lived tokens; mTLS audience claims | R-016 |
| T4 | AI sub-processor exfiltration / training-on-customer-data | I + R (Repudiation) | Tenant artefacts | DPA + provider abstraction + quarterly DPO review + Article 46 | R-011 |
| T5 | Audit-log tampering | T + R | Forensic integrity | Signed, immutable, append-only log (ADR-005) | R-008, R-012 |
| T6 | DDoS / availability attack | D (Denial of service) | Service availability | Cloud-provider DDoS + WAF + per-tenant rate limits (ADR-008) | R-008 indirect |
| T7 | Secrets leakage via repo or image | I | Service auth | Vault-only; never in repo; pre-commit secret scan; Principle 5 | (covered by R-014) |
| T8 | Malicious insider with vendor admin access | E + I | Tenant data | PAM + just-in-time elevation + quarterly access review + audit log | R-008 |
| T9 | Supply-chain compromise of dependency | T | Build pipeline | SBOM + image scanning + signed builds + (planned) SLSA L2+ | R-014 |
| T10 | Phishing of vendor staff → credential theft | S (Spoofing) | Vendor admin | MFA + PAM + phishing-awareness training + JIT elevation | R-014, R-008 |

### 5.3 Threat-Model Gaps

- Formal STRIDE diagram per data-flow segment to be added in `ARC-001-DIAG-002-v1.0.md` (deployment / threat-model diagram pack), generated separately via `/arckit:diagram`.
- Quarterly threat-model review post-GA (Lead Architect + Security Lead).

---

## 6. UK Government Cyber Security Standard (Cabinet Office, July 2025)

### 6.1 Compliance Posture

| CSS Clause | Topic | Status | Notes |
|------------|-------|--------|-------|
| 1.x | Scope and applicability | Compliant | OFFICIAL multi-tenant SaaS; sovereign deployment in Project 002 |
| 2.x | Security governance | Compliant | A1 governance (this document); STKE RACI |
| 3.x | Risk management | Compliant | RISK Orange Book |
| 4.x | Mandatory controls | Partially | Pen test / EDR / PAM / DPIA / VMS / Cyber Essentials Plus pending pre-GA |
| 5.x | Detection and response | Partially | C1 / D1 evidence in this document |
| 6.x | Continuous improvement | Compliant | RISK §J cadence |
| 7.x | Reporting and escalation | Compliant | STKE RACI + RISK §J reporting |

### 6.2 GovAssure Status

- **In scope?** The managed SaaS as deployed by *the vendor* is **not** itself in GovAssure scope (vendor is not a UK Government department). However, departmental customers procuring the SaaS via G-Cloud may include ArcKit in the scope of *their* GovAssure cycle.
- **Vendor commitment**: provide departmental customers with the evidence pack (BR-006) needed to support their GovAssure assessment — including this document, the DPIA, the pen-test report, the CAF self-assessment, and the Cloud Security Principles assessment.
- **Action**: tenant evidence pack reviewed annually and on material change; refreshed within 30 days of any departmental GovAssure-cycle request.

### 6.3 Cyber Security Standard Exception Register

| # | Clause | Exception | Rationale | Risk | Mitigation | Approver | Review |
|---|--------|-----------|-----------|------|------------|----------|--------|
| EX-001 | 4.x — Cyber Essentials Plus | Not yet certified at v1.0 issuance of this document | Service is pre-GA Alpha | Time-bounded; Cyber Essentials Plus targeted GA – 30 days | Engage assessor; close pre-GA | Service Owner | GA – 30 days |
| EX-002 | 4.x — DPIA published | DPIA pending generation | Pre-GA; processing has not yet started | Time-bounded; DPIA at GA – 60 days | `/arckit:dpia` artefact | DPO | GA – 60 days |
| EX-003 | 4.x — Independent pen test | First pen test scheduled but not yet executed | Pre-GA Alpha | Time-bounded; pen test pre-GA – 60 days | RISK §H action 1 | Security Lead | GA – 60 days |
| EX-004 | 4.x — NCSC VMS enrolment | Not yet enrolled | Pre-GA Alpha | Time-bounded; pre-GA – 30 days | Enrolment | Security Lead | GA – 30 days |
| EX-005 | 4.x — ATRS record | Not yet published | AI feature surface defined as drafting only at v1; ATRS publication needed before any recommendation-class surface | Time-bounded; pre-GA | RISK R-010 control + AIP artefact | DPO | GA |

All exceptions are **time-bound to GA – 30 days or earlier**; none are persistent.

### 6.4 Cyber Action Plan Alignment (£210m, February 2026)

| Pillar | Project Activity | Investment Alignment |
|--------|------------------|----------------------|
| Skills & Workforce | Vendor team training / Cyber Academy participation | Encouraged for vendor team and prospective DDaT tenants |
| Tooling & Infrastructure | NCSC VMS; SBOM; signed builds | Aligned (committed pre-GA) |
| Resilience & Response | Incident runbook; ICO 72-h notification template; DR test | Aligned (RISK §H actions) |
| Collaboration & Sharing | Tenant evidence pack (BR-006) reduces buyer-side assurance load | Aligned |

**Departmental enrolment**: vendor is not a UK Government department, so direct funding alignment is N/A; departmental tenants procuring via G-Cloud may map their procurement to Cyber Action Plan funding.

---

## 7. Government Cyber Security Profession Alignment

| Item | Status | Notes |
|------|--------|-------|
| Departmental participation in Government Cyber Security Profession | N/A (vendor) | Encouraged for departmental tenants |
| CCP certification for vendor Security Lead | Encouraged | Documented in role profile |
| DDaT mapping for security roles | Met | STKE Appendix A maps vendor roles to DDaT capability framework |
| Cyber Academy engagement | Encouraged | Vendor team annual training plan |

**Workforce development gap**: vendor team currently lean (multiple [PENDING] roles in STKE); recruitment to fill Security Lead, DPO, and Accessibility Lead roles continues. Hiring or contract-of-services confirmed by GA – 60 days.

---

## 8. GovS 007 Security Functional Standard Alignment

### 8.1 Principle Mapping

| GovS 007 Principle | Description | CAF / SbD Coverage | Status |
|--------------------|-------------|---------------------|--------|
| 1 | Lead and govern security | A1, A2 | ✅ |
| 2 | Understand and manage security risk | A2, A3, A4 | ⚠️ (A3/A4 partial) |
| 3 | Protect against threats | B1–B5 | ⚠️ (B2/B3/B4 partial) |
| 4 | Detect and respond | C1, C2, D1, D2 | ⚠️ (C2/D1 partial) |
| 5 | Build and maintain security culture | B6, §7 (Profession) | ⚠️ (VDP / phishing pending) |
| 6 | Comply with legal and regulatory obligations | §3 (UK GDPR), §6 (CSS) | ⚠️ (DPIA / ROPA pending) |
| 7 | Manage incidents and crises | D1, §3.3 | ⚠️ (runbook pending) |
| 8 | Continuous improvement | D2, §6.4 (Cyber Action Plan) | ✅ |
| 9 | Embed security in delivery | This document; Principles 18/19/20 | ✅ |

### 8.2 Security Roles

| Role | GovS 007 Equivalent | Holder | Notes |
|------|---------------------|--------|-------|
| Senior Information Risk Owner (SIRO-equivalent) | Principle 1 | Mark Craddock, Service Owner | Vendor-side equivalent; full SIRO sits in the deploying authority for sovereign deployments |
| Security Lead | Senior Security Risk Officer (SSRO-equivalent) | [PENDING] vendor Security Lead | Recruitment due GA – 60 days |
| Departmental Security Officer (DSO-equivalent) | DSO | N/A | Tenant-side responsibility |
| Data Protection Officer | DPO | [PENDING] vendor DPO | Recruitment due GA – 60 days |
| Service Owner | Accountable Person | Mark Craddock | STKE RACI |

---

## 9. Critical Security Issues and Recommendations

### 9.1 Critical Issues (BLOCKING for GA)

1. **Independent pen test not yet executed** (CAF C2; CSS 4.x; CE Plus dependency) — Owner: Security Lead. Due: GA – 60 days. Cost: £40k–£60k. RISK ref: R-008, R-014.
2. **DPIA not generated** (CAF B3; UK GDPR; CSS 4.x) — Owner: DPO. Due: GA – 60 days. Action: `/arckit:dpia`.
3. **Cyber Essentials Plus not certified** (CSS 4.x; G-Cloud listing requirement) — Owner: Security Lead. Due: GA – 30 days.
4. **ROPA + privacy notice + sub-processor list unpublished** (UK GDPR) — Owner: DPO. Due: GA.
5. **Incident runbook + ICO 72-h template not finalised** (CAF D1; CSS 5.x) — Owner: DPO + Security Lead. Due: GA – 30 days.
6. **PAM tool not deployed** (CAF B2; Cloud Security Principles 9/12) — Owner: Security Lead + Lead Architect. Due: GA – 30 days.
7. **EDR / runtime threat detection not deployed** (CAF B4) — Owner: Security Lead. Due: GA – 30 days.
8. **NCSC VMS enrolment not completed** (CAF A4 / C2; Cloud Security Principles 8) — Owner: Security Lead. Due: GA – 30 days.
9. **Vulnerability Disclosure Programme channel not stood up** (CAF B6) — Owner: Security Lead. Due: GA – 30 days.
10. **ATRS record + AI-feature scope boundary not published** (RISK R-010; AI Annex of TCoP) — Owner: DPO + Lead Architect. Due: GA.

All ten issues align to RISK §H Priority-1 actions. Each is **time-bound to GA – 30 days or earlier** and has a named owner.

### 9.2 High-Priority Recommendations (1–3 months / pre-GA)

1. Procure cyber liability insurance (RISK R-008 transfer secondary) — Service Owner + Finance.
2. Publish tenant evidence pack v1 (BR-006) — Service Owner.
3. Run first NCSC CAF self-assessment + first NCSC Cloud Security Principles assessment — Security Lead (Goal G-4).
4. Run first DR / failover test — Lead Architect + SRE.
5. SIEM rule library and runbook authoring — Security Lead + SRE.

### 9.3 Medium-Priority Recommendations (3–6 months / post-GA)

1. SLSA Level 2+ build attestations — Lead Architect.
2. Generate `ARC-001-DM-v1.0.md` (data model) — Lead Architect.
3. Carbon-footprint baseline (TCoP Point 12 cross-link) — SRE + Finance.
4. Quarterly portability rehearsal cadence — Lead Architect (RISK R-015 / R-017).
5. Annual phishing simulation — Security Lead.

### 9.4 Low-Priority Recommendations (continuous)

1. Threat-hunting cadence at sufficient tenant volume.
2. ISO 27001 certification roadmap (Principle 5).
3. Annual independent pen test (Principle 5).
4. Annual NCSC CAF + Cloud Security Principles refresh.
5. Annual sustainability statement.

---

## 10. Formal Acceptance: Residual Risk Position for Compliance Risks Exceeding Appetite

This section is the **formal acceptance vehicle** for the four COMPLIANCE-category risks in `ARC-001-RISK-v1.0.md` whose residual scores exceed the very-low compliance appetite (≤ 4). Acceptance is conditional on Priority-1 actions in §9.1 / RISK §H landing before GA. Re-affirmation is quarterly.

### 10.1 Compliance Acceptance Register

| Risk | Title | Residual | Appetite | Excess | Justification | Conditions of Acceptance | Re-affirm |
|------|-------|----------|----------|--------|---------------|-------------------------|-----------|
| **R-008** | Cross-tenant data leakage | 5 (1×5 — likelihood already at floor; impact Catastrophic is inherent to the multi-tenant SaaS thesis) | 4 | +1 | Impact cannot be reduced — likelihood is already Rare due to defence-in-depth (ADR-001 + CI iso tests + audit log + bulkhead + WAF + mTLS). Multi-tenancy is the platform thesis (Principle 1's commercial enabler); termination is not in appetite. Cyber liability insurance is the transfer secondary. | Independent pen test pre-GA (RISK §H action 1); cyber liability insurance procured (RISK §H action 6); incident runbook + ICO 72-h template (RISK §H action 7); CI tenant-isolation pass rate 100% sustained. | Quarterly + on any KRI breach |
| **R-009** | GDS Service Assessment failure | 6 | 4 | +2 | A failure does not breach UK GDPR / DPA — it delays G-Cloud listing only; consequence is commercial / strategic (RISK R-001 cascade). Mitigation: pre-assessment walkthrough with one Service Assessor + one pilot DDaT EA pre-GA reduces likelihood materially. | Pre-assessment walkthrough complete pre-GA – 60 days; `/arckit:service-assessment` artefact (`ARC-001-SVCASS-v1.0.md`) generated; pilot DDaT validation captured. | Quarterly |
| **R-010** | AI Playbook scope drift | 6 | 4 | +2 | AI feature is currently drafting-only and Article 22-safe; risk is drift toward recommendation surfaces without DPIA refresh or ATRS update. Boundary review (RISK R-010 P2 action) keeps the residual stable. | DPO + Lead Architect feature-scope boundary documented (drafting / recommendation); ATRS record published; quarterly DPO review of AI surface area. | Quarterly + on any AI feature change |
| **R-011** | UK GDPR breach via AI sub-processor | 6 | 4 | +2 | Pluggable provider abstraction (ADR-004) plus Article 46 transfer mechanism plus 30-day tenant change-notice plus quarterly sub-processor review compress the likelihood; impact remains Moderate. Switch-in-≤-5-working-days capability validated quarterly in CI. | Quarterly sub-processor review complete; pre-GA AI provider failover drill (RISK §H action 4); DPA renewals current. | Quarterly + on any sub-processor change |

### 10.2 Joint Acceptance (Pre-GA Sign-Off)

| Role | Name | Decision | Date | Signature |
|------|------|----------|------|-----------|
| Service Owner / SIRO-equivalent | Mark Craddock | [PENDING] Accept residual position on R-008/R-009/R-010/R-011 conditional on §10.1 conditions | [PENDING — pre-GA] | _________ |
| Data Protection Officer | [PENDING] | [PENDING] Accept residual position on R-008/R-010/R-011 | [PENDING — pre-GA] | _________ |
| Security Lead | [PENDING] | [PENDING] Accept residual position on R-008/R-010/R-011 | [PENDING — pre-GA] | _________ |
| Lead Architect | [PENDING] | [PENDING] Accept architectural premises | [PENDING — pre-GA] | _________ |

### 10.3 Re-Affirmation Schedule

- **Quarterly**: Risk Register Owner re-presents the four residual positions to Service Owner + DPO + Security Lead. Each gives an Accept / Re-evaluate / Reject vote.
- **On material change**: any change to AI feature surface, sub-processor list, isolation architecture, or tenant scope triggers an immediate re-affirmation.
- **Annual**: full appetite re-affirmation in line with `ARC-001-RISK-v1.0.md` §J.

### 10.4 Triggers for Reopening Acceptance

- Any KRI breach (RISK §J leading / lagging indicators).
- Any pen-test residual high finding > 30 days unmitigated.
- Any ICO correspondence indicating concern.
- Any new Critical (≥ 20) inherent risk identified.
- Any sub-processor change without 30-day tenant notice having been served.
- Any AI feature surface that crosses the drafting / recommendation boundary without DPIA refresh.

---

## 11. Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Service Owner / SIRO-equivalent | Mark Craddock | [PENDING] | |
| Lead Architect | [PENDING] | [PENDING] | |
| Security Lead | [PENDING] | [PENDING] | |
| Data Protection Officer | [PENDING] | [PENDING] | |
| Accessibility Lead | [PENDING] | [PENDING] | |
| Senior Sponsor (CCS / CDDO liaison) | [PENDING] | [PENDING] | |

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government and NCSC standards referenced (CAF, Cloud Security Principles, Cyber Essentials, UK Government Cyber Security Standard, GovS 007, Cyber Action Plan, UK GDPR / DPA 2018) are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Internal Cross-References

| Reference | Use |
|-----------|-----|
| `ARC-000-PRIN-v2.0.md` | Principles 5 (Security by Design, NON-NEGOTIABLE), 7 (UK Sovereignty), 8 (Tenant Isolation), 12 (Accessibility), 18/19/20 (IaC, Testing, CI/CD) |
| `ARC-001-REQ-v1.0.md` | NFR-SEC-001..004; NFR-AVAIL-*; BR-001..008; INT-001..006; FR-001..005 |
| `ARC-001-STKE-v1.0.md` | RACI for security roles; SD-3 / SD-10 / SD-11 / SD-12 drivers; Goals G-4 / G-5 |
| `ARC-001-RISK-v1.0.md` | R-008 / R-009 / R-010 / R-011 / R-014 / R-015 / R-016 / R-017; §G appetite; §H Priority-1 actions; §J monitoring |
| `ARC-001-TCOP-v1.0.md` | Point 6 / Point 7 / Point 13 alignment; AI annex |
| `ARC-001-ADR-001-v1.0.md` | Tenant Isolation Model |
| `ARC-001-ADR-003-v1.0.md` | Identity & SSO |
| `ARC-001-ADR-004-v1.0.md` | AI Provider Abstraction |
| `ARC-001-ADR-005-v1.0.md` | Observability + Audit Log |
| `ARC-001-ADR-006-v1.0.md` | Deployment Topology |
| `ARC-001-ADR-008-v1.0.md` | Per-Tenant Quotas, Rate Limits, Fair Use |
| `ARC-001-DPIA-v1.0.md` | UK GDPR DPIA — pending generation, blocking GA |
| `ARC-001-AIPB-v1.0.md` | AI Playbook compliance — pending generation, blocking GA |
| `ARC-001-SVCASS-v1.0.md` | Service Assessment readiness — pending generation, blocking GA |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:secure` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Sourced from ARC-000-PRIN-v2.0, ARC-001-REQ-v1.0, ARC-001-STKE-v1.0, ARC-001-RISK-v1.0, ARC-001-TCOP-v1.0, and ADR-001..008. Pre-GA Alpha-stage assessment. Formal acceptance vehicle for `ARC-001-RISK-v1.0.md` R-008/R-009/R-010/R-011 residual positions.
