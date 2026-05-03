# High-Level Design (HLD) Review: ArcKit as a Service

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:hld-review`

## Document Control

| Field | Value |
|-------|-------|
| Document ID | ARC-001-HLDR-v1.0 |
| Document Type | High-Level Design Review |
| Project | ArcKit as a Service (001-arckit-saas) |
| Classification | OFFICIAL |
| Status | DRAFT |
| Version | 1.0 |
| Created Date | 2026-05-03 |
| Last Modified | 2026-05-03 |
| Review Cycle | Quarterly |
| Next Review Date | 2026-06-02 |
| Owner | Mark Craddock, Service Owner |
| Reviewed By | [PENDING — Architecture Review Board] |
| Approved By | [PENDING — Architecture Review Board Chair] |
| Distribution | Project Team, Architecture Team |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:hld-review` command | [PENDING] | [PENDING] |

## Document Purpose

This document records the Architecture Review Board (ARB) High-Level Design review for the ArcKit as a Service (ArcKit SaaS) platform — a managed, multi-tenant SaaS for UK SMEs supplying UK Government. The review evaluates HLD readiness against the requirements (REQ), the eight accepted Architecture Decision Records (ADR-001 to ADR-008), and the 21 enterprise architecture principles (PRIN v2.0). It is the formal gate before Detailed Design (DLD) begins.

---

## 1. Review Overview

### 1.1 Purpose

To assess whether the proposed High-Level Design for ArcKit SaaS is architecturally sound, principle-aligned, requirement-complete, and feasible to deliver — with particular attention to multi-tenant isolation (Principle 8), UK data sovereignty (Principle 7), sovereign / air-gapped portability (Principle 21, binding), SME affordability (Principle 1), and secure-by-design posture (Principle 5).

### 1.2 HLD Document Under Review

**Document**: ArcKit SaaS HLD synthesis from REQ + ADR-001..008 + PRIN v2.0 (this document is itself the synthesised HLD review)
**ArcKit Version**: 4.12.3
**Submitted By**: ArcKit Vendor Architecture Team
**Submission Date**: 2026-05-03
**Stage**: Pre-GA Alpha

### 1.3 Review Participants

| Name | Role | Organisation | Review Focus |
|------|------|--------------|--------------|
| [PENDING] | Lead Reviewer / Enterprise Architect | ArcKit Vendor | Overall architecture, principle compliance |
| [PENDING] | Security Architect | ArcKit Vendor | Tenant isolation, threat model, NCSC CAF |
| [PENDING] | Domain Architect | ArcKit Vendor | Artefact authoring fit, governance idiom |
| [PENDING] | Infrastructure Architect | ArcKit Vendor | Managed K8s, cells, UK region topology |
| [PENDING] | Data Architect / DPO | ArcKit Vendor | UK GDPR, residency, portability |
| [PENDING] | SRE Lead | ArcKit Vendor | Observability, SLOs, DR |
| [PENDING] | Project 002 Liaison | ArcKit Vendor | Sovereign-route parity |

### 1.4 Review Criteria

The HLD is evaluated against:

- **Architecture Principles** — all 21 principles in `ARC-000-PRIN-v2.0.md`, with weight given to the four CRITICAL non-negotiables (P-1 SME affordability, P-5 Security by Design, P-7 UK Data Sovereignty, P-12 Accessibility, P-21 Sovereign / Air-Gapped Deployment).
- **Requirements Alignment** — coverage of BR-001..008, FR-001..015, all NFR categories, INT-001..009, DR-001..007.
- **ADR Implementation** — explicit traceability to all eight ADRs with no architectural drift.
- **Technical Feasibility** — implementability inside the small-team operating model.
- **Security and Compliance** — NCSC CAF, NCSC Cloud Security Principles 14, UK GDPR / DPA 2018, GDS Service Standard, TCoP.
- **Resilience and Operational Readiness** — NFR-A-001 99.9% availability, NFR-A-002 RPO < 15 min / RTO < 4 h, observability, runbooks.

---

## 2. Executive Summary

### 2.1 Overall Assessment

**Status**: APPROVED WITH CONDITIONS

**Summary**:

The High-Level Design for ArcKit as a Service demonstrates a coherent, principle-aligned, multi-tenant SaaS architecture built on managed Kubernetes (ADR-006), with a pool-with-tenant-ID-enforcement isolation model on a cell-based growth path (ADR-001), running in a UK-resident hyperscaler region (ADR-002), authenticated via OIDC/SAML federation plus a hardened operator IdP (ADR-003), with a pluggable AI-provider abstraction (ADR-004), an OpenTelemetry-instrumented observability stack with tamper-evident audit log (ADR-005), open-format Markdown / JSON / YAML data portability tested by CI round-trip (ADR-007), and tier-differentiated quotas enforced at the API gateway (ADR-008).

The design is unusually disciplined on the load-bearing concern of this project — Principle 21 sovereign / air-gapped portability — by ensuring every architectural layer (runtime, identity adaptor, AI adaptor, observability SDKs, data format, quota enforcement) ships from one codebase to both the SaaS route and the project-002 sovereign route. This is the right answer to the strategic Y-statement of every ADR.

The conditions for approval are not architectural reversals but instrumentation and evidence gaps that must close before DLD: (i) the runtime threat model and NCSC CAF self-assessment must be drafted and aligned to ADR-001 / ADR-006; (ii) explicit SLO / SLI definitions and error-budget policy must be set so NFR-A-001 / NFR-M-001 are measurable from day one; (iii) the cell-management automation (provisioning, capacity monitoring, tenant-to-cell assignment, cell-fill discipline) must have a named DLD artefact; (iv) FinOps tagging, per-tenant cost-to-serve calculation, and the cross-subsidy break-even dashboard (R-001, BR-005) must have a concrete component; (v) the GOV.UK Design System alignment (FR-013) and PSBAR / WCAG 2.2 AA testing approach (NFR-C-003) must have a documented design rather than be deferred wholesale to DLD.

### 2.2 Key Strengths

- **Principle 21 sovereign-route portability is engineered, not asserted**. ADR-001, ADR-004, ADR-005, ADR-006, ADR-007, ADR-008 each commit to one codebase serving both SaaS and project-002 sovereign deployments via values overlays / configuration. CI gates (sovereign smoke test, round-trip export, portability test) enforce this binding constraint per release.
- **Defence-in-depth tenant isolation** is layered: tenant_id propagation at the application boundary (ADR-001), namespace + network policy + admission control at the runtime layer (ADR-006), tenant-ID-native observability signals (ADR-005), per-tenant quotas at the API gateway (ADR-008). Each layer is independently testable; loss of one does not breach isolation alone — a strong response to R-008 (existential cross-tenant leak) and R-014 (isolation defect).
- **Open-standards exit is contractual, not aspirational**. ADR-007's CI-tested round-trip on Markdown / JSON / YAML / JSONL archive is a release-blocker, satisfying BR-007, FR-006, NFR-I-002, UK GDPR Articles 17 and 20, and Principle 4 with one mechanism. Same archive shape doubles as the project-002 backup format.

### 2.3 Key Concerns

