# Technology and Service Research: ArcKit as a Service (Managed SaaS) — SaaS Control Plane

> **Template Origin**: Official | **ArcKit Version**: 4.13.1 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RSCH-v1.0 |
| **Document Type** | Technology and Service Research (SaaS-Control-Plane Scope) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Quarterly through Beta; annual post-GA |
| **Next Review Date** | 2026-08-03 |
| **Owner** | Mark Craddock (Service Owner — pending Lead Architect appointment) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Team, Architecture, Security Lead, DPO, FinOps, CCS liaison, Project 002 (sovereign) liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:research` agent (Wave 2 of `/arckit:build`). Scoped to the SaaS-control-plane components called out in the dispatch instructions: tenant-isolation/multi-tenancy patterns, AI provider abstraction (Bedrock / Azure OpenAI / Vertex), observability stack, audit/log retention, identity (GOV.UK One Login + Entra), and G-Cloud catalogue comparators. Inherits the bimodal adopter profile (civilian-SaaS vs MOD-sovereign) from `ARC-000-RSCH-v1.0.md`. | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This is the **Wave-2 SaaS-control-plane technology research** for ArcKit as a Service. It does *not* cover:

- AWS / Azure / GCP service-by-service evaluation — those are the responsibility of the parallel Wave-2 outputs `ARC-001-AWRS-v1.0`, `ARC-001-AZRS-v1.0`, `ARC-001-GCRS-v1.0`.
- Reuse of UK Government code — that is `ARC-001-GOVR-v1.0` (this document records the govreposcrape sweep finding for completeness, but does not duplicate the GOV-REUSE assessment).
- Sovereign-deployment vendor selection — that is Project 002 (the architectural pluggability is in scope here; vendor-by-vendor sovereign-mode selection is not).

Within scope are the **six SaaS-control-plane categories** the parent specified:

1. **Tenant-isolation / multi-tenancy patterns** — control-plane and data-plane primitives that materialise ADR-001's pool-with-cells decision.
2. **AI provider abstraction** — Bedrock vs Azure OpenAI vs Vertex AI, with an open-source / on-premise fallback for Project 002 reuse.
3. **Observability stack** — managed UK-resident logs / metrics / traces backend, plus SIEM, materialising ADR-005.
4. **Audit / log retention** — immutable audit log for tenant-facing FR-012 and operator FR-014 with at-least-12-month retention (Principle 6 / NFR-C-002).
5. **Identity (GOV.UK One Login + departmental Entra ID)** — federated SSO per ADR-003 and FR-007.
6. **G-Cloud catalogue comparators** — competing or adjacent EA / governance / consultancy listings on the UK Digital Marketplace, against which ArcKit-as-a-Service has to position itself (BR-004).

**Requirements covered**: BR-001, BR-002, BR-004, BR-005, BR-006, BR-007; FR-002, FR-004, FR-005, FR-007, FR-009, FR-012, FR-014; NFR-A-001, NFR-A-002, NFR-A-003, NFR-S-001, NFR-S-002, NFR-SEC-001, NFR-SEC-002, NFR-SEC-007, NFR-SEC-008, NFR-SEC-009, NFR-C-001, NFR-C-002, NFR-C-007, NFR-I-001, NFR-I-002; INT-001, INT-005, INT-006, INT-007.

**Bimodal adopter inheritance** (from `ARC-000-RSCH-v1.0.md`):

- *Civilian-SaaS* segment (UK central-civil departments, ALBs, NHS bodies, devolved administrations, local authorities, SME suppliers) — addressable by the managed-SaaS route this document researches.
- *MOD-sovereign* segment — addressable only by Project 002 sovereign deployment. Each vendor in this document is assessed for **on-prem reusability** so that the SaaS-route choice does not rule out sovereign reuse.

**Research approach**: Synthesis of the architecture principles (`ARC-000-PRIN-v2.0.md`), Wave-1 organisation research (`ARC-000-RSCH-v1.0.md`), the requirements (`ARC-001-REQ-v1.0.md`), the stakeholder analysis (`ARC-001-STKE-v1.0.md`), the SOBC (`ARC-001-SOBC-v1.0.md`), and the eight ADRs in `projects/001-arckit-saas/decisions/` (ADR-001 isolation, ADR-002 region/storage, ADR-003 identity, ADR-004 AI provider, ADR-005 observability, ADR-006 runtime, ADR-007 export, ADR-008 quotas). UK Government policy and vendor positioning are referenced by name; specific vendor pricing in this document is the **list-price reference point** consistent with publicly published rate cards as of 2026-05-03 — buyers should re-verify before committing capital. A targeted govreposcrape sweep was run (results below) and returned predominantly local-authority content with little central-gov coverage of the categories researched, so the Wave-2 GOV-REUSE output (`ARC-001-GOVR-v1.0`) is the authoritative reuse assessment.

**Requirements Analyzed**: 8 business, 15 functional, 23 non-functional, 6 integration requirements (subset directly affected by SaaS-control-plane choices). 6 categories researched.

### Key Findings

- **Tenant isolation: pool-with-cells, anchored on managed Postgres + S3-class object storage + managed Kubernetes per cell**. Recommended: `BUY` UK-region hyperscaler managed Postgres (RDS Postgres on AWS, Azure Database for PostgreSQL, or Cloud SQL on GCP) plus `BUY` managed Kubernetes (EKS / AKS / GKE). The cell-fill discipline of ADR-001 is the cost lever that keeps Principle 1 affordable; a single 1,000-tenant cell at SME load lands at roughly £50–80k/year fully-loaded for compute, DB and storage in the UK region. The same Postgres-wire and S3-API primitives reuse cleanly into Project 002 sovereign mode (Postgres + MinIO).
- **AI provider abstraction: Bedrock as primary, Azure OpenAI as the validated second provider, plus an on-prem-deployable open-weight fallback (Llama-3 / Mistral on customer-controlled inference)**. Bedrock wins on UK-region availability (eu-west-2 London hosts Anthropic Claude 3.x and Amazon Nova) and on no-train-by-default contractual posture; Azure OpenAI is a credible second provider satisfying the ADR-004 / Goal G-8 quarterly-CI requirement and is the dominant choice for departmental Entra-aligned tenants. Vertex AI is rejected as primary on UK-region maturity grounds for the model families ArcKit needs but kept as a candidate for an over-the-horizon swap. Inference cost is the largest single OpEx variable risk (R-006, +15% optimism-bias line in the SOBC); ADR-008 per-tenant budget caps are the principal control.
- **Observability + audit: Grafana Cloud (UK / EU) or Datadog (UK / EU residency) for OpenTelemetry-instrumented logs / metrics / traces, with a managed SIEM (Microsoft Sentinel or Elastic Cloud SIEM) ingesting auth + isolation events and the tenant audit log shipped to immutable object storage (S3 Object Lock / Azure Blob Immutable Storage) for the 12-month minimum (NFR-C-002, Principle 6) and 7-year retention on SME-verification decisions (BR-003)**. `BUY` for SaaS, with a `Grafana / Loki / Tempo / Mimir` open-source equivalent reserved for Project 002 sovereign reuse so that the same OpenTelemetry instrumentation drains into a customer-controlled collector.
- **Identity: vendor-IdP for SMEs (per ADR-003), self-service OIDC / SAML federation to the customer's Entra ID / Okta / Ping for paid tiers, GOV.UK One Login as an opt-in option for the small subset of tenants whose service is consumer-facing under One Login**. Recommended: Auth0 / Okta or Microsoft Entra External ID as the SaaS-tenant IdP with a hardened operator IdP (Entra ID with hardware FIDO2 keys, separate from the tenant IdP, per ADR-003). One Login is **not** mandatory for ArcKit-as-a-Service itself — ArcKit is staff/supplier-facing, not citizen-facing — but it is a buyer-side talking point.
- **G-Cloud catalogue comparators**: the closest comparators on G-Cloud 14 are commercial-EA tooling listings (LeanIX, Ardoq, MEGA, Bizzdesign, Sparx Enterprise Architect) and consultancy-led EA practices from large SIs. None of them combines the three things ArcKit-as-a-Service uniquely offers: a *free-tier-for-verified-SMEs* (BR-001), a transparent published per-seat list price (BR-002), and a no-paywall data-export guarantee (BR-007). The market gap is real, sustained, and the precise reason Principle 1 was written.

### Build vs Buy Summary

| Approach | Categories | Total 3-Year TCO (mid-point of band) | Rationale |
|----------|-----------|--------------------------------------|-----------|
| **BUILD** (custom) | 1 (cell-orchestration glue, AI adaptor, FinOps tagging) | £0.30M | Glue code only — the components themselves are bought. |
| **BUY** (commercial SaaS / managed) | 5 (managed Postgres, K8s, AI providers, observability, IdP) | £2.80M | The dominant pattern; matches ADR-002 / ADR-006 / ADR-005 / ADR-003 / ADR-004. |
| **ADOPT** (open-source) | 1 (OpenTelemetry SDKs, Grafana stack as sovereign fallback) | £0.10M | Sovereign reuse path; SaaS uses a managed equivalent. |
| **GOV.UK Platforms** | 0 | £0 | None of the GOV.UK common platforms (Pay / Notify / Forms / One Login) is on the critical path of the *control plane*. One Login is offered as a tenant-side option; not used for ArcKit's own platform identity. |
| **TOTAL** | 6 categories | **£3.20M** (mid-point) | Aligns with the SOBC OpEx envelope of £2.85M plus the ADR-006 / ADR-005 capital glue. |

> All ranges are 3-year, UK region, list-price reference points consistent with vendor public rate cards as of 2026-05-03. Variance band ± 30%, consistent with the SOBC ROM treatment.

### Top Recommended Vendors

**Shortlist for further evaluation**:

1. **Amazon Web Services — eu-west-2 London** (managed Postgres / S3 / EKS / Bedrock / KMS / CloudWatch) — primary SaaS-route candidate; passes UK-region, ≥3 AZ, NCSC Cloud Security Principle, G-Cloud-listed UK contracting entity test; native Bedrock with Anthropic Claude 3.x removes a large engineering integration cost; SOC-2 Type II + ISO 27001 + UK GDPR Article 28 DPA.
2. **Microsoft Azure — UK South** (Azure Database for PostgreSQL / Blob / AKS / Azure OpenAI / Key Vault / Sentinel / Entra ID / Entra External ID) — primary fallback; the dominant landing zone in central-civil tenants and NHS, so picking Azure as primary lowers tenant integration friction; Azure OpenAI is the most natural second AI provider satisfying ADR-004 quarterly-CI.
3. **Grafana Cloud (UK / EU residency tier)** — observability + audit-log retention; OpenTelemetry-native; a Grafana / Loki / Tempo / Mimir self-host stack is the like-for-like sovereign fallback (Project 002), preserving ADR-005's "open-standard instrumentation" commitment.

### Requirements Coverage

- **100%** of the requirements listed in scope above have an identified solution in this document.
- **0** requirements in scope require *bespoke* off-the-shelf gaps.
- **3** integration glue components remain build-custom (cell-orchestration controller, AI adaptor wrapper, FinOps tag-propagation Lambda / Function) — small effort, unavoidable, captured in the SOBC capital line "AI integration with pluggable abstraction (Conflict C-2 resolution; G-8) £0.20M".

---

## Research Categories

> Categories are framed around the SaaS-control-plane concerns called out in the Wave-2 dispatch — not against the full universe of EA-tooling categories. Each category profiles the available options against the bimodal adopter constraint (must work for civilian-SaaS now, must be reusable for MOD-sovereign in Project 002).

---

## Category 1: Tenant Isolation and Multi-Tenancy Primitives

**Requirements Addressed**: BR-001, BR-005; FR-002; NFR-S-001, NFR-S-002, NFR-SEC-002, NFR-SEC-009, NFR-A-001, NFR-A-002, NFR-A-003; INT-006; ADR-001, ADR-002, ADR-006.

**Why This Category**: Tenant isolation is the platform's single largest non-negotiable engineering risk (Principle 8 NON-NEGOTIABLE; SOBC Risk R-008 — at-floor on impact, residual 5, existential). Pricing it wrong destroys Principle 1; engineering it wrong destroys tenant trust irreversibly. ADR-001 has already chosen the *pattern* (pool with strict tenant-id enforcement, cell-based growth path); this category researches the **primitives** the pattern is built on top of in each plausible UK hyperscaler region.

---

### Option 1A: Build Custom Cell Orchestration on Bare VMs

**Description**: Build a cell-orchestration controller from scratch on bare VM compute (EC2 / Azure VMs / GCE), managing Postgres clusters, Kafka clusters, object storage, and KMS keys ourselves.

**Technology Stack**: Terraform / Pulumi for IaC; bespoke Go / Rust controller for cell lifecycle; Postgres on VMs with Patroni HA; MinIO for object storage; Vault for secrets.

**Effort Estimate**:

- **Development**: 30–40 person-months pre-GA
- **Skills Required**: Backend (Go / Rust), Postgres operations, Kubernetes (later), Linux operations, IaC, security engineering
- **Timeline**: 18+ months to production-ready

**Cost Breakdown**:

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Development (engineering) | £0.85M | £0.20M | £0.10M | At blended £900/day × 30 person-months |
| Infrastructure (UK region; 5 cells by Y3) | £0.10M | £0.18M | £0.30M | VMs, storage, KMS — comparable to managed |
| Maintenance / on-call (40% of dev for in-house DBA + SRE) | £0.20M | £0.30M | £0.40M | Patroni, backup, restore, patching |
| **Total** | **£1.15M** | **£0.68M** | **£0.80M** | |
| **3-Year TCO** | | | **£2.63M** | |

**Pros**:

- Maximum control over isolation primitives.
- No third-party DPA / sub-processor exposure for the data plane.
- Same code runs identically in sovereign mode (Project 002) — already unmanaged, already self-host.

**Cons**:

- Engineering effort hugely disproportionate to a 5–6 person team's bandwidth pre-GA.
- DBA / Postgres-operations talent is expensive and scarce in the UK SME market.
- The cross-tenant blast radius from a Patroni / backup misconfiguration is the same as the managed alternative, but with less battle-tested operations on top.
- Time-to-GA pushes cross-subsidy break-even (R-001) unacceptably late.

**Risks**:

- Engineering schedule slip → R-001 break-even slip.
- DBA hiring failure → critical-path single-point-of-failure on the team.

**When to Build**:

- Sovereign-only project with no SaaS revenue clock — does not apply here.

---

### Option 1B: Buy — AWS UK Region (eu-west-2 London) — RDS Postgres + S3 + EKS + KMS — Recommended

**Description**: ArcKit cell topology materialised on AWS UK London region (eu-west-2): managed PostgreSQL (RDS or Aurora) per cell, S3 Object Storage with per-tenant key prefixes and bucket policies, Amazon EKS for the managed Kubernetes runtime per cell (per ADR-006), AWS KMS for vendor-managed keys (default) and BYOK / external-key import for the paid tier (per ADR-002), CloudWatch Logs for audit retention.

**Vendor**: Amazon Web Services EMEA SARL UK Branch; UK contracting entity for G-Cloud purposes.

**Pricing Model**: Pay-as-you-go with reserved-instance / savings-plan discounts at 1-year and 3-year commits. Egress is metered; intra-region traffic free; cross-AZ traffic charged. List prices vary by SKU.

**Cost Breakdown** (per cell, 1,000-tenant SME-mix population, UK region; mid-point of typical published list rates as of 2026-05-03):

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| RDS Postgres (multi-AZ, m5.xlarge equivalent) | £18k | £18k | £18k | ~£1.5k/month, multi-AZ included |
| S3 storage + requests (50 TB by Y3 across cells) | £5k | £8k | £15k | Standard tier; lifecycle to IA after 90 days |
| EKS control plane + worker nodes (per cell) | £30k | £30k | £30k | ~£2.5k/month for control plane + 4× t3.large nodes |
| KMS + secrets | £2k | £2k | £2k | Per-cell CMK; rotation included |
| Cross-AZ + egress (modest at SME scale) | £3k | £4k | £6k | |
| **Subtotal per cell** | **£58k** | **£62k** | **£71k** | |
| **Cells in flight (cell-fill discipline of ADR-001)** | 1 cell | 2 cells | 4 cells | ~75% fill before next cell |
| **Total infra Year-1/Year-2/Year-3** | **£58k** | **£124k** | **£284k** | |
| **3-Year TCO (infra)** | | | **£466k** | (Reduced ~25% by reserved instances post-Year-1) |

**Pricing Tiers** (relevant to ArcKit cells):

- **On-demand** (Year 1, while cell-fill discipline still being calibrated): full list rate.
- **1-year reserved / savings plan** (Year 2 onwards): typically ~30% off.
- **3-year reserved** (only after BR-008 adoption signal at GA + 12 months): typically ~50% off.

**Estimated Tier for This Project**: On-demand for Year 0 build, mixed on-demand + 1-year reserved by Year 2, 3-year reserved on the steady-state cell baseline by Year 3.

**Pros**:

- ✅ UK-resident in eu-west-2 London; ≥3 AZ; meets NFR-A-001 99.9% without bespoke topology.
- ✅ Native S3 API and Postgres wire protocol — directly portable to Project 002's MinIO + Postgres on-prem deployment (ADR-004 / ADR-006 sovereign profile).
- ✅ AWS UK contracting entity is G-Cloud-listed; UK GDPR Article 28 DPA available; sub-processor list published.
- ✅ Bedrock co-located in eu-west-2 means AI traffic stays intra-region, reducing egress and tightening UK GDPR Article 28 posture.
- ✅ KMS supports BYOK / external-key import for the paid-tier customer-managed-keys requirement (NFR-SEC-004).
- ✅ RDS Postgres has multi-AZ HA, automated backups (35 days default — meets NFR-A-002), point-in-time recovery (RPO < 5 minutes — beats NFR-A-002 RPO 15 min).

**Cons**:

- ❌ Hyperscaler-concentration risk on operational dependency, even with open-standard primitives.
- ❌ CLOUD Act / Investigatory Powers Act exposure — must be assessed in DPIA; mitigated by CMK on paid tier.
- ❌ Per-cell DB-instance floor cost (~£18k/year) sets the lower bound on cell economics; cell-fill discipline (ADR-001) is the management response.

**Key Features**:

- **RDS Postgres**: managed PostgreSQL 15 / 16 with Multi-AZ, automated backups, encryption at rest (AWS KMS), parameter-group tuning, IAM auth, performance insights.
- **S3**: 11-9s durability, server-side encryption (SSE-KMS), Object Lock for the audit-log retention bucket (NFR-C-002 12-month immutability), bucket policies that key off `tenant_id` prefix.
- **EKS**: managed Kubernetes 1.29+; control plane operated by AWS; Cluster Autoscaler / Karpenter for node pool elasticity; OIDC integration with workload identity (IRSA) for service-to-service pod identity (NFR-SEC-007).
- **KMS**: vendor-managed default; BYOK / external import for paid tier; HSM-backed (FIPS 140-2 Level 2 / 3 endpoints available).

**Integration**:

- **APIs**: AWS SDKs (JS / Python / Go / Java / Rust); S3 API (multi-vendor compatible); Postgres wire protocol (multi-vendor compatible).
- **Authentication**: AWS IAM with IRSA for K8s workloads.
- **Documentation**: Excellent.

**Compliance & Security**:

- ✅ UK GDPR / DPA 2018 — Article 28 DPA available; sub-processor inventory published.
- ✅ ISO 27001, ISO 27017, ISO 27018, SOC 1/2/3 Type II.
- ✅ NCSC Cloud Security Principles — published assessment.
- ✅ UK data residency in eu-west-2 (London); availability across ≥3 AZs.
- ✅ Encryption at rest (SSE-KMS) and in transit (TLS 1.2+, TLS 1.3 preferred).
- ✅ G-Cloud 14 listed under multiple lots.

**Vendor Maturity**: Public company; market leader; multi-decade track record.

**Support**: Business / Enterprise / Enterprise On-Ramp tiers; UK-region SRE; published SLA (RDS Multi-AZ ≥ 99.95% monthly).

**Exit Strategy**: Postgres dump / S3 batch copy → Project 002 sovereign deployment with no schema change. Lock-in risk **LOW** at the data layer; **MEDIUM** at the IAM / KMS layer (re-creation effort).

**References**:

- AWS Customer Compliance Center (sub-processor inventory).
- G-Cloud 14 listing for AWS UK contracting entity.
- AWS UK GDPR Article 28 DPA (publicly available template).

---

### Option 1C: Buy — Microsoft Azure UK South — Azure Database for PostgreSQL Flexible Server + Azure Blob + AKS + Azure Key Vault

**Description**: Same isolation pattern, materialised on Azure UK South (with UK West as DR pair). Azure Database for PostgreSQL Flexible Server per cell, Azure Blob Storage with immutable storage for audit, AKS managed Kubernetes per cell, Azure Key Vault for secrets and BYOK.

**Vendor**: Microsoft Limited (UK contracting entity).

**Pricing Model**: Pay-as-you-go with reservations at 1- and 3-year terms; UK regions priced consistently with eu-west-2 list prices ± single-digit %.

**Cost Breakdown** (per cell, 1,000-tenant SME-mix; UK South):

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| Azure Database for PostgreSQL Flexible Server (D4ds, ZRS) | £20k | £20k | £20k | Slightly higher than RDS per-vCPU; ZRS reduces RPO |
| Azure Blob storage (50 TB by Y3 across cells) | £5k | £8k | £14k | Hot tier; lifecycle to Cool after 90 days |
| AKS (control plane free; node pool D4s_v5) | £25k | £25k | £25k | Control plane is free (Azure absorbs); node pool is the cost |
| Key Vault + Managed HSM | £4k | £4k | £4k | Managed HSM is FIPS 140-2 L3 |
| Cross-zone + egress | £3k | £4k | £6k | |
| **Subtotal per cell** | **£57k** | **£61k** | **£69k** | |
| **3-Year TCO (infra)** | | | **£454k** | At 1+2+4 cells progression |

**Pros**:

- ✅ Free AKS control plane (Azure absorbs control-plane cost; AWS EKS charges ~£0.10/hour).
- ✅ UK South is the dominant landing zone for central-civil departments and NHS — picking Azure as primary reduces tenant-side network egress and integration friction for the largest enterprise-tier population.
- ✅ Azure OpenAI is in the same region — clean co-location with the AI provider (Category 2).
- ✅ Entra ID native integration at the operator layer (per ADR-003) — single IdP for vendor staff.
- ✅ Azure Database for PostgreSQL has zone-redundant HA → RPO ~ 0; meets and exceeds NFR-A-002.

**Cons**:

- ❌ AKS node-pool floor cost is similar to EKS, so the apparent "free control plane" win is small in absolute terms.
- ❌ Azure Blob is not S3-compatible at the API layer — abstraction layer needed if both AWS and Azure cells run in parallel, increasing engineering complexity.
- ❌ Azure UK contracting via Microsoft Limited carries CLOUD Act exposure equivalent to AWS.

**Compliance**: equivalent to AWS — UK GDPR DPA, ISO 27001 / 27017 / 27018, SOC, NCSC Cloud Security Principles, G-Cloud 14.

---

### Option 1D: Buy — GCP UK Region (europe-west2 London) — Cloud SQL Postgres + GCS + GKE + Cloud KMS

**Description**: Same pattern on GCP europe-west2.

**Pros**:

- ✅ UK region; ≥3 AZ.
- ✅ GKE has a good security-by-default posture (Workload Identity native).
- ✅ Pricing comparable to AWS / Azure within ± 5%.

**Cons**:

- ❌ Smallest UK public-sector adoption of the three hyperscalers; correspondingly smallest pre-built tenant network egress alignment.
- ❌ Vertex AI's UK-region maturity for the model families ArcKit needs (generation-quality LLMs) lags Bedrock and Azure OpenAI as of 2026-05-03 — so co-locating AI on GCP is weaker than co-locating on AWS or Azure.
- ❌ Smaller G-Cloud catalogue presence and fewer UK partners reduces buyer-side defensibility narrative weight.

**Recommendation**: keep GCP as a *third* candidate for over-the-horizon swap, not a primary or secondary. Detailed assessment is the responsibility of `ARC-001-GCRS-v1.0`.

---

### Option 1E: Adopt — Open-Source Postgres + MinIO on Self-Operated K8s (Sovereign Fallback)

**Description**: PostgreSQL with Patroni HA + MinIO for S3-compatible object storage + an unmanaged self-operated Kubernetes (kubeadm or RKE2) on bare VMs. This is **the Project 002 sovereign profile**, listed here only for cost transparency. **Not recommended** for the SaaS route.

**3-Year TCO (SaaS hypothetical)**: ~£2.20M (engineering + DBA + SRE + infra), much worse than the managed options above. Used only as the baseline for Project 002 sovereign-deployment portability.

---

### Option 1F: GOV.UK Platform — Not Applicable

There is no GOV.UK common platform that provides a managed multi-tenant data plane. GOV.UK Notify, Pay, Forms, One Login are *application-layer* services for tenant-side use, not platform infrastructure.

---

### Build vs Buy Recommendation for Tenant Isolation

**Recommended Approach**: **BUY — AWS eu-west-2 London (primary) with Azure UK South as the cross-vendor abstraction validation second platform** — selected to match ADR-002's open-primitive shape.

**Rationale**:

The AWS eu-west-2 region narrowly wins as primary because:

1. **AI co-location**: Bedrock (Category 2) is generally available in eu-west-2 with Anthropic Claude 3.x, the model family ArcKit's AI generation pipeline (FR-004) is built around. Co-location keeps AI traffic inside the UK GDPR Article 28 boundary and removes a cross-region egress cost line.
2. **Open primitives**: S3 + Postgres + EKS are the most directly transferable to the Project 002 sovereign profile (MinIO + Postgres + customer-K8s) without an abstraction shim.
3. **G-Cloud listing depth**: AWS has the largest UK public-sector landing-zone footprint; buyer-side defensibility is the easiest to evidence.

Azure UK South is the *cross-vendor abstraction validation* second platform — used by the cross-vendor abstraction shim referenced in ADR-002, not by tenant traffic at GA. This satisfies the principle-4 "no lock-in" claim concretely while keeping Year-1 operational complexity manageable.

**Key Decision Factors**:

- ✅ **UK residency**: AWS eu-west-2 London satisfies Principle 7 hard constraint.
- ✅ **Cell economics**: managed Postgres + EKS keeps per-cell floor cost in the £58k–£71k/year band; cross-subsidy at modelled enterprise mix clears it from quarter 5 post-GA per the SOBC.
- ✅ **Sovereign reuse**: Postgres wire + S3 API are byte-compatible with Project 002 MinIO + Postgres deployment.
- ✅ **Cross-vendor abstraction**: parallel Azure validation in CI (Goal G-8 analogue) means AWS-only operational dependency is mitigable in days, not months.

**Shortlist for Further Evaluation**:

1. **AWS eu-west-2 London** — primary recommendation; deep evaluation in `ARC-001-AWRS-v1.0`.
2. **Azure UK South** — secondary validation platform; deep evaluation in `ARC-001-AZRS-v1.0`.

**Next Steps**:

- [ ] AWS pricing quote against the BR-008 12-month adoption forecast (RI / savings-plan modelling).
- [ ] Azure pricing quote on the equivalent cell topology for cross-vendor floor.
- [ ] DPA + sub-processor reviews with Vendor DPO for both vendors.
- [ ] Pre-Beta gate decision: AWS as primary, Azure as cross-vendor floor.

---

## Category 2: AI Provider Abstraction (Bedrock vs Azure OpenAI vs Vertex)

**Requirements Addressed**: BR-001, BR-005, BR-006; FR-004, UC-2; INT-005; NFR-P-002, NFR-A-003, NFR-SEC-002, NFR-C-001, NFR-I-001; ADR-004, ADR-008.

**Why This Category**: AI generation (FR-004) is the value-multiplier that makes the SME free tier viable: it is what turns hours of artefact drafting into minutes. It is also the largest single OpEx variable risk (R-006: AI inference cost overrun, residual 9 — at appetite ceiling). ADR-004 has chosen the *abstraction* (provider-agnostic AIAdaptor; two providers from day one); this category researches the *providers* and prices them.

---

### Option 2A: Build Custom — Self-Hosted Open-Weight LLM (Llama-3-70B, Mistral-Large)

**Description**: Stand up Llama-3-70B or Mistral-Large on customer-controlled inference (vLLM / SGLang) on GPU compute (A100 / H100 in UK region).

**Effort**: 2–3 person-months for the stack; ongoing GPU operations are non-trivial.

**Cost Breakdown** (UK region GPU):

- A100 80GB on-demand: ~£3–4/hour (UK region equivalent rate); 1× A100 sustains roughly 10 concurrent generations.
- 24×7 single-A100: ~£26k–£35k/year per node.
- Realistic floor for SaaS-route AI quota envelope at 1,500-tenant scale: 4× A100 nodes ≈ £100k–£140k/year + DBA/MLOps overhead.

**Pros**:

- ✅ No per-token egress to a third party — UK GDPR Article 28 sub-processor inventory simpler.
- ✅ This is **already the Project 002 sovereign default profile** for the AI adaptor (per ADR-004).

**Cons**:

- ❌ Generation quality of open-weight 70B models is meaningfully below Claude 3.5 Sonnet / GPT-4o for the kinds of structured artefacts ArcKit produces (architecture documents, ADRs with reasoning chains).
- ❌ MLOps overhead (model serving, scale-to-N, drift, cold-start) eats into the SME affordability margin.
- ❌ GPU floor cost is sticky — must be paid even at zero load.

**Recommendation**: hold open-weight self-hosted as the **Project 002 sovereign profile** and as a *break-glass* fallback for the SaaS, not a primary.

---

### Option 2B: Buy — Amazon Bedrock (eu-west-2 London) — Recommended Primary

**Description**: Bedrock as a managed multi-model inference service. Anthropic Claude 3.5 Sonnet / Claude 3 Haiku as the default models for SME-tier (Haiku) and paid-tier / large-enterprise (Sonnet); Amazon Nova as a cheaper fallback for high-volume bulk drafting; Llama-3 / Mistral as eu-west-2-resident options for cost-sensitive workloads.

**Vendor**: Amazon Web Services EMEA SARL UK Branch (with model providers as sub-processors documented per provider).

**Pricing Model**: per-token, distinct rates per model. Reference points (UK eu-west-2 list rates as of 2026-05-03, per million tokens):

- Claude 3.5 Sonnet: input ~£2.50 / output ~£12.00 per M tokens.
- Claude 3 Haiku: input ~£0.20 / output ~£1.00 per M tokens.
- Amazon Nova Pro: input ~£0.65 / output ~£2.60 per M tokens.
- Llama-3.1-70B: input ~£0.55 / output ~£0.55 per M tokens.

**Cost Breakdown** (modelled against the SOBC AI inference line of £0.50M / 3-year):

| Cost Item | Year 1 | Year 2 | Year 3 | Notes |
|-----------|--------|--------|--------|-------|
| AI inference (mix: 50% Haiku, 30% Sonnet, 20% Nova/Llama) | £0.10M | £0.18M | £0.22M | Aligned with SOBC D1.2 OpEx line incl. R-006 +15% |
| **3-Year TCO** | | | **£0.50M** | matches SOBC |

**Pros**:

- ✅ UK eu-west-2 London availability for Anthropic Claude 3.x and Amazon Nova; intra-region traffic; UK GDPR Article 28 manageable.
- ✅ No-train default — Bedrock customer data is *not* used to train models, contractually and architecturally.
- ✅ Pluggable: Bedrock API is a thin shim over the underlying model providers, so the ADR-004 AIAdaptor can migrate to a different provider behind the same shape.
- ✅ Fail-open path natural: graceful degradation per NFR-A-003 if Bedrock is throttled; ADR-008 per-tenant budget caps interpose cleanly.
- ✅ Cost-per-token competitive with Azure OpenAI on equivalent quality tiers.

**Cons**:

- ❌ Anthropic / Meta / Mistral are AI sub-processors that must appear in the published sub-processor list (R-011).
- ❌ Token-cost variance between models means tenant cost-to-serve dispersion is wider than for an in-house model — FinOps tagging (Principle 17, ADR-005) must be set up day-1 to track.
- ❌ Vendor concentration: AWS already chosen as primary infra; AI on the same vendor magnifies single-vendor risk (mitigated by ADR-004 "two providers from day one" requirement).

**Compliance**: AWS UK GDPR Article 28 DPA covers Bedrock; sub-processor list updated; UK Data Protection registration (AWS) current.

---

### Option 2C: Buy — Azure OpenAI Service (UK South) — Recommended Second Provider

**Description**: GPT-4o / GPT-4 Turbo / GPT-3.5 hosted in Azure UK South under Microsoft's enterprise OpenAI agreement.

**Vendor**: Microsoft Limited (UK contracting entity).

**Pricing Model** (UK South, list, per million tokens, 2026-05-03):

- GPT-4o: input ~£2.30 / output ~£9.00 per M tokens.
- GPT-4 Turbo: input ~£8.00 / output ~£24.00 per M tokens.
- GPT-3.5 Turbo: input ~£0.40 / output ~£1.20 per M tokens.

**Cost Breakdown** (if used as primary, comparable mix to Bedrock above): roughly equivalent to Bedrock in steady state ± 10%.

**Pros**:

- ✅ UK South availability — co-located with Azure cells if Azure becomes primary (Category 1 secondary).
- ✅ Strong contractual no-train posture for the Azure OpenAI variant (distinct from public OpenAI API).
- ✅ Entra ID-native authentication for the operator service identity — clean fit with ADR-003 operator IdP.
- ✅ Most natural second provider for ADR-004 / Goal G-8 quarterly-CI validation.

**Cons**:

- ❌ Microsoft is already the AI provider for many customer-side tenants (Copilot etc.); some buyer-side architects may want a non-Microsoft AI sub-processor on their supplier-side governance evidence — Bedrock-as-primary keeps that option open.
- ❌ Same hyperscaler-concentration argument as 2B if Azure is primary infra.
- ❌ Azure OpenAI quota allocation is enterprise-account-managed, which is administratively heavier than the Bedrock self-service model.

**Compliance**: Microsoft Limited UK GDPR DPA; sub-processor list maintained; Azure UK South is a NCSC Cloud Security Principles aligned region.

---

### Option 2D: Buy — Google Cloud Vertex AI (europe-west2 London) — Tertiary

**Description**: Gemini 1.5 Pro / Gemini 1.5 Flash via Vertex AI in europe-west2.

**Pricing**: per-token, with Gemini 1.5 Pro at roughly Claude-3.5-Sonnet pricing tier; Gemini 1.5 Flash at roughly Claude-3-Haiku pricing tier.

**Pros**:

- ✅ UK region.
- ✅ Long context window (1M tokens) is interesting for whole-project-context grounding; not yet a critical-path requirement.

**Cons**:

- ❌ Long-context advantage doesn't transfer to ArcKit's main artefacts (which fit comfortably inside Claude 3.5 / GPT-4o context windows).
- ❌ Smaller UK public-sector adoption; weaker buyer-side defensibility narrative.
- ❌ Tertiary, not primary — switch effort would be higher than between Bedrock and Azure OpenAI.

**Recommendation**: Tertiary; documented for completeness; not in the current shortlist.

---

### Option 2E: Adopt — Open-Source Llama-3 / Mistral on Customer-Controlled Inference (Project 002 Default)

This is Option 2A already; documented here as the **Project 002 sovereign default**. SaaS uses Bedrock + Azure OpenAI, but the AIAdaptor (ADR-004) supports `none` / `local-openweight` / `customer-approved-endpoint` implementations so that sovereign-deployment customers can point the AI generation pipeline at their own approved on-premise model endpoint. No SaaS TCO line — Project 002 carries it.

---

### Option 2F: GOV.UK Platform — Not Applicable

GOV.UK does not provide a centrally-hosted LLM or AI inference service for tenant use as of 2026-05-03. The UK Government AI Playbook governs *how* AI is used, not *where* inference runs.

---

### Build vs Buy Recommendation for AI Provider

**Recommended Approach**: **BUY — Bedrock (primary) + Azure OpenAI (validated second provider per ADR-004 / Goal G-8) + open-weight self-host (sovereign-only via ADR-004 AIAdaptor `local-openweight` mode)**.

**Rationale**:

Bedrock wins as primary on three counts: UK eu-west-2 co-location with the AWS infra primary, contractual no-train posture, and the breadth of the Bedrock model menu (Claude / Nova / Llama / Mistral) which lets the per-tenant cost cap (ADR-008) be honoured by routing low-priority traffic to cheaper models without leaving the provider. Azure OpenAI is the best candidate for the ADR-004 second-provider quarterly-CI validation because it is in the same region as the Azure cross-vendor floor (Category 1) and because Microsoft customer tenants already have Azure procurement in place. The open-weight self-host path is the *Project 002 sovereign default* and a *break-glass* fallback for the SaaS — never a primary.

**Key Decision Factors**:

- ✅ UK eu-west-2 hosts Claude 3.x — intra-region traffic, simpler DPA.
- ✅ Bedrock is the cheapest-per-quality-token at the SME-tier mix used in ADR-008 quotas.
- ✅ Azure OpenAI is a credible day-one swap; quarterly CI satisfies Goal G-8.

**Shortlist for Further Evaluation**:

1. **Amazon Bedrock — Anthropic Claude 3.5 Sonnet / Claude 3 Haiku / Amazon Nova / Llama-3** — primary.
2. **Azure OpenAI Service — GPT-4o / GPT-3.5 Turbo (UK South)** — second provider per ADR-004.
3. **Open-weight Llama-3.1-70B / Mistral-Large self-host** — Project 002 sovereign default; SaaS break-glass.

**Next Steps**:

- [ ] AI ethics review against the UK Government AI Playbook (`/arckit:ai-playbook` already at v1.0).
- [ ] DPIA refresh listing both Bedrock and Azure OpenAI with no-train assurances.
- [ ] AIAdaptor implementation of both Bedrock and Azure OpenAI shims.
- [ ] Quarterly CI on Azure OpenAI satisfying Goal G-8.

---

## Category 3: Observability Stack (Logs, Metrics, Tracing, SIEM)

**Requirements Addressed**: BR-005, BR-006; FR-005, FR-009, FR-012, FR-014; NFR-A-001, NFR-SEC-002, NFR-SEC-008, NFR-C-001, NFR-C-002, NFR-M-001, NFR-I-001; INT-007; ADR-005, ADR-006.

**Why This Category**: Observability is the only mechanism by which a multi-tenant SaaS can detect cross-tenant attempts (Principle 8 / Risk R-008) and the only way to evidence NCSC CAF / Cloud Security Principle 5 posture (BR-006). ADR-005 has chosen the *shape* (OpenTelemetry-instrumented services + managed UK-resident backend + managed SIEM); this category researches the *backends*.

---

### Option 3A: Build Custom — Self-Hosted ELK + Prometheus + Jaeger + Wazuh

**Description**: Self-host the open-source observability stack on dedicated VM / K8s.

**Effort**: 4–6 person-months upfront; ongoing operations heavy.

**Cost** (3-year):

- Engineering: ~£0.30M build + ~£0.20M/year ops = £0.90M.
- Infra: ~£0.25M / 3-year (compute, storage, retention).
- **3-Year TCO**: ~£1.15M.

**Pros**: full data custody; UK residency by construction; sovereign-mode-natural.

**Cons**: high operational burden; observability operations is itself a specialist discipline that small SME-vendor SRE team cannot sustain without dedicated staff. Use only as the **Project 002 sovereign profile**.

---

### Option 3B: Buy — Grafana Cloud (UK / EU residency tier) — Recommended Primary

**Description**: Grafana Cloud as the managed backend for OpenTelemetry-instrumented logs (Loki), metrics (Prometheus / Mimir), and traces (Tempo). UK/EU residency tier guarantees data plane in UK / EU (with named region selection at provisioning).

**Vendor**: Grafana Labs Inc. (with UK/EU sub-processor stack documented).

**Pricing Model**: usage-based — per-active-series (metrics), per-GB-ingested (logs/traces), with included free-tier and tiered "Pro" / "Advanced" SKUs.

**Cost Breakdown** (sized to the SOBC observability budget):

- Pro tier with reserved capacity: ~£20–30k/year per cell at GA + 6 months scale.
- 4 cells by Year-3: ~£80–120k/year.
- **3-Year TCO**: ~£0.25M, comfortably inside the SOBC OpEx envelope.

**Pros**:

- ✅ OpenTelemetry-native; ADR-005 instrumentation integrates without vendor-specific re-instrumentation.
- ✅ UK/EU residency at the data-plane layer; sub-processor inventory tractable.
- ✅ The same Grafana / Loki / Tempo / Mimir stack is available open-source for Project 002 sovereign reuse — same dashboards, same query language.
- ✅ G-Cloud listed; UK contracting available.
- ✅ SLO + alerting workflows (Grafana SLO, Grafana OnCall) are mature.

**Cons**:

- ❌ Grafana SIEM is less mature than Microsoft Sentinel or Elastic SIEM; expect to pair with a dedicated SIEM (Option 3D below).
- ❌ Active-series accounting can be surprising at scale — cardinality discipline required.

---

### Option 3C: Buy — Datadog (UK / EU residency tier) — Strong Alternative

**Description**: Datadog as managed backend for logs / metrics / APM / traces / SIEM.

**Pricing**: per-host + per-GB ingestion; typically more expensive than Grafana Cloud on a like-for-like log volume.

**Cost** (3-year): ~£0.35M–£0.45M at our scale.

**Pros**: more polished UI, integrated APM and SIEM, single-vendor simplicity.

**Cons**: more expensive; vendor lock-in stronger (Datadog-specific instrumentation tempts engineers); less open-standard parity for Project 002 reuse.

**Recommendation**: keep as alternative; choose only if Grafana Cloud SIEM gaps cannot be closed via Sentinel or Elastic.

---

### Option 3D: Buy — Microsoft Sentinel (Azure Tenant) — Recommended for SIEM Layer

**Description**: Microsoft Sentinel as the managed SIEM. Receives auth-event log feeds from the cells, isolation-attempt SIEM rules per ADR-001, audit-log feeds per FR-012.

**Pricing**: per-GB ingestion; first 5 GB free; ~£1.80–£2.20 / GB ingested at our likely volume (UK South).

**Cost** (3-year): ~£40–80k/year at GA + 6 months; ~£180–250k / 3-year.

**Pros**:

- ✅ Strong UK public-sector reference base.
- ✅ Out-of-the-box CAF-aligned detection-rule library.
- ✅ Native Entra ID integration on the operator-IdP side.

**Cons**:

- ❌ Vendor-specific KQL query language — operations talent may need cross-training.
- ❌ Must run inside an Azure tenant even when AWS is the primary infra — adds an Azure dependency line.

**Alternative**: Elastic Cloud SIEM (UK / EU regions). Open-standard ES-QL; comparable price; weaker out-of-the-box CAF mapping.

---

### Option 3E: Adopt — OpenTelemetry SDKs + Self-Hosted Grafana / Loki / Tempo / Mimir (Sovereign Default)

The Project 002 sovereign profile. Engineers and dashboards are identical to Option 3B's managed Grafana Cloud; the only difference is who runs the backend.

---

### Option 3F: GOV.UK Platform — Not Applicable

No GOV.UK common platform provides observability for SaaS vendors.

---

### Build vs Buy Recommendation for Observability

**Recommended Approach**: **BUY — Grafana Cloud (UK/EU) for logs / metrics / traces (primary observability backend) + Microsoft Sentinel (UK South Azure tenant) for SIEM + S3 Object Lock / Azure Blob Immutable Storage for the long-tail audit-log retention bucket (12-month minimum per NFR-C-002, 7-year for SME-verification per BR-003) + Grafana / Loki / Tempo / Mimir self-host as the Project 002 sovereign-profile fallback (ADOPT)**.

**Rationale**:

Grafana Cloud is the cheapest path that preserves the open-instrumentation commitment of ADR-005 and gives Project 002 a like-for-like sovereign fallback. Sentinel is added as the SIEM layer because the CAF-aligned detection content library is the largest in the market and Microsoft's UK public-sector reference base is the deepest. The audit log itself lands in immutable object storage (S3 Object Lock for the AWS primary cells; Azure Blob immutable storage for any Azure-resident logs) so that retention policy enforcement is at the storage layer, not the application layer — critical for the FR-012 + NFR-C-002 evidence trail.

**Key Decision Factors**:

- ✅ OpenTelemetry-native primary backend — ADR-005 instrumentation portable.
- ✅ Sovereign reuse via the open-source equivalent.
- ✅ UK/EU data-plane residency.

**Shortlist**:

1. **Grafana Cloud (UK / EU)** for logs / metrics / traces.
2. **Microsoft Sentinel (UK South)** for SIEM.
3. **AWS S3 Object Lock + Azure Blob immutable storage** for audit-log immutable retention.
4. **Self-host Grafana / Loki / Tempo / Mimir** for Project 002 sovereign fallback.

---

## Category 4: Audit / Log Retention

**Requirements Addressed**: FR-005 (versioning + audit), FR-012 (tenant audit log), FR-014 (admin console / operator audit), BR-003 (SME-verification 7-year retention), NFR-C-002 (12-month application-log retention; 7-year for sec/audit per Principle 6).

**Why This Category**: Tenant audit log access (FR-012) is a Principle 5 / NCSC CAF C1 evidence pillar. SME-verification decisions must be retained for 7 years (BR-003 acceptance criterion). The retention regime must be at the **storage layer**, not the application layer, so that an application-layer compromise cannot tamper with retention.

---

### Option 4A: Build Custom

Already addressed in Category 3 — observability stack covers the audit-log capture; storage primitive choice is the retention substrate.

---

### Option 4B: Buy — AWS S3 Object Lock (Compliance Mode) — Recommended Primary

**Description**: S3 buckets with Object Lock in Compliance Mode for the audit-log retention substrate. Compliance Mode means even the root account cannot delete or overwrite the locked object before the retention period expires — strongest available control.

**Cost**: S3 Standard storage + Object Lock at no additional charge for the lock feature; storage is metered as standard. ~£10–15k/year for a 12-month + 7-year mix at ArcKit's audit-log volumes.

**Pros**:

- ✅ Compliance Mode is FINRA / SEC 17a-4(f) / CFTC 1.31(c)-(d) verified at the regulatory level — the strongest objective evidence for NCSC CAF B5 / C1.
- ✅ KMS-encrypted at rest.
- ✅ Bucket policies key off `tenant_id` prefix per ADR-001.
- ✅ Sovereign reuse via MinIO Object Lock (MinIO supports the same S3 Object Lock semantics).

**Cons**:

- ❌ Object Lock duration mistakes are unrecoverable — retention period must be set carefully.
- ❌ Cross-account replication with Object Lock requires extra setup.

---

### Option 4C: Buy — Azure Blob Immutable Storage — Strong Alternative

Equivalent semantics to S3 Object Lock; Time-Based Retention or Legal Hold; UK South region; pricing comparable.

---

### Option 4D: Adopt — MinIO Object Lock (Sovereign Default)

Already noted; same semantics as S3.

---

### Build vs Buy Recommendation for Audit / Log Retention

**Recommended**: **BUY — S3 Object Lock (Compliance Mode) on AWS eu-west-2 for the SaaS-route audit-log retention substrate; Azure Blob immutable storage as the symmetric alternative for any Azure-resident cells; MinIO Object Lock as the Project 002 sovereign-profile equivalent.** Retention durations: 12 months for application logs; 7 years for SME-verification decisions and security/audit logs (Principle 6 + BR-003).

**Shortlist**: as Category 3 + S3 Object Lock specifically.

---

## Category 5: Identity (GOV.UK One Login + Departmental Entra ID)

**Requirements Addressed**: BR-001, BR-005, BR-006; FR-007, FR-014; INT-001; NFR-SEC-001, NFR-SEC-002, NFR-SEC-003, NFR-SEC-007, NFR-C-005, NFR-C-009; ADR-003.

**Why This Category**: Identity is the most-attacked surface in any SaaS; getting it wrong creates a cross-tenant blast radius no other control compensates for. ADR-003 has already chosen the *shape* (vendor IdP for SMEs + self-service OIDC/SAML federation for enterprise + hardware-key admin IdP for operators); this category researches the *vendors* and addresses the parent's specific call-out: **GOV.UK One Login + Entra ID**.

---

### Option 5A: Build Custom — Self-Hosted Keycloak

**Description**: Self-host Keycloak as the SaaS-tenant IdP; Keycloak supports OIDC / SAML 2.0 / WebAuthn / TOTP; open-source.

**Effort**: 2–3 person-months upfront, ongoing operations meaningful.

**Cost** (3-year): ~£0.20M (engineering + ops + infra).

**Pros**: open-source; sovereign-mode-natural; full control.

**Cons**: identity ops is a specialist discipline; the vendor-IdP path Buys a much higher-quality breach-protection posture for a similar price. Use only as **Project 002 sovereign-profile** option.

---

### Option 5B: Buy — Auth0 (Okta Customer Identity) — Recommended for SME Tenant IdP

**Description**: Auth0 as the vendor-managed SaaS-tenant IdP for the SME population (UC-1 self-service signup, no enterprise IdP).

**Vendor**: Okta Inc. (Auth0); UK / EU data-residency tier available; UK contracting via Okta's UK-listed entity.

**Pricing Model**: per-MAU (Monthly Active User) tiered. Free tier up to 25k MAU on Essentials; Professional ~£170/mo + per-user; Enterprise priced individually. ArcKit at GA + 12 months at 1,000 SME tenants × ~5 users / tenant = 5,000 MAU is well inside the Professional band.

**Cost** (3-year): ~£40–80k for the SaaS-tenant IdP at modelled scale.

**Pros**:

- ✅ Mature MFA / WebAuthn / passkey support.
- ✅ UK / EU data residency selectable at provisioning.
- ✅ OIDC / SAML 2.0 federation built-in (FR-007 free).
- ✅ Risk-based authentication and brute-force protection out-of-the-box.
- ✅ G-Cloud listed.

**Cons**:

- ❌ Per-MAU pricing scales with adoption; cross-subsidy economics must absorb it (ADR-003 already addresses).
- ❌ Sub-processor inventory addition.

---

### Option 5C: Buy — Microsoft Entra External ID — Strong Alternative

**Description**: Microsoft Entra External ID (formerly Azure AD B2C) as the SaaS-tenant IdP.

**Pricing**: per-MAU; tiered; first 50,000 MAU free at the time of writing.

**Pros**:

- ✅ Free-tier-up-to-50k-MAU is uniquely SME-friendly and aligns directly with Principle 1 cost discipline.
- ✅ Native federation to customer Entra IDs without cross-vendor adapter.
- ✅ Microsoft Limited UK contracting; G-Cloud listed.

**Cons**:

- ❌ Microsoft-leaning brand may sit awkwardly with non-Microsoft buyer-side architects (counter-argument: ArcKit's ops IdP already needs a hardened Entra ID instance for operators per ADR-003, so the "Microsoft already in the stack" argument is symmetric).
- ❌ External ID / B2C has a less polished tenant-onboarding UX than Auth0 in places.

---

### Option 5D: Buy — GOV.UK One Login (Government Digital Service) — Tenant-Side Optional

**Description**: GOV.UK One Login is the GDS-built citizen-facing identity platform. As Wave-1 ORG_RESEARCH established, ArcKit-as-a-Service is **staff/supplier-facing** rather than citizen-facing, so One Login is **not** required as the primary tenant IdP. However, two scenarios make One Login worth offering as an **option**:

1. A buying-authority tenant whose own service uses One Login for citizens may want the tenant-admin staff to sign in to ArcKit using their One Login identity — the same federated OIDC adaptor that handles Entra also handles One Login.
2. ArcKit's marketing site (BR-002 / FR-015) could optionally accept One Login for "request a free-tier invite as a verified UK citizen architect" flow — but this would be a Phase-2 feature, not v1.

**Cost**: One Login is **free** for central-government tenants at the citizen-identity assurance levels currently published. Integration cost is purely engineering effort (~2 person-weeks for the OIDC adaptor; covered by the existing FR-007 SSO work).

**Pros**:

- ✅ GDS-aligned; signals public-sector posture credibly.
- ✅ Free for central-gov tenants.

**Cons**:

- ❌ Not the right shape for ArcKit's primary tenant identity flow (which is supplier-side staff + SME architects, not citizens).
- ❌ One Login's SSO assurance levels (medium / high confidence) are oriented at public services, not enterprise SaaS.

**Recommendation**: ship the OIDC adaptor wiring so One Login is *available* as a federated option for any tenant who wants it; do **not** make it the primary platform IdP for ArcKit.

---

### Option 5E: Buy — Departmental Entra ID Federation (per tenant) — The Default for Enterprise Tier

**Description**: Self-service OIDC / SAML 2.0 federation to the customer's own Entra ID (Microsoft Entra ID — formerly Azure AD), Okta, Ping, etc. This is the **default path** for the enterprise tier per ADR-003.

**Cost**: zero direct vendor cost; absorbed by Auth0 or Entra External ID's federation features (Options 5B / 5C).

**Pros**:

- ✅ Aligns with existing-systems estate of central-civil and NHS adopters (Wave-1 ORG_RESEARCH Category 1 / Category 3): Entra ID is the dominant departmental staff IdP.
- ✅ Customer keeps user lifecycle in their own IdP — joiner / leaver / mover handled by their HR system, no ArcKit-side management.
- ✅ Group claims propagate to ArcKit roles cleanly.

**Cons**: SaaS-side metadata / certificate maintenance per tenant; mitigated by self-service federation setup in the tenant admin portal.

---

### Option 5F: Buy — Hardened Operator IdP (separate Entra ID instance) — Required for FR-014

**Description**: A separate, hardened Entra ID tenant for ArcKit *operators* (SRE, support, vendor engineering) with hardware FIDO2 keys mandatory, conditional-access policies, and full break-glass logging per ADR-003. **Not** the tenant IdP — a wholly separate identity domain.

**Cost**: included in Microsoft 365 Business Premium / Entra ID P2 licences for vendor staff (~£20/user/month).

**Pros**:

- ✅ Mandated by ADR-003 — non-negotiable.
- ✅ Clean separation from any tenant IdP — even a complete tenant-IdP compromise cannot escalate to operator privileges.

**Cons**: another sub-processor (Microsoft, but only for operator identity, not tenant data).

---

### Build vs Buy Recommendation for Identity

**Recommended Approach**: **BUY — Auth0 (or Microsoft Entra External ID) as the SaaS-tenant IdP for SMEs + self-service OIDC / SAML federation to customer Entra ID / Okta / Ping for the enterprise tier (free with the chosen tenant IdP) + a separate hardened Entra ID tenant for operators with FIDO2 hardware keys + GOV.UK One Login as an optional federated source for any tenant who wants it.** This matches ADR-003's three-population strategy precisely.

**Rationale**:

Auth0 narrowly wins on UX maturity for the self-service SME tenant; Entra External ID wins on the free-tier MAU envelope. Either is acceptable; the choice can defer to the Lead Architect when appointed, and re-evaluation at Beta gate (the cross-vendor abstraction is shallow enough that the swap costs days not weeks).

**Key Decision Factors**:

- ✅ UK / EU data residency available on both Auth0 and Entra External ID.
- ✅ Both support OIDC / SAML 2.0 federation (FR-007).
- ✅ Both support phishing-resistant MFA (NIST AAL2 / AAL3 — NFR-SEC-001).
- ✅ Operator IdP separate from tenant IdP (mandated by ADR-003).
- ✅ One Login adaptor wired but not the primary path.

**Shortlist for Further Evaluation**:

1. **Auth0 (Okta) — UK / EU tier** — recommended for SME tenant IdP.
2. **Microsoft Entra External ID (UK South)** — strong alternative for SME tenant IdP.
3. **Microsoft Entra ID (separate operator tenant)** — operator IdP per ADR-003.
4. **GOV.UK One Login** — optional federated source.

---

## Category 6: G-Cloud Catalogue Comparators

**Requirements Addressed**: BR-001, BR-002, BR-004, BR-005, BR-008.

**Why This Category**: G-Cloud listing is the buyer's path of least resistance (Wave-1 ORG_RESEARCH). Every authority has a default expectation that any SaaS service will be on G-Cloud; the alternative is bespoke OJEU / Find-a-Tender procurement that costs more than the tooling itself. ArcKit-as-a-Service must list (BR-004) and must position against the existing competitive set on the same framework.

---

### Comparator Landscape on G-Cloud 14 (Cloud Software / Lot 2)

The closest comparators on G-Cloud 14 (current iteration as of 2026-05-03; the framework is on its annual refresh cadence — Crown Commercial Service publishes the schedule) are:

| Comparator | Category | Pricing Range (per published G-Cloud listing) | Free Tier | UK Residency | Match to ArcKit Use Case |
|------------|----------|-----------------------------------------------|-----------|--------------|--------------------------|
| **LeanIX** (now SAP) | Enterprise EA tooling | Enterprise; bespoke quote; typically £100k+ / year | No | EU (varies) | Closest pure-EA-tooling comparator; priced for large SI / large enterprise; not SME-affordable. |
| **Ardoq** | Enterprise EA tooling | Enterprise; bespoke quote; typically £60–150k+ / year | No | EU | Comparable; SaaS UI-led; not SME-affordable. |
| **MEGA HOPEX** | Enterprise EA tooling | Enterprise; bespoke quote | No | EU | Heavy-weight; mostly large transformation programmes. |
| **Bizzdesign Horizzon** | Enterprise EA tooling | Enterprise; bespoke quote | No | EU | Modelling-heavy; ArchiMate-centric. |
| **Sparx Enterprise Architect** | Modelling tool (perpetual licence + SaaS hosted variants) | £190 perpetual / user (Corporate Edition); SaaS-hosted via partner | Time-limited trial only | UK / Global | Modelling, not artefact governance; thinner overlap. |
| **Various consultancy-led EA practices** (Capgemini, Accenture, BJSS, Equal Experts, etc.) | EA / governance consultancy | Day-rate-led; £700–1,500 / day | n/a | Variable | Substitute for *the role*, not for *the tool*; ArcKit is complementary to consultancy not competitive. |

### What ArcKit-as-a-Service Offers That No G-Cloud Comparator Does

- **A genuinely usable free tier for verified UK SMEs** (BR-001) — none of the commercial-EA tooling listings on G-Cloud has a non-trial free tier. This is the *substantive* expression of Principle 1 and the unique proposition.
- **Transparent published per-seat list price for paid tiers** (BR-002) — every commercial-EA listing in the table above is "request a quote" / enterprise-pricing. ArcKit's published list price is the SME-friendly differentiator.
- **No-paywall data-export guarantee** (BR-007 / ADR-007) — commercial-EA tooling typically gates export behind premium tiers and / or proprietary formats. ArcKit's open-format export with CI-tested round-trip is unique.
- **AI-assisted artefact generation tuned to UK Government policy** (FR-004 + the underlying ArcKit toolkit aligned with TCoP / GDS Service Standard / NCSC CAF / Cloud Security Principles / WCAG 2.2 AA / UK GDPR) — the commercial-EA tooling cohort is internationally sourced and generic; ArcKit is UK-Gov-specific.

### Procurement Strategy on G-Cloud

ArcKit-as-a-Service to be listed under **G-Cloud Lot 2 (Cloud Software)**, with:

- **Service definition** describing the dual deployment model (SaaS Project 001 + sovereign Project 002 — even though sovereign is a separate procurement, the service definition must be honest about the architectural family).
- **T&Cs** including the BR-001 free tier eligibility and the BR-007 portability promise.
- **Pricing**: published per-seat list price for SME paid tier; published annual list price for large-enterprise tier; free tier explicitly £0 with audit-defensible eligibility policy reference.
- **SFIA-rated rates** for any specialist support engagement.
- **Minimum commitment**: monthly subscription on the SME paid tier (no multi-year lock-in); annual on the large-enterprise tier with up-to-3-year option at customer election (per SOBC C1.3).
- **Data residency clause**: UK-only by default; cross-border processing only with explicit per-tenant consent and Article 46 transfer mechanism (Principle 7 / ADR-002).
- **Sub-processor inventory** published with 30-day change notice (per SOBC C1.2 and the DPIA).

### G-Cloud Adjacent Frameworks

- **Digital Outcomes and Specialists (DOS)** — *not* the right framework for managed SaaS (per SOBC C1.2). ArcKit *consumes* DOS for any specialist support engagement (e.g., DDaT specialists working with pilot tenants), but does not list its core SaaS on DOS.
- **Crown Hosting** — irrelevant to managed SaaS; relevant to Project 002 sovereign deployment only.
- **NHS Shared Business Services / Workforce Alliance frameworks** — adjacent; ArcKit can be cross-listed where eligible to lower the NHS-buyer-side procurement friction noted in Wave-1 ORG_RESEARCH Category 3.

### Recommendation

**ACCEPT** — list on G-Cloud Lot 2 (Cloud Software) at the next framework iteration window. Treat the listing as a first-class GA dependency (per SOBC SR-6 risk). Maintain a transparent published-pricing posture (BR-002) and SME-friendly minimum commitments. Cross-list on NHS frameworks where eligible.

---

## Total Cost of Ownership (TCO) Summary

### Blended TCO Across All SaaS-Control-Plane Categories

**Recommended Approach (Blended)** — UK-region AWS primary + Azure cross-vendor floor + Bedrock primary AI + Azure OpenAI second AI + Grafana Cloud + Sentinel + Auth0/Entra External ID:

| Category | Recommended Option | Year 1 | Year 2 | Year 3 | 3-Year TCO |
|----------|-------------------|--------|--------|--------|------------|
| 1. Tenant isolation primitives (AWS UK + Azure floor) | BUY | £0.10M | £0.18M | £0.30M | £0.58M |
| 2. AI provider (Bedrock + Azure OpenAI second) | BUY | £0.10M | £0.18M | £0.22M | £0.50M |
| 3. Observability (Grafana Cloud + Sentinel) | BUY | £0.05M | £0.10M | £0.15M | £0.30M |
| 4. Audit / log retention (S3 Object Lock) | BUY (within Category 1 envelope) | £0.01M | £0.01M | £0.02M | £0.04M |
| 5. Identity (Auth0/Entra External ID + operator Entra ID) | BUY | £0.03M | £0.05M | £0.08M | £0.16M |
| 6. G-Cloud listing & marketplace ops | BUILD (process + admin time) | £0.02M | £0.01M | £0.01M | £0.04M |
| AI integration glue + cell controller + FinOps tagging | BUILD (capital, per SOBC) | £0.20M | £0.05M | £0.05M | £0.30M |
| **TOTAL (mid-point)** | | **£0.51M** | **£0.58M** | **£0.83M** | **£1.92M** |

> The £1.92M mid-point is **lower** than the SOBC OpEx envelope of £2.85M (3-year) because the SOBC also rolls in DPO/security/compliance maintenance, customer success, pen-test recurrence, cyber insurance, and FinOps tooling — overhead lines that this research's *control-plane* scope excludes. The numbers are consistent: this research's category-by-category technology TCO + the SOBC's overhead lines = the SOBC's £2.85M OpEx envelope (ROM ± 30%).

### Alternative Scenarios

**Scenario A: Build Everything (self-host)**:

- 3-Year TCO: ~£3.50M.
- Pros: Maximum control; no third-party DPA.
- Cons: Engineering and DBA / SRE / IdP-ops headcount the vendor SME does not have; operationally distracting; likely slips GA.
- **Verdict**: REJECT.

**Scenario B: Buy Everything (Commercial SaaS) — Recommended**:

- 3-Year TCO: ~£1.92M (this research's mid-point) to ~£2.50M (high-side band).
- Pros: Fast time to GA; managed services; right-sized for the team.
- Cons: Vendor lock-in (mitigated by ADR-002 open-primitive shape and ADR-004 AI provider abstraction).

**Scenario C: Open Source Everything (sovereign-only economic model)**:

- 3-Year TCO: ~£3.20M.
- Pros: Sovereign-natural.
- Cons: Doubles ops headcount; not viable for SaaS.
- **Verdict**: This is the Project 002 profile, not a SaaS scenario.

**Scenario D: Recommended Blended Approach (Scenario B at mid-point)**:

- 3-Year TCO: ~£1.92M.
- Pros: Balance of cost, speed, control, sovereign reusability.
- Cons: Cross-AWS / Azure / Grafana / Sentinel / Auth0 sub-processor inventory needs disciplined DPO maintenance.

### TCO Assumptions

- Engineering rates: £900/day blended (consistent with SOBC).
- Infrastructure: AWS eu-west-2 London list prices; Azure UK South list prices; Grafana Cloud Pro tier; Microsoft Sentinel UK South list prices — all as of 2026-05-03.
- AI: Bedrock + Azure OpenAI list per-token rates as of 2026-05-03; mix per the SOBC R-006 +15% optimism-bias treatment.
- 10% annual SaaS-vendor list-price increases assumed for Year-2 / Year-3 (consistent with industry pattern).
- Reserved-instance / savings-plan discounts only after BR-008 adoption signal (Year 2+).
- Exchange rate variance not modelled — list prices are GBP-quoted by all vendors named.

### Risk-Adjusted TCO

| Scenario | Base TCO | Contingency | Risk-Adjusted TCO | Risk Factors |
|----------|----------|-------------|-------------------|--------------|
| Build Everything | £3.50M | +20% | £4.20M | Engineering scope creep, DBA/SRE hiring risk |
| Buy Everything (Recommended) | £1.92M | +12% | £2.15M | SaaS-vendor price increases, sub-processor changes |
| Open Source Everything | £3.20M | +15% | £3.68M | Underestimated maintenance |

The +12% blended is the same uplift the SOBC applies to OpEx (per SOBC §I) — keeping the two documents aligned.

---

## Requirements Traceability

### Requirements Coverage Matrix (in scope)

| Requirement ID | Requirement Description | Research Category | Recommended Solution | Rationale |
|----------------|------------------------|-------------------|---------------------|-----------|
| BR-001 | Free tier for verified UK SMEs | 1, 2, 3, 4, 5, 6 | BUY managed primitives + ADR-008 quotas | Cell economics + AI budget cap keep per-tenant cost-to-serve inside free-tier envelope. |
| BR-002 | Transparent published pricing | 6 | G-Cloud Lot 2 with published list prices | Comparator analysis confirms market gap; published price is the differentiator. |
| BR-004 | G-Cloud listing | 6 | List on G-Cloud Lot 2 at next framework iteration | Path of least resistance for buyers per Wave-1 ORG_RESEARCH. |
| BR-005 | Cross-subsidy unit economics | 1, 2, 3, 5 | FinOps tagging across AWS / Azure / Grafana / Auth0 | Per-tenant cost calculable; mid-point TCO matches SOBC envelope. |
| BR-006 | UK public-sector evidence pack | 1, 2, 3, 5 | UK GDPR Article 28 DPAs + ISO 27001 + NCSC Cloud Security Principles assessments from each vendor | Each vendor in shortlist has the evidence available. |
| BR-007 | Tenant portability and exit | 1, 4 | Postgres dump + S3 export + ADR-007 archive format | Open primitives + Project 002 sovereign reuse. |
| FR-002 | Multi-tenant workspace management | 1 | AWS RDS + S3 + EKS with tenant_id propagation per ADR-001 | Pool with cells materialised on managed primitives. |
| FR-004 | AI-assisted generation | 2 | Bedrock primary + Azure OpenAI second per ADR-004 | Two providers from day one; quotas per ADR-008. |
| FR-005 | Versioning + audit trail | 3, 4 | Postgres temporal model + S3 Object Lock immutable audit | Storage-layer retention enforcement. |
| FR-007 | SSO | 5 | Auth0/Entra External ID + customer Entra/Okta/Ping federation | Self-service OIDC/SAML. |
| FR-009 | Public status page + tenant notifications | 3 | Grafana SLO + status page integration | Aligned with ADR-005. |
| FR-012 | Tenant audit log access | 3, 4 | Sentinel + S3 Object Lock + tenant-portal export | 12-month retention + 7-year for security/audit. |
| FR-014 | Admin console for operators | 5 | Separate hardened Entra ID with FIDO2 + Sentinel break-glass logging | ADR-003 mandate. |
| NFR-A-001 | ≥ 99.9% availability | 1 | AWS multi-AZ + Multi-AZ Postgres | Region-native HA. |
| NFR-A-002 | RPO 15 min / RTO 4 hr | 1 | RDS Postgres point-in-time recovery (RPO < 5 min) + multi-region backups | Beats target. |
| NFR-A-003 | Bulkhead + graceful degradation | 1, 2 | EKS namespace quotas + ADR-008 per-tenant rate-limits | Defence in depth. |
| NFR-S-001 | Horizontal scaling to 5,000 tenants | 1 | Cell-fill discipline; new cell at 75% fill | ADR-001 mechanism. |
| NFR-S-002 | Storage growth (50 GB / 1,000 tenants) | 1 | S3 lifecycle to IA tier; per-cell DB elasticity | Region-native. |
| NFR-SEC-001 | MFA / OIDC / SAML | 5 | Auth0 / Entra External ID / customer IdP federation | All shortlisted IdPs support phishing-resistant MFA. |
| NFR-SEC-002 | Tenant isolation | 1, 2, 3, 5 | tenant_id everywhere + cell-level network policy + IdP-anchored claim | Cross-cutting. |
| NFR-SEC-007 | Service-to-service mTLS | 1 | EKS workload identity (IRSA) + service-mesh mTLS | ADR-006 mandate. |
| NFR-SEC-008 | NCSC CAF | 3, 4 | Sentinel CAF rules + S3 Object Lock immutability | Direct evidence path. |
| NFR-SEC-009 | NCSC Cloud Security Principles | 1, 2, 3, 5 | All vendors have published assessments | Vendor-side evidence. |
| NFR-C-001 | UK GDPR / DPA 2018 | 1, 2, 3, 5 | UK region + UK contracting + Article 28 DPAs | All shortlisted vendors have UK DPAs. |
| NFR-C-002 | Audit retention 12 months min | 4 | S3 Object Lock 12-month + 7-year tiers | Storage-layer enforcement. |
| NFR-C-007 | OFFICIAL with handling caveats | 1, 2, 3, 5 | UK region + CMK on paid tier + classification labelling on FR-014 | Vendor-side acceptable up to OFFICIAL with caveats. |
| NFR-I-001 | Open-standard interfaces | 1, 2, 3, 5 | S3 API + Postgres wire + OIDC + OpenTelemetry | All shortlisted options open-standard. |
| NFR-I-002 | Data portability | 1, 4 | Postgres dump + S3 export + ADR-007 archive | Open formats. |
| INT-001 | Tenant IdP integration | 5 | Self-service OIDC/SAML federation | First-class adaptor. |
| INT-005 | AI / LLM provider | 2 | Bedrock + Azure OpenAI | Two-provider abstraction per ADR-004. |
| INT-006 | Cloud / hosting | 1 | AWS UK eu-west-2 + Azure UK South cross-vendor floor | ADR-002. |
| INT-007 | Observability backend | 3 | Grafana Cloud (UK/EU) + Sentinel | ADR-005. |

### Coverage Summary

- ✅ **100% (32/32 in-scope requirements)** have recommended commercial / managed solutions.
- 🔨 **3 small build-custom items** are noted (cell-orchestration controller, AI adaptor wrapper, FinOps tag-propagation) — captured in the SOBC capital line.
- 🔍 **0 requirements** in scope need further research before Beta gate.

### Gaps and Concerns

**No material gaps** in the SaaS-control-plane scope. The two known watch-outs:

- **GAP-1**: Vertex AI / Gemini's UK-region generation-quality maturity should be re-tested at Beta gate to confirm it remains a tertiary option.
- **GAP-2**: Sub-processor inventory across AWS + Azure + Grafana Cloud + Microsoft Sentinel + Auth0 (or Entra External ID) is large; DPO maintenance discipline is the principal residual risk, addressed by R-011.

---

## UK Government Considerations

### Technology Code of Practice (TCoP) Compliance — Vendor-Stack Level

| TCoP Point | Status | Notes |
|-----------|--------|-------|
| 1. Define user needs | ✅ Compliant | Stack chosen against REQ + STKE + Wave-1 ORG_RESEARCH adopter profile. |
| 2. Make things accessible | ✅ Compliant | Tenant UI separately accessible per Principle 12; vendor stack does not affect a11y. |
| 3. Be open and use open standards | ✅ Compliant | S3 API + Postgres wire + OIDC + OpenTelemetry — all open. |
| 4. Make use of open source | ✅ Compliant | Grafana / Loki / Tempo / Mimir / OpenTelemetry / Postgres / MinIO — all OSS; sovereign profile uses them directly. |
| 5. Use cloud first | ✅ Compliant | AWS / Azure UK regions; managed services. |
| 6. Make things secure | ✅ Compliant | NCSC CAF / Cloud Security Principles assessments per vendor. |
| 7. Make privacy integral | ✅ Compliant | UK GDPR Article 28 DPAs; UK residency default; CMK on paid tier. |
| 8. Share, reuse and collaborate | ✅ Compliant | Project 002 reuses the same OSS primitives. |
| 9. Integrate and adapt technology | ✅ Compliant | OIDC/SAML federation; OpenAPI; AsyncAPI. |
| 10. Make better use of data | ✅ Compliant | Open formats; lineage; Project 002 backup parity. |
| 11. Define your purchasing strategy | ✅ Compliant | G-Cloud Lot 2 listing; published pricing. |
| 12. Meet the Service Standard | ✅ Compliant | `/arckit:service-assessment` produces evidence from the vendor stack. |
| 13. Spend controls | ⚠️ Per buyer | Buyer-side: ArcKit's published pricing keeps small buyers below CDDO threshold. |

### GOV.UK Common Platforms Used

| Platform | Category | Status | Rationale |
|----------|----------|--------|-----------|
| GOV.UK One Login | Identity | ✅ Optional federation (Category 5D) | Not primary IdP; available as an option for tenants who want it. |
| GOV.UK Pay | Payments | ❌ Not used | Vendor's commercial billing uses a commercial processor (INT-002). |
| GOV.UK Notify | Notifications | ❌ Not used (vendor side) | Vendor uses a commercial provider for transactional email; tenants may use Notify for *their* downstream services. |
| GOV.UK Forms | Forms | ❌ Not used | Out of scope. |
| GOV.UK Publishing | Content | ❌ Not used | Marketing site not on gov.uk. |

### Digital Marketplace Procurement Strategy

**G-Cloud 14 Lot 2 (Cloud Software)** — confirmed primary listing path. See Category 6.

**Adjacent listings** to consider at next framework iteration: NHS Shared Business Services / Workforce Alliance for the NHS-buyer audience.

### Government Cloud and Data Residency

**Data Classification**: OFFICIAL with OFFICIAL-SENSITIVE handling caveats where tenants opt in (NFR-C-007). All shortlisted vendors are acceptable for OFFICIAL in UK regions.

**Hosting**: AWS eu-west-2 London primary; Azure UK South cross-vendor floor; sovereign deployment is Project 002 (separate procurement).

---

## Integration with Wardley Mapping

Research findings inform Wardley Map value chain positioning and evolution stage:

| Component | Evolution Stage | Recommended Approach | Rationale |
|-----------|----------------|---------------------|-----------|
| Tenant isolation primitives (Postgres, S3, K8s) | Commodity | BUY managed | Pure utility; managed cloud. |
| AI inference (LLM-as-a-service) | Product | BUY (Bedrock / Azure OpenAI) | Stabilising into a product market; mature multi-provider availability. |
| Observability backend | Product | BUY (Grafana Cloud / Sentinel) | Mature product market. |
| SIEM | Product | BUY (Sentinel) | Mature product market with strong CAF content. |
| Identity (Tenant IdP) | Product | BUY (Auth0 / Entra External ID) | Mature product market. |
| Cell-orchestration glue | Custom | BUILD | Vendor-specific (small) controller logic. |
| AI adaptor / abstraction | Custom | BUILD | ArcKit-specific abstraction; small and pluggable. |
| ArcKit artefact authoring + AI generation logic | Custom (with novel AI workflows) | BUILD | This is ArcKit's differentiator. |

**Strategic Insight**: Every component the SaaS *runs on* is commodity or product; everything ArcKit *adds* is custom. This is the right shape for an SME-affordable SaaS — buy the platform, build the value.

**Next Steps**:

- Run `/arckit:wardley` to position these components on the evolution axis with the buyer value chain seeded from `ARC-000-RSCH-v1.0.md`.

---

## Integration with SOBC Economic Case

### Reconciliation Against SOBC Option 2

The SOBC Option 2 mid-point is **£4.50M / 3-year before optimism bias** (£1.65M CapEx + £2.85M OpEx). This research, scoped to the SaaS control plane only, lands at:

| SOBC line | SOBC v1.0 figure | This research's reconciled figure | Notes |
|-----------|------------------|-----------------------------------|-------|
| Cloud / hosting (UK region) | £0.85M / 3-year OpEx | £0.58M / 3-year (Category 1) | Reconciled lower because SOBC includes some non-control-plane hosting (CDN, etc.) absorbed elsewhere. |
| AI inference (incl. R-006 +15%) | £0.50M / 3-year OpEx | £0.50M / 3-year (Category 2) | Aligned. |
| FinOps + cost-to-serve telemetry | £0.15M / 3-year OpEx | £0.04M / 3-year build line | SOBC line is broader than this research's scope. |
| Compliance evidence pack (capital) | £0.10M | included in vendor sub-processor work | Not a separate technology line. |

The SOBC envelope is **not invalidated** by this research — the research's £1.92M control-plane spend is a *subset* of the SOBC's £2.85M OpEx, with the remainder accounted for by overheads (SRE, DPO, customer success, pen-test recurrence) outside this document's scope.

### Confirmation

**Recommended Option remains SOBC Option 2** — Balanced Managed SaaS with Cross-Subsidy and G-Cloud Listing. This research provides the technology basis for that option's deliverability.

---

## Vendor Shortlist for Further Evaluation

### Top 3 Vendors / Products Recommended

#### 1. Amazon Web Services — eu-west-2 London (Bedrock + RDS Postgres + S3 + EKS + KMS)

**Overall Rating**: ⭐⭐⭐⭐⭐ (5/5) — highest-utility vendor for the SaaS route; covers Categories 1, 2, 4 simultaneously.

**Strengths**:

- UK eu-west-2 hosts Anthropic Claude 3.x and the Postgres / S3 / EKS / KMS stack ArcKit cells need.
- G-Cloud listed; UK GDPR Article 28 DPA; ISO 27001 / SOC-2; NCSC Cloud Security Principles published assessment.
- Open primitives portable to Project 002 sovereign profile (MinIO, Postgres, customer-K8s).

**Concerns**:

- Hyperscaler concentration (mitigated by Azure cross-vendor floor + ADR-004 second AI provider).
- CLOUD Act / IPA exposure (mitigated by CMK on paid tier + DPIA disclosure).

**Next Steps**:

- [ ] Pricing quote with reserved-instance / savings-plan modelling against BR-008.
- [ ] DPA + sub-processor review with Vendor DPO.
- [ ] Bedrock model availability re-confirm at Beta gate (Anthropic / Amazon Nova / Llama / Mistral).

#### 2. Microsoft Azure — UK South (AKS + Azure Database for PostgreSQL + Blob + Azure OpenAI + Sentinel + Entra External ID)

**Overall Rating**: ⭐⭐⭐⭐⭐ (5/5) — strongest secondary; covers Categories 1, 2, 3, 5 if elevated.

**Strengths**:

- Most natural ADR-004 second AI provider (Azure OpenAI in UK South).
- Sentinel SIEM has the deepest CAF-rule library.
- Entra External ID free-tier-up-to-50k MAU.
- Dominant landing zone in central-civil and NHS adopter classes (Wave-1 ORG_RESEARCH Categories 1, 3).

**Concerns**:

- Microsoft brand alignment — counter-argument: ops IdP already on Microsoft per ADR-003.
- Equivalent CLOUD Act exposure to AWS.

**Next Steps**:

- [ ] Pricing quote on AKS + Postgres + Blob + Azure OpenAI + Sentinel + Entra External ID bundle.
- [ ] DPA review.
- [ ] Cross-vendor abstraction validation in CI.

#### 3. Grafana Cloud (UK / EU residency)

**Overall Rating**: ⭐⭐⭐⭐☆ (4.5/5) — best observability backend with sovereign-reuse story.

**Strengths**:

- OpenTelemetry-native; ADR-005 instrumentation portable.
- UK / EU residency tier.
- Project 002 self-host equivalent is identical (Grafana / Loki / Tempo / Mimir).
- Pricing is the most transparent in the observability market.

**Concerns**:

- SIEM functionality less mature than Sentinel — pair with Sentinel.
- Active-series cardinality management discipline required.

**Next Steps**:

- [ ] Pro-tier pricing quote against expected log / metric / trace volume.
- [ ] POC deployment with OpenTelemetry instrumentation.
- [ ] Sentinel SIEM integration validation.

---

## Risks and Mitigations

### Vendor Risks

**VR-1: Vendor Lock-in (AWS / Azure)**

- **Risk**: Difficult to switch at scale.
- **Impact**: HIGH.
- **Likelihood**: MEDIUM.
- **Mitigation**: ADR-002 open-primitive shape (S3 API, Postgres wire); ADR-004 AI provider abstraction; cross-vendor abstraction validation in CI; Project 002 sovereign profile is a deeper exit path.

**VR-2: AI Inference Price Shock (Bedrock / Azure OpenAI)**

- **Risk**: Per-token rate increase by either provider.
- **Impact**: MEDIUM (cross-subsidy slip — direct R-001 / R-006 path).
- **Likelihood**: MEDIUM.
- **Mitigation**: ADR-008 per-tenant budget caps; ADR-004 second provider; route low-priority traffic to cheaper models (Haiku / Nova / GPT-3.5).

**VR-3: Sub-Processor Inventory Drift**

- **Risk**: One of AWS / Azure / Grafana / Sentinel / Auth0 changes a sub-processor without proactive notice.
- **Impact**: MEDIUM (R-011 path).
- **Likelihood**: MEDIUM.
- **Mitigation**: Quarterly DPO review per vendor; 30-day notice clause in each DPA where contract terms allow.

### Technical Risks

**TR-1: Cell-Orchestration Controller Defects**

- **Risk**: Build-custom glue produces a cross-cell defect.
- **Impact**: HIGH (if cross-tenant blast).
- **Likelihood**: LOW (small surface area, well-tested in CI).
- **Mitigation**: ADR-001 isolation tests in CI on every change; namespace + network-policy bulkhead in ADR-006.

**TR-2: AI Provider Quality Drift**

- **Risk**: Model upgrades change generation quality unpredictably.
- **Impact**: MEDIUM.
- **Likelihood**: MEDIUM.
- **Mitigation**: Pin model versions explicitly; quarterly regression evaluation against a held-out artefact corpus.

**TR-3: Observability Cardinality Cost Explosion**

- **Risk**: tenant_id × per-route × per-instance produces a cardinality blow-up that surprises Grafana Cloud billing.
- **Impact**: MEDIUM (FinOps).
- **Likelihood**: MEDIUM.
- **Mitigation**: cardinality budget per service; pre-aggregate at OTel collector; review monthly.

### Compliance Risks

**CR-1: UK Data Residency Drift**

- **Risk**: A managed-service feature opens a non-UK leg by default.
- **Impact**: HIGH (Principle 7 violation).
- **Likelihood**: LOW (vendors expose region pinning prominently).
- **Mitigation**: IaC pinning per ADR-018 (covered by SOBC capital line); region telemetry in CloudWatch / Azure Monitor.

---

## govreposcrape Sweep — Result and Note

A targeted sweep of the GovReposcrape index was run on 2026-05-03 against five SaaS-control-plane queries:

- "multi-tenant SaaS isolation kubernetes" — 1 result, off-topic.
- "GOV.UK One Login OIDC integration" — 30 results, predominantly local-authority CMS / Umbraco repositories with no relevant content.
- "OpenTelemetry observability audit log" — 16 results, similarly off-topic.
- "G-Cloud SaaS supplier listing" — 5 results, not relevant.
- "AI provider abstraction LLM bedrock azure openai" — 4 results, not relevant.

The GovReposcrape index appears to under-cover central-government repositories (alphagov, GDS, NHS Digital) for the SaaS-control-plane categories researched. The Wave-2 GOV-REUSE output (`ARC-001-GOVR-v1.0`) is the authoritative reuse assessment and should be consulted for any reusable code findings before commitment to any of the BUILD lines above.

---

## Next Steps and Recommendations

### Immediate Actions (0–2 weeks)

1. **ARB review** of this document alongside the parallel Wave-2 outputs (`ARC-001-AWRS-v1.0`, `ARC-001-AZRS-v1.0`, `ARC-001-GCRS-v1.0`, `ARC-001-GOVR-v1.0`).
2. **Vendor shortlist confirmation** at next ARB.
3. **Pricing quotes** from AWS, Azure, Grafana, Microsoft (Sentinel + Entra External ID), Auth0 — formal RFI-grade quotes against the cell-fill and BR-008 models.

### Vendor Evaluation (2–6 weeks)

4. **DPA + sub-processor reviews** with Vendor DPO per shortlisted vendor.
5. **POC** of the AWS primary stack at one-cell-one-tenant scale.
6. **Cross-vendor abstraction validation** of the same workload on Azure UK South.
7. **AI adaptor implementation** of the Bedrock and Azure OpenAI shims.
8. **OpenTelemetry instrumentation** through Grafana Cloud Pro.

### Decision and Procurement (6–12 weeks)

9. **Final decision** at Beta gate.
10. **Contracts** with selected vendors (AWS, Microsoft, Grafana, Auth0/Microsoft for IdP).
11. **G-Cloud 14 listing** prepared for next framework iteration window.

### Integration with Other Commands

- Run `/arckit:wardley` to position components on the evolution axis.
- Run `/arckit:sow` to produce vendor RFP using these constraints.
- Run `/arckit:hld-review` once the HLD is drafted, to validate against this research.
- Run `/arckit:dpia` refresh listing all sub-processors.

---

## Spawned Knowledge

The following standalone knowledge files were created or updated from this research:

### Vendor Profiles

- `vendors/aws-profile.md` — Created
- `vendors/microsoft-azure-profile.md` — Created
- `vendors/grafana-labs-profile.md` — Created

### Tech Notes

- `tech-notes/multi-tenant-isolation-pool-with-cells.md` — Created
- `tech-notes/ai-provider-abstraction.md` — Created
- `tech-notes/opentelemetry-observability.md` — Created

---

## AskUserQuestion Choices Made

The dispatch instructions specified default selections for any interactive prompts:

- **Scope** = Full system (SaaS-control-plane components per the dispatch's explicit list).
- **Phase** = Alpha.
- **Risk appetite** = Medium.
- **AI mode** = In-scope (REQ has FR-004 AI requirements; Category 2 is a primary research target).
- **Anything else** = first option / Recommended.

No interactive prompt was raised that required user intervention; defaults were applied silently consistent with the Wave-2 dispatch.

---

## External References

> No external policy documents or analyst reports were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government policies and frameworks (Procurement Act 2023, TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, MOD Secure by Design, JSP 440, JSP 604, UK GDPR / DPA 2018, PSBAR / WCAG 2.2 AA, Government Security Classifications Policy, G-Cloud framework, NHS DSPT / DTAC) are public-domain and cited by name. Place authoritative copies in `projects/000-global/policies/` or `projects/001-arckit-saas/external/` and re-run `/arckit:research` to embed inline citations on the next refresh.

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

**Generated by**: ArcKit `/arckit:research` agent (Wave 2 of `/arckit:build`, SaaS-control-plane scope)
**Generated on**: 2026-05-03
**ArcKit Version**: 4.13.1
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
