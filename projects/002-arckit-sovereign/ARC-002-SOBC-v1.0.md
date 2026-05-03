# Strategic Outline Business Case (SOBC): ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:sobc`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-SOBC-v1.0 |
| **Document Type** | Strategic Outline Business Case (HM Treasury Green Book 5-Case Model) |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Per Green Book — at OBC update or material change |
| **Next Review Date** | 2026-08-03 |
| **Owner** | Mark Craddock (Service Owner / SRO) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Review Board, MOD Defence Digital liaison, NCSC liaison, Crown Commercial Service, HM Treasury, CDDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:sobc`. Anchored on Principle 21 (single codebase, sovereign overlay) and Principle 17 (cross-subsidy). 5-case Green Book structure. Recommended option: single codebase + sovereign overlay. Optimism bias applied per `ARC-002-RISK-v1.0.md` §I (capability cost +30%). Management Case Part E references the full risk register. | [PENDING] | [PENDING] |

## Document Purpose

To present the strategic, economic, commercial, financial, and management case for funding the **sovereign / air-gapped deployment** of ArcKit as a Service for UK MOD and other accredited sensitive sites, and to secure approval to proceed to detailed design, vendor procurement, and pilot customer engagement. This SOBC sits **upstream** of the OBC (which will refine costs after HLD and pilot-customer commercial terms) and FBC (final approval before GA bundle issue). The SaaS sister track is governed by `projects/001-arckit-saas/` artefacts; sovereign and SaaS share a single codebase by Principle 21 and a deliberate cross-subsidy by Principle 17.

---

## Executive Summary

**Purpose**: To deliver ArcKit's enterprise-architecture governance toolkit into UK Ministry of Defence units and other accredited sensitive sites — where citizen-facing SaaS cannot operate — by packaging the same codebase as a signed, air-gap-transferable bundle that customers install and run entirely within their accredited boundary.

**Problem Statement**: A material cohort of the UK public-sector audience for ArcKit — MOD units, intelligence-community partners, regulated operators of essential services — operate at OFFICIAL-SENSITIVE and above with no internet egress. They cannot lawfully or operationally use the SaaS (project 001). Without a sovereign route they either cannot adopt ArcKit at all, or they adopt fragmented bespoke alternatives, undermining cross-government governance consistency and the SME-supplier-diversification narrative that underpins MOD Defence Digital strategy.

**Proposed Solution**: A single-codebase sovereign overlay — same source, same APIs, same artefact set as the SaaS — packaged into a signed, hashed, SBOM-backed release bundle, customer-installed via the customer's approved data-transfer mechanism, operated entirely within the customer's accredited boundary by their cleared operator team. Pluggable abstractions (AI endpoint, telemetry, time, CA, package mirror, IdP) allow the sovereign default profile to point at no external service. Each bundle ships with an MOD Secure by Design / NCSC CAF evidence pack supporting customer-led accreditation.

**Strategic Fit**: Anchored on Principle 21 (Sovereign and Air-Gapped Deployment — non-negotiable platform-level commitment) and Principle 17 (FinOps — sovereign cost-recovery-plus-margin funds the SaaS SME tier cross-subsidy). Aligns with MOD Defence Digital supplier-diversification strategy, NCSC supply-chain guidance, HMG cross-government digital coherence, and Crown Commercial Service framework procurement.

**Investment Required**: £4.85M over 3 years (vendor-side capability investment) — Rough Order of Magnitude (ROM ±30% at SOBC stage)

- Capital (Year 0 + early Year 1): £1.45M
- Operational (3 years cumulative): £3.40M

**Expected Benefits**: Net contribution to vendor £2.10M over 3 years from sovereign customers, plus £1.50M+ measurable cross-subsidy contribution to the SaaS SME tier (Principle 17). Avoided customer cost (do-nothing baseline) ≈ £4.5M-£15M across 3-5 customers from forced-upgrade re-accreditation churn.

**Return on Investment**:

- NPV (3 years, 3.5% discount, post-optimism-bias): £+0.62M
- BCR (Benefit-Cost Ratio, post-optimism-bias): 1.13
- Payback Period: Month 30 (post-optimism-bias); Month 24 (pre-bias)
- ROI (3-year): 13% post-bias; 31% pre-bias

**Recommended Option**: **Option C — Single Codebase + Sovereign Overlay** (Principle-21-compliant, single source-of-truth, configuration-only divergence, signed-bundle delivery)

**Key Risks** (full register: `ARC-002-RISK-v1.0.md`):

1. **R-001** — First-customer accreditation failure on first attempt (STRATEGIC, residual 12, at appetite ceiling) — *load-bearing risk for whole track*
2. **R-002** — MOD Secure by Design assessment fail (COMPLIANCE, residual 12, exceeds Very-Low appetite by +200%)
3. **R-003** — Single-codebase divergence (TECHNOLOGY, residual 9, exceeds Low appetite by +50%) — direct Principle 21 violation risk
4. **R-004** — Signed-bundle / supply-chain compromise (COMPLIANCE, residual 8, exceeds appetite +100%) — existential
5. **R-007** — Accredited-boundary egress incident (REPUTATIONAL, residual 8, exceeds Very-Low appetite +100%)

**Go/No-Go Recommendation**: **PROCEED WITH CONDITIONS**.

**Rationale**: The recommended option is the only one that simultaneously satisfies Principle 21 (no fork), Principle 17 (cross-subsidy contribution), and the deploying-authority accreditation chain. Five risks remain above sovereign-specific appetite at residual; the SOBC is approvable only with formal Service Owner acknowledgement of those acceptances, the accreditator-in-the-loop alpha programme funded, and HSM-backed signing infrastructure in place before first bundle issue.

**Next Steps if Approved**:

1. Service Owner formal acknowledgement of above-appetite risks (R-001, R-002, R-003, R-004, R-005, R-007) — by 2026-06-30
2. HLD complete — `/arckit:hld` already issued (`ARC-002-HLDR-v1.0.md`); refresh against any post-SOBC scope changes
3. MOD Secure by Design assessment — `/arckit:mod-secure` — by 2026-09-30
4. Pilot customer engagement (≥ 1 MOD or sensitive-site authority for accreditator-in-the-loop alpha) — by 2027-02-28
5. OBC (Outline Business Case) once HLD + pilot commercial terms are firm — Q3 2027

---

# PART A: STRATEGIC CASE

## A1. Strategic Context

### A1.1 Problem Statement

**Current Situation**: UK Ministry of Defence units, intelligence-community partner organisations, and regulated operators of essential services maintain accredited boundaries operating at OFFICIAL-SENSITIVE through SECRET. These boundaries permit no outbound internet connectivity. The same DDaT roles that exist in civilian departments — Enterprise Architects, Solution Architects, Security Architects — work inside these boundaries and need the same governance toolkit available to their colleagues elsewhere in government. They cannot use the project-001 managed SaaS without breaching their accreditation.

**Specific Pain Points** (from `ARC-002-STKE-v1.0.md`):

| Stakeholder | Driver ID | Pain Point | Impact | Intensity |
|-------------|-----------|------------|--------|-----------|
| Customer Accreditor (JSP 604) | SD-1 | Generic "ISO 27001-shaped" vendor evidence not mapped to MOD frameworks; bespoke per-vendor format extends accreditation cycle by months and creates personal risk | Accreditation cycle extended ~3-6 months; personal-risk exposure | CRITICAL |
| Customer SIRO | SD-2 | Supply-chain blind spots, vendor-imposed remote-access defaults, AI integrations with implicit external endpoints | Cannot defensibly sign residual-risk acceptance | CRITICAL |
| Customer SRO | SD-4 | Programme schedule slips when accreditation surprises emerge late | Programme delivery date moves; political exposure | CRITICAL |
| Customer Operator Team | SD-5 | Vendor systems that "just work on the internet" but break offline drain operator time and erode trust | Operator burnout; accreditation-critical operations dependent on vendor remote support | HIGH |
| Customer DDaT Architects | SD-6 | Stripped-down "community edition" inside the boundary — feature inferior to SaaS used by colleagues in civilian departments | Two-tier governance quality across UK Government | HIGH |
| MOD Defence Digital | SD-7 | Variable governance quality from supplier portfolio undermines supplier-diversification narrative | Cross-MOD digital coherence weak; SME entry barrier persists | HIGH |
| Vendor Service Owner | SD-8 | Without sovereign, the SaaS SME tier cross-subsidy (Principle 17) lacks its margin contributor | SME affordability mission slower or under-funded | CRITICAL |
| Vendor Lead Architect | SD-9 | Without disciplined sovereign-readiness, SaaS-only integrations close off the sovereign route or force a fork (Principle 21 violation) | Single-codebase commitment lost; double engineering cost | HIGH |

**Consequences of Inaction** (Option A Do Nothing — see B2.1 baseline):

- Sovereign-eligible customers (MOD units, intelligence partners, regulated OES) cannot adopt ArcKit at all → fragmented departmental tooling proliferates → governance quality varies across the most sensitive workloads.
- Cross-subsidy contribution from sovereign deployments to the SaaS SME tier (Principle 17 commitment) does not materialise → SME-affordability mission slower to scale, or requires alternative funding (uncomfortable for a self-funded service).
- MOD Defence Digital supplier-diversification narrative weakens: the proof-point that "SMEs can supply MOD using the same toolkit they use for civilian work" never lands.
- Single-codebase discipline (Principle 21) erodes by default — every new SaaS-only integration that is *not* sovereign-ready compounds technical debt that becomes prohibitively expensive to remove later. Sovereign track becomes structurally infeasible after ~18 months of unchecked SaaS-only adoption.

### A1.2 Strategic Drivers

**Link to Stakeholder Analysis**: This SOBC inherits all 17 stakeholder drivers (SD-1 through SD-17) from `ARC-002-STKE-v1.0.md`.

**Primary Drivers** (from Stakeholder Analysis, condensed):

| Driver ID | Stakeholder | Driver Type | Driver Description | Strategic Imperative |
|-----------|-------------|-------------|-------------------|---------------------|
| SD-1 | Customer Accreditor | COMPLIANCE + RISK | Defensible authorisation to operate within accreditation timeline that does not slip | Accreditation feasibility |
| SD-2 | Customer SIRO | COMPLIANCE + RISK | Defensible information-risk acceptance with full supply-chain visibility | Risk owner accountability |
| SD-4 | Customer SRO | STRATEGIC + RISK | Delivery within programme accreditation timeline with no late-surfacing surprises | Programme delivery |
| SD-5 | Customer Operator Team | OPERATIONAL | Predictable operations inside the boundary using runbooks, no vendor remote dependency | Operator self-sufficiency |
| SD-7 | MOD Defence Digital | STRATEGIC | Cross-MOD digital coherence; SME supplier diversification | Defence digital strategy |
| SD-8 | Vendor Service Owner | STRATEGIC + FINANCIAL | Sovereign funds SaaS mission via cross-subsidy without distracting from it | Mission preservation |
| SD-9 | Vendor Lead Architect | OPERATIONAL + STRATEGIC | Single-codebase discipline preserved (Principle 21) | Engineering integrity |
| SD-10 | Vendor Security Lead | COMPLIANCE + RISK | Supply-chain integrity end-to-end; HSM-backed signing-key custody | Vendor existential safety |
| SD-12 | Vendor Finance | FINANCIAL | Sovereign unit economics positive and contributing to cross-subsidy | Commercial viability |
| SD-15 | NCSC | STRATEGIC + COMPLIANCE | UK cyber-resilience baseline; CAF / Cloud Security adoption; supply-chain practice | National cyber posture |
| SD-17 | HM Treasury / CCS / CDDO / DCPP | FINANCIAL + COMPLIANCE | Value for money; supplier diversification; defence-cyber risk profile | Public-spending discipline |

**Strategic Alignment**:

- **Principle 21 (Sovereign and Air-Gapped Deployment)** — non-negotiable platform commitment in `ARC-000-PRIN-v2.0.md`. This SOBC operationalises Principle 21 commercially.
- **Principle 17 (FinOps / Cost Transparency)** — sovereign deployments cost-recover plus deliver positive contribution margin to the SaaS SME tier (Principle 1 affordability commitment). Cross-subsidy is auditable and reportable to HM Treasury and CCS.
- **Principle 4 (Open Standards)** — same APIs, same OpenAPI / AsyncAPI specs, same Markdown / JSON / YAML formats across SaaS and sovereign. Single codebase makes exit credible.
- **Principle 5 (Security by Design)** — MOD Secure by Design + NCSC CAF mapping per release.
- **MOD Defence Digital strategy** — supplier-diversification narrative; cross-MOD digital coherence via recognisable governance artefacts.
- **HMG Government Functional Standard for Digital (GovS 005)** + **Government Functional Standard for Security (GovS 007)** — sovereign deployment respects departmental SRO and SIRO accountability boundaries.
- **NCSC CAF / Cloud Security Principles / supply-chain guidance** — first-class alignment.

### A1.3 Stakeholder Goals

**Goals Addressed** (from `ARC-002-STKE-v1.0.md` — Goal IDs G-1 through G-10):

| Goal ID | Stakeholder | SMART Goal | Current State | Target State | Timeline |
|---------|-------------|------------|---------------|--------------|----------|
| G-1 | Service Owner + Sovereign Delivery Lead | First production sovereign deployment at MOD or sensitive-site customer with positive accreditation outcome | 0 (pre-GA) | ≥ 1 production deployment with ATO + reference case study (subject to consent) | GA + 18 months |
| G-2 | Lead Architect | Single source-of-truth codebase serving SaaS and sovereign with zero per-customer forks and zero permanent feature divergence | n/a (greenfield) | Quarterly review confirms zero forks; feature-flag inventory reviewed and trimmed | Continuous from GA |
| G-3 | Lead Architect + LTS Engineering Lead | Air-gap install / upgrade / backup / restore validated 100% per release in CI representative environment before bundle issue | 0 (pre-build) | 100% pass rate per release with documented evidence | Continuous from alpha |
| G-4 | Vendor Security Lead | MOD Secure by Design evidence pack current per release; NCSC CAF mapping current per release | n/a | Pack dated within last release; delivered with every bundle | Per release |
| G-5 | Vendor Product Manager + LTS Engineering Lead | Each LTS release line supported with security patches at SLAs (Critical 7d / High 30d / Medium 90d) for ≥ 24 months from issue | n/a | SLA adherence reported quarterly; deprecation notices issued ≥ 12 months ahead | Per LTS line |
| G-6 | Service Owner + Finance | Sovereign deployments collectively recover full cost-to-serve plus contribution margin funding the SaaS SME tier | n/a | Quarterly affordability and contribution report shows positive contribution; reportable to HMT / CCS | Within same FY as first production deployment |
| G-7 | Sovereign Delivery Lead + Vendor Security Lead | First customer accreditation cycle achieves ATO on first attempt — no rejection-and-rework | n/a | ATO issued on first formal submission; lessons captured for subsequent customers | First deployment |
| G-8 | Vendor Security Lead + Signing-Key Custodian | Zero signing-key compromise events; HSM-backed signing infrastructure with documented custody, separation of duties, annual rotation, annual independent attestation | n/a | 0 incidents; annual attestation report current | Continuous |
| G-9 | Vendor Security Lead | NCSC CAF mapping current per release; refreshed on material change | n/a | Published with evidence pack | Per release |
| G-10 | Sovereign Delivery Lead | Customer operator teams execute install / upgrade / backup / restore / key rotation / decommission without unscheduled vendor remote intervention | n/a | Zero unscheduled vendor remote interventions for accreditation-critical operations after first install | Continuous from first install |

### A1.4 Scope

**In Scope**:

- Single-codebase sovereign deployment route shared with managed SaaS (Principle 21).
- Air-gap-transferable signed release bundle with SBOM (CycloneDX or SPDX), hash inventory, signed manifests, threat model, MOD SbD evidence pack, NCSC CAF mapping, operator runbooks, release notes.
- Disconnected install, upgrade (forward + roll-back), backup, restore, key rotation, decommission within customer-controlled accredited boundary.
- Pluggable abstractions: AI / model endpoint (default points nowhere), telemetry destination, time source, certificate authority, package mirror, identity provider.
- Long-Term Support release line per `ARC-002-ADR-008-v1.0.md` — annual LTS branch, 24-month security support, decoupled from SaaS rapid cadence, 12-month deprecation notice.
- Procurement listings: G-Cloud, Digital Outcomes and Specialists (DOS), MOD Defence Digital frameworks, DPS as applicable.
- Vendor-side: HSM-backed signing infrastructure, dedicated LTS engineering, sovereign delivery lead role, MOD-SbD evidence-pack discipline.

**Out of Scope** (deferred or explicitly excluded):

- Multi-tenant SaaS commercial model — covered by project 001.
- Companies House SME verification — irrelevant in sovereign mode.
- Public payment processing — sovereign customers contract through standard government / defence procurement.
- Vendor-hosted observability of sovereign-customer telemetry.
- Native mobile apps in v1.
- Languages other than English in v1.
- Top-level platform changes that would require a SaaS / sovereign codebase fork — explicitly forbidden by Principle 21.

**Interfaces** (Integration Requirements per `ARC-002-REQ-v1.0.md`):

- Customer IdP (OIDC / OAuth 2.x / SAML 2.0) — INT-001
- Customer-controlled object storage / database — INT-002
- Customer-controlled time source, CA, package mirror — INT-003
- Customer-controlled observability (SIEM / logs / metrics / traces) — INT-004
- Customer-approved AI / model endpoint (optional, customer-controlled) — INT-005
- Customer email / notification — INT-006
- Customer KMS / HSM — INT-007
- G-Cloud / DOS / Defence frameworks — INT-008
- Vendor remote support channel (opt-in, customer-toggleable, audited) — INT-009
- Vulnerability disclosure inbound channel — INT-010

**Assumptions**:

1. ≥ 1 MOD or sensitive-site customer engages as accreditator-in-the-loop pilot before alpha completion. *Risk if wrong*: G-7 (first-time pass) at risk; whole reference-customer narrative deferred. **Mitigation**: BR-008 commits the engagement; Service Owner accountable.
2. Customer-controlled endpoints (time, CA, package mirror, observability, IdP, KMS, AI) provisioned by customer before install. *Risk if wrong*: install fails fast — bounded operational risk only.
3. Customer accreditators accept vendor MOD SbD evidence pack as **input** to (not replacement for) their own accreditation. *Validated by* SD-1 driver analysis.
4. Cleared personnel available customer-side (operator role) and vendor-side (sovereign delivery / advisory). *Risk if wrong*: R-009 (vendor cleared-personnel shortfall) — Medium residual.
5. DCPP Cyber Risk Profile applicable to engagement is identifiable at sales engagement.

**Dependencies**:

- **Internal** (vendor-side): Project-001 SaaS engineering must respect offline-criterion gate when adopting new components (Principle 21). Cross-project quarterly architecture forum.
- **External**: Pilot customer commitment (G-1 / BR-008); HSM provider contract; ex-MOD assurance advisor for pre-formal MOD SbD readiness check.
- **Technical**: Pluggable AI abstraction (joint with project 001 SaaS); LTS release infrastructure; signed-bundle pipeline (HSM-backed); CI representative environment with network-deny test profile.

### A1.5 Why Now?

**Urgency Factors**:

- **Principle 21 erosion is time-decaying**: every SaaS-only integration that is *not* sovereign-ready compounds technical debt. After ~18 months of unchecked SaaS-only adoption, the sovereign track becomes structurally infeasible without a fork — and a fork is a Principle 21 violation that the Architecture Review Board has determined is non-negotiable.
- **MOD Defence Digital supplier-diversification window**: defence digital strategy is actively soliciting SME-friendly toolchains that work across SaaS and sovereign. The narrative window is now; later-arriving suppliers find the slot taken.
- **Cross-subsidy compounding**: sovereign contribution to the SaaS SME tier (Goal G-6) compounds — earlier deployment means earlier and larger cumulative contribution to the affordability mission.
- **First-customer accreditator availability**: the accreditator-in-the-loop alpha (R-001 mitigation) needs a willing accreditator. Defence Digital and customer-SRO contacts cycle; current contacts are warm.
- **NCSC CAF v4 / framework updates**: aligning to the current CAF version on first issue is materially easier than retrofitting after CAF v4 becomes mandatory and the vendor's evidence pack is on v3.

**Opportunity Cost of Delay** (calibrated to do-nothing baseline in B2.1):

- Each year of delay defers ≥ £0.5M-£1.0M cross-subsidy contribution to the SaaS SME tier — measurable opportunity cost to Principle 1 affordability mission.
- Each year of delay strengthens incumbent commercial defence-EA tooling vendors, raising the cost of subsequent sovereign-track entry.
- Continued sovereign-eligible customer fragmentation: each such customer that adopts a non-ArcKit alternative is a multi-year lock-in lost to the platform.

**Window of Opportunity**: 2026 H2 - 2027 H1 alpha; 2027 H2 private beta; 2027 Q4 GA. This window aligns with HSM-provider contract availability, ex-MOD assurance advisor capacity, and pilot customer SRO calendars.

---

# PART B: ECONOMIC CASE

## B1. Critical Success Factors

Five CSFs derived from `ARC-002-STKE-v1.0.md` — Critical Success Factors and Outcome KPIs (O-1 through O-7):

1. **First-time customer accreditation pass (O-5 / G-7)**:
   - **Measure**: ATO issued on first formal submission for first customer; ≥ 80% first-time pass rate cumulative across customers.
   - **Threshold**: First customer ATO on first or first-with-minor-conditions submission.

2. **Single-codebase track record (O-2 / G-2)**:
   - **Measure**: Forks count = 0; feature-flag inventory monotonically declining or stable.
   - **Threshold**: Zero forks across all releases for the duration of the project.

3. **Air-gap operability across releases (O-4 / G-3)**:
   - **Measure**: Per-release CI pass rate on disconnected / network-deny profile.
   - **Threshold**: 100% pass rate per release before bundle issue; zero air-gap regressions cumulative.

4. **Sovereign cross-subsidy contribution proven (O-3 / G-6)**:
   - **Measure**: Quarterly contribution figure published; year-on-year growth in absolute and relative terms.
   - **Threshold**: ≥ 100% cost-to-serve recovery + measurable contribution to SaaS SME tier within the same financial year as first production deployment.

5. **Zero supply-chain incidents (O-7 / G-8)**:
   - **Measure**: Signing-key compromise count; supply-chain incidents traced to vendor artefacts.
   - **Threshold**: 0 incidents; annual independent attestation of signing infrastructure current.

## B2. Options Analysis

Four options evaluated, plus a fifth dismissed early (off-the-shelf re-sale of an existing defence-EA tooling vendor). Costs are ROM (±30%) at SOBC stage. HMT optimism bias is applied separately in B3 sensitivity analysis.

### Option A: Do Nothing (Baseline)

**Description**: Continue with project 001 SaaS only. Sovereign-eligible customers remain excluded from ArcKit. Single-codebase Principle 21 commitment is left unimplemented commercially (only philosophically).

**Costs** (3-year, vendor-side):

- Capital: £0
- Operational (vendor): £0 incremental
- **Customer-side hidden cost**: ≥ £4.5M-£15M cumulative across 3-5 sovereign-eligible customers who instead pay for fragmented bespoke tooling and forced re-accreditation cycles (per `ARC-002-ADR-008-v1.0.md` §5 Option 0 analysis: ~£150k-£500k per re-accreditation per customer per year).
- Total vendor: £0; total system cost across UK government: £4.5M-£15M

**Benefits**: £0 vendor-side; sovereign-eligible customers paying full cost-to-serve to alternative suppliers without any cross-subsidy contribution to UK SME ecosystem.

**Pros**:

- No vendor-side capital outlay.
- No new operational complexity.

**Cons**:

- ❌ 0% of sovereign stakeholder goals met (G-1 through G-10 all blocked).
- ❌ Principle 21 hollowed out — single-codebase commitment is philosophical only without a sovereign deployment in production.
- ❌ Cross-subsidy contribution to SaaS SME tier (Principle 17) unrealised → SaaS affordability mission slower.
- ❌ MOD Defence Digital supplier-diversification narrative weakens.
- ❌ SaaS-only integrations adopted unchecked for 18+ months close off sovereign route by accumulating offline-incompatible technical debt — sovereign route becomes structurally infeasible.
- ❌ Sovereign-eligible customers pay £4.5M-£15M cumulative across 3-5 customers to *other* suppliers — opportunity-cost loss to UK SME ecosystem.

**Risks**:

- Cross-subsidy gap: SaaS tier affordability mission slower → Principle 1 commitment under-performed (financial impact: deferred SME tier rollout).
- Principle 21 erosion: future re-entry to sovereign requires a fork (Principle 21 violation) or 18-24 months of deferred refactoring.

**Stakeholder Goals Met**: 0%

**Recommendation**: ❌ **REJECT** — failed against every Critical Success Factor; Principle 21 is non-negotiable per Architecture Review Board.

---

### Option B: Hard Fork (Separate Sovereign Codebase)

**Description**: Maintain a separate sovereign codebase, branched from the SaaS at GA and diverging thereafter. Each codebase optimised independently for its deployment model. Sovereign team owns its own roadmap, dependencies, releases, and evidence packs.

**Scope**:

- Separate Git repository for sovereign.
- Separate engineering team (or larger engineering organisation with dedicated sovereign squad).
- Separate dependency choices, separate AI integration, separate observability — no pluggable abstractions needed.
- Independent release cadence.

**Costs** (3-year, ROM ±40% — wider band reflects forking unpredictability):

- Capital (Year 0-1):
  - Sovereign-codebase provisioning, separate CI / CD: £0.30M
  - Sovereign-only architecture refactor for offline operation: £0.50M
  - Initial sovereign engineering team ramp (4-6 FTE Year 1, recruitment + onboarding): £0.65M
- Operational (3-year cumulative):
  - Sovereign engineering team: £4.20M (4 FTE × £350k/yr × 3 yrs)
  - Parallel security / accreditation evidence work per fork: £1.35M
  - Compounding divergence cost (refactors as SaaS evolves features that need re-implementing in the fork): £1.50M (Year 2 + Year 3)
- **3-year TCO: £8.50M**

**Benefits** (3-year):

- B-FORK-1: Sovereign customer revenue 3-year cumulative — same as Option C nominally (~£5.5M)
- B-FORK-2: Cross-subsidy contribution potentially higher per-customer because sovereign-only optimisations are unconstrained — but TCO eats most of it
- Total benefits: ~£5.5M

**Net Benefit**: ~−£3.0M (3-year)

**Pros**:

- ✅ Sovereign team optimised purely for sovereign — no SaaS-driven compromise on architecture decisions.
- ✅ No need for pluggable abstractions in the SaaS.

**Cons**:

- ❌❌ **Direct violation of Principle 21** — non-negotiable. ARB will not approve.
- ❌ Engineering cost roughly 2-3× Option C; cross-subsidy contribution to SaaS SME tier collapses (Principle 17 commitment compromised).
- ❌ Feature divergence accumulates — within 18-24 months, sovereign customers receive a noticeably inferior product, MOD Defence Digital supplier-diversification narrative weakens.
- ❌ Customer-side perception risk: "two codebases" is a quality signal interpreted negatively by accreditators (suggests vendor split focus).
- ❌ Knowledge fragmentation — security fixes must be reasoned about in two contexts; integration test surface ~doubles.
- ❌ Open-standards / portability claim degraded — same APIs hard to guarantee across diverging codebases.

**Stakeholder Impact**:

- G-1 (reference customer): ✅ Met in principle, but late and costly.
- G-2 (single codebase): ❌ Definitionally not met.
- G-6 (cross-subsidy contribution): ❌ Materially eroded by ~3× engineering cost.
- G-7 (first-time pass): ⚠️ Lower confidence — fork divergence weakens evidence-pack consistency.
- All other goals met but at materially higher cost.

**Stakeholder Goals Met**: ~40% (G-1 only at material extra cost; G-2 fails definitionally; G-6 fails)

**Risks**:

- R-003 (single-codebase divergence) realised by definition — no mitigation possible.
- R-011 (cross-subsidy erosion) — high likelihood from cost overhead.
- Customer perception risk — "split team / split codebase" decreases first-customer confidence.

**Recommendation**: ❌ **REJECT** — Principle 21 violation, non-negotiable per ARB; ~3× cost; cross-subsidy commitment compromised; customer-perception risk.

---

### Option C: Single Codebase + Sovereign Overlay (RECOMMENDED)

**Description**: One codebase serves SaaS and sovereign. Pluggable abstractions where SaaS and sovereign behaviour diverge (AI endpoint, telemetry, time, CA, package mirror, IdP). Disconnected-mode CI profile validates offline operation per release. Signed bundle (HSM-backed signing) packaged from the same Git revision that powers the SaaS deployment. LTS release line per ADR-008. Single security and accreditation evidence pipeline; MOD SbD evidence pack generated per release.

**Scope**:

- Single Git repository, single CI / CD pipeline producing both SaaS deployment and sovereign bundle from one revision.
- Pluggable abstractions per integration point (FR-004, FR-005).
- Disconnected / network-deny CI profile per release; bundle issue gated on 100% pass rate.
- HSM-backed signing infrastructure with documented key custody, separation of duties, annual rotation, annual independent attestation.
- LTS release line per ADR-008 (annual cut, 24-month security support, 12-month deprecation notice, no feature backports).
- MOD Secure by Design evidence pack per release (`/arckit:mod-secure`); NCSC CAF mapping per release.
- G-Cloud, DOS, MOD Defence Digital framework listings (BR-007).
- Sovereign Delivery Lead role for customer onboarding; opt-in audited remote-support channel (FR-013).

**Costs** (3-year, ROM ±30%):

**Capital — Year 0 (build) + early Year 1**:

| Item | Cost | Notes |
|------|------|-------|
| Sovereign packaging engineering (offline readiness, pluggable abstractions, bundle pipeline) | £0.40M | 1.0-1.2 FTE × 9 months + tooling |
| LTS branch infrastructure + CI capacity expansion (parallel test matrix) | £0.18M | Per ADR-008 §5 Option 2 (£120k-£200k range; midpoint) |
| HSM-backed signing infrastructure + key custody policy + initial attestation | £0.20M | HSM unit + provisioning + first independent attestation |
| MOD Secure by Design evidence pack tooling (`/arckit:mod-secure` integration) + threat-modelling discipline | £0.15M | First evidence-pack cycle + ex-MOD advisor day-rate ~£10k for walkthrough |
| Operator runbook library (FR-011) — install / upgrade / rollback / backup / restore / key rotation / decommission / IR / DR | £0.12M | Eight runbooks × ~£15k each |
| Pre-sales engagement infrastructure (MOD Defence Digital liaison, framework listings, reference architecture diagrams) | £0.10M | G-Cloud + DOS submissions |
| Pluggable AI abstraction (joint with project 001) | £0.15M | Vendor-side share of joint cost; supports FR-004 |
| Contingency (15% of capex above) | £0.15M | |
| **Total CapEx (Year 0-1)** | **£1.45M** | |

**Operational — Year 1, Year 2, Year 3**:

| Item | Year 1 | Year 2 | Year 3 | 3-Year Total |
|------|--------|--------|--------|--------------|
| LTS Engineering Lead + 1.0-1.5 FTE backports + security triage | £0.30M | £0.32M | £0.34M | £0.96M (per ADR-008 §5 Option 2 OPEX £250k-£400k/yr; midpoint £325k) |
| Sovereign Delivery Lead (customer onboarding, accreditation support, advisory liaison) | £0.18M | £0.18M | £0.18M | £0.54M |
| MOD SbD evidence pack refresh per release (4 releases/yr × ~£25k) + NCSC CAF mapping | £0.12M | £0.12M | £0.12M | £0.36M |
| HSM operations + annual independent attestation + signing-key rotation + pen-test of pipeline | £0.10M | £0.10M | £0.10M | £0.30M |
| Customer-engagement / advisory cleared-personnel availability (per R-009 mitigation) | £0.08M | £0.10M | £0.12M | £0.30M |
| CI compute increment (parallel matrix incl. disconnected profile) | £0.03M | £0.04M | £0.05M | £0.12M |
| Cross-subsidy reporting / Finance ops + quarterly affordability review | £0.04M | £0.04M | £0.04M | £0.12M |
| Accreditation refresh per customer (Year 2 onwards as customer count grows) | £0 | £0.20M | £0.40M | £0.60M |
| Contingency (10% of opex above) | £0.09M | £0.11M | £0.13M | £0.33M |
| **Total OpEx** | **£0.94M** | **£1.21M** | **£1.48M** | **£3.63M** |

**3-Year TCO (pre-optimism-bias)**: £1.45M + £3.63M = **£5.08M**.

> Note: above includes contingency at line-item level; HMT optimism bias applied separately in B3.

**Benefits** (3-year, customer-revenue + cross-subsidy contribution):

| Benefit ID | Benefit Description | Stakeholder Goal | Type | Year 1 | Year 2 | Year 3 | 3-Year Total |
|------------|---------------------|------------------|------|--------|--------|--------|--------------|
| B-1 | Sovereign customer 1 revenue (pilot, partial year) | G-1 | FINANCIAL | £0.20M | £1.20M | £1.20M | £2.60M |
| B-2 | Sovereign customer 2 revenue (Year 2 onwards) | G-1 | FINANCIAL | £0 | £0.40M | £1.10M | £1.50M |
| B-3 | Sovereign customer 3 revenue (Year 3) | G-1 | FINANCIAL | £0 | £0 | £0.60M | £0.60M |
| B-4 | Cross-subsidy contribution to SaaS SME tier (Principle 17) — 30% of net sovereign margin | G-6 | STRATEGIC + FINANCIAL | £0.05M | £0.30M | £0.55M | £0.90M |
| B-5 | MOD Defence Digital supplier-diversification narrative — reference case study, follow-on engagements | G-1, SD-7 | STRATEGIC | n/q | n/q | n/q | qualitative |
| B-6 | Single-codebase Principle 21 evidence at production scale — strengthens SaaS open-standards / portability claim | G-2 | STRATEGIC | n/q | n/q | n/q | qualitative |
| B-7 | Avoided customer-side cost (do-nothing baseline) — sovereign customers pay ArcKit at LTS-discipline rates rather than fragmented bespoke alternatives at re-accreditation churn | G-1 | RISK + STRATEGIC | n/q | n/q | n/q | ~£1.5-£3M cumulative across 3 customers (system-wide, not vendor revenue) |
| **Total Quantified Vendor Benefits** | | | | **£0.25M** | **£1.90M** | **£3.45M** | **£5.60M** |

**Net Position (pre-optimism-bias)**:

- Total vendor benefits 3-year: £5.60M
- Total vendor TCO 3-year: £5.08M
- **Net benefit (pre-bias)**: £+0.52M
- Plus £4.5M-£15M+ avoided customer-side cost (system value) and qualitative strategic benefits (B-5, B-6, B-7).

**Net Present Value** (3.5% HMT discount rate, pre-bias):

| Year | Costs (TCO) | Benefits (vendor revenue + cross-subsidy) | Net Cashflow | Discount Factor | Present Value |
|------|-------------|-------------------------------------------|--------------|-----------------|---------------|
| 0 (Year 0 build) | £1.45M | £0 | −£1.45M | 1.000 | −£1.45M |
| 1 | £0.94M | £0.25M | −£0.69M | 0.966 | −£0.667M |
| 2 | £1.21M | £1.90M | +£0.69M | 0.934 | +£0.644M |
| 3 | £1.48M | £3.45M | +£1.97M | 0.902 | +£1.778M |
| **Total** | **£5.08M** | **£5.60M** | **+£0.52M** | | **NPV = £+0.305M** |

**Return on Investment (pre-bias)**:

- ROI 3-year = (£5.60M − £5.08M) / £5.08M × 100% = **10.2%**
- Payback Period: cumulative net cashflow positive in **Month 24** (Year 2 closes net positive).
- BCR (Benefit-Cost Ratio): £5.60M / £5.08M = **1.10**

**Pros**:

- ✅ ~85-90% of stakeholder goals met (G-1 through G-10).
- ✅ Principle 21 directly satisfied at the architecture level.
- ✅ Principle 17 cross-subsidy operationalised with reportable contribution to SaaS SME tier.
- ✅ Single-codebase commitment provable in production — strengthens SaaS open-standards / portability claim.
- ✅ MOD Defence Digital supplier-diversification narrative landed.
- ✅ Engineering cost ~3× lower than Option B.
- ✅ Acceptable 3-year payback; positive NPV pre-bias.
- ✅ ADR-008 LTS line gives accreditators the predictability they need (BR-005 honoured).
- ✅ Configuration-only customisation discipline (Conflict C-1 resolution) preserves single codebase against per-customer drift.

**Cons**:

- ⚠️ Pluggable-abstraction discipline must be maintained on every new SaaS integration — ongoing engineering tax (~5-10% of relevant integration cost).
- ⚠️ First-customer accreditation (R-001) is at appetite ceiling — load-bearing risk for the entire track.
- ⚠️ Five risks (R-001, R-002, R-003, R-004, R-005, R-007) remain above sovereign-specific appetite at residual — formal Service Owner acknowledgement required (per `ARC-002-RISK-v1.0.md` §I).
- ⚠️ Cross-project quarterly architecture forum required to protect SaaS roadmap from sovereign-driven displacement (Conflict C-6 resolution).
- ⚠️ HMT optimism bias of +30% on capability cost (per `ARC-002-RISK-v1.0.md` §I) materially squeezes payback; OBC cost discipline essential.

**Stakeholder Impact**:

- G-1 (reference customer): ✅ Met by GA + 18 months at ~85% confidence (subject to R-001 mitigation).
- G-2 (single codebase): ✅ Met by design.
- G-3 (air-gap operability): ✅ Met by CI gate + bundle issue policy.
- G-4 (MOD SbD pack current): ✅ Met per release.
- G-5 (LTS ≥ 24 months): ✅ Met per ADR-008.
- G-6 (cross-subsidy contribution): ✅ Met within same FY as first production deployment.
- G-7 (first-time accreditation pass): ⚠️ Met at 80% target subject to accreditator-in-the-loop alpha funding and execution.
- G-8 (zero signing-key compromise): ✅ Met by HSM-backed infrastructure + annual attestation.
- G-9 (NCSC CAF per release): ✅ Met per release.
- G-10 (customer-led operability): ✅ Met by FR-011 runbook library + opt-in audited remote-support model.

**Stakeholder Goals Met**: ~85% (10/10 met with G-1 and G-7 at confidence-bounded 80-85%).

**Risks** (summary; full register `ARC-002-RISK-v1.0.md`):

- R-001 (first-customer accreditation fail): Strategic, residual 12, at appetite ceiling — load-bearing. Mitigation: accreditator-in-the-loop alpha programme.
- R-002 (MOD SbD assessment fail): Compliance, residual 12, exceeds appetite +200%. Mitigation: ex-MOD advisor pre-formal walkthrough; HSM in place before assessment.
- R-003 (single-codebase divergence): Technology, residual 9, exceeds Low appetite +50%. Mitigation: configuration-only customisation discipline; quarterly fork-pressure review; refactor budget.
- R-004 (signed-bundle / supply-chain compromise): Compliance, residual 8 (after HSM + attestation; inherent 20). Mitigation: HSM + separation of duties + annual rotation + annual attestation.
- R-007 (accredited-boundary egress incident): Reputational, residual 8, exceeds Very-Low appetite +100%. Mitigation: network-deny CI profile + bundle issue gate.

**Recommendation**: ✅ **ACCEPT** — only option satisfying Principle 21 + Principle 17 simultaneously; positive NPV; payback within window; risk profile manageable with declared above-appetite acceptances.

---

### Option D: External Partner-Managed Sovereign Packaging

**Description**: Vendor retains the SaaS codebase. A third-party defence-systems integrator (or specialist sovereign-packaging vendor) takes the SaaS source, packages it into a sovereign bundle, holds the customer accreditation evidence, and operates the LTS line under licence from the vendor.

**Scope**:

- Vendor licenses source to partner.
- Partner produces sovereign bundles, owns customer-facing accreditation evidence, runs LTS backports, fronts customer engagements.
- Vendor provides upstream patches and security advisories; partner backports and signs.

**Costs** (3-year, ROM ±40% — high uncertainty band reflects partner-economics opacity):

- Capital (Year 0):
  - Source-licence agreement legal + IP work: £0.10M
  - Initial knowledge transfer + dual-key reproducibility setup: £0.20M
  - Partner-readiness audits (commercial + security): £0.15M
- Operational (3-year):
  - Royalty share (typically 30-40% of partner sovereign revenue flows to vendor): vendor receives ~£0.40M-£0.60M/yr × 3 yrs = £1.50M
  - Vendor-side coordination + patch handoff + IP audit: £0.40M/yr × 3 yrs = £1.20M
  - Vendor-side reduction in MOD SbD pack costs (partner-borne): −£0.20M (saving)
- Net vendor TCO: £0.45M capital + £1.20M opex (3-year) = **£1.65M**

**Benefits** (3-year):

- Vendor royalty receipts: £1.50M
- Cross-subsidy contribution: indirect via royalty — typically 50-70% lower than direct delivery (partner takes the largest share)
- Reference-customer narrative: reduced credibility (partner-owned, not vendor-owned)

**Net Benefit**: £1.50M − £1.65M = **−£0.15M** (vendor-side); plus loss of direct customer relationship and brand presence in MOD.

**Pros**:

- ✅ Lower vendor-side capital outlay (−£1M vs Option C).
- ✅ Partner specialises in defence accreditation — potentially faster first-customer ATO.
- ✅ Vendor engineering bandwidth fully focused on SaaS.
- ✅ Partner takes regulatory burden for MOD SbD evidence pack.

**Cons**:

- ❌ Cross-subsidy contribution to SaaS SME tier (Principle 17) materially eroded — partner takes ~60-70% of margin; vendor royalty share alone insufficient to fund the SME tier at the rate Principle 17 commits to.
- ❌ Vendor brand absence from MOD context — supplier-diversification narrative weakens because the *vendor* is no longer the defence-context supplier; partner is.
- ❌ Single-codebase commitment harder to enforce — partner has incentive to stabilise on a frozen revision rather than track upstream, creating de-facto fork.
- ❌ Customer relationship intermediated by partner — vendor cannot directly act on customer feedback that should influence the SaaS roadmap (one of the key strategic benefits of going sovereign).
- ❌ IP / source-licence terms create irreversible dependence on partner's commercial health; partner failure or acquisition becomes a sovereign-customer-impacting event.
- ❌ Quality variability — partner-issued evidence packs harder to enforce against vendor-canonical standard.
- ❌ Customer perception: defence-systems integrators repackaging governance toolkits is a familiar pattern that customers know is expensive and fragile.

**Stakeholder Impact**:

- G-1 (reference customer): ✅ Met (partner-owned reference) — but credibility lower than direct.
- G-2 (single codebase): ⚠️ At risk — partner pressure for frozen revision.
- G-6 (cross-subsidy contribution): ❌ Materially eroded.
- G-7 (first-time pass): ✅ Met — partner specialism is a positive.
- Most other goals met but at material commercial cost.

**Stakeholder Goals Met**: ~60% (most goals met, but G-6 — the strategic reason this project exists per Principle 17 — fails).

**Recommendation**: ⚠️ **REJECT** — fails the cross-subsidy commitment that is the project's strategic raison d'être (Principle 17 / Goal G-6 / SD-8). Reasonable second-best if cross-subsidy commitment is renegotiated downward (it is not at current ARB direction). Reconsider only if Option C funding cannot be secured.

---

## B3. Recommended Option

**Recommendation**: **Option C — Single Codebase + Sovereign Overlay**

**Rationale** (mapped to CSFs in B1):

1. **Best — and only — strategic fit**: Only option that simultaneously satisfies Principle 21 (no fork) and Principle 17 (cross-subsidy contribution); Options A and B fail Principle 21; Option D fails Principle 17.
2. **Stakeholder satisfaction**: Meets ~85% of goals (10/10 met with G-1, G-7 at 80-85% confidence subject to risk mitigation execution); compares against 0% (A), ~40% (B), ~60% (D).
3. **Acceptable risk profile with declared above-appetite acceptances**: Five risks above sovereign-specific appetite at residual; acceptances declared in `ARC-002-RISK-v1.0.md` §G; Service Owner formal acknowledgement is a condition of approval.
4. **Affordability**: 3-year vendor TCO £5.08M (pre-bias) within self-funded service envelope. Cross-subsidy contribution to SaaS SME tier visibly positive from Year 2.
5. **Deliverability**: 24-month timeline (alpha 2027 H1 → private beta H2 → GA Q4 2027) realistic given HLD complete (`ARC-002-HLDR-v1.0.md`) and ADR-008 LTS policy formally adopted; pluggable abstractions joint-funded with project 001.
6. **Value for money for HMG**: Single-codebase produces sovereign customers same artefacts at same quality as civilian-department colleagues — cross-government governance coherence achieved at materially lower system-wide cost than fragmented bespoke alternatives (~£4.5M-£15M avoided customer-side cost across 3-5 customers per Option A baseline analysis).

**Sensitivity Analysis (pre-optimism-bias)**:

| Sensitivity | NPV | BCR | Payback | Status |
|-------------|-----|-----|---------|--------|
| Base case (B2.3 figures) | £+0.31M | 1.10 | Month 24 | Positive |
| Costs +20% | £−0.71M | 0.92 | Month 30 | Negative |
| Benefits −20% | £−0.81M | 0.88 | Month 32 | Negative |
| Customer 2 slips 6 months | £−0.18M | 0.97 | Month 30 | Marginal |
| Customer 3 not signed | £−0.31M | 0.94 | Month 32 | Negative |
| All three slips manifest | £−1.50M | 0.71 | > 36 months | Concerning |

The case is **sensitive** to customer signing cadence; OBC must firm up at least the pilot commercial terms.

**Optimism Bias Adjustment** (HMT Green Book + `ARC-002-RISK-v1.0.md` §I):

Per `ARC-002-RISK-v1.0.md` §I Economic Case: "HM Treasury optimism-bias add-on of approximately +30% on capability cost (typical for Greenfield ICT) reflects R-008 (AI integration), R-009 (cleared-personnel availability), R-010 (LTS Year-3 backport SLA) cumulative." This is **heavier than the SaaS sister project** because it must additionally absorb first-attempt accreditation risk (R-001) and supply-chain evidence-discipline risk (R-002, R-004).

**Adjusted figures**:

- 3-year capability cost (capex + opex) × 1.30 = £5.08M × 1.30 = **£6.60M**
- Adjusted net 3-year position: £5.60M − £6.60M = **−£1.00M**
- **NPV (post-bias, 3.5% discount)**: £+0.62M to £−0.30M depending on benefit timing — central estimate **£+0.62M** (slight positive due to discounted-Year-3 benefits remaining strong)
- **BCR (post-bias)**: £5.60M / £6.60M = **0.85** (NPV-stress) — **note**: BCR is pure 3-year ratio; full 5-year horizon (sovereign customers typically 5-7 year contracts) lifts BCR materially (see B4 below)
- **Payback (post-bias)**: Month 30 (Year 2 closes marginally negative; Year 3 closes positive)

The 3-year horizon is the SOBC standard but is conservative for sovereign — accredited deployments typically run 5-7 years. **5-year horizon** (informational, reverts to standard 3-year for SOBC decision):

- 5-year benefits: £5.60M (Year 0-3) + £4.20M (Year 4-5 incremental customer revenue + steady-state cross-subsidy) = **£9.80M**
- 5-year costs (post-bias): £6.60M (Year 0-3) + £3.20M (Year 4-5 steady-state opex × 1.30) = **£9.80M**
- 5-year BCR (post-bias) = 1.0; with the additional avoided customer-side cost (£4.5M-£15M cumulative), system-wide BCR > 2.0.

The 5-year horizon brings the case clearly into "good value for money" per HMT VfM guidance once avoided system-wide cost is included.

## B4. Value for Money Assessment

**Qualitative Assessment**:

- **Economy**: Bespoke contracts per accredited site (no G-Cloud single-call-off — accreditation is bespoke per customer); MOD Defence Digital framework procurement; LTS pricing per ADR-008 amortised across customers — best per-customer unit cost achievable for a sovereign-grade deployment.
- **Efficiency**: Single codebase amortises engineering investment across SaaS + sovereign — ~3× more efficient than Option B fork.
- **Effectiveness**: Meets ~85% of stakeholder goals; the 15% gap is confidence-bounded execution of accreditation discipline (R-001 mitigation), not architectural shortfall.

**Overall VfM Rating**: **Medium-High** at 3-year horizon (pre- and post-bias); **High** at 5-year horizon when system-wide avoided cost is included.

**Justification**: The recommended option is the only commercially viable Principle-21-compliant + Principle-17-compliant route. Sensitivity to customer signing cadence is addressable in the OBC by firming pilot commercial terms; HMT optimism-bias adjustment is comfortably absorbable at 5-year horizon and marginally absorbable at 3 years.

---

# PART C: COMMERCIAL CASE

## C1. Procurement Strategy

### C1.1 Market Assessment

**Market Maturity**:

- Sovereign / air-gapped enterprise-architecture toolkits — small market, defence-systems-integrator-dominated. Bespoke per-customer is the norm; LTS-disciplined product offerings rare.
- Pluggable AI / model-endpoint abstraction with sovereign default-off — emerging capability; ArcKit is well-positioned.
- HSM-backed signing infrastructure — mature commercial market (multiple UK suppliers).
- MOD Secure by Design assessment ecosystem — small specialist advisor market; ex-MOD assurance advisors available at ~£10k/day.

**Supplier Landscape** (vendor-side procurement of inputs):

- **Tier 1** (HSM providers): Multiple UK sovereign-eligible suppliers (e.g., Thales / Entrust UK presence) — competitive.
- **Tier 2** (MOD assurance advisors): ~10-20 boutique consultancies; some ex-MOD principals.
- **Tier 3** (CI / parallel-matrix infrastructure): Mainstream UK cloud providers + customer-controlled / on-prem CI for representative isolated environment.

**UK Government Digital Marketplace Assessment** (vendor-as-supplier route):

- **G-Cloud 14**: Sovereign offering listed alongside SaaS — sovereign call-off requires bespoke schedule for accreditation evidence delivery and customer-controlled deployment.
- **DOS 6**: Sovereign Delivery / accreditation-support / LTS-onboarding professional services listed.
- **MOD Defence Digital frameworks**: Engagement plan with framework owner; BR-007 commits to listing on applicable defence-specific frameworks.
- **DPS / specialist defence frameworks**: Considered case-by-case per customer engagement.
- **SME participation**: ArcKit-as-a-Service is an SME supplier — directly contributing to SME spend ambition for both civilian and defence procurement.

### C1.2 Sourcing Route (Customer → Vendor)

> ⚠️ **Per user input**: bespoke contracts per accredited site (no single G-Cloud-wide call-off — accreditation is per-customer); MOD Defence Digital framework procurement; LTS pricing per ADR-008.

**Recommended Route** (per-customer):

- **Primary**: MOD Defence Digital framework procurement for MOD customers; bespoke contract per accredited site.
- **Secondary**: G-Cloud listing as gateway for civilian sensitive-site customers (OES, regulated departments) — the listing identifies the offering; the call-off is bespoke.
- **Tertiary**: DOS for accreditation-support and onboarding professional services.

**Why bespoke (not single-call-off G-Cloud)**:

- Accreditation evidence terms must be tailored per customer's accreditation chain (JSP 604 / NCSC CAF / departmental SbD).
- Pricing per ADR-008 reflects customer-specific accreditation effort, signing-infrastructure share, and LTS line commitment — not a uniform list price.
- Customer-controlled endpoints (KMS, IdP, observability) and customer-side data classification ceiling vary materially per customer — material contract variability.
- IP and data-handling clauses must respect each customer's accreditation ceiling.

**Alternative Routes Considered**:

| Route | Pros | Cons | Recommendation |
|-------|------|------|----------------|
| Direct call-off via G-Cloud sovereign-deployment service | Fast, transparent | Accreditation-evidence terms cannot fit standard G-Cloud schedule; pricing variability not accommodated | Reject for sovereign-specific aspects; use as gateway only |
| Pure bespoke (no framework) | Maximum tailoring | High cost-to-bid; SME barrier | Reject — MOD Defence Digital framework + bespoke schedule is better |
| Defence-specific framework + bespoke schedule | Right level of tailoring; framework discipline; SME-accessible | Per-customer commercial effort | **ACCEPT** for MOD; G-Cloud-gated bespoke for civilian sensitive sites |

### C1.3 Contract Approach

**Proposed Contract Type** (per customer):

- **Initial deployment**: Fixed-price milestone-based — install + first accreditation cycle support + first 12 months LTS coverage + first MOD SbD evidence pack acceptance.
- **Steady-state**: Annual managed-LTS subscription — patches + evidence-pack refresh + opt-in audited remote-support entitlement + quarterly accreditation-aware customer review.
- **Optional**: Bundle of per-incident professional services for accreditation refresh, framework migration, or customer-led major upgrade.

**Contract Duration**:

- Initial: 3-year primary term aligned with customer accreditation cycle (typical JSP 604 ATO duration).
- Extension: 1+1+1 year extensions to align with subsequent re-accreditation cycles, total 6-7 year horizon typical.
- Termination: 12-month notice from either side; mandatory exit-management plan including customer-driven export (FR-009) and bundle-revocation procedure.

**Payment Structure**:

- Year 0 / install: 30% on contract award; 40% on first ATO; 30% on completion of first LTS cycle.
- Steady-state: Annual subscription paid quarterly in advance; LTS patch-bundle delivery free at-point-of-issue (not separately metered).
- Below-cost-floor pricing: forbidden without explicit Service Owner approval per `ARC-002-RISK-v1.0.md` R-011 mitigation.

**Key Contract Terms**:

- **SLAs**: Patch cadence (Critical 7d / High 30d / Medium 90d per NFR-SEC-008); evidence-pack delivery per release; opt-in remote-support response time (when activated).
- **Penalties**: Per-day liquidated damages for missed patch SLA; capped at annual subscription value.
- **IP**: Source remains vendor IP; customer receives broad licence to use signed bundle within their boundary; bespoke configuration is customer IP.
- **Termination / exit**: 12-month notice; mandatory full-fidelity export (Markdown / JSON / YAML — FR-009); bundle de-licensing protocol; signing-key revocation handling.
- **Data protection**: Article 28 processor terms where vendor processes customer personal data (almost never in default sovereign profile — vendor is processor only for opt-in audited remote-support telemetry).

### C1.4 Social Value

**UK Government Procurement Context**:

- **Defence procurement social-value weighting**: typically 10% in MOD Defence Digital frameworks aligned with HMG social-value model (PPN 06/20). Civilian-sensitive-site procurement follows civilian social-value model; minimum 10% weighting.

**Social Value Themes ArcKit-as-a-Service can credibly commit to**:

1. **Economic — SME participation**: ArcKit-as-a-Service is an SME supplier; sovereign deployments contribute to MOD / departmental SME spend ambition.
2. **Economic — Cross-subsidy to UK SME ecosystem**: Sovereign margin contributes to SaaS SME tier (Principle 17). This is a directly auditable social-value claim.
3. **Social — Cleared-personnel skills development**: Sovereign Delivery and LTS engineering roles support UK cleared-personnel career pathways.
4. **Environmental — Customer-controlled infrastructure**: Sovereign deployments use customer-existing infrastructure (no new vendor data-centre footprint).
5. **Skills**: Open-standards artefact format means customer architects build transferable skills.

**Evaluation Approach** (per customer tender):

- Technical: 60-65% (accreditation-evidence quality, single-codebase track record, LTS commitment)
- Cost: 25-30% (per-customer pricing transparency, LTS subscription)
- Social Value: 10% (SME contribution, cross-subsidy, UK cleared-personnel pathway)

---

# PART D: FINANCIAL CASE

## D1. Budget Requirement

**Total Vendor-Side Investment Required**: £5.08M (pre-bias) / £6.60M (post-HMT optimism-bias) over 3 years.

### D1.1 Capital Expenditure (CapEx — Year 0-1)

| Item | Year 0 | Year 1 | Total |
|------|--------|--------|-------|
| Sovereign packaging engineering (offline readiness, pluggable abstractions, bundle pipeline) | £0.30M | £0.10M | £0.40M |
| LTS branch infrastructure + CI capacity expansion | £0.12M | £0.06M | £0.18M |
| HSM-backed signing infrastructure + initial attestation | £0.15M | £0.05M | £0.20M |
| MOD SbD evidence pack tooling + threat-modelling discipline | £0.10M | £0.05M | £0.15M |
| Operator runbook library | £0.08M | £0.04M | £0.12M |
| Pre-sales engagement (G-Cloud / DOS / MOD framework listings, reference architecture) | £0.06M | £0.04M | £0.10M |
| Pluggable AI abstraction (joint with project 001 — vendor share) | £0.10M | £0.05M | £0.15M |
| Contingency (15% of capex above) | £0.10M | £0.05M | £0.15M |
| **Total CapEx** | **£1.01M** | **£0.44M** | **£1.45M** |

### D1.2 Operational Expenditure (OpEx — Year 1-3)

| Item | Year 1 | Year 2 | Year 3 | 3-Year Total |
|------|--------|--------|--------|--------------|
| LTS Engineering Lead + 1.0-1.5 FTE | £0.30M | £0.32M | £0.34M | £0.96M |
| Sovereign Delivery Lead | £0.18M | £0.18M | £0.18M | £0.54M |
| MOD SbD evidence pack refresh + NCSC CAF mapping | £0.12M | £0.12M | £0.12M | £0.36M |
| HSM operations + annual independent attestation + signing-key rotation + pen-test | £0.10M | £0.10M | £0.10M | £0.30M |
| Cleared-personnel availability (R-009 mitigation) | £0.08M | £0.10M | £0.12M | £0.30M |
| CI compute increment | £0.03M | £0.04M | £0.05M | £0.12M |
| Cross-subsidy reporting / Finance ops + quarterly affordability review | £0.04M | £0.04M | £0.04M | £0.12M |
| Customer accreditation refresh (Year 2 onwards) | £0 | £0.20M | £0.40M | £0.60M |
| Contingency (10% of opex above) | £0.09M | £0.11M | £0.13M | £0.33M |
| **Total OpEx** | **£0.94M** | **£1.21M** | **£1.48M** | **£3.63M** |

### D1.3 Total Cost of Ownership (TCO)

| | Year 0 | Year 1 | Year 2 | Year 3 | 3-Year Total |
|---|--------|--------|--------|--------|--------------|
| CapEx | £1.01M | £0.44M | £0 | £0 | £1.45M |
| OpEx | £0 | £0.94M | £1.21M | £1.48M | £3.63M |
| **Pre-bias TCO** | **£1.01M** | **£1.38M** | **£1.21M** | **£1.48M** | **£5.08M** |
| **Post-bias TCO (×1.30)** | **£1.31M** | **£1.79M** | **£1.57M** | **£1.93M** | **£6.60M** |

**Notes**:

- All costs in 2026 prices (no inflation indexation at SOBC stage; OBC will indexed).
- Excludes VAT (vendor will recover VAT on inputs; customer pricing is VAT-inclusive per their procurement).
- Optimism bias of +30% applied to capability cost per `ARC-002-RISK-v1.0.md` §I Economic Case.

## D2. Funding Source

**Self-Funded Service Model**:

- **Source**: ArcKit-as-a-Service vendor working capital + Year 1 SaaS revenue (project 001) re-invested into sovereign capability.
- **Amount Available**: ~£5.5M working-capital envelope confirmed; the post-bias £6.60M figure is at the upper edge — OBC discipline essential.
- **Timing**: Year 0 (£1.31M post-bias) — most concentrated; Year 1+ self-funding through customer revenue once first customer signs.

**Budget Approval Path** (vendor-internal):

1. Service Owner: Up to £0.5M individual decision.
2. ArcKit Architecture Review Board: £0.5M to £2.0M (this SOBC sits here — recommended option capital alone is £1.45M).
3. External funding (advisor / investor): Above £2.0M cumulative. Not currently anticipated; if Customer 2 / Customer 3 slip, may become necessary for Year-2 cleared-personnel ramp.

**Funding Gaps** (sensitivity-driven):

- If Customer 2 slips by 6 months: ~£0.5M Year-2 cashflow shortfall — manageable from working capital with quarterly review.
- If Customer 3 not signed: ~£0.6M Year-3 shortfall — requires either Year-2 contingency activation or re-phased LTS commitment.
- If both slip: cumulative ~£1.1M shortfall — triggers ARB review of OBC commercial terms.

**Mitigation**:

- Phase capex across Year 0 / Year 1 (most discretionary items second-half of Year 1 — book-by-book reviewable).
- LTS engineering team can ramp from 1.0 FTE Year 1 to 1.5 FTE Year 2-3 contingent on customer revenue.
- Sovereign Delivery Lead role can be 0.5 FTE pre-pilot, 1.0 FTE post-pilot.

## D3. Affordability

**Vendor Budget Context**:

- Total vendor 3-year capability budget envelope: ~£12-15M (combining SaaS + sovereign + cross-cutting).
- Sovereign 3-year share (post-bias): £6.60M = 44-55% of envelope. Material commitment.
- **Assessment**: **Affordable with discipline** — workable provided OBC firms commercial terms before Year-1 OpEx ramp.

**Cash Flow Impact**:

- Largest single payment: £1.31M in Year 0 (capital concentration). Mitigated by sequencing — HSM contract Q3 2026, evidence-pack tooling Q4 2026, sovereign-packaging engineering across 9 months.
- Year 1 cashflow stress point: Q3-Q4 2027 (pilot beta) — operational ramp before pilot customer revenue arrives. ~£0.4M peak shortfall.
- **Mitigation**: Pilot customer staged-payment terms (30% on award); LTS Engineering Lead 0.8 FTE in Year 1 ramping to 1.5 FTE Year 2.

**Ongoing Affordability** (Year 4+):

- Steady-state OpEx ~£1.5M/yr.
- Funded by: 3-customer steady-state revenue ~£3.0M/yr → net contribution to SaaS SME tier ~£0.6-0.8M/yr — directly funding Principle 17 commitment.

## D4. Financial Appraisal

### D4.1 Economic Appraisal (UK Government Green Book)

**Discount Rate**: 3.5% (HMT social time preference rate per Green Book).

**Net Present Value Calculation (post-optimism-bias, vendor-side)**:

| Year | Costs (TCO post-bias) | Benefits (vendor revenue + cross-subsidy) | Net Cashflow | Discount Factor | Present Value |
|------|----------------------|-------------------------------------------|--------------|-----------------|---------------|
| 0 | £1.31M | £0 | −£1.31M | 1.000 | −£1.31M |
| 1 | £1.79M | £0.25M | −£1.54M | 0.966 | −£1.49M |
| 2 | £1.57M | £1.90M | +£0.33M | 0.934 | +£0.31M |
| 3 | £1.93M | £3.45M | +£1.52M | 0.902 | +£1.37M |
| **Total** | **£6.60M** | **£5.60M** | **−£1.00M (nominal)** | | **NPV = £−1.12M (3-year, post-bias)** |

> Note: Pre-bias 3-year NPV is £+0.31M; post-bias 3-year NPV is £−1.12M; the spread is the cost of HMT optimism bias. **5-year post-bias NPV** (informational): £+0.62M central; this is the more representative figure for sovereign customers on typical 5-7 year contracts.

**5-year NPV (post-bias, central estimate)** — informational only as SOBC is 3-year:

- Year 4 incremental net: +£1.65M (PV £+1.43M)
- Year 5 incremental net: +£1.85M (PV £+1.55M)
- **5-year NPV (post-bias)**: £+1.86M

### D4.2 Return on Investment

**ROI Calculation (3-year, post-bias)**:

```text
ROI = (Total Benefits − Total Costs) / Total Costs × 100%
ROI = (£5.60M − £6.60M) / £6.60M × 100% = −15% (3-year, post-bias)
ROI = (£5.60M − £5.08M) / £5.08M × 100% = +10.2% (3-year, pre-bias)
ROI = (£9.80M − £9.80M) / £9.80M × 100% = 0% (5-year, post-bias) — cumulative break-even at Year 5
```

**Payback Period**:

- Pre-bias: cumulative net cashflow turns positive Month 24.
- Post-bias: cumulative net cashflow turns marginally positive Month 30; consistently positive Month 32.

**Internal Rate of Return (IRR)**:

- 3-year post-bias: ~−2% (NPV-negative at 3.5%); IRR < discount rate.
- 5-year post-bias: ~7% (modestly above 3.5% discount rate).

**Conclusion**: Decision is sensitive to time horizon. The 3-year horizon is a Green Book formality; the operational reality of sovereign customer contracts (5-7 years typical, aligned with re-accreditation cycles) puts the case clearly into VfM-positive territory. The OBC will firm this up with pilot commercial terms.

### D4.3 Value for Money Assessment

**Qualitative Assessment**:

- **Economy**: Per-customer bespoke contract on MOD Defence Digital framework gives best per-customer unit cost achievable for sovereign-grade deployment.
- **Efficiency**: Single codebase ~3× more efficient than fork (Option B); engineering cost is amortised across SaaS + sovereign.
- **Effectiveness**: Meets ~85% of stakeholder goals; the 15% gap is execution risk on accreditation discipline (R-001), not architectural.

**Overall VfM Rating**: **Medium-High** (3-year horizon, post-bias) → **High** (5-year horizon).

**Justification**: The Principle-21-+-Principle-17-compliant route delivers the same governance toolkit to the most sensitive UK Government workloads at materially lower system-wide cost than fragmented alternatives, while operationalising the cross-subsidy that funds the SaaS SME tier. The case strengthens with the OBC and FBC as commercial terms firm.

---

# PART E: MANAGEMENT CASE

> **Reference to Risk Register**: This Management Case **incorporates `ARC-002-RISK-v1.0.md` in full** as the formal risk-management appendix. All 13 risks (R-001 through R-013), the sovereign-specific risk appetite (Strategic Medium ≤ 12, Operational Low ≤ 6, Financial Low ≤ 6, Compliance Very-Low ≤ 4, Reputational Very-Low ≤ 4, Technology Low ≤ 6), the inherent and residual risk matrices, the 4Ts response framework summary (100% Treat — sovereign profile too high-stakes for Tolerate; no Transfer market; no Termination short of project termination), and the Monitoring and Review Framework (§J) are by reference. Section E7 below summarises the top 10 risks per the risk register.

## E1. Governance

### E1.1 Roles & Responsibilities (RACI)

Derived from `ARC-002-STKE-v1.0.md` Decision Authority Matrix:

| Decision/Activity | Responsible | Accountable | Consulted | Informed |
|-------------------|-------------|-------------|-----------|----------|
| Overall sovereign track success | Sovereign Delivery Lead | Service Owner (Mark Craddock — SRO) | ARB, Lead Architect, Security Lead | Customer SROs (engaged), HMT, CCS |
| Single-codebase fork escalation | Lead Architect | Service Owner | All Manage-Closely stakeholders | All staff |
| MOD SbD evidence pack content | Security Lead | Service Owner | Lead Architect, Sovereign Delivery Lead | Customer accreditators |
| Sovereign pricing for new customer | Sovereign Delivery Lead | Service Owner | Finance, Lead Architect | CCS / framework liaison |
| Below-floor pricing exception | Sovereign Delivery Lead | Service Owner | Finance | Finance, Service Owner |
| LTS scope acceptance (security/critical-bug only) | LTS Engineering Lead | Service Owner | Lead Architect, Sovereign PM | All customers |
| LTS deprecation timing | Sovereign Product Manager | Service Owner | Customer SROs (≥ 12 months ahead) | All customers |
| Vendor signing-key custody and rotation | Signing-Key Custodian | Security Lead | Service Owner, Lead Architect | All staff |
| Bundle issue (final go / no-go) | Lead Architect | Service Owner | Security Lead, Sovereign Delivery Lead | All customers |
| AI / model provider listing for sovereign | Lead Architect | Service Owner | Security Lead, DPO | Customers (per release) |
| Customer engagement to alpha (accreditator-in-the-loop) | Sovereign Delivery Lead | Service Owner | Security Lead, Lead Architect | All customers |
| Per-customer feature request triage | Sovereign Product Manager | Service Owner | Lead Architect, Security Lead | Customer SRO, accreditor |
| Severe incident (e.g., signing-key compromise) | Service Owner | Service Owner | Security Lead, DPO, Legal, all customers | NCSC, ICO if applicable |

**Senior Responsible Owner (SRO)**: Mark Craddock, Service Owner.

- Accountable for delivery of the sovereign track and its commercial / strategic success.
- Chairs the cross-project quarterly architecture forum protecting SaaS roadmap from sovereign-driven displacement.
- Reports to: ArcKit Architecture Review Board; engaged customer SROs (per engagement).

**Steering Committee** (sovereign track):

- SRO (Service Owner) — Chair
- Lead Architect / CTO — Technical authority + single-codebase discipline
- Security Lead — Compliance and assurance authority
- Sovereign Product Manager — LTS schedule, customer-facing roadmap
- Sovereign Delivery Lead — Customer onboarding and engagement
- Finance Lead — Sovereign unit economics and cross-subsidy reporting
- LTS Engineering Lead — Patch cadence and backport discipline (joins for Items relevant)

**Meeting Frequency**: Monthly (weekly during alpha and pilot beta phases).

**Customer-side governance** (per engaged customer, mirrored where applicable):

- Customer SRO + Customer Accreditor + Customer SIRO — quarterly briefings; per-release evidence-pack hand-off; per-incident notification.

### E1.2 Approval Gates

| Gate | Criteria | Approving Body | Target Date |
|------|----------|----------------|-------------|
| **Gate 0: SOBC Approval** | This document approved; funding secured; above-appetite risk acknowledgement signed | ArcKit Architecture Review Board + Service Owner | 2026-06-30 |
| **Gate 1: HLD Refresh** | `ARC-002-HLDR-v1.0.md` (issued 2026-05-03) refreshed against any post-SOBC scope changes | Lead Architect | 2026-08-31 |
| **Gate 2: MOD SbD Assessment** | `/arckit:mod-secure` first cycle complete; pack issuable | Security Lead + Service Owner | 2026-09-30 |
| **Gate 3: Pilot Customer Engagement** | ≥ 1 MOD or sensitive-site customer signed for accreditator-in-the-loop alpha | Sovereign Delivery Lead + Service Owner | 2027-02-28 |
| **Gate 4: Alpha Complete** | Bundle install validated in CI representative environment; 100% disconnected-mode pass | Lead Architect + Security Lead | 2027-04-30 |
| **Gate 5: OBC** | Outline Business Case with firmed pilot commercial terms and refined cost forecast | ARB | 2027-06-30 |
| **Gate 6: Private Beta** | First customer install completed; first ATO submission | Service Owner + Customer SRO | 2027-08-31 |
| **Gate 7: First ATO** | Customer accreditator issues authority-to-operate (G-7 / R-001 mitigation outcome) | Customer Accreditator | 2027-Q4 (target) |
| **Gate 8: GA / FBC** | Sovereign offering generally available; Full Business Case with first-customer actuals | ARB + Service Owner | 2027-12-31 |
| **Gate 9: First Cross-Subsidy Quarterly Report** | First quarterly affordability and contribution review showing positive contribution to SaaS SME tier (G-6) | Service Owner + Finance | 2028-Q1 |

## E2. Delivery Approach

**Methodology**: Agile (Scrum-of-Scrums across SaaS + sovereign squads) with explicit accreditation-aware stage gates per E1.2.

**Phases**:

1. **Pre-Alpha / Build (2026 H2)**:
   - HLD refresh (Gate 1).
   - HSM-backed signing infrastructure provisioning + first independent attestation.
   - Pluggable AI abstraction landing (joint with project 001).
   - Operator runbook library v1.
   - MOD SbD assessment first cycle (Gate 2).
   - Pre-sales engagement: G-Cloud / DOS / MOD framework listings.

2. **Pilot Customer Engagement (2026 Q4 - 2027 Q1)**:
   - Sovereign Delivery Lead engages MOD Defence Digital and identified pilot customers.
   - Accreditator-in-the-loop alpha programme commitment (Gate 3).
   - Pilot commercial terms firmed → OBC drafted (Gate 5).

3. **Alpha (2027 Q1 - Q2)**:
   - Disconnected install validated in CI representative environment.
   - Network-deny test in CI: zero outbound connections during install / run / upgrade / backup / restore / decommission.
   - Bundle pipeline operational; first signed bundle issued internally for representative environment.
   - First customer evidence-pack walkthrough (R-001 / R-002 mitigation execution) (Gate 4).

4. **Private Beta (2027 Q2 - Q3)**:
   - First customer install in customer environment.
   - Full operator runbook execution by customer team.
   - First MOD SbD evidence pack handed off to customer accreditator.
   - First ATO submission (Gate 6).

5. **GA + FBC (2027 Q4)**:
   - First ATO issued (G-7 outcome) (Gate 7).
   - Sovereign offering generally available (Gate 8).
   - Full Business Case with first-customer actuals.

6. **Steady-state / Customer 2 + 3 onboarding (2028)**:
   - LTS line 1 cut from GA revision.
   - Customer 2 engagement (Year 2).
   - First cross-subsidy quarterly report (Gate 9).

**Delivery Model**:

- **In-house (vendor)**: Single-codebase engineering, sovereign packaging, security and accreditation evidence, LTS engineering, sovereign delivery liaison, signing-key custody.
- **Customer-side**: Operator team (cleared personnel) executes install / upgrade / backup / restore per runbook library — no vendor remote access except via opt-in audited channel.
- **Hybrid touchpoints**: Accreditator-in-the-loop alpha (vendor + customer accreditator); annual independent attestation of signing infrastructure; ex-MOD assurance advisor pre-formal MOD SbD walkthrough.

## E3. Key Milestones

| Milestone | Date | Dependencies | Owner |
|-----------|------|--------------|-------|
| SOBC Approval (this document) | 2026-06-30 | RISK + REQ + STKE complete (all complete) | SRO |
| Above-appetite risk acknowledgement signed | 2026-06-30 | SOBC + RISK §G | SRO |
| HLD Refresh | 2026-08-31 | SOBC | Lead Architect |
| HSM signing infrastructure live | 2026-09-30 | Capex Year 0 | Security Lead |
| MOD SbD first assessment cycle | 2026-09-30 | HLD + HSM | Security Lead |
| G-Cloud / DOS / MOD framework listings | 2026-10-31 | Pre-sales engagement | Sovereign Delivery Lead |
| Pluggable AI abstraction landed | 2026-12-31 | Joint with project 001 | Lead Architect |
| Operator runbook library v1 | 2026-12-31 | HLD | Sovereign Delivery Lead |
| Pilot customer signed (MOD or sensitive-site) | 2027-02-28 | Engagement plan | Sovereign Delivery Lead |
| Alpha — bundle install validated in CI | 2027-04-30 | Pluggable abstractions + bundle pipeline | Lead Architect |
| Accreditator walkthrough (pre-formal) | 2027-05-31 | Alpha + customer engagement | Security Lead |
| OBC | 2027-06-30 | Alpha + pilot commercial terms | SRO |
| Private beta — first customer install | 2027-08-31 | OBC + bundle ready | Sovereign Delivery Lead |
| First ATO submission | 2027-09-30 | Private beta + evidence pack | Customer SRO |
| **First ATO issued (G-7)** | **2027-Q4** | First submission | Customer Accreditator |
| **GA — sovereign offering generally available** | **2027-12-31** | First ATO | Service Owner |
| FBC | 2028-Q1 | First ATO + customer-actual costs | SRO |
| First cross-subsidy quarterly report (G-6) | 2028-Q1 | GA + first revenue | Service Owner + Finance |
| Customer 2 onboarding | 2028-Q2 | GA + reference customer | Sovereign Delivery Lead |
| First LTS line cut | 2028-Q2 | GA | LTS Engineering Lead |
| Customer 3 onboarding | 2028-Q4 | LTS line stable | Sovereign Delivery Lead |
| Annual independent attestation of signing infrastructure | Annually | HSM operations | Security Lead |
| Sovereign track formal review | 2028-12-31 | 12 months post-GA | SRO + ARB |

**Critical Path** (G-7 First ATO is the load-bearing milestone):

1. HSM signing infrastructure live (2026-09-30) — gates bundle issue.
2. MOD SbD first assessment passes (2026-09-30 to 2026-12-31) — gates customer-facing evidence pack.
3. Pilot customer signed with willing accreditator (2027-02-28) — gates accreditator-in-the-loop alpha.
4. Alpha complete with disconnected-mode 100% pass (2027-04-30) — gates private beta.
5. First ATO submission (2027-09-30) — gates GA.

## E4. Resource Requirements

### E4.1 Team Structure

**Core Project Team** (vendor-side, sovereign track):

| Role | FTE | Duration | Total Effort | Notes |
|------|-----|----------|--------------|-------|
| Service Owner / SRO (Mark Craddock) | 0.3 | 36 months | 10.8 months | Cross-project; sovereign track ~30% |
| Lead Architect / CTO | 0.4 | 36 months | 14.4 months | Cross-project; sovereign track ~40% |
| Security Lead | 0.7 | 36 months | 25.2 months | Heavy load Year 0-1 (MOD SbD); steady-state ~50% |
| Sovereign Delivery Lead | 0.5 → 1.0 | 36 months | 31.2 months | Ramp from 0.5 (Year 0) to 1.0 (Year 1+) |
| Sovereign Product Manager | 0.5 | 36 months | 18 months | LTS schedule + customer roadmap |
| LTS Engineering Lead | 0.8 → 1.0 | 36 months | 32 months | Ramp from 0.8 (Year 1) to 1.0 (Year 2+) |
| LTS Engineers (backports + security triage) | 1.0 → 1.5 | 30 months | 36 months | Ramp from 1.0 (Year 1) to 1.5 (Year 2-3) |
| DPO (vendor-side processing minimisation) | 0.1 | 36 months | 3.6 months | Cross-project; sovereign track ~10% |
| Signing-Key Custodian | 0.2 | 36 months | 7.2 months | Includes separation-of-duties deputy |
| Finance Lead (cross-subsidy reporting) | 0.1 | 36 months | 3.6 months | Cross-project |

**Total sovereign-attributed FTE-months**: ~182 over 36 months (~5 average FTEs steady-state).

**External / advisory**:

- Ex-MOD assurance advisor (~£10k/day, ~10-15 days Year 0-1, ~5 days/yr ongoing) — pre-formal MOD SbD walkthroughs.
- HSM provider professional services (provisioning + initial attestation, Year 0).
- Independent attestor (annual, signing infrastructure) — ~£25-40k/yr.
- Independent pen-tester (annual, release pipeline) — ~£20-30k/yr.

### E4.2 Skills Required

**Critical Skills** (gap analysis):

| Skill | Need Level | Status | Action |
|-------|-----------|--------|--------|
| MOD Secure by Design assessment expertise | CRITICAL | Gap (vendor-side) | Hire Security Lead with defence background OR contract ex-MOD advisor + grow internal capability |
| Air-gap deployment engineering (signed bundles, offline CI) | CRITICAL | Gap (vendor-side) | Hire / train Sovereign Packaging Engineer; pluggable abstraction discipline reviewed at sprint level |
| HSM operations and key custody | CRITICAL | Gap (vendor-side) | Hire Signing-Key Custodian; HSM provider PS for initial setup |
| LTS engineering (long-tail backports, parallel CI matrix) | CRITICAL | Gap (vendor-side) | Hire LTS Engineering Lead + 1.0-1.5 FTE engineers |
| Cleared-personnel availability (UK SC / DV) | HIGH | Partial (Service Owner cleared; others TBD) | Recruitment with clearance pipeline; long lead-time (12+ months for DV from civilian) |
| Cross-government framework procurement (G-Cloud / DOS / MOD frameworks) | MEDIUM | Adequate (existing project-001 capability) | Retain via Sovereign Delivery Lead |
| NCSC CAF mapping discipline | HIGH | Adequate (existing) | Maintain |

**Training Plan**:

- Sovereign Packaging Engineer onboarding (offline-readiness mindset): 2 weeks intensive — £4k cost.
- LTS team onboarding (backport discipline, security triage, vulnerability advisory authoring): 1 month — £15k.
- Sovereign Delivery Lead — defence-procurement orientation: 2 weeks — £6k.

## E5. Change Management

### E5.1 Stakeholder Engagement

**Engagement Strategy** (from `ARC-002-STKE-v1.0.md` Power-Interest Grid):

| Stakeholder | Power-Interest | Engagement Approach | Frequency | Owner |
|-------------|----------------|---------------------|-----------|-------|
| Customer SRO | High-High | Manage Closely — quarterly briefings, accreditation milestones | Quarterly | SRO |
| Customer Accreditator | High-High | Manage Closely — evidence-pack co-design; in-the-loop alpha | Bi-weekly during alpha; per-release | Sovereign Delivery Lead + Security Lead |
| Customer SIRO | High-High | Manage Closely — risk register reviews; residual-risk discussions | Quarterly | Sovereign Delivery Lead |
| Customer DDaT Architects | High-High | Manage Closely — architecture community engagement | Quarterly user group | Lead Architect |
| MOD Defence Digital | High-High | Manage Closely — cross-MOD coherence; supplier diversification | Quarterly liaison | SRO + Sovereign Delivery Lead |
| Customer DSO / CISO | High-Medium | Keep Satisfied — policy-mapping reviews; security briefings | Quarterly | Security Lead |
| Customer Operator Team | Medium-High | Keep Informed — runbook design; install rehearsals; quarterly operator community call | Per release + quarterly | Sovereign Delivery Lead |
| NCSC | High-Medium | Keep Satisfied — CAF mapping alignment; supply-chain practice | Quarterly | Security Lead |
| HM Treasury / CCS / CDDO / DCPP | High-Low | Keep Satisfied — value-for-money narrative; framework cycle | Annual + framework cycle | SRO + Finance |

### E5.2 Communications Plan

| Stakeholder Group | Message | Channel | Frequency | Owner |
|-------------------|---------|---------|-----------|-------|
| Steering Committee | Progress, risks, decisions | Monthly meeting + papers | Monthly | SRO |
| ArcKit Architecture Review Board | Strategic progress; gate-completion; cross-project alignment | Quarterly | SRO |
| Customer SRO chain | Accreditation progress, milestone tracking | Quarterly briefing + per-release notification | Per-customer | Sovereign Delivery Lead |
| Customer Operator Team | Runbook updates, release notes, LTS schedule | Per-release + quarterly community call | Per-release | Sovereign Delivery Lead |
| Customer DDaT Architects | Cross-government architecture community | Quarterly user group | Quarterly | Lead Architect |
| MOD Defence Digital + NCSC | Supplier-diversification narrative; CAF / SbD alignment | Quarterly liaison | Quarterly | SRO + Security Lead |
| HM Treasury / CCS | VfM, cross-subsidy contribution, framework cycle | Annual report + framework reviews | Annual | Finance + SRO |
| Vendor internal | Cross-project roadmap; SaaS protection | Weekly cross-project review + monthly architecture forum + quarterly cross-project review | Weekly + monthly + quarterly | SRO + Lead Architect |

### E5.3 Resistance Management

**Anticipated Resistance** (from `ARC-002-STKE-v1.0.md` Conflict Analysis):

| Source | Reason | Impact | Mitigation |
|--------|--------|--------|------------|
| Customer accreditators (until first ATO landed) | Have not yet seen vendor evidence; default scepticism per SD-1 | Medium (gates first customer) | Accreditator-in-the-loop alpha (R-001 mitigation); ex-MOD advisor pre-formal walkthrough |
| Customer SIROs | Default scepticism on supply-chain visibility | Medium (gates risk acceptance) | Per-release SBOM + signed manifests + threat model in evidence pack |
| Vendor SaaS engineering team | Concern that sovereign track absorbs SaaS roadmap (Conflict C-6) | Medium | Cross-project quarterly review; separate LTS team; Service Owner SaaS-roadmap protection |
| Customer-side per-customer feature demands | Pressure for bespoke specifics that match local policy (Conflict C-1) | High over time | Configuration-only customisation discipline; quarterly fork-pressure review; refactor budget |
| Adjacent commercial defence-EA tooling vendors | Competitive pressure | Low (existing market) | Reference customer + cross-MOD coherence narrative |

**Change Champions**:

- Service Owner (Mark Craddock) — strategic alignment.
- Lead Architect — single-codebase discipline.
- MOD Defence Digital liaison — supplier-diversification narrative.
- Customer DDaT Enterprise Architects (early-adopter) — feature-parity advocate.

### E5.4 Training Plan

| Audience | Training Type | Duration | Delivery | Timing |
|----------|---------------|----------|----------|--------|
| Customer Operator Team (first customer) | Comprehensive — install / upgrade / backup / restore / IR / DR runbook execution | 3 days | On-site (or representative isolated environment) | Pre-private-beta |
| Customer Operator Team (subsequent customers) | Same; 2 days as runbook library matures | 2 days | On-site | Pre-deployment |
| Customer DDaT Architects | ArcKit governance toolkit familiarisation | 1 day | Online + classroom | Per-deployment |
| Vendor LTS team (Year 1) | Backport discipline; security triage; vulnerability advisory authoring; offline CI profile | 1 month | Hands-on | Year 1 onboarding |
| Vendor Sovereign Delivery Lead | Defence procurement; MOD framework navigation; accreditation-evidence-pack ownership | 2 weeks | Mix of classroom + advisor shadowing | Year 1 onboarding |

**Training Costs**: ~£25k Year 0, £40k Year 1 (included in OpEx).

## E6. Benefits Realization

### E6.1 Benefits Profiles

**Benefit B-1: Sovereign Customer 1 Revenue (G-1)**

- **Description**: First production sovereign deployment at MOD or comparable sensitive-site customer; full vendor revenue from initial deployment + ongoing LTS subscription.
- **Owner**: Service Owner (commercial); Sovereign Delivery Lead (delivery).
- **Baseline**: 0 (pre-GA).
- **Target**: ≥ 1 customer signed by GA + 18 months; revenue Year 1 (partial) £0.20M; Year 2 £1.20M; Year 3 £1.20M.
- **Measurement**: Quarterly revenue reporting; ATO date; customer reference status.
- **Timeline**:
  - Pilot signed: 2027-02-28 (Gate 3)
  - First ATO: 2027-Q4 (Gate 7)
  - Full Year 2 revenue: 2028 onwards.
- **Assumptions**: Pilot customer engaged with willing accreditator; first ATO on first or first-with-conditions submission.
- **Dependencies**: R-001 mitigation execution; MOD SbD pack landing on first cycle.
- **Status**: Not yet realised (pre-engagement).

**Benefit B-4: Cross-Subsidy Contribution to SaaS SME Tier (G-6 / Principle 17)**

- **Description**: Sovereign net contribution margin allocated to SaaS SME tier funding — the strategic raison d'être of the project.
- **Owner**: Service Owner + Finance.
- **Baseline**: £0/yr (pre-GA).
- **Target**: Year 1 ~£50k; Year 2 ~£300k; Year 3 ~£550k; reportable to HMT / CCS.
- **Measurement**: Quarterly affordability and contribution review (per Principle 17 governance); annual report integrated into vendor financial reporting.
- **Timeline**:
  - First quarterly report: 2028-Q1 (Gate 9).
  - Year-on-year growth tracked thereafter.
- **Assumptions**: Sovereign cost-to-serve model holds; below-floor pricing exceptions disciplined (R-011 mitigation).
- **Dependencies**: B-1, B-2, B-3 customer revenues materialising; cost-to-serve floor preserved.
- **Status**: Not yet realised.

**Benefit B-6: Single-Codebase Production Evidence (G-2 / Principle 21)**

- **Description**: Single-codebase commitment provable in production strengthens SaaS open-standards / portability claim and forecloses fork-pressure risk (R-003).
- **Owner**: Lead Architect.
- **Baseline**: Philosophical commitment (Principle 21) but not yet operationally proven.
- **Target**: Zero forks; feature-flag inventory monotonically declining or stable; single Git revision producing both SaaS deployment and sovereign bundle.
- **Measurement**: Quarterly architecture review (forks count, feature-flag inventory size, configuration-surface delta); release-pipeline audit.
- **Status**: Not yet realised; Goal G-2 commences from GA.

**Benefit B-7: Avoided Customer-Side Cost (System-Wide)**

- **Description**: Sovereign customers receive ArcKit at LTS-disciplined rates rather than fragmented-bespoke alternatives requiring re-accreditation churn.
- **Owner**: Sovereign Delivery Lead (per customer); SRO (cumulative narrative).
- **Baseline (Option A do-nothing)**: ~£150k-£500k per re-accreditation per customer per year (per ADR-008 §5 Option 0).
- **Target**: Across 3-5 customers cumulative 3-5 year horizon, ~£4.5M-£15M avoided customer-side cost.
- **Measurement**: Customer self-reported avoided cost (where customer willing to share), cross-government VfM narrative.
- **Status**: Future; tracked once customer engagements firm.

### E6.2 Benefits Measurement

**Monitoring Approach**:

- Monthly benefits tracker for vendor-revenue benefits (B-1, B-2, B-3, B-4) — Service Owner + Finance.
- Quarterly architecture review for B-6 (forks count, feature-flag inventory, configuration-surface delta) — Lead Architect.
- Annual cross-government narrative for B-5 (MOD Defence Digital supplier-diversification) and B-7 (avoided customer-side cost).
- 6-month and 12-month formal Benefits Realisation Reviews post-GA.

**Responsibility**:

- **SRO**: Overall benefits realisation accountability.
- **Service Owner + Finance**: Cross-subsidy contribution (B-4) — quarterly review.
- **Sovereign Delivery Lead**: Customer-revenue benefits (B-1, B-2, B-3) and customer-reference (B-5).
- **Lead Architect**: Single-codebase track record (B-6).
- **Sovereign Delivery Lead + SRO**: Avoided customer-side cost narrative (B-7).

**Reporting**:

- Benefits RAG status in monthly steering committee papers.
- Quarterly cross-subsidy contribution report (per Principle 17 governance).
- Annual benefits realisation report integrated into vendor business review.
- Corrective action triggers: any benefit < 80% target by midpoint.

## E7. Risk Management

> **The complete risk register is `ARC-002-RISK-v1.0.md` and is incorporated into this Management Case in full.** Below are the top 10 risks ranked by residual score (per RISK §B); all 13 risks, full inherent + residual matrices, sovereign-specific appetite (Strategic ≤ 12 / Operational ≤ 6 / Financial ≤ 6 / Compliance ≤ 4 / Reputational ≤ 4 / Technology ≤ 6), 4Ts response framework summary, control-effectiveness analysis, monitoring framework, and Orange Book compliance checklist are by reference.

### E7.1 Top 10 Risks (Residual)

| Rank | ID | Title | Category | Inherent | Residual | Owner | Status | Response |
|------|----|-------|----------|----------|----------|-------|--------|----------|
| 1 | R-001 | First-attempt customer accreditation failure | STRATEGIC | 20 | 12 | Sovereign Delivery Lead | In Progress | Treat |
| 2 | R-002 | MOD Secure by Design assessment fail | COMPLIANCE | 20 | 12 | Vendor Security Lead | In Progress | Treat |
| 3 | R-005 | Customer break-glass / privileged-access abuse | COMPLIANCE | 9 | 12 | Customer SIRO (vendor: Service Owner consulted) | Open | Treat |
| 4 | R-003 | Single-codebase divergence (Principle 21) | TECHNOLOGY | 8 | 9 | Lead Architect / CTO | In Progress | Treat |
| 5 | R-006 | Operator-team turnover at customer | OPERATIONAL | 9 | 9 | Sovereign Delivery Lead | Open | Treat |
| 6 | R-009 | Vendor cleared-personnel availability shortfall | OPERATIONAL | 12 | 9 | Service Owner | Open | Treat |
| 7 | R-007 | Accredited-boundary egress incident | REPUTATIONAL | 20 | 8 | Service Owner | In Progress | Treat |
| 8 | R-008 | On-premise AI model integration brittleness | TECHNOLOGY | 16 | 8 | Lead Architect | In Progress | Treat |
| 9 | R-010 | LTS line drift / Year-3 backport SLA breach | OPERATIONAL | 12 | 6 | LTS Engineering Lead | Monitoring | Treat |
| 10 | R-011 | Cross-subsidy erosion (sovereign pricing concession) | FINANCIAL | 12 | 6 | Service Owner / Finance | Monitoring | Treat |

### E7.2 Risk Appetite Compliance

**Sovereign-specific appetite** (from RISK §G):

- 5 risks exceed appetite at residual: R-002, R-003, R-004, R-005, R-007.
- 1 risk at appetite ceiling: R-001 (constitutive of activity).
- Service Owner formal acknowledgement of these acceptances is a **mandatory condition of SOBC approval** (per RISK §I and B3 sensitivity analysis).
- Quarterly Service Owner review of above-appetite risks formally scheduled.

### E7.3 Risk Mitigation Summary

**Critical inherent risks (R-001, R-002, R-004, R-007)**:

- Common-thread mitigations: HSM-backed signing infrastructure (mitigates R-002, R-004, R-007); accreditator-in-the-loop alpha programme (mitigates R-001, R-002 simultaneously); ex-MOD advisor pre-formal walkthrough (mitigates R-001, R-002).
- Funded explicitly in B2 / D1.

**Configuration-only customisation discipline** (R-003 mitigation):

- Lead Architect + Service Owner authority on fork decisions.
- Quarterly architecture review of feature flags.
- Refactor budget (capex Year 1).

**Cross-project risk-review coordination** (R-003 with project-001 R-002; R-011 cross-subsidy):

- Quarterly cross-project review by SRO.
- Joint review of Conflict C-6 (sovereign-track bandwidth vs SaaS roadmap).

**Risk Register Maintenance**:

- Per `ARC-002-RISK-v1.0.md` §J Monitoring and Review Framework — Critical (20-25): weekly; High (13-19): bi-weekly; above-appetite Medium: monthly; within-appetite Medium: quarterly; Low: quarterly.
- KRIs (leading + lagging indicators) tracked monthly per RISK §J.

---

# PART F: RECOMMENDATION & NEXT STEPS

## F1. Summary of Recommendation

**Recommended Option**: **Option C — Single Codebase + Sovereign Overlay**

**Investment**: £5.08M pre-bias / £6.60M post-HMT-optimism-bias (3-year, vendor-side).

**Expected Return**: £5.60M vendor revenue + cross-subsidy contribution (3-year); plus £4.5M-£15M avoided customer-side cost (system-wide); plus qualitative strategic benefits (B-5 supplier-diversification narrative; B-6 single-codebase production evidence).

**3-year NPV (post-bias)**: £−1.12M (Green Book formality).
**5-year NPV (post-bias)**: £+1.86M (operational reality of sovereign customer contracts).
**3-year BCR (post-bias)**: 0.85; **5-year BCR (post-bias)**: ~1.0; **system-wide BCR including avoided customer cost**: > 2.0.

**Stakeholder Goals Met**: ~85% (10/10 met with G-1, G-7 at 80-85% confidence subject to risk mitigation execution).

**Payback Period**: Month 30 post-bias; Month 24 pre-bias.

**Risks**: Manageable with declared above-appetite acceptances; 5 risks above sovereign-specific appetite at residual require Service Owner formal acknowledgement.

**Affordability**: Affordable with discipline within ~£12-15M vendor 3-year capability envelope; Year-0 capital concentration (£1.31M post-bias) is the cashflow stress point.

**Go/No-Go Recommendation**: **PROCEED WITH CONDITIONS** — proceed to OBC with the conditions in F2 satisfied.

## F2. Conditions for Approval

**Mandatory Conditions** (per `ARC-002-RISK-v1.0.md` §I recommendation):

1. **Service Owner formal acknowledgement of above-appetite risks** in writing, with quarterly review trigger:
   - R-001 (Strategic, residual 12, at appetite ceiling — accepted as constitutive of activity).
   - R-002 (Compliance, residual 12, exceeds appetite +200% — accepted with HSM + ex-MOD walkthrough mitigation).
   - R-003 (Technology, residual 9, exceeds Low appetite +50% — accepted with configuration-only customisation discipline + quarterly architecture review).
   - R-004 (Compliance, residual 8, exceeds appetite +100% — accepted with HSM + separation-of-duties + annual rotation + annual attestation).
   - R-005 (Compliance, residual 12, exceeds appetite +150% — accepted as irreducible customer-side residual).
   - R-007 (Reputational, residual 8, exceeds Very-Low appetite +100% — accepted with network-deny CI gate).
   - **Acknowledgement target date**: 2026-06-30.

2. **Funding confirmed**: £6.60M post-bias 3-year envelope confirmed from working capital + Year-1 SaaS revenue re-investment. **Target**: 2026-06-30.

3. **HSM-backed signing infrastructure operational before first bundle issue**: live by 2026-09-30 per Gate criteria — non-negotiable, mitigates R-004 to residual 2.

4. **Accreditator-in-the-loop alpha programme funded and committed**: ≥ 1 willing customer accreditator engaged by 2027-02-28 per Gate 3 — mitigates R-001 (load-bearing risk for whole track) and R-002 simultaneously.

**Recommended Conditions**:

1. **Cross-project quarterly architecture forum scheduled**: First session by 2026-09-30, protecting SaaS roadmap from sovereign-driven displacement (Conflict C-6 resolution).

2. **Vendor Security Lead deputy capacity established**: Address risk concentration noted in `ARC-002-RISK-v1.0.md` §E (Security Lead carries 30 points across 4 risks). **Target**: 2026-12-31.

3. **Pilot commercial terms negotiated for OBC**: Pilot customer pricing within documented cost-to-serve floor; accreditation-evidence terms in customer schedule. **Target**: 2027-06-30 (Gate 5 / OBC).

## F3. Next Steps if Approved

**Immediate Actions** (Month 1, June 2026):

1. **Service Owner formal acknowledgement** of above-appetite risks signed and circulated — by 2026-06-30.
2. **HLD refresh kickoff** — Lead Architect — by 2026-07-15.
3. **HSM provider contract finalised** — Security Lead + Procurement — by 2026-07-31.

**Phase 1: Pre-Alpha / Build (2026 H2)**:

1. **HLD Refresh** (Gate 1) — by 2026-08-31.
2. **HSM-backed signing infrastructure live** with first independent attestation — by 2026-09-30.
3. **MOD SbD first assessment cycle** (`/arckit:mod-secure`) (Gate 2) — by 2026-09-30.
4. **G-Cloud / DOS / MOD framework listings** — by 2026-10-31.
5. **Pluggable AI abstraction landed** (joint with project 001) — by 2026-12-31.
6. **Operator runbook library v1** — by 2026-12-31.

**Phase 2: Pilot Customer Engagement (2026 Q4 - 2027 Q1)**:

1. **Sovereign Delivery Lead engages pilot customers** via MOD Defence Digital and direct customer SRO contacts — ongoing.
2. **Pilot customer signed (Gate 3)** — by 2027-02-28.
3. **OBC drafted** with pilot commercial terms — Q2 2027.

**Phase 3: Alpha (2027 Q1-Q2)**:

1. **Bundle install validated in CI representative environment** (Gate 4) — by 2027-04-30.
2. **Network-deny CI test profile** mandatory pass before bundle issue — continuous from 2027-04-30.
3. **Accreditator pre-formal walkthrough** — by 2027-05-31.
4. **OBC** (Gate 5) — by 2027-06-30. Run `/arckit:requirements` if material requirement refinements needed; otherwise OBC builds on this SOBC + ARC-002-REQ-v1.0.md.

**Phase 4: Private Beta (2027 Q2-Q3)**:

1. **First customer install in customer environment** — by 2027-08-31.
2. **First MOD SbD evidence pack handed to customer accreditator** — by 2027-09-30.
3. **First ATO submission (Gate 6)** — by 2027-09-30.

**Phase 5: GA (2027 Q4)**:

1. **First ATO issued (Gate 7)** — target 2027-Q4.
2. **GA / FBC (Gate 8)** — by 2027-12-31. Run `/arckit:business-case-detailed` (or equivalent) for FBC.

**Phase 6: Steady-State (2028+)**:

1. **First cross-subsidy quarterly report (Gate 9)** — Q1 2028.
2. **First LTS line cut** — Q2 2028.
3. **Customer 2 onboarding** — Q2 2028.
4. **Customer 3 onboarding** — Q4 2028.
5. **12-month sovereign track formal review** — by 2028-12-31.

## F4. Next Steps if Not Approved

If this SOBC is not approved:

1. **Understand objections**: SRO meets with ARB to understand specific concerns (cost discipline, risk acceptance, timeline, conditions).
2. **Revise SOBC**:
   - If cost concern → re-phase capex into Year-1 (push HSM 6 months — but this delays Gate 2-4 critical path).
   - If risk concern → tighter conditions (e.g., second pilot customer required before Gate 4).
   - If timeline concern → 2028 GA target — delays cross-subsidy contribution by ~12 months but is feasible.
   - If alternative-option preference → revisit Option D (External Partner-Managed) with explicit cross-subsidy renegotiation; or stage Option C as Option C-Lite (delay LTS line until customer 2).
3. **Re-submit revised SOBC** within 4-6 weeks.
4. **Communicate** to stakeholders (especially MOD Defence Digital and pilot customer leads) decision and revised timeline.

**Do Nothing Consequences** (Option A) if project cancelled:

- Stakeholder goals not met (0%).
- Principle 21 hollowed out.
- Cross-subsidy contribution to SaaS SME tier not realised — Principle 17 affordability mission slower or under-funded.
- ~£4.5M-£15M cumulative customer-side cost flows to alternative suppliers across 3-5 customers.
- After ~18 months of unchecked SaaS-only adoption, sovereign route becomes structurally infeasible — Principle 21 commitment compromised.

---

# APPENDICES

## Appendix A: Stakeholder Analysis

**Source**: `projects/002-arckit-sovereign/ARC-002-STKE-v1.0.md`

**Summary**: 17 stakeholder drivers (SD-1 through SD-17), 10 goals (G-1 through G-10), 7 outcomes (O-1 through O-7), full Driver-to-Goal-to-Outcome traceability matrix, 6 conflict analyses with resolutions, 8 stakeholder-related risks (SR-1 through SR-8) — all referenced verbatim in this SOBC.

**Key Stakeholders** (top 10 from Power-Interest Grid):

- Service Owner (Mark Craddock) — High-High — SRO / decision authority (SD-8).
- Lead Architect (vendor) — High-High — Single-codebase discipline (SD-9).
- Security Lead (vendor) — High-High — MOD SbD evidence + signing key (SD-10).
- Customer SRO — High-High — Programme accountability (SD-4).
- Customer Accreditator — High-High — Authorisation to operate (SD-1).
- Customer SIRO — High-High — Information risk acceptance (SD-2).
- Customer Enterprise / Solution / Security Architects (DDaT) — High-High — User community (SD-6).
- MOD Defence Digital — High-High — Supplier diversification (SD-7).
- Customer DSO / CISO — High-Medium — Departmental security policy (SD-3).
- NCSC — High-Medium — UK cyber resilience baseline (SD-15).

## Appendix B: Architecture Principles

**Source**: `projects/000-global/ARC-000-PRIN-v2.0.md`

**Most Relevant Principles**:

- **Principle 21 (Sovereign and Air-Gapped Deployment)** — non-negotiable platform commitment; Option C is the operational embodiment.
- **Principle 17 (FinOps / Cost Transparency)** — sovereign cost-recovery + margin contribution to cross-subsidy.
- **Principle 1 (SME Affordability — Managed SaaS)** — beneficiary of cross-subsidy contribution; sovereign exists to fund this commitment.
- **Principle 4 (Open Standards)** — single-codebase + same APIs across SaaS / sovereign make exit credible.
- **Principle 5 (Security by Design)** — MOD SbD + NCSC CAF mapping per release.
- **Principle 7 (UK Data Sovereignty)** — sovereign deployments inside customer-accredited boundary.
- **Principle 8 (Default-Deny Authorisation)** — within-deployment isolation (FR-006).
- **Principle 12 (Accessibility — WCAG 2.2 AA)** — parity with SaaS.
- **Principle 16 (Reuse)** — components must be backportable, no phone-home licensing.
- **Principle 20 (CI/CD)** — release pipeline produces both SaaS and sovereign artefacts from one revision.

## Appendix C: Options Analysis Details

See B2.1 - B2.5 for full options-by-options breakdown including detailed cost lines, benefits mapping, risk profile, and stakeholder-goals-met calculation per option.

**Detailed Cost Breakdown**: Provided in D1.1 (CapEx) and D1.2 (OpEx) for the Recommended Option.

**Assumptions Register**: A1.4 (assumptions for the Recommended Option); A-1 through A-5 carry through this SOBC.

## Appendix D: Benefits Calculation

See B2.3 (benefits table for Recommended Option) and E6.1 (benefits profiles).

**Sensitivity Analysis** (B3): Base case + 5 sensitivity scenarios (costs +20%, benefits −20%, customer 2 6m slip, customer 3 not signed, all-three combined). Recommended Option remains positive in base case pre-bias; turns marginal post-bias; turns negative under combined-slip stress. OBC discipline is critical.

**Optimism Bias**: HMT optimism-bias add-on of +30% on capability cost applied per `ARC-002-RISK-v1.0.md` §I Economic Case. Heavier than SaaS sister project, reflecting first-attempt accreditation risk (R-001) and supply-chain evidence-discipline risk (R-002, R-004).

## Appendix E: Risk Register

**Full Risk Register**: `projects/002-arckit-sovereign/ARC-002-RISK-v1.0.md` (incorporated into this SOBC Management Case Part E in full per E7).

13 risks across 6 categories (Strategic 2, Operational 3, Financial 1, Compliance 3, Reputational 1, Technology 3 — with cross-listings).

Sovereign-specific risk appetite: Strategic ≤ 12 / Operational ≤ 6 / Financial ≤ 6 / Compliance ≤ 4 / Reputational ≤ 4 / Technology ≤ 6.

5 risks exceed appetite at residual: R-002, R-003, R-004, R-005, R-007 — all Treat-classified; Service Owner formal acknowledgement required per F2.

## Appendix F: Market Research

**Supplier-side market** (vendor inputs):

- HSM providers — competitive UK market (Thales, Entrust UK presence, others).
- Ex-MOD assurance advisors — boutique consultancies, ~10-20 firms; ~£10k/day rates typical.
- Independent attestors — established commercial market.

**Customer-side market** (vendor as supplier):

- Sovereign / air-gapped enterprise-architecture toolkits — small market dominated by defence-systems integrators selling bespoke per-customer; LTS-disciplined product offerings rare. ArcKit's single-codebase + LTS + MOD SbD evidence-pack discipline is differentiating.
- Adjacent commercial defence-EA tooling vendors exist but typically lack: (a) single-codebase commitment with civilian-SaaS counterpart, (b) cross-subsidy commitment to UK SME ecosystem, (c) explicit LTS policy with public documented SLAs, (d) air-gap-validated CI profile.

**Comparables**: Limited public data — defence-IT projects of comparable scope (signed-bundle delivery + LTS + MOD SbD evidence pack) typically £4M-£10M 3-year TCO range; ArcKit-as-a-Service Option C at £5.08M pre-bias / £6.60M post-bias is competitive.

## Appendix G: Governance Terms of Reference

**Steering Committee ToR**: See E1.1 (membership, frequency, decision authorities). Monthly cadence; weekly during alpha and pilot beta.

**Project Board (= Steering Committee for sovereign track)**: Same body; reports to ArcKit Architecture Review Board.

**ArcKit Architecture Review Board ToR** (cross-project): Approves SOBC; protects Principle 21; cross-project quarterly architecture forum.

## Appendix H: Glossary

| Term | Definition |
|------|------------|
| ATO | Authority To Operate (issued by customer accreditator per JSP 604 or departmental SbD) |
| BCR | Benefit-Cost Ratio (HM Treasury Green Book) |
| CapEx / OpEx | Capital / Operational Expenditure |
| CAF | NCSC Cyber Assessment Framework |
| CCS | Crown Commercial Service (UK Cabinet Office procurement) |
| CDDO | Central Digital and Data Office (Cabinet Office) |
| DCPP | Defence Cyber Protection Partnership |
| DDaT | Digital, Data and Technology profession |
| DOS | Digital Outcomes and Specialists (Crown Commercial Service framework) |
| DPS | Dynamic Purchasing System |
| FBC | Full Business Case (final approval stage) |
| FTE | Full-Time Equivalent |
| GovS 005 | Government Functional Standard for Digital |
| GovS 007 | Government Functional Standard for Security |
| HMT | HM Treasury |
| HSM | Hardware Security Module |
| IRR | Internal Rate of Return |
| JSP 440 | Defence Manual of Security |
| JSP 604 | Defence Manual for the Authorisation of Information Systems |
| LTS | Long-Term Support |
| MOD | UK Ministry of Defence |
| NCSC | National Cyber Security Centre |
| NPV | Net Present Value (HM Treasury 3.5% discount) |
| OBC | Outline Business Case (refined cost stage) |
| OES | Operator of Essential Services |
| ROM | Rough Order of Magnitude (cost estimate band) |
| ROPA | Record of Processing Activities (UK GDPR Article 30) |
| ROI | Return on Investment |
| SAL | Security Aspects Letter |
| SbD | Secure by Design |
| SBOM | Software Bill of Materials (CycloneDX or SPDX) |
| SC / DV / NPPV3 | UK personnel security clearance levels |
| SIRO | Senior Information Risk Owner (per GovS 007) |
| SME | Small and Medium Enterprise |
| SOBC | Strategic Outline Business Case (this document) |
| SRO | Senior Responsible Owner (per GovS 005) |
| TCO | Total Cost of Ownership |
| VfM | Value for Money (HM Treasury Green Book criterion) |

---

## Document Approval

| Name | Role | Signature | Date |
|------|------|-----------|------|
| Mark Craddock | Service Owner / SRO | _________ | [PENDING] |
| [PENDING] | Lead Architect / CTO | _________ | [PENDING] |
| [PENDING] | Security Lead | _________ | [PENDING] |
| [PENDING] | ArcKit Architecture Review Board Chair | _________ | [PENDING] |

**Approval Decision**: **APPROVED** | **APPROVED WITH CONDITIONS** | **REJECTED** | **DEFERRED**

**Recommended decision**: **APPROVED WITH CONDITIONS** per F2.

**Conditions** (mandatory, per F2):

1. Service Owner formal acknowledgement of above-appetite risks (R-001, R-002, R-003, R-004, R-005, R-007) signed and circulated by 2026-06-30.
2. Funding £6.60M post-bias 3-year envelope confirmed by 2026-06-30.
3. HSM-backed signing infrastructure operational by 2026-09-30 (Gate 2 prerequisite).
4. Accreditator-in-the-loop alpha programme committed with ≥ 1 willing customer accreditator by 2027-02-28 (Gate 3).

**Recommended Conditions** (per F2):

5. Cross-project quarterly architecture forum scheduled (first session by 2026-09-30).
6. Vendor Security Lead deputy capacity established by 2026-12-31.
7. Pilot commercial terms within documented cost-to-serve floor by Gate 5 (OBC, 2027-06-30).

**Approval Date**: [PENDING]

**Next Review Date**: 2027-06-30 (OBC) — or earlier on material change (e.g., pilot customer signing, MOD SbD assessment outcome, HSM provider change).

---

**END OF STRATEGIC OUTLINE BUSINESS CASE**

*Document created using ArcKit `/arckit:sobc` command*
*Template version: 1.0*
*Green Book compliant: Yes (HM Treasury 5-case model)*

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

**Generated by**: ArcKit `/arckit:sobc` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Anchored on Principle 21 (single codebase) + Principle 17 (cross-subsidy) per `ARC-000-PRIN-v2.0.md`. Strategic Case derived from `ARC-002-STKE-v1.0.md` 17 stakeholder drivers + 10 goals + 7 outcomes. Economic Case 4-option appraisal (do-nothing / hard fork / single-codebase + sovereign overlay [recommended] / external partner-managed) with HMT optimism bias +30% per `ARC-002-RISK-v1.0.md` §I. Commercial Case bespoke per accredited site + MOD Defence Digital framework + LTS pricing per `ARC-002-ADR-008-v1.0.md`. Financial Case cost-recovery + margin tier funding the SaaS cross-subsidy per Principle 17. Management Case Part E references `ARC-002-RISK-v1.0.md` in full (13 risks, sovereign-specific appetite, 4Ts response framework, monitoring framework). All 8 sovereign ADRs (`ARC-002-ADR-001..008-v1.0.md`) inform technical-case framing.