- **SLO / SLI and error-budget policy not yet defined**. NFR-A-001 commits to ≥ 99.9% rolling-30-day availability, NFR-M-001 commits to RED metrics and SLO-based alerting, but the HLD does not yet specify the SLI taxonomy, the per-service SLO targets, or the error-budget burn-down policy. Without these, alerting will be tactically configured rather than principle-anchored. Block on DLD.
- **Cell-management automation is unspecified at component level**. ADR-001 and ADR-006 both rely on automated cell provisioning, tenant-to-cell assignment, cell-fill discipline (75% threshold), and cell migration — yet there is no named component or HLD section that owns this. The risk is that cell discipline becomes a manual, brittle ops task at GA + 12 months.
- **FinOps and cross-subsidy reporting component is implied but not designed**. BR-005 (cross-subsidy break-even at GA + 18 months) and Principle 17 (FinOps + sovereign unit economics) need a concrete cost-to-serve component pulling per-tenant signals from ADR-005 telemetry plus per-cell cost from cloud billing. R-001 (cross-subsidy fail) is the #1 strategic risk; its primary control instrument is missing from HLD.

### 2.4 Conditions for Approval

**MUST Address Before Detailed Design**:

1. **[BLOCKING-01]** — Produce a runtime-layer threat model anchored to ADR-001 + ADR-006, mapped to NCSC CAF (objectives B1–B5, C1–C2) and NCSC Cloud Security Principles 1–14. Owner: Security Lead.
2. **[BLOCKING-02]** — Define SLI taxonomy and SLO targets per service (with error-budget policy and burn-rate alerting) sufficient to operationalise NFR-A-001, NFR-A-003, NFR-P-001, NFR-P-002, NFR-P-003. Owner: SRE Lead.
3. **[BLOCKING-03]** — Name the Cell Management component (provisioning, capacity monitoring, assignment, migration, fill-discipline enforcement) and its interfaces. Owner: Lead Architect.
4. **[BLOCKING-04]** — Name the FinOps / Cost-to-Serve component, its data sources (ADR-005 per-tenant telemetry, cloud billing, AI-inference metering from ADR-004 / ADR-008), and the cross-subsidy reporting cadence. Owner: FinOps Lead + Service Owner.

**SHOULD Address During Detailed Design**:

1. **[ADVISORY-01]** — Document GOV.UK Design System alignment scope for FR-013 (which patterns adopted, which deferred, accessibility-evidence model for bespoke components).
2. **[ADVISORY-02]** — Document the WCAG 2.2 AA automated + manual assistive-technology testing pipeline (NFR-C-003 / NFR-U-002).
3. **[ADVISORY-03]** — Document the AI-content human-in-the-loop UX (per ADR-004 risk on hallucinated content presented as fact) and the AI-Playbook provenance metadata schema as an OpenAPI-versioned contract.
4. **[ADVISORY-04]** — Document the public Status Page (FR-009) as a component, with its data source (the same observability pipeline) and tenant notification channel.
5. **[ADVISORY-05]** — Specify how `pg_dump`-equivalent reproducibility is preserved across managed-K8s vendor changes (R-015 mitigation portability rehearsal must be documented as a runbook, not just an ADR commitment).

### 2.5 Recommendation

- [ ] **APPROVED**: Proceed to detailed design with no conditions
- [x] **APPROVED WITH CONDITIONS**: Proceed after addressing blocking items listed above
- [ ] **APPROVED WITH ADVISORIES**: Proceed but address advisory items in DLD
- [ ] **REJECTED**: Significant rework required; resubmit revised HLD for review

**Target Resubmission Date** (for blocking items closure): 2026-06-02

---

## 3. Architecture Overview

> Diagrams are out of scope for this artefact and are produced separately as `ARC-001-DIAG-001` (Context, C4 L1), `ARC-001-DIAG-002` (Container, C4 L2 / deployment), and `ARC-001-DIAG-003` (Component, C4 L3) in Wave 6. The text representation below is normative; the diagrams will visualise the same model.

### 3.1 Context Layer (C4 Level 1) — Text Representation

**System under design**: ArcKit SaaS — multi-tenant managed SaaS for SME architects and SME founders supplying UK Government, plus buying-authority architects evaluating supplier governance evidence. Operated by ArcKit Service Operators (vendor SRE / support).

**Primary actors**:

- **SME Architect** (Persona 1) — primary tenant user; authors principles, requirements, ADRs, diagrams.
- **SME Founder / Bid Lead** (Persona 2) — tenant admin; manages tenancy and billing.
- **Buying Authority Architect** (Persona 3) — read-only or invited reviewer; evaluates supplier evidence.
- **ArcKit Service Operator** (Persona 4) — vendor staff; admin console only; logged break-glass.

**External systems consumed by ArcKit SaaS**:

- **Tenant Identity Providers** (INT-001) — OIDC / SAML 2.0; includes GOV.UK One Login as an external IdP option (ADR-003).
- **Companies House API** (INT-003) — UK SME eligibility verification (BR-003, FR-001).
- **Payment Processor** (INT-002) — card / direct-debit + G-Cloud purchase orders (FR-011).
- **Email Delivery Provider** (INT-004) — verification, invites, notifications, signed-export delivery.
- **AI / LLM Provider** (INT-005) — pluggable; minimum two production-tested providers (ADR-004); UK or adequate jurisdiction with documented Article 46 transfer mechanism.
- **Object Storage and Database** (INT-006) — UK-region cloud; S3-compatible storage and PostgreSQL wire protocol per ADR-002.
- **Observability Backend / SIEM** (INT-007) — managed UK-resident; OpenTelemetry-fed (ADR-005).
- **G-Cloud / Digital Marketplace** (INT-008) — listing and call-off PO acceptance (BR-004).
- **Vulnerability Disclosure Channel** (INT-009) — security.txt + ISO 29147 process.

**External systems consuming ArcKit SaaS**:

- Tenant-side automation via the public REST API (NFR-I-001) and AsyncAPI event subscriptions (FR-008).
- Buying-authority assessors via signed export downloads (FR-006, ADR-007).

### 3.2 Container Layer (C4 Level 2) — Text Representation

The deployment topology is **per cell** (ADR-001 + ADR-006). A cell is a managed Kubernetes cluster in a UK-region (ADR-002) with multi-AZ (≥ 3 AZs) compute, hosting up to ~1,000 tenants in shared namespaces with tenant_id enforcement at every boundary.

**Per-cell containers (Kubernetes namespaces)**:

