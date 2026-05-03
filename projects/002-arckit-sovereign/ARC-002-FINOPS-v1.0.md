# FinOps Strategy — Sovereign Deployment

> **Project**: ArcKit as a Service (Sovereign Deployment) — Project 002
> **Recipe**: UK-SaaS baseline with sovereign overrides (per-site cost-to-serve, bespoke contracts, no G-Cloud listing for the sovereign route).
> **Scope**: Sovereign / air-gapped deployments (MOD and comparable sensitive sites). The managed SaaS unit economics are out of scope here and are governed by `projects/001-arckit-saas/ARC-001-FINOPS-v1.0.md`. This document defines the cost-to-serve model, pricing, and the **cross-subsidy contribution** that flows from sovereign customers to the SaaS SME tier per **Principle 17** of `ARC-000-PRIN-v2.0.md`.

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-FINOPS-v1.0 |
| **Document Type** | FinOps Strategy (Sovereign) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL (commercial figures handled OFFICIAL-SENSITIVE per customer NDA) |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-08-03 (quarterly review with sovereign P&L; per-customer review at each accreditation refresh) |
| **Owner** | [PENDING] Finance Lead + Service Owner (joint — Finance Lead RACI Accountable for cost model; Service Owner Accountable for pricing) |
| **Reviewed By** | [PENDING] Lead Architect, Sovereign Delivery Lead, LTS Engineering Lead, Vendor Security Lead |
| **Approved By** | [PENDING] Service Owner |
| **Distribution** | Project Team, Architecture Team, Finance, Steering, Sovereign customer commercial leads (under NDA), HM Treasury / CCS liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:finops`. Per-site cost model. HSM key custody £28k/yr (ADR-002). LTS ~3× CI overhead per branch (ADR-008). Cross-subsidy contribution target ≥ 25% of vendor margin earmarked to SaaS SME tier per Principle 17. Pricing tiers: single-cell vs multi-cell × AI-enabled vs no-AI. | PENDING | PENDING |

---

## 1. FinOps Overview

### 1.1 Strategic Objectives

| # | Objective | Target | Rationale / Trace |
|---|-----------|--------|-------------------|
| FO-S1 | **Full cost-to-serve recovery per site** | Each sovereign contract recovers 100% of allocated capital + recurring cost over its term, with documented contribution margin | Principle 17, BR-006 (cost-to-serve recovery), R-FIN-001 (cross-subsidy must remain positive) |
| FO-S2 | **Cross-subsidy contribution to SaaS SME tier** | ≥ **25% of vendor margin** on each sovereign contract earmarked, transferred quarterly to project-001 cost centre `CC-PROD-FREE` | **Principle 17 (NON-NEGOTIABLE)**, project-001 FO-1 (cross-subsidy break-even) |
| FO-S3 | **Per-site cost-to-serve visibility** | 100% of vendor-side delivery + recurring cost allocable per customer site within ±5% by GA + 6 months | Principle 17 implications, prerequisite for FO-S1/FO-S2 |
| FO-S4 | **LTS engineering cost containment** | LTS engineering load ≤ 3× a single-branch CI overhead (per ADR-008); marginal cost of an additional concurrent LTS branch < 60% of the first | ADR-008 economic envelope; protects unit economics for multi-LTS world |
| FO-S5 | **HSM key custody cost stable** | HSM custody recurring cost ≤ £28k/year baseline (per ADR-002) ± 10% year-on-year | ADR-002 cost driver; predictable for pricing |
| FO-S6 | **Accreditation refresh predictability** | Per-site accreditation refresh effort budgeted at issue of every LTS bundle; variance ≤ ±20% of forecast | BR-004 (formal accreditation support), BR-005 (LTS line) |
| FO-S7 | **Tagging compliance (vendor side)** | ≥ 95% of vendor-controlled sovereign-build resources tagged with site, branch, release | Principle 17 cost allocation gate |
| FO-S8 | **Bespoke contract margin floor** | No sovereign contract signed below contribution-margin floor without written Service Owner exception | Protects FO-S2 cross-subsidy obligation |

### 1.2 FinOps Maturity

| Level | Pre-GA (now) | GA (first signed sovereign contract) | GA + 18m (target — multi-customer) |
|-------|--------------|--------------------------------------|------------------------------------|
| **Crawl** — per-site spreadsheet costing, manual margin tracking | **Yes (current)** | — | — |
| **Walk** — standard per-site cost model template, quarterly per-contract P&L, cross-subsidy ledger live | Partial | **Yes** | — |
| **Run** — per-site forecast vs actual variance dashboard, automated cross-subsidy transfer to SaaS, accreditation-refresh cost predicted from CI telemetry | No | Partial | **Yes** |

**Direction of travel**: Crawl → Walk before first signed contract; Walk → Run by GA + 18 months in lockstep with the SaaS cross-subsidy break-even target (project-001 FO-1).

### 1.3 Team Structure

| Role | Responsibility | Owner |
|------|----------------|-------|
| Finance Lead | Sovereign cost model, per-site P&L, cross-subsidy ledger, pricing-floor sign-off | [PENDING] (RACI Accountable for FO-S1/S2/S8) |
| Service Owner | Bespoke contract approval, exception decisions, steering reporting | Mark Craddock |
| Lead Architect | Cost-model accuracy, LTS branching strategy economics (ADR-008), HSM key custody (ADR-002) | [PENDING] |
| LTS Engineering Lead | Backport effort forecast, CI capacity per LTS branch | [PENDING] |
| Sovereign Delivery Lead | Per-site delivery effort estimate, training cost, on-site support hours | [PENDING] |
| Vendor Security Lead | Accreditation evidence-pack effort, HSM operational cost | [PENDING] |
| LTS / Security joint | Patch-bundle distribution cost per site | [PENDING] |

### 1.4 RACI Matrix

| Activity | Finance Lead | Service Owner | Lead Architect | Sov Delivery | LTS Eng | Sec Lead | Steering |
|----------|--------------|---------------|----------------|--------------|---------|----------|----------|
| Per-site cost model (FO-S3) | **A/R** | A | C | C | C | C | I |
| Bespoke contract pricing (FO-S1) | **R** | **A** | C | C | C | C | I |
| Cross-subsidy quarterly transfer (FO-S2) | **A/R** | A | I | I | I | I | C |
| LTS branch cost forecast (FO-S4) | A | C | C | I | **R** | I | I |
| HSM key custody cost (FO-S5) | A | C | C | I | I | **R** | I |
| Accreditation refresh budget (FO-S6) | A | C | C | C | C | **R** | I |
| Tag enforcement (FO-S7) | C | A | **R** | I | I | C | I |
| Pricing-floor exception | C | **A/R** | C | C | C | C | I |
| Per-customer P&L review | **A/R** | A | I | C | I | I | C |
| KRI feed to RISK §J (R-FIN-001) | **A/R** | C | C | C | C | C | I |

---

## 2. Cloud / Estate Overview — Sovereign-Specific

The sovereign deployment runs **inside the customer's accredited boundary** on customer-provisioned infrastructure. The vendor does **not** carry the production runtime cost — that sits on the customer's balance sheet. The vendor cost base is:

| Vendor-side cost domain | What it covers | Charged to customer? |
|-------------------------|----------------|----------------------|
| **Sovereign build / CI** | Hardened build pipeline (SLSA L3), reproducible build, per-LTS-branch CI capacity | Yes — recovered through delivery + recurring fees |
| **HSM key custody (ADR-002)** | Hardware Security Module hosting + dual-control operations + audit | Yes — recurring, ~£28k/yr baseline allocated across active sovereign customers |
| **Engineering (LTS backports)** | Backporting security patches across active LTS branches (ADR-008) | Yes — recurring patch-stream fee |
| **Delivery & on-site enablement** | Per-customer architecture, install support, training, runbook tailoring | Yes — capital fee (one-off per site) |
| **Accreditation evidence pack** | Per-release MOD SbD / NCSC CAF evidence, threat model update, SBOM diff, signed manifests (ADR-002) | Yes — capital (initial) + recurring (refresh per LTS bundle) |
| **Patch-bundle distribution** | Signed patch-bundle production, secure courier or accredited transfer mechanism | Yes — recurring per-bundle fee |
| **Vendor support** | Named contacts, SLA-bound responses, optional remote-support arrangements | Yes — recurring, tiered |
| **Vendor R&D / overhead** | Product engineering, sales, finance, legal — not directly attributable | Yes — recovered through margin loading; **margin is the source of FO-S2 cross-subsidy** |

> **Important**: Customer-side costs (their infrastructure, their operator team, their accreditor's time, their HSM if separate) are **not** in this vendor-side estate. They are visible to the customer in their own FinOps and in the SOBC option appraisal but are deliberately excluded from the vendor cost-recovery target.

### 2.1 Vendor Sovereign Cost Centres

| Cost centre | Description | Owner |
|-------------|-------------|-------|
| `CC-SOV-BUILD` | Sovereign CI: hardened build runners, per-LTS-branch capacity, reproducible-build infrastructure | Lead Architect |
| `CC-SOV-HSM` | HSM key custody (per ADR-002) — recurring £28k/yr baseline | Vendor Security Lead |
| `CC-SOV-LTS-ENG` | LTS engineering — backport effort, branch maintenance, deprecation comms | LTS Engineering Lead |
| `CC-SOV-DELIVERY-{SITE}` | Per-site delivery effort, training, runbook tailoring (one cost centre per signed site) | Sovereign Delivery Lead |
| `CC-SOV-ACCRED-{SITE}` | Per-site accreditation evidence and refresh effort | Vendor Security Lead |
| `CC-SOV-DIST-{SITE}` | Per-site patch-bundle production and accredited transfer | Sovereign Delivery Lead |
| `CC-SOV-SUPPORT-{SITE}` | Per-site named-contact support, optional remote-support arrangement | Sovereign Delivery Lead |
| `CC-SOV-MARGIN` | Vendor margin pool — **source of FO-S2 cross-subsidy transfer** | Service Owner |

---

## 3. Tagging Strategy

Tagging here applies to **vendor-side** cost-allocable resources (CI runners, HSM telemetry, delivery time records, etc.) — there is no tagging across the customer accreditation boundary.

### 3.1 Mandatory Tags (Vendor-Side Sovereign Resources)

| Tag | Purpose | Allowed values |
|-----|---------|----------------|
| `arckit:project` | Project identification | `002-sovereign` (fixed for this estate) |
| `arckit:site` | Customer site allocation | `{customer-code}` or `shared` (HSM, build) or `unallocated` |
| `arckit:branch` | LTS branch served | `main`, `lts-{YY}.{N}` (per ADR-008) |
| `arckit:cost-centre` | One of the `CC-SOV-*` centres | Closed list (§2.1) |
| `arckit:release` | Release version producing artefact | `v{X.Y.Z}` or `lts-{YY}.{N}-patch-{NN}` |
| `arckit:classification` | Handling caveat | `OFFICIAL`, `OFFICIAL-SENSITIVE` |
| `arckit:owner` | Cost-centre owner email | RFC-5322 format |

### 3.2 Optional Tags

| Tag | Purpose |
|-----|---------|
| `arckit:contract` | Contract identifier for chargeback |
| `arckit:ai-enabled` | `true` / `false` — pricing tier traceability |
| `arckit:cell-topology` | `single-cell` / `multi-cell` — pricing tier traceability |
| `arckit:effort-hours` | Recorded delivery effort (manual entry from time-tracking) |

### 3.3 Enforcement

- IaC policy (Principle 18) rejects any sovereign-side resource lacking the mandatory tag set at provision time.
- Time-tracking entries against `CC-SOV-DELIVERY-{SITE}` and `CC-SOV-ACCRED-{SITE}` MUST tag `arckit:site`. Untagged time is parked in `unallocated` and triaged weekly by the Sovereign Delivery Lead.
- Untagged resources surviving > 7 days trigger a KRI feed to RISK §J (FO-S7 breach).
- Quarterly tag audit by Finance Lead with sample cross-check against contract scope.

---

## 4. Cost Visibility & Reporting

### 4.1 Reporting Cadence

| Report | Cadence | Audience | Owner |
|--------|---------|----------|-------|
| Per-site contract P&L (forecast vs actual) | **Monthly** | Finance Lead, Service Owner | Finance Lead |
| Cross-subsidy ledger (transfer to project 001) | **Quarterly** | Finance Lead, project-001 Finance Lead, Steering | Finance Lead |
| LTS branch cost (CI + engineering effort) | Monthly | Lead Architect, LTS Engineering Lead | Lead Architect |
| HSM custody cost vs baseline (ADR-002) | Quarterly | Security Lead, Finance Lead | Vendor Security Lead |
| Accreditation refresh effort vs forecast (ADR-002 / BR-004) | Per LTS bundle issue | Security Lead, Finance Lead | Vendor Security Lead |
| Per-site contribution margin | Monthly (live), **At each customer review meeting** | Service Owner, customer commercial lead (filtered) | Finance Lead |
| Sovereign portfolio dashboard (all sites, all KRIs) | Real-time | Finance Lead, Service Owner | Finance Lead |

### 4.2 Cost Allocation Methodology

| Allocation type | Method |
|-----------------|--------|
| **Direct (per site)** | `CC-SOV-DELIVERY-{SITE}`, `CC-SOV-ACCRED-{SITE}`, `CC-SOV-DIST-{SITE}`, `CC-SOV-SUPPORT-{SITE}` charged 1:1 to that customer |
| **Branch-shared** | `CC-SOV-LTS-ENG` allocated across all sites pinned to that LTS branch, weighted by contract value |
| **Estate-shared** | `CC-SOV-HSM` (£28k/yr) and `CC-SOV-BUILD` allocated across all active sovereign customers, weighted by contract value with a **floor allocation** so first customer doesn't carry 100% of the £28k HSM baseline alone |
| **Vendor overhead** | Loaded into margin (`CC-SOV-MARGIN`) — never charged separately |

### 4.3 First-Customer Pre-Funding

The HSM (`CC-SOV-HSM`, £28k/yr) and a sovereign-build pipeline (`CC-SOV-BUILD`, ~3× single-branch CI per ADR-008) must exist **before** the first customer signs. These are **pre-funded** from the vendor balance sheet (or from an explicit grant — see RISK financial cluster) and recovered over the first 3 customers via a uniform 12-month uplift on each contract's recurring fee. Service Owner approves the recovery schedule at first contract signature.

---

## 5. Cost Model — Per-Site

### 5.1 Capital (One-Off, on Site Stand-Up)

| Cost line | Driver | Indicative range (GBP) | Notes |
|-----------|--------|------------------------|-------|
| Delivery (architecture, install support, IaC tailoring, runbook adaptation) | Site complexity, single-cell vs multi-cell | £80k–£250k | Multi-cell sites at top of range |
| Accreditation evidence pack (initial — MOD SbD / JSP 604 / CAF) | Customer framework, classification | £40k–£120k | MOD with JSP 604 toward top; civilian SbD toward bottom |
| Training (operator team, accreditor handover) | Number of operators, on-site vs remote | £15k–£40k | |
| AI integration (where AI-enabled tier selected) | On-prem model endpoint validation, pluggability tests | £20k–£70k | £0 for No-AI tier |
| **Capital subtotal range** | | **£135k–£480k** | |

### 5.2 Recurring (Annual, per Site)

| Cost line | Driver | Indicative range (GBP/yr) | Notes |
|-----------|--------|---------------------------|-------|
| LTS patch stream (engineering backports, allocated share of `CC-SOV-LTS-ENG`) | Number of sites on that branch | £35k–£90k | Per ADR-008 ~3× CI overhead per branch is the engineering backbone |
| HSM key custody (allocated share of £28k/yr `CC-SOV-HSM` per ADR-002) | Sites in cohort | £4k–£28k | First sole customer carries full baseline (recovered per §4.3) |
| Patch-bundle distribution (production + accredited transfer) | Bundle frequency, transfer mechanism | £15k–£40k | MOD courier transfers higher than civilian electronic |
| Accreditation refresh (per LTS bundle, per BR-004) | Customer framework, scope of change | £20k–£60k | Per refresh; refreshes typically 2–4 per year |
| Vendor support (named-contact, SLA-bound) | Tier (silver / gold / platinum) | £30k–£120k | Optional remote-support arrangement priced separately |
| AI integration support (AI-enabled tier only) | Model endpoint changes, eval re-runs | £10k–£35k | £0 for No-AI |
| **Recurring subtotal range** | | **£114k–£373k/yr** | |

### 5.3 Per-Site Cost-to-Serve Range (Year-1 Total)

> **Year-1 cost-to-serve (capital + first-year recurring), vendor-side, before margin**:
> **Low**: £135k + £114k = **~£250k** (single-cell, No-AI, civilian sensitive site, lean accreditation framework)
> **High**: £480k + £373k = **~£850k** (multi-cell, AI-enabled, MOD JSP 604 site, multi-branch LTS)
> **Median planning assumption**: **~£500k** Year-1, ~£250k/yr steady-state thereafter

### 5.4 Margin Loading and Cross-Subsidy

| Component | Calculation |
|-----------|-------------|
| Vendor delivery margin | Loaded onto cost-to-serve. Floor: **20%** of total contract value over term. |
| Cross-subsidy contribution (FO-S2) | **≥ 25% of vendor margin** earmarked to project-001 `CC-PROD-FREE` |
| Effective cross-subsidy as % of contract | ≥ 25% × 20% = **≥ 5% of contract value** flows to SaaS SME tier |

> **Worked example (median site)**: £500k Year-1 cost-to-serve × 1.20 margin = **£600k Year-1 contract**. Margin = £100k. Cross-subsidy transfer to SaaS = **≥ £25k Year-1**, recurring at ~£12.5k/yr steady state. Two such customers fully fund a non-trivial chunk of the SaaS SME free-tier AI-inference budget tracked in project-001 FO-3.

> **Pricing-floor rule (FO-S8)**: No contract signs below cost-to-serve × 1.10 (i.e. minimum 10% margin) without Service Owner written exception. Exceptions logged and reviewed quarterly. Below cost-to-serve is **never** signed — that breaches Principle 17 directly (would undermine, not cross-subsidise, the SaaS tier).

---

## 6. Pricing Tiers

Sovereign pricing is **bespoke per site** — there is **no G-Cloud listing for the sovereign route** (procurement is via DOS / DPS / direct award under defence frameworks; see BR-007). The tier matrix below is an **internal pricing scaffold**, not a published catalogue.

### 6.1 Tier Matrix (Internal Scaffold)

| | **No-AI** | **AI-Enabled** |
|---|-----------|----------------|
| **Single-cell** (one accredited boundary, one operator team) | **Tier S1** — £250k–£400k Y1 / £150k–£220k recurring | **Tier S2** — £320k–£500k Y1 / £190k–£270k recurring |
| **Multi-cell** (≥ 2 accredited boundaries, federated operator teams) | **Tier S3** — £400k–£600k Y1 / £230k–£320k recurring | **Tier S4** — £500k–£850k Y1 / £290k–£373k recurring |

Indicative ranges only; every contract is independently costed against §5.

### 6.2 Tier Modifiers

| Modifier | Cost effect |
|----------|-------------|
| **Classification** (OFFICIAL-SENSITIVE → SECRET) | +15–30% on accreditation evidence + cleared-personnel premium on delivery effort |
| **First-of-cohort on a new LTS branch** | +10% on Year-1 recurring (recovered over first three customers per §4.3) |
| **Accelerated delivery** (< 6 months) | +20% on capital |
| **Bespoke AI model** (customer-supplied weights, custom eval) | +£40k–£100k Y1 capital |
| **Disaster-recovery cell / hot standby** | +50–80% on relevant cost lines |
| **No remote support** (default; per BR-003) | Baseline |
| **Optional accredited remote support** | +£20k–£60k/yr |

### 6.3 Contract Term

| Term | Pricing posture |
|------|-----------------|
| 1 year | Standard |
| 3 years (typical accreditation cycle) | -5% on recurring (locks branch commitment, evens out CI overhead) |
| 5+ years | -8–10% on recurring, with right-of-review at LTS branch retirement |

---

## 7. Showback / Chargeback Model

**Internal showback** (between vendor cost centres):

| Flow | From → To | Method |
|------|-----------|--------|
| HSM allocation | `CC-SOV-HSM` → each `CC-SOV-DELIVERY-{SITE}` | Quarterly, weighted by contract value with floor allocation |
| Build allocation | `CC-SOV-BUILD` → each `CC-SOV-DELIVERY-{SITE}` | Quarterly, weighted by contract value |
| LTS engineering allocation | `CC-SOV-LTS-ENG` → sites on that branch | Quarterly, weighted by contract value within branch |
| Margin gathering | All `CC-SOV-DELIVERY-{SITE}` margin component → `CC-SOV-MARGIN` | Quarterly |
| **Cross-subsidy transfer (FO-S2)** | `CC-SOV-MARGIN` → project-001 `CC-PROD-FREE` | Quarterly, ≥ 25% of margin, evidenced in cross-subsidy ledger |

**External chargeback** (to customers): direct billing per signed contract schedule. No showback; the customer commercial lead receives a quarterly P&L extract under NDA showing only their site's costs and any modifier applications, never aggregate cohort data.

### 7.1 Unit Economics

| Metric | Definition | Target |
|--------|------------|--------|
| Cost-to-serve per site (Y1) | Σ(allocated capital + Y1 recurring) | ≤ £500k median per §5.3 |
| Cost-to-serve per site (steady) | Σ(allocated annual recurring) | ≤ £250k median per §5.3 |
| Gross margin per site | (Contract revenue − cost-to-serve) / contract revenue | ≥ 20% (FO-S8 floor) |
| Cross-subsidy per site | 25% × (margin) | ≥ 5% of contract value |
| LTS marginal cost (Nth concurrent branch) | Δ`CC-SOV-LTS-ENG` per added branch | < 60% of first branch (FO-S4) |
| Time-to-cost-recovery on a new LTS branch | Months to recover branch stand-up cost across cohort | ≤ 18 months |

---

## 8. Cost Optimization Strategies

### 8.1 LTS Branch Economics (per ADR-008)

- LTS lines are **annual**, with 24-month security support overlap. ADR-008 establishes ~3× single-branch CI overhead at steady state (one main + two concurrent LTS branches).
- **Lever**: Branch retirement. Aggressive deprecation comms (≥ 12 months) and customer migration support to keep concurrent LTS branches at 2 (not 3+). Each additional concurrent branch beyond 2 must be approved by Service Owner with explicit unit-economics analysis.
- **Lever**: Backport scope discipline. Security-only backports (no features) per ADR-008 — feature backport requests are converted into customer migration to a newer LTS, never bespoke patches.
- **Lever**: CI cache reuse across branches (build-base layers shared) — protects FO-S4 marginal-cost target.

### 8.2 HSM Custody Economics (per ADR-002)

- HSM baseline **~£28k/year** is mostly fixed cost — the cost-optimisation lever is **utilisation**, not unit cost.
- **Lever**: Multi-branch signing on shared HSM (already designed in ADR-002); avoid spinning up a second HSM unless audit / classification policy demands physical separation.
- **Lever**: Recover £28k baseline across the active sovereign cohort with a floor allocation so first customer doesn't shoulder it alone (§4.3).
- **Lever**: HSM dual-control rota optimisation — keep two trained custodians per HSM, no more, no fewer.

### 8.3 Delivery Effort Economics

- **Lever**: Runbook reuse. Each site delivery improves the canonical runbook (Principle 4 open standards). Year-2 site delivery should be 25–35% cheaper than Year-1 first delivery.
- **Lever**: Alpha customer accreditator-in-the-loop programme (per RISK R-001 mitigation) reduces per-site accreditation evidence-pack effort by an estimated 30% from second customer onwards.
- **Lever**: Pre-built training materials amortise capital line `Training` from £40k to £15k by site #4.

### 8.4 Distribution Economics

- **Lever**: Bundle frequency negotiation. Default 2 LTS bundles + 4 patch bundles per year, customer can pay for higher cadence.
- **Lever**: Electronic accredited transfer (where customer accreditation permits) replaces courier — saves £8k–£20k/yr.

### 8.5 Anti-Levers (deliberately NOT used)

- **NOT** undercutting cost-to-serve to win contracts (breach of Principle 17).
- **NOT** pulling LTS support short to save engineering hours (breach of BR-005).
- **NOT** outsourcing HSM custody to a non-vendor party where chain-of-custody for signing keys would be diluted (breach of ADR-002).
- **NOT** sharing tenant-attributable costs into vendor-overhead pool (would erode FO-S3 and breach Principle 17 transparency).

---

## 9. Commitment Management

Sovereign deployments do **not** consume vendor-side public-cloud commitments (the runtime is on customer infrastructure). Vendor-side commitments apply to:

| Asset | Commitment posture |
|-------|--------------------|
| HSM hardware + service contract (ADR-002) | **3-year commitment** (matches typical sovereign customer term); reviewed annually |
| Sovereign-build CI runners (`CC-SOV-BUILD`) | Mixed: 1-year reserved capacity for steady-state ~3× single-branch CI; on-demand burst for release weeks |
| Code signing certs, SLSA attestation services (ADR-002) | Annual commitments aligned with HSM contract |
| LTS engineer headcount | Hired against a 24-month rolling LTS-cohort forecast; never against a single contract |

---

## 10. Anomaly Detection & Alerts

| Signal | Threshold | Action |
|--------|-----------|--------|
| Per-site forecast vs actual margin variance | > ±15% in any month | Sovereign Delivery Lead investigates within 5 working days; Finance Lead flag at next monthly review |
| LTS branch CI overhead | Approaching 3× per ADR-008 with > 2 concurrent branches | Lead Architect + LTS Engineering Lead trigger branch-retirement review |
| HSM custody cost | > £30.8k/yr (£28k + 10%) | Vendor Security Lead investigates within 10 working days; refresh ADR-002 if structural |
| Cross-subsidy quarterly transfer | < 25% of margin in any quarter | **Critical** — Finance Lead briefs Service Owner within 5 working days; mandatory steering report |
| Accreditation refresh effort | > 120% of forecast | Vendor Security Lead post-mortem within 30 days; calibrate FO-S6 forecast |
| Untagged sovereign resources | > 5% of estate for > 7 days | KRI breach (FO-S7) — Lead Architect remediation plan within 5 working days |
| Pricing-floor exception count | > 1 active exception | Service Owner steering escalation |

---

## 11. Governance & Policies

### 11.1 Approval Workflow

| Decision | Approver | Threshold |
|----------|----------|-----------|
| New sovereign contract within standard tier matrix | Service Owner | Up to £1.5M total contract value |
| Contract above £1.5M | Service Owner + Steering | All contracts > £1.5M |
| Pricing-floor exception (margin < 10%) | Service Owner (written) | Per exception |
| New concurrent LTS branch (3rd or beyond) | Service Owner + Lead Architect | Per ADR-008 economic envelope |
| Cross-subsidy quarterly suspension (FO-S2 deferral) | Steering only — not Service Owner alone | Any non-zero deferral; **default-deny** |
| New HSM commissioning | Service Owner + Vendor Security Lead | Per ADR-002 |
| Tier discount > 10% | Service Owner | Per contract |

### 11.2 Cross-Subsidy Policy

The cross-subsidy obligation in Principle 17 is **non-negotiable**. The 25% target in FO-S2 is a floor, not a ceiling. A quarter where the cross-subsidy transfer would push the sovereign cost centre into deficit triggers a **Steering decision**, not a unilateral suspension — Steering may permit a short-term deferral with a documented catch-up plan, or may absorb the gap from vendor reserves, but cannot waive the obligation.

### 11.3 Exception Handling

All exceptions logged in a sovereign-FinOps exceptions ledger held by the Finance Lead. Quarterly Steering review.

---

## 12. FinOps Tooling

| Tool / artefact | Purpose | Status |
|-----------------|---------|--------|
| Per-site cost-model spreadsheet (canonical template) | Costing for new contracts | Pre-GA — to be locked at Walk-stage transition |
| Cross-subsidy ledger | Quarterly transfer tracking from `CC-SOV-MARGIN` to project-001 `CC-PROD-FREE` | Pre-GA — design with project-001 Finance Lead |
| Sovereign portfolio dashboard | Live per-site P&L, KRIs, exceptions | GA + 6m target |
| Time-tracking integration | `arckit:site` and `arckit:cost-centre` tagging on all delivery / accreditation effort | GA target |
| HSM cost report (ADR-002) | Quarterly HSM utilisation + cost vs baseline | GA target |
| LTS CI overhead report (ADR-008) | Branch-by-branch CI cost + concurrency status | GA target |

No third-party FinOps platforms are assumed. Customer-side cost tooling sits inside the customer's accreditation boundary and is not the vendor's concern.

---

## 13. Sustainability & Carbon

- Sovereign deployments run on customer-controlled infrastructure; sustainability reporting is owned by the customer, not the vendor.
- Vendor-side: prefer UK-region build runners with documented carbon intensity. HSM hosting site disclosed in `CC-SOV-HSM` reporting.
- LTS branch retirement discipline (§8.1) reduces CI carbon footprint — directly aligned with sustainability objectives.

---

## 14. UK Government Compliance

| Item | Application |
|------|-------------|
| Cabinet Office digital spend controls | Customer-side procurement; vendor produces a value-for-money narrative on request |
| HM Treasury Green Book (5-case model) alignment | Sovereign SOBC produced on request to support customer business case |
| G-Cloud / Digital Marketplace | **Not used for sovereign route** (per BR-007). Procurement via DOS / DPS / direct award under defence frameworks. |
| Public sector procurement (Procurement Act 2023) | Bespoke contracts compliant with PA 2023 transparency obligations as required by deploying authority |
| MOD commercial framework alignment | Per customer commercial agreement; framework call-offs respected |
| Annual technology spend disclosure | Vendor produces customer-facing extract on request to support customer reporting |

---

## 15. FinOps Operating Model

### 15.1 Cadence

| Cadence | Activity | Participants |
|---------|----------|--------------|
| **Weekly** | Untagged-resource sweep; time-tracking review; in-flight contract pipeline | Finance Lead, Sovereign Delivery Lead |
| **Monthly** | Per-site P&L review; LTS CI overhead; HSM cost; KRI scoreboard | Finance Lead, Service Owner, Lead Architect, LTS Engineering Lead |
| **Quarterly** | Cross-subsidy transfer to project 001; pricing-floor exceptions review; tier-matrix calibration; ADR-002 / ADR-008 economic envelope re-test; accreditation refresh forecast | All FinOps roles + Steering |
| **Per LTS bundle issue** | Accreditation refresh effort actual vs forecast | Vendor Security Lead, Finance Lead, customer security lead |
| **Per contract signature** | Cost model lock; first-customer pre-funding allocation if applicable | Finance Lead, Service Owner |
| **Annual** | Tier-matrix refresh; HSM commitment renewal; cross-subsidy contribution-rate review (≥ 25% floor) | All + Steering |

### 15.2 Stakeholder Engagement

- Customer commercial leads: quarterly P&L extract under NDA (their site only).
- Project-001 Finance Lead: quarterly cross-subsidy ledger reconciliation.
- HM Treasury / CCS liaison: annual sovereign portfolio summary on request.
- Steering: monthly KRI dashboard; quarterly cross-subsidy report.

---

## 16. Metrics & KPIs

### 16.1 Cost Efficiency

| KPI | Definition | Target |
|-----|------------|--------|
| Per-site Y1 cost-to-serve | Σ(capital + Y1 recurring) per site | Median ≤ £500k |
| Per-site steady-state cost-to-serve | Σ(annual recurring) per site | Median ≤ £250k |
| LTS branch CI overhead | Σ(`CC-SOV-BUILD`) for all active branches | ≤ 3× single-branch baseline (ADR-008) |
| HSM custody cost | `CC-SOV-HSM` annualised | ≤ £28k/yr ± 10% (ADR-002) |
| Delivery cost reduction across cohort | Y2-onwards site delivery cost vs Y1 first-delivery | ≥ 25% reduction by site #4 |

### 16.2 Margin & Cross-Subsidy

| KPI | Definition | Target |
|-----|------------|--------|
| Per-site contribution margin | (Contract revenue − cost-to-serve) / contract revenue | ≥ 20% (FO-S8 floor) |
| Cross-subsidy contribution rate | Quarterly transfer to project-001 / `CC-SOV-MARGIN` | ≥ 25% (FO-S2 floor) |
| Cross-subsidy in absolute terms | Quarterly £ transferred to `CC-PROD-FREE` | Tracked, reported to Steering |
| Pricing-floor exceptions | Active exceptions count | ≤ 1 at any time |

### 16.3 Governance & Compliance

| KPI | Definition | Target |
|-----|------------|--------|
| Tag compliance | % vendor-side sovereign resources with mandatory tag set | ≥ 95% (FO-S7) |
| Forecast variance per site | |actual − forecast| / forecast on monthly P&L | ≤ ±15% |
| Accreditation refresh forecast variance | |actual effort − FO-S6 forecast| / forecast | ≤ ±20% |
| Time-to-cross-subsidy-transfer | Days from quarter end to transfer execution | ≤ 30 days |

### 16.4 Top 3 Cost Levers (for executive summary)

1. **LTS branch concurrency discipline** (§8.1 / ADR-008) — every additional concurrent LTS branch beyond 2 lifts engineering cost ~3× → 4×+ and erodes the cross-subsidy.
2. **Per-site delivery cost amortisation** (§8.3) — runbook reuse + accreditator-in-the-loop alpha programme is the largest controllable cost reducer once site #2 starts.
3. **HSM utilisation** (§8.2 / ADR-002) — £28k baseline is a fixed cost; spreading it across the cohort and avoiding a second HSM unless mandated is the single largest fixed-cost lever.

### 16.5 Top 3 KRIs (Key Risk Indicators) Fed to RISK §J

1. **Cross-subsidy contribution shortfall** — quarterly transfer < 25% of margin or < £0 (deficit). Threshold: amber at any single quarter < 25%; red at two consecutive quarters or any deficit. Trace: R-FIN-001 in `ARC-002-RISK-v1.0.md`, FO-S2.
2. **Pricing-floor exception count** — > 1 active sub-10%-margin exception OR any sub-cost-to-serve contract. Threshold: red on any below-cost-to-serve signature. Trace: FO-S8, Principle 17.
3. **LTS branch concurrency / CI overhead breach** — > 2 concurrent LTS branches OR `CC-SOV-LTS-ENG` > 3.5× single-branch baseline. Threshold: amber > 2 concurrent; red > 3.5× baseline. Trace: ADR-008, FO-S4.

---

## 17. Traceability

### 17.1 Requirements → FinOps

| Requirement / Principle / ADR | FinOps element |
|-------------------------------|----------------|
| Principle 17 (Cost Transparency and FinOps) | **Whole document**; explicit FO-S2 cross-subsidy ≥ 25% of margin |
| Principle 21 (Sovereign and Air-Gapped Deployment) | §2 vendor-side cost-base scope; §6 bespoke pricing; §14 no-G-Cloud |
| Principle 1 (Equitable Access for SMEs) | §7 cross-subsidy transfer to `CC-PROD-FREE`; FO-S2 |
| BR-001 (single codebase) | §8.1 anti-fork lever discipline |
| BR-004 (formal accreditation support) | §5.1 accreditation evidence pack capital; §5.2 accreditation refresh recurring; FO-S6 |
| BR-005 (LTS line ≥ 24 months) | §5.2 LTS patch stream; §8.1 LTS lever |
| BR-006 (cost-to-serve recovery + cross-subsidy) | §5 cost model; §5.4 margin loading; §11.2 cross-subsidy policy |
| BR-007 (defence procurement routes) | §6 bespoke contracts; §14 no-G-Cloud |
| BR-008 (reference customer within 18m of GA) | §4.3 first-customer pre-funding; §8.3 alpha cost reducer |
| ADR-002 (Cosign + HSM key custody) | §5.2 HSM £28k/yr; §8.2; §9 HSM 3-yr commit; §16.1 |
| ADR-008 (Annual LTS, 24-month support) | §5.2 LTS patch stream; §8.1; FO-S4 marginal-cost target; §16.1 |
| R-FIN-001 (cross-subsidy must remain positive) | FO-S2; §10 cross-subsidy alert; §16.5 KRI #1 |

### 17.2 Project-001 Cross-References

| Project-001 element | Project-002 link |
|---------------------|------------------|
| Project-001 FO-1 (cross-subsidy break-even GA + 18m) | Project-002 FO-S2 supplies the funding flow |
| Project-001 `CC-PROD-FREE` | Project-002 `CC-SOV-MARGIN` → `CC-PROD-FREE` quarterly transfer |
| Project-001 FINOPS §1 cross-subsidy break-even target | Project-002 §11.2 cross-subsidy policy underwrites it |

---

## 18. Validation Gates

- [x] Per-site cost model defined with capital + recurring lines
- [x] HSM custody cost (£28k/yr per ADR-002) explicitly modelled
- [x] LTS engineering cost (~3× CI overhead per ADR-008) explicitly modelled
- [x] Pricing tiers cover single-cell vs multi-cell × AI-enabled vs no-AI
- [x] Tagging strategy covers vendor-side cost attribution
- [x] Cross-subsidy contribution target ≥ 25% of margin set and policy-protected
- [x] Pricing-floor rule prevents undermining the SaaS tier (Principle 17)
- [x] Bespoke per-site contracts (no G-Cloud) reflected in §14
- [x] Governance cadence covers monthly, quarterly, per-bundle, annual
- [x] KRIs feed into project RISK §J
- [x] Cross-references to project 001 FINOPS for cross-subsidy reconciliation

---

## 19. External References

None directly cited. All referenced artefacts are internal:

- `projects/000-global/ARC-000-PRIN-v2.0.md` (Principle 17, Principle 21, Principle 1)
- `projects/002-arckit-sovereign/ARC-002-REQ-v1.0.md` (BR-001 through BR-008)
- `projects/002-arckit-sovereign/ARC-002-RISK-v1.0.md` (R-FIN-001, R-001, sovereign appetite)
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-002-v1.0.md` (HSM key custody)
- `projects/002-arckit-sovereign/decisions/ARC-002-ADR-008-v1.0.md` (LTS release line)
- `projects/001-arckit-saas/ARC-001-FINOPS-v1.0.md` (cross-subsidy receiving end — referenced, not duplicated)

---

**Generated by**: ArcKit `/arckit:finops` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