| # | Container | Responsibility | Technology / Standard | ADR / REQ |
|---|-----------|----------------|-----------------------|-----------|
| C1 | **API Gateway** | Public TLS termination; OIDC token verification; tenant_id resolution from claims; tier-differentiated token-bucket rate-limiting; AI-budget enforcement; export rate-limit; routes to internal services. | OCI container; OIDC; OpenAPI 3.x routes | ADR-003, ADR-008, NFR-I-001 |
| C2 | **Web Application** | Tenant-facing UI; GOV.UK Design System aligned where suitable; WCAG 2.2 AA. | OCI container | FR-013, NFR-C-003 |
| C3 | **Tenant Service** | Tenant lifecycle: signup, SME verification, tier change, offboarding, deletion + destruction certificate. | OCI container; calls Companies House (INT-003) | FR-001, FR-002, FR-010, FR-011 |
| C4 | **Project & Artefact Service** | Multi-project workspace; artefact CRUD + versioning; tenant_id default-deny; row-level security; storage prefix policy. | OCI container; PostgreSQL; object storage | FR-002, FR-003, FR-005 |
| C5 | **AI Generation Service** | Pluggable AI adaptor (provider-agnostic interface); per-tenant budget enforcement; provenance metadata recording; golden-prompt regression. | OCI container; ADR-004 adaptor pattern | FR-004, INT-005, NFR-P-002 |
| C6 | **Export Service** | Full-fidelity tenant export to signed Markdown/JSON/YAML/JSONL tarball; CI-tested round-trip; signed-URL delivery. | OCI container; Cosign + SHA-256 manifest | FR-006, NFR-P-003, NFR-I-002 |
| C7 | **Audit & Tenant Log Service** | Tenant-visible audit log surface derived from the same OpenTelemetry pipeline; tamper-evident integrity hash chain; ≥ 12-month retention. | OCI container | FR-012, NFR-C-002 |
| C8 | **Billing & Subscription Service** | Tier subscription, invoicing, VAT, G-Cloud PO acceptance; integrates payment processor (INT-002). | OCI container | FR-011, BR-002, BR-004 |
| C9 | **Notification Service** | Transactional email + tenant in-product notifications; SPF/DKIM/DMARC aligned. | OCI container; INT-004 | FR-009, FR-010 |
| C10 | **Admin Console (Operator)** | Vendor-side operator console; hardware-key WebAuthn MFA (separate IdP per ADR-003); break-glass + step-up flows; uplift workflow for quota requests. | OCI container; separate ingress | FR-014, ADR-008 |
| C11 | **Status Page** | Public, externally accessible service health; subscribed by tenant admins via email/webhook. | OCI container or static-hosted; data from observability | FR-009 |
| C12 | **Public Marketing & Pricing Site** | GOV.UK-aligned public site; pricing, eligibility, T&Cs, accessibility statement, security/compliance evidence summary. | Static hosting | FR-015, BR-002, BR-006 |
| C13 | **Cell Management Service** *(condition BLOCKING-03)* | Cell provisioning, capacity monitoring, tenant-to-cell assignment, cell-fill discipline, cell migration runbook automation. | OCI container; Argo / Flux GitOps reconciler | ADR-001, ADR-006 |
| C14 | **FinOps / Cost-to-Serve Service** *(condition BLOCKING-04)* | Per-tenant cost calculation from ADR-005 telemetry and cloud billing; per-cell cost domain; cross-subsidy break-even dashboard. | OCI container | BR-005, Principle 17, R-001 |

**Per-cell shared infrastructure (managed services, not in-cluster)**:

- **PostgreSQL (managed)** — primary persistence with row-level security; tenant_id NOT NULL convention; daily off-site backups within UK region; backup retention 35 days; encrypted at rest (KMS); CMK on large-enterprise tier.
- **Object Storage (S3-compatible, managed)** — artefact attachments, export staging area, signed URLs (24-hour expiry); per-tenant prefix policy.
- **Coordinated Rate-Limit Store (Redis or managed cache)** — shared across gateway pods (ADR-008).
- **Managed OpenTelemetry Backend + SIEM** (ADR-005) — UK-resident; tenant_id-native; tiered retention; PII redaction at source.
- **Identity Provider (vendor-hosted) + Federation Adaptor** — OIDC for SME default; OIDC/SAML self-service federation for enterprise/government tenants; separate operator IdP with hardware-key WebAuthn.

**Cross-cell / vendor-global**:

- **Image Registry** (OCI; signed by Cosign; SBOM-attested per release; admission-controller blocks unsigned) — shared across cells.
- **GitOps Repository** (single source of truth for production manifests across all cells; emergency break-glass auto-expiring + SIEM-alerted).
- **Sovereign-profile CI Bench** — smoke-tests the same images and Helm charts against a no-egress test cluster on every release (project 002 BR-001 / Principle 21).

### 3.3 Component Layer (C4 Level 3) — Text Representation, selected key containers

**C1 API Gateway components**:
- *OIDC Token Verifier* — validates tenant IdP claims; resolves `tenant_id` claim → request context.
- *Tenant Context Middleware* — fails closed if `tenant_id` missing.
- *Token-Bucket Rate-Limiter* — per-tenant + per-(tenant,user) buckets; tier-differentiated; soft-warn at 80%, hard-throttle at 100%.
- *AI-Budget Coordinator* — calls + tokens dimensions; concurrent-call coordination via Redis.
- *Export Rate-Limit* — protects ADR-007 pipeline.
- *Quota-Event Emitter* — emits to ADR-005 pipeline for SIEM abuse detection.

**C5 AI Generation Service components**:
- *Provider-Agnostic Adaptor Interface* — single interface; lint-blocked from leaking provider specifics.
- *Provider Implementations* — minimum two production-tested (e.g., one primary + one alternate); provider DPA-tracked; quarterly review.
- *Tier-Based Default-Model Selector* — selects model based on tenant tier; budget-aware.
- *Prompt + Project-Context Assembler* — applies ArcKit templates; minimises tenant data sent.
- *Provenance Metadata Recorder* — command, model, model version, prompt hash, timestamp; AI Playbook evidence asset.
- *Golden-Prompt Regression Suite* — green-required per release.

**C4 Project & Artefact Service components**:
- *Authoring API* — versioned per artefact; OpenAPI 3.x.
- *Versioning Engine* — diffs + editor identity per change.
- *Tenant-ID-Default-Deny Repository Layer* — every query carries tenant_id; row-level security at PostgreSQL.
- *Storage Prefix Adaptor* — per-tenant S3 prefix; signed-URL issuance.
- *Search Index Adaptor* — tenant-scoped index partition (search index failure = graceful degradation per NFR-A-003).

**C13 Cell Management Service components** *(to be detailed in DLD per BLOCKING-03)*:
- *Cell Provisioner* — cluster + namespace + GitOps reconcile in < 4 hours, automated.
- *Capacity Monitor* — cell-fill 75% trigger.
- *Tenant Assignment Service* — onboarding-time cell selection.
- *Cell Migration Runbook Automation* — rehearsed in non-prod.

### 3.4 Deployment Layer Summary

- **Region**: UK-resident hyperscaler region (ADR-002), ≥ 3 AZs primary; UK secondary region for backup/DR.
- **Runtime**: managed Kubernetes, one cluster per cell (ADR-006); namespace-per-tenant within cluster (with default-deny network policy + Pod Security Standards `restricted` + admission control blocking unsigned images).
- **CI/CD**: GitOps as the only path to production; auto-expiring break-glass token for emergencies (SIEM-alerted on issue + use; monthly review).
- **Release artefacts**: signed OCI images + SBOM; same images deploy to SaaS cells and to project-002 sovereign clusters via values overlay.

---

## 4. Architecture Principles Compliance

### 4.1 Principle Compliance Checklist (all 21 principles)

| # | Principle | Status | Anchor |
|---|-----------|--------|--------|
| 1 | Equitable Access for SMEs (managed SaaS) | ✅ Compliant | BR-001, ADR-001, ADR-008 |
| 2 | Scalability and Elasticity | ✅ Compliant | NFR-S-001, ADR-006 (HPA + cluster autoscaler) |
| 3 | Resilience and Fault Tolerance | ⚠️ Partial — patterns committed, SLOs not yet defined | NFR-A-003, BLOCKING-02 |
| 4 | Open Standards and Interoperability | ✅ Compliant | NFR-I-001/002, ADR-002, ADR-007 |
| 5 | Security by Design | ⚠️ Partial — threat model + CAF self-assessment pending | NFR-SEC-001..009, BLOCKING-01 |
| 6 | Observability | ⚠️ Partial — pipeline committed, SLI/SLO definitions pending | ADR-005, NFR-M-001, BLOCKING-02 |
| 7 | UK Data Sovereignty and Governance | ✅ Compliant | ADR-002, ADR-005, INT-006, NFR-C-001/007 |
| 8 | Tenant Isolation and Single Source of Truth | ✅ Compliant | ADR-001, ADR-006, NFR-SEC-002 |
| 9 | Data Quality, Lineage, and Portability | ✅ Compliant | ADR-007, FR-005, FR-006, NFR-I-002 |
| 10 | Loose Coupling | ✅ Compliant | C1..C14 service decomposition; OpenAPI/AsyncAPI |
| 11 | Asynchronous Communication | ✅ Compliant | FR-008 AsyncAPI; on-prem broker support inherent in OCI portability |
| 12 | Accessibility (WCAG 2.2 AA) | ⚠️ Partial — testing pipeline pending | NFR-C-003, NFR-U-002, ADVISORY-02 |
| 13 | Performance and Efficiency | ⚠️ Partial — load testing approach pending | NFR-P-001/002/003, BLOCKING-02 |
| 14 | Availability and Reliability | ⚠️ Partial — DR drill cadence committed, SLO policy pending | NFR-A-001/002, BLOCKING-02 |
| 15 | Maintainability and Evolvability | ✅ Compliant | NFR-M-002, ADR series + GitOps |
| 16 | Open Source First and Reuse | ✅ Compliant | OCI / Kubernetes / OpenTelemetry / Cosign / SBOM |
| 17 | Cost Transparency and FinOps | ⚠️ Partial — component absent at HLD | BR-005, BLOCKING-04 |
| 18 | Infrastructure as Code | ✅ Compliant | ADR-006 GitOps single path to prod |
| 19 | Automated Testing | ✅ Compliant | NFR-SEC-002 isolation suite; ADR-007 round-trip; ADR-006 sovereign smoke test |
| 20 | CI/CD | ✅ Compliant | ADR-006 GitOps + admission gates |
| 21 | Sovereign and Air-Gapped Deployment (binding) | ✅ Compliant | Engineered across ADR-001/004/005/006/007/008 with per-release CI smoke test |

**Summary**: 14/21 fully compliant, 7/21 partial (all closable in DLD via BLOCKING-01 / BLOCKING-02 / BLOCKING-04 plus ADVISORY-02). Zero non-compliant. Crucially, **all four CRITICAL non-negotiables (P-1, P-7, P-8, P-21)** are fully compliant. **P-5 and P-12 (also CRITICAL non-negotiable)** are partial pending threat model and accessibility testing pipeline — both in-scope for DLD.

### 4.2 Principle Compliance Details — selected critical principles

#### P-1 Equitable Access for SMEs (CRITICAL non-negotiable)

**Assessment**: ✅ Compliant.

**Evidence**: ADR-001 pool-with-tenant-ID model is the only isolation choice that supports SME-affordable unit economics; ADR-008 fair-use quotas with soft-warn-then-throttle preserve transparency; FR-006 export available on every tier including free; FR-007 SSO not paywalled away from any tier; ADR-007 export format identical regardless of tier; ADR-002 cell-fill discipline mitigates per-cell DB-instance floor cost.

**Recommendation**: Operationalise via the FinOps / Cost-to-Serve component (BLOCKING-04) so the cross-subsidy economics (R-001) are observed in real time, not deduced quarterly.

#### P-5 Security by Design (CRITICAL non-negotiable)

**Assessment**: ⚠️ Partial.

**Evidence of compliance**: NFR-SEC-001..009 covers the security control taxonomy; ADR-001 + ADR-006 give defence-in-depth tenant isolation; ADR-003 hardware-key operator MFA closes the asymmetric-blast-radius operator-account vector; OCI image signing + SBOM + admission control gates supply chain; ADR-005 tamper-evident audit log + SIEM gives forensic capability.

**Concerns**: The HLD does not yet present a runtime threat model anchored to ADR-001 / ADR-006, nor a current NCSC CAF self-assessment with target profile (NFR-SEC-008). NFR-SEC-009 NCSC Cloud Security Principles assessment is committed but not produced.

**Recommendation**: BLOCKING-01 — produce both before DLD. Reference frame: NCSC CAF objectives B1 (Service protection policies), B2 (Identity and access control), B3 (Data security), B4 (System security), B5 (Resilient networks), C1 (Security monitoring), C2 (Proactive security event discovery).

#### P-7 UK Data Sovereignty and Governance (CRITICAL non-negotiable)

**Assessment**: ✅ Compliant.

**Evidence**: ADR-002 commits UK-resident hyperscaler region with UK secondary for backup/DR; INT-006 storage UK residency; ADR-005 observability backend UK residency; INT-005 AI provider must operate in UK or adequate jurisdiction with documented Article 46 transfer mechanism; NFR-C-007 OFFICIAL with OFFICIAL-SENSITIVE handling caveats — content above OFFICIAL-SENSITIVE explicitly out of scope and rejected at the application layer; NFR-C-001 UK GDPR + DPA 2018 ROPA / DSR / DPIA / 72-hour breach process committed; CMK on the large-enterprise tier (ADR-002 / NFR-SEC-004) addresses CLOUD Act / IPA residual.

**Recommendation**: Maintain quarterly sub-processor inventory review; document the published government-disclosure-request handling procedure (DPO ownership) in the operational runbook (NFR-M-003).

#### P-8 Tenant Isolation and Single Source of Truth (CRITICAL)

**Assessment**: ✅ Compliant.

**Evidence**: NFR-SEC-002 (default-deny, per-request tenant_id propagation, automated CI isolation tests, external pen testing covering cross-tenant scenarios) is directly anchored. ADR-001 specifies the pool model with mandatory CI isolation suite and quarterly external pen testing. ADR-006 adds runtime layer defence in depth (namespace + network policy + admission control). ADR-005 makes tenant_id native to every observability signal. ADR-008 quotas per tenant.

**Recommendation**: The CI isolation suite is the single most important compensating control. DLD must specify: (i) the synthetic-tenant fixture model; (ii) the public-surface coverage matrix (every API, every UI flow, export, AI generation); (iii) the admission policy and network policy CI-validation procedure.

#### P-12 Accessibility — WCAG 2.2 AA (CRITICAL non-negotiable)

**Assessment**: ⚠️ Partial.

**Evidence**: NFR-C-003 / NFR-U-002 commit to WCAG 2.2 AA + assistive-technology testing on every release + accessibility statement aligned with PSBAR 2018; FR-013 commits to GOV.UK Design System alignment where suitable.

**Concerns**: Neither the testing pipeline (automated + manual) nor the GOV.UK Design System alignment scope is documented at HLD level.

**Recommendation**: ADVISORY-01 + ADVISORY-02 — close in DLD.

#### P-21 Sovereign and Air-Gapped Deployment (CRITICAL non-negotiable, binding)

**Assessment**: ✅ Compliant — and architecturally exemplary.

**Evidence**: Every relevant ADR has a sovereign-route commitment baked in:
- ADR-001 — same codebase, single-tenant configuration of the pool model, no fork.
- ADR-002 — open-standard primitives (S3-compatible, PostgreSQL wire, OIDC/SAML) so project-002 can use MinIO + Postgres in air-gapped boundary.
- ADR-003 — generic OIDC/SAML adaptor; project 002 plugs customer IdP into the same interface.
- ADR-004 — provider-agnostic AI adaptor; AI degrades gracefully when no provider configured.
- ADR-005 — OpenTelemetry SDKs unchanged; backend swappable.
- ADR-006 — same OCI images + Helm charts, sovereign values overlay; per-release sovereign smoke test against a no-egress cluster, release-blocked.
- ADR-007 — same archive format used as project-002 backup format.
- ADR-008 — same quota enforcement code; deploying authority sets thresholds via values overlay.

**Recommendation**: Maintain CI sovereign smoke test discipline; document in runbook the canonical project-002 customer-controlled cluster minimum (managed K8s of major hyperscalers OR vanilla K8s ≥ N-1).

---

## 5. Requirements Coverage Analysis

### 5.1 Business Requirements Coverage

| Req | Title | Addressed | Container(s) | Assessment |
|-----|-------|-----------|--------------|------------|
| BR-001 | Free tier for verified UK SMEs | Yes | C3 Tenant Service, C8 Billing | ✅ |
| BR-002 | Transparent published pricing | Yes | C12 Marketing site, C8 Billing | ✅ |
| BR-003 | SME eligibility verification | Yes | C3 Tenant Service + INT-003 | ✅ |
| BR-004 | G-Cloud procurement route | Yes | C8 Billing (PO acceptance) + INT-008 | ✅ |
| BR-005 | Cross-subsidy funding model | Partial | **C14 FinOps (BLOCKING-04)** | ⚠️ |
| BR-006 | UK public sector policy evidence | Yes | C12 + compliance documents | ✅ |
| BR-007 | Tenant portability and exit | Yes | C6 Export Service (ADR-007) | ✅ |
| BR-008 | Adoption and activation | Yes | UC-1 path through C2/C3 | ✅ |

### 5.2 Functional Requirements Coverage

| Req | Title | Container(s) | Assessment |
|-----|-------|--------------|------------|
| FR-001 | Tenant provisioning + SME verification | C3 + INT-003 | ✅ |
| FR-002 | Multi-tenant workspace management | C3 + C4 (default-deny RLS) | ✅ |
| FR-003 | Architecture artefact authoring | C4 + C2 | ✅ |
| FR-004 | AI-assisted generation | C5 (ADR-004) | ✅ |
| FR-005 | Artefact versioning + audit trail | C4 + C7 | ✅ |
| FR-006 | Full-fidelity export | C6 (ADR-007) | ✅ |
| FR-007 | SSO integration | C1 + INT-001 (ADR-003) | ✅ |
| FR-008 | Public API + event interfaces | C1 + asynchronous broker | ✅ |
| FR-009 | Public status page + tenant notifications | C11 + C9 | ⚠️ component scope thin (ADVISORY-04) |
| FR-010 | Tenant offboarding + data deletion | C3 + C9 + C7 | ✅ |
| FR-011 | Billing and subscription management | C8 + INT-002 + INT-008 | ✅ |
| FR-012 | Tenant audit log access | C7 (derived from ADR-005 pipeline) | ✅ |
| FR-013 | GOV.UK Design System alignment | C2 + C12 | ⚠️ scope undefined (ADVISORY-01) |
| FR-014 | Admin console for service operators | C10 + ADR-003 hardware-key MFA | ✅ |
| FR-015 | Public marketing + pricing site | C12 | ✅ |

**Gaps**: BR-005 cross-subsidy reporting and FR-013 GOV.UK Design System alignment scope are the only material gaps.

### 5.3 Non-Functional Requirements Coverage

#### Performance

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-P-001 | Page < 1 s p95; API read < 200 ms p95; API write < 1 s p95 | API Gateway + caching layer + tenant-scoped DB reads; CDN for marketing/static | ⚠️ — load testing approach pending DLD (BLOCKING-02) |
| NFR-P-002 | AI generation < 60 s p95 with progress feedback | C5 streaming response pattern; per-tenant budget enforcement | ✅ design committed; SLO numeric targets pending DLD |
| NFR-P-003 | Bulk export < 10 min for typical SME | C6 staged pipeline; signed-URL delivery | ✅ |

#### Availability and Resilience

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-A-001 | ≥ 99.9% rolling-30-day | ≥ 3 AZ + multi-AZ DB + cluster autoscaler + GitOps rollback < 10 min | ⚠️ — error-budget policy pending (BLOCKING-02) |
| NFR-A-002 | RPO < 15 min; RTO < 4 h; daily backup + 35-day retention; UK secondary region; annual DR drill | ADR-002 secondary region + ADR-006 GitOps cluster reprovision; ADR-007 export pipeline doubles as offline backup | ✅ design committed |
| NFR-A-003 | Graceful degradation; circuit breaker; retry+backoff; timeout; bulkhead; reduced functionality | C5 graceful degradation when AI unavailable; C4 search index optional; ADR-008 token-bucket bulkhead | ✅ |

#### Scalability

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-S-001 | Horizontal scaling without code change | HPA + cluster autoscaler (ADR-006); cell provisioning at 75% fill (ADR-001) | ✅ |
| NFR-S-002 | Storage growth ~50 GB / 1,000 tenants; hot/warm tiering | Object storage with lifecycle policy; cell-fill discipline | ✅ |

#### Security

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-SEC-001 | OIDC/SAML + MFA; session policy | ADR-003 IdP layout; hardware-key for operators; absolute session 12 h | ✅ |
| NFR-SEC-002 | Tenant isolation default-deny + CI tests | ADR-001 + ADR-006 layered controls; CI isolation suite | ✅ |
| NFR-SEC-003 | RBAC least-privilege | Roles per FR-002; time-boxed elevation | ✅ |
| NFR-SEC-004 | Encryption in transit + at rest; CMK on enterprise tier | TLS strong ciphers; KMS at rest; CMK on large-enterprise (ADR-002) | ✅ |
| NFR-SEC-005 | No secrets in code/config/images; managed vault; rotation ≤ 90 d | Managed secrets store integrated with K8s | ✅ |
| NFR-SEC-006 | Vuln mgmt; SAST/DAST; pen test; ISO 29147 disclosure | OCI signing + SBOM + admission control + scan gates; INT-009 disclosure | ✅ |
| NFR-SEC-007 | Service-to-service auth (mTLS or signed tokens) | Service mesh OR app-layer mTLS — DLD selects (per ADR-006 §7.3) | ⚠️ deferred to DLD |
| NFR-SEC-008 | NCSC CAF self-assessment with target profile | **Pending** — BLOCKING-01 | ⚠️ |
| NFR-SEC-009 | NCSC Cloud Security Principles 14 evidence | **Pending** — BLOCKING-01 | ⚠️ |

#### Compliance

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-C-001 | UK GDPR + DPA 2018 | ROPA + DSR + DPIA + 72-h breach process; UK residency by default | ✅ |
| NFR-C-002 | Audit logging + retention; tamper-evident | C7 + ADR-005 hash chain; ≥ 12-month retention | ✅ |
| NFR-C-003 | PSBAR / WCAG 2.2 AA | C2 + testing pipeline (ADVISORY-02) | ⚠️ |
| NFR-C-004 | TCoP self-assessment | Already covered by `/arckit:tcop` artefact | ✅ |
| NFR-C-005 | GDS Service Standard | Already covered by `/arckit:service-assessment` artefact | ✅ |
| NFR-C-006 | ISO 27001 alignment | SHOULD_HAVE v1, MUST_HAVE GA + 18 months | ✅ |
| NFR-C-007 | OFFICIAL with OFFICIAL-SENSITIVE caveats; > OFFICIAL-SENSITIVE rejected | Application-layer rejection rule at C3 / C4 | ✅ |

#### Maintainability and Portability

| NFR | Requirement | HLD Approach | Assessment |
|-----|-------------|--------------|------------|
| NFR-M-001 | Observability — logs + RED metrics + traces + status page | ADR-005 + C11 status page | ⚠️ SLO/SLI definitions pending (BLOCKING-02) |
| NFR-M-002 | Tenant + operator + developer documentation | Doc pipeline aligned with release | ✅ |
| NFR-M-003 | Operational runbooks | Runbooks for deploy / rollback / backup / restore / incident / scaling / DR | ⚠️ inventory committed; content pending DLD |
| NFR-I-001 | OpenAPI 3.x + AsyncAPI; ≥ 12-month backwards-compatible window | All public APIs published & versioned | ✅ |
| NFR-I-002 | Markdown / JSON / YAML export with lineage; importable | ADR-007 round-trip CI test, release blocker | ✅ |

### 5.4 Integration Requirements Coverage

| INT | Title | Container(s) | Assessment |
|-----|-------|--------------|------------|
| INT-001 | Tenant IdP (SSO) | C1 + ADR-003 | ✅ |
| INT-002 | Payment processor | C8 | ✅ |
| INT-003 | Companies House | C3 | ✅ |
| INT-004 | Email delivery | C9 | ✅ |
| INT-005 | AI / LLM | C5 (pluggable per ADR-004) | ✅ |
| INT-006 | Object storage + database | C4 + shared infra | ✅ |
| INT-007 | Observability backend | ADR-005 | ✅ |
| INT-008 | G-Cloud / Digital Marketplace | C8 + manual listing | ✅ |
| INT-009 | Vulnerability disclosure | INT-009 published security.txt | ✅ |

### 5.5 Data Requirements Coverage

| DR | Entity | Owning Container | Storage | Assessment |
|----|--------|------------------|---------|------------|
| DR-001 | Tenant | C3 | PostgreSQL | ✅ |
| DR-002 | User | C3 | PostgreSQL | ✅ |
| DR-003 | Project | C4 | PostgreSQL + object storage | ✅ |
| DR-004 | Artefact | C4 | PostgreSQL (metadata) + object storage (content) | ✅ |
| DR-005 | Audit Event | C7 | tamper-evident store | ✅ |
| DR-006 | Subscription | C8 | PostgreSQL | ✅ |
| DR-007 | SME Verification Record | C3 | PostgreSQL (7-year retention) | ✅ |

---

## 6. Architecture Quality Assessment

### 6.1 Scalability

- ✅ Horizontal — HPA + cluster autoscaler per cell (ADR-006); cell-based growth path with 1,000-tenants/cell initial cap (ADR-001).
- ✅ Database — managed PostgreSQL Multi-AZ; per-cell instance; CMK on large-enterprise tier; row-level security.
- ✅ Object storage — UK region; per-tenant prefix; lifecycle policies for hot/warm tiering.
- ✅ Caching — coordinated rate-limit store (Redis-equivalent) per cell; CDN for marketing/static.
- ✅ Stateless services — every container is stateless; state in managed DB / object storage / cache.

### 6.2 Performance

- ⚠️ p95 / p99 NFR targets are committed but the load-testing approach and SLI taxonomy are pending DLD (BLOCKING-02).
- ✅ AI generation streaming with progress feedback addresses NFR-P-002.
- ✅ Export staging + signed-URL delivery addresses NFR-P-003.

### 6.3 Security

- ✅ Supply chain — OCI image signing + SBOM + admission-controller blocking + CI scan gates (ADR-006).
- ✅ Identity — OIDC + SAML federation; vendor IdP for SMEs; hardware-key WebAuthn for operators; step-up for tenant-data-impacting operations.
- ✅ Network — managed K8s namespace + default-deny network policy + Pod Security Standards `restricted`.
- ✅ Data — TLS strong ciphers in transit; KMS at rest; CMK on large-enterprise tier.
- ✅ Audit — ADR-005 tamper-evident log + SIEM; tenant_id-native; ≥ 12-month retention.
- ⚠️ Threat model + NCSC CAF self-assessment + Cloud Security Principles 14 evidence pending (BLOCKING-01).

### 6.4 Resilience

- ✅ Multi-AZ in primary region; UK secondary region for DR.
- ✅ NFR-A-003 patterns committed: circuit breaker, retry+backoff, timeout, bulkhead, graceful degradation.
- ✅ ADR-006 GitOps rollback < 10 minutes mean.
- ⚠️ Error-budget policy and chaos / DR drill cadence pending DLD.

### 6.5 Operational Excellence

- ✅ ADR-005 OpenTelemetry-instrumented; SIEM rule review part of every ADR sign-off; quota events feed SIEM (ADR-008).
- ✅ ADR-006 GitOps single path to production; emergency break-glass SIEM-alerted.
- ✅ Runbook inventory committed (NFR-M-003).
- ⚠️ SLI / SLO and runbook content pending DLD.

### 6.6 Architecture Patterns

- ✅ Pool-with-tenant-ID isolation (ADR-001) — recognised secure pattern when correctly enforced.
- ✅ Cell-based growth path — caps blast radius, supports zonal upgrades.
- ✅ Provider-agnostic adaptors — applied to AI (ADR-004), identity (ADR-003), observability (ADR-005), data format (ADR-007), runtime (ADR-006).
- ✅ GitOps + signed-image-supply-chain — recognisable to NCSC / TCoP / GDS assessors.
- ✅ No anti-patterns observed: no shared database between containers; no in-cluster databases; no custom operators for application logic; no bypass of GitOps.

### 6.7 Technology Stack

| Layer | Technology | Approved | Assessment |
|-------|------------|----------|------------|
| Frontend | TBD (likely React or similar) + GOV.UK Design System where suitable | Pending DLD selection | ⚠️ |
| API Gateway | OCI container; OpenAPI 3.x routes | Open-standard | ✅ |
| Backend services | OCI containers; language TBD | Open-standard | ✅ |
| Database | Managed PostgreSQL (UK region) | ADR-002 | ✅ |
| Object storage | S3-compatible (UK region) | ADR-002 | ✅ |
| Messaging / events | AsyncAPI; broker selected in DLD | Open-standard | ✅ |
| Container orchestration | Managed Kubernetes (vendor selected via /arckit:research) | ADR-006 | ✅ |
| CI/CD | GitOps (Argo CD or Flux selected via /arckit:research) | ADR-006 | ✅ |
| Image signing / SBOM | Cosign + SBOM tooling | Open-standard | ✅ |
| Observability | OpenTelemetry SDKs + managed UK-resident backend + managed SIEM | ADR-005 | ✅ |
| Identity | Vendor-hosted OIDC IdP + OIDC/SAML federation adaptor + hardware-key WebAuthn admin IdP | ADR-003 | ✅ |
| AI / LLM | Two production-tested providers via provider-agnostic adaptor | ADR-004 | ✅ |

**Vendor lock-in risks**: Managed K8s vendor (R-015), AI provider (R-017), hyperscaler concentration (R-003) — all mitigated by portability ADRs and CI portability tests, with annual exit-plan rehearsal. The mitigations are credible on paper but unproven; quarterly portability rehearsal is the load-bearing operational control.

---

## 7. Risk Assessment

### 7.1 Top Architectural Risks (anchored to ARC-001-RISK-v1.0)

| Risk ID | Title | Inherent | Residual | HLD Mitigation |
|---------|-------|----------|----------|----------------|
| R-008 | Cross-tenant data leakage (existential) | 25 | 5 | Defence-in-depth: ADR-001 tenant_id propagation + ADR-006 namespace+netpolicy+admission + ADR-005 tenant_id-native telemetry + NFR-SEC-002 CI isolation suite + ADR-008 quotas |
| R-014 | Tenant isolation defect (ADR-001) | 20 | 8 | CI isolation tests on every release; quarterly external pen test; bug bounty (INT-009) |
| R-001 | Cross-subsidy break-even fails | 16 | 9 | **C14 FinOps component (BLOCKING-04)** + ADR-008 AI budget cap + ADR-001 cell-fill discipline |
| R-002 | MOD sovereign-route divergence | 16 | 6 | Principle 21 engineered across ADR-001/004/005/006/007/008; per-release sovereign smoke test |
| R-006 | AI inference cost overrun | 12 | 9 | ADR-008 monthly budget cap (calls + tokens); ADR-004 tier-based default-model selector |
| R-015 | Managed K8s vendor lock-in (ADR-006) | 9 | 6 | OCI + K8s API open standards; quarterly portability rehearsal; vendor exchangeable in months not years |

### 7.2 New Risks Surfaced in HLD Review

| Risk | Severity | Mitigation Recommendation |
|------|----------|---------------------------|
| Cell-management automation becomes brittle / manual at GA + 12 months | MEDIUM | BLOCKING-03 — name C13 component and its CI/runbook coverage |
| SLO / error-budget gap means alerting is tactically configured | MEDIUM | BLOCKING-02 — define before DLD; SRE Lead owns |
| FinOps reporting lag → R-001 detected too late | MEDIUM-HIGH | BLOCKING-04 — name C14 component with real-time per-tenant cost-to-serve |
| WCAG 2.2 AA testing pipeline not yet defined → P-12 non-negotiable becomes a late finding | MEDIUM | ADVISORY-02 |
| AI hallucinated content presented as fact (ADR-004 risk) — UX response not yet specified | MEDIUM | ADVISORY-03 — human-in-the-loop UX + AI-Playbook provenance schema |

---

## 8. Issues and Recommendations

### 8.1 Critical Issues (BLOCKING)

| ID | Issue | Impact | Recommendation | Owner | Target Date |
|----|-------|--------|----------------|-------|-------------|
| BLOCKING-01 | Threat model + NCSC CAF self-assessment + Cloud Security Principles 14 evidence not yet produced | HIGH — P-5 CRITICAL non-negotiable | Produce all three, anchored to ADR-001 + ADR-006; map to CAF B1–B5 + C1–C2 | Security Lead | 2026-05-25 |
| BLOCKING-02 | SLI taxonomy + SLO targets + error-budget policy not defined | HIGH — NFR-A-001, NFR-M-001, P-3, P-6, P-13, P-14 | Define per service; alert on burn-rate; document in runbook | SRE Lead | 2026-05-25 |
| BLOCKING-03 | Cell Management component (provisioning, capacity, assignment, migration, fill-discipline) not named in HLD | HIGH — operationalising ADR-001 + ADR-006 at GA + 12 months | Name C13; specify interfaces and CI coverage | Lead Architect | 2026-05-25 |
| BLOCKING-04 | FinOps / Cost-to-Serve component absent — primary instrument for R-001 (#1 strategic risk) | HIGH — BR-005, P-17, R-001 | Name C14; specify data sources (ADR-005 telemetry + cloud billing + ADR-004/008 metering); cross-subsidy dashboard cadence | FinOps Lead + Service Owner | 2026-05-25 |

### 8.2 High-Priority Issues (ADVISORY)

| ID | Issue | Impact | Recommendation | Owner | Target Date |
|----|-------|--------|----------------|-------|-------------|
| ADVISORY-01 | GOV.UK Design System alignment scope (FR-013) undefined | MEDIUM | Document patterns adopted; accessibility-evidence model for bespoke components | Domain Architect | DLD |
| ADVISORY-02 | WCAG 2.2 AA automated + manual assistive-technology testing pipeline (NFR-C-003 / P-12 non-negotiable) not specified | MEDIUM | Specify the pipeline; pen-test scope to include accessibility | Domain Architect + Security Lead | DLD |
| ADVISORY-03 | AI human-in-the-loop UX and AI-Playbook provenance schema not specified | MEDIUM | UX badging for AI-generated content; provenance schema versioned in OpenAPI | Service Owner + Lead Architect | DLD |
| ADVISORY-04 | Status Page (FR-009) component scope thin — data source and tenant notification channel | LOW-MEDIUM | Document as a component derived from observability pipeline (ADR-005) | SRE Lead | DLD |
| ADVISORY-05 | R-015 portability rehearsal procedure not yet a runbook | MEDIUM | Document quarterly portability rehearsal as NFR-M-003 runbook entry | Lead Architect | DLD |

### 8.3 Low-Priority Items (INFORMATIONAL)

| ID | Suggestion | Benefit | Owner |
|----|------------|---------|-------|
| INFO-01 | Consider adding a synthesised end-to-end "tenant lifecycle" sequence diagram in DIAG-003 | Improves assessor readability for buying-authority architects | Domain Architect |
| INFO-02 | Document the Prometheus exposition format choice for OpenTelemetry metrics | Useful evidence for project 002 sovereign deployments | SRE Lead |
| INFO-03 | Consider publishing the JSON Schemas for ADR-007 export format on the public marketing site | Strengthens the BR-007 exit promise as a marketing differentiator | Service Owner |

---

## 9. Review Decision

### 9.1 Final Decision

**Status**: APPROVED WITH CONDITIONS

**Effective Date**: 2026-05-03

**Conditions**:

1. BLOCKING-01 must be resolved by 2026-05-25 (threat model + CAF + CSP14 evidence).
2. BLOCKING-02 must be resolved by 2026-05-25 (SLI / SLO / error-budget policy).
3. BLOCKING-03 must be resolved by 2026-05-25 (Cell Management component named in HLD).
4. BLOCKING-04 must be resolved by 2026-05-25 (FinOps / Cost-to-Serve component named).
5. Updated HLD §3.2 / §3.3 sections resubmitted for confirmatory review prior to DLD kickoff.

**Next Steps**:

- [ ] Vendor addresses blocking issues (Security Lead, SRE Lead, Lead Architect, FinOps Lead).
- [ ] Revised HLD sections submitted for re-review by 2026-05-25.
- [ ] Re-review meeting scheduled: 2026-06-02.
- [ ] On condition closure, proceed to Detailed Design phase (DLD).
- [ ] HLD documentation finalised and baselined alongside DIAG-001/002/003.

### 9.2 Reviewer Sign-Off

| Reviewer | Role | Decision | Signature | Date |
|----------|------|----------|-----------|------|
| [PENDING] | Lead Reviewer / Enterprise Architect | Conditional | _________ | 2026-05-03 |
| [PENDING] | Security Architect | Conditional | _________ | 2026-05-03 |
| [PENDING] | Domain Architect | Conditional | _________ | 2026-05-03 |
| [PENDING] | Infrastructure Architect | Conditional | _________ | 2026-05-03 |
| [PENDING] | Data Architect / DPO | Conditional | _________ | 2026-05-03 |
| [PENDING] | SRE Lead | Conditional | _________ | 2026-05-03 |
| [PENDING] | Project 002 Liaison | Conditional | _________ | 2026-05-03 |

**Unanimous Approval Required**: Yes

**Escalation** (if reviewers cannot reach consensus): Architecture Steering Committee chaired by Service Owner.

---

## 10. Appendices

### Appendix A: Source Document Reference

| Document | Path |
|----------|------|
| REQ — Requirements | `projects/001-arckit-saas/ARC-001-REQ-v1.0.md` |
| RISK — Risk Register | `projects/001-arckit-saas/ARC-001-RISK-v1.0.md` |
| STKE — Stakeholders | `projects/001-arckit-saas/ARC-001-STKE-v1.0.md` |
| PRIN — Architecture Principles v2.0 | `projects/000-global/ARC-000-PRIN-v2.0.md` |
| ADR-001 — Tenant Isolation Model | `projects/001-arckit-saas/decisions/ARC-001-ADR-001-v1.0.md` |
| ADR-002 — Cloud Region and Storage Selection | `projects/001-arckit-saas/decisions/ARC-001-ADR-002-v1.0.md` |
| ADR-003 — Identity Provider Integration and SSO | `projects/001-arckit-saas/decisions/ARC-001-ADR-003-v1.0.md` |
| ADR-004 — AI Provider Abstraction and Model Strategy | `projects/001-arckit-saas/decisions/ARC-001-ADR-004-v1.0.md` |
| ADR-005 — Observability Stack | `projects/001-arckit-saas/decisions/ARC-001-ADR-005-v1.0.md` |
| ADR-006 — Deployment Topology and Runtime Platform | `projects/001-arckit-saas/decisions/ARC-001-ADR-006-v1.0.md` |
| ADR-007 — Data Portability and Export Format | `projects/001-arckit-saas/decisions/ARC-001-ADR-007-v1.0.md` |
| ADR-008 — Per-Tenant Quotas, Rate Limits, and Fair Use | `projects/001-arckit-saas/decisions/ARC-001-ADR-008-v1.0.md` |

### Appendix B: Requirements → Container Traceability Matrix

The matrix in §5 (BR / FR / NFR / INT / DR coverage tables) constitutes the forward traceability from requirements to HLD containers. Backward traceability — container → requirements — will be regenerated by `/arckit:traceability` after DLD.

### Appendix C: ADR → Container Traceability

| ADR | Containers / Cross-cutting | Containers Most Affected |
|-----|----------------------------|--------------------------|
| ADR-001 Tenant Isolation | All containers carry tenant_id; **C13** owns cell management | C1, C4, C13 |
| ADR-002 UK Region | Shared infrastructure | DB + object storage + observability |
| ADR-003 Identity | C1 + C10 (separate operator IdP) | C1, C10 |
| ADR-004 AI Adaptor | C5 | C5 |
| ADR-005 Observability | Cross-cutting; C7 derives from same pipeline | C7, all |
| ADR-006 Runtime | All containers; GitOps boundary | All |
| ADR-007 Data Portability | C6 | C6 |
| ADR-008 Quotas | C1 (gateway-enforced); C5 (AI budget) | C1, C5 |

### Appendix D: Review Meeting Notes

To be attached after the formal ARB review session scheduled for 2026-05-25.

### Appendix E: Traceability with Other ArcKit Artefacts

| Artefact | Path | Use |
|----------|------|-----|
| DPIA | `projects/001-arckit-saas/ARC-001-DPIA-v1.0.md` | UK GDPR / NFR-C-001 evidence |
| TCoP review | `projects/001-arckit-saas/ARC-001-TCOP-v1.0.md` | TCoP / NFR-C-004 evidence |
| Secure by Design | `projects/001-arckit-saas/ARC-001-SECD-v1.0.md` | NCSC SbD posture |
| AI Playbook | `projects/001-arckit-saas/ARC-001-AIPB-v1.0.md` | ADR-004 evidence |
| Stakeholders | `projects/001-arckit-saas/ARC-001-STKE-v1.0.md` | Persona + RACI inputs |

---

## External References

> This section provides traceability from generated content back to source documents.
> All sources are internal ArcKit artefacts within this project; no external citations required for this artefact.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| INT-REQ | ARC-001-REQ-v1.0.md | Internal | projects/001-arckit-saas/ | Requirements (BR/FR/NFR/INT/DR) |
| INT-RISK | ARC-001-RISK-v1.0.md | Internal | projects/001-arckit-saas/ | Risk register |
| INT-STKE | ARC-001-STKE-v1.0.md | Internal | projects/001-arckit-saas/ | Stakeholders |
| INT-PRIN | ARC-000-PRIN-v2.0.md | Internal | projects/000-global/ | Architecture principles v2.0 |
| INT-ADR-001..008 | ARC-001-ADR-00{1..8}-v1.0.md | Internal | projects/001-arckit-saas/decisions/ | Architecture Decision Records |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| INT-REQ-1 | INT-REQ | §FR-001..015 | Functional | Used to derive container responsibilities in §3.2 |
| INT-REQ-2 | INT-REQ | §NFR-* | Non-functional | Used to derive coverage in §5.3 |
| INT-PRIN-1 | INT-PRIN | All 21 principles | Principles | Used in §4 compliance checklist |
| INT-ADR-1 | INT-ADR-001..008 | §6 Decision Outcome | Decisions | Used in §3 architecture overview and §4 principle anchors |
| INT-RISK-1 | INT-RISK | §B Top 10 + R-008/R-014/R-015 | Risk | Used in §7.1 |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| ARC-001-DPIA-v1.0.md | projects/001-arckit-saas/ | Cross-referenced in Appendix E only |
| ARC-001-TCOP-v1.0.md | projects/001-arckit-saas/ | Cross-referenced in Appendix E only |
| ARC-001-SECD-v1.0.md | projects/001-arckit-saas/ | Cross-referenced in Appendix E only |
| ARC-001-AIPB-v1.0.md | projects/001-arckit-saas/ | Cross-referenced in Appendix E only |
| ARC-000-PRIN-v1.0.md | projects/000-global/ | Superseded by v2.0 |

---

**Generated by**: ArcKit `/arckit:hld-review` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Project 001)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Synthesised from REQ (BR/FR/NFR/INT/DR), all eight ADRs (ADR-001..008), Architecture Principles v2.0 (21 principles), and Risk Register top 10. Diagrams (DIAG-001/002/003) deferred to Wave 6.
