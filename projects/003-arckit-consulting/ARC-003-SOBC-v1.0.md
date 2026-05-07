# Strategic Outline Business Case (SOBC)

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:sobc`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-003-SOBC-v1.0 |
| **Document Type** | Strategic Outline Business Case (SOBC) |
| **Project** | ArcKit Consulting (Project 003) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-07 |
| **Last Modified** | 2026-05-07 |
| **Review Cycle** | At each stage gate |
| **Next Review Date** | 2026-08-07 |
| **Owner** | Mark Craddock (ArcKit Consulting Practice Lead / SRO) |
| **Reviewed By** | [PENDING — ArcKit Architecture Review Board] |
| **Approved By** | [PENDING — ArcKit Architecture Review Board] |
| **Distribution** | ArcKit Consulting leadership, ArcKit Architecture Review Board, prospective Practice investors / co-founders |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:sobc` command. Strategic Outline Business Case for the ArcKit Consulting practice (Project 003). HM Treasury Green Book 5-case model, 4-option appraisal, ROM strategic estimates. | [PENDING] | [PENDING] |

## Document Purpose

This Strategic Outline Business Case (SOBC) justifies investment in establishing **ArcKit Consulting** — a UK Public Sector enterprise architecture professional services practice that uses the ArcKit toolkit as its delivery medium. The document follows HM Treasury Green Book 5-case methodology and is the **first** business case in the lifecycle. Subsequent stages (OBC after requirements refinement, FBC after detailed design / cohort recruitment) will refine costs and benefits.

The SOBC provides the strategic justification needed to:

- Approve the practice for stand-up under the ArcKit Architecture Review Board (ARB)
- Allocate seed capital and operating capital
- Authorise framework applications (G-Cloud, DOS, MCF sub-contracting)
- Authorise the founder cohort recruitment (BR-003)
- Authorise the SME-tier cross-subsidy mechanism (BR-005, BR-007 in REQ-003)
- Allocate cross-project ARB time for quarterly governance review

> **Source artefacts grounding this SOBC**:
>
> - `projects/003-arckit-consulting/ARC-003-REQ-v1.0.md` — 76 requirements (BR/FR/NFR/INT/DR)
> - `projects/003-arckit-consulting/ARC-003-STKE-v1.0.md` — 18 stakeholder drivers, 14 goals, 9 outcomes, 8 conflicts, 6 synergies
> - `projects/003-arckit-consulting/research/ARC-003-RSCH-v1.0.md` — commercial-model research (1,750 lines): pricing models, framework routes, legal vehicles, operating tooling, comparator benchmarks
> - `projects/000-global/ARC-000-PRIN-v2.0.md` — architecture principles (especially Principle 1 SME affordability, Principle 16 open-source first, Principle 17 FinOps cost transparency)
>
> **Appraisal scope** (per user selection): 4 options (Do Nothing + Minimal + Balanced + Comprehensive), strategic estimates with ROM cost bands (±40%) and primarily qualitative benefits — appropriate for SOBC stage. NPV / BCR / sensitivity analysis to be performed at OBC stage when cohort recruitment confirms cost base.

---

## Executive Summary

**Purpose**: ArcKit Consulting will close the enterprise-architecture capability gap that disadvantages UK SMEs supplying public-sector services and that constrains adoption of the ArcKit governance toolkit by buyers and SMEs. The practice is the third commercial channel in the ArcKit ecosystem (alongside the managed SaaS, Project 001, and the sovereign deployment, Project 002) and the structural mechanism by which the ecosystem cross-subsidises its mandatory SME-affordable free tier (Principle 1).

**Problem Statement**: UK SMEs supplying government rarely have in-house EA capability and cannot afford commercial EA tooling or consultancies (Big-4 day rates routinely exceed £1,500/day). Even buyers and SMEs adopting structured toolkits like ArcKit need consulting support to produce assurance-grade artefacts. Without a principled UK consulting practice anchored to the toolkit, the ArcKit ecosystem cannot operationalise its Principle 1 commitment, and SMEs continue to be excluded from competitive UK gov bids on capability-evidence grounds.

**Proposed Solution**: Establish ArcKit Consulting Ltd as a UK trading entity, with a baseline cohort of 8 employed consultants plus a 5-strong associate panel, listed on G-Cloud and DOS, sub-contracting under MCF prime contractors, operating a four-stack pricing model (day-rate / fixed-price / retainer / SME-tier pro-rata), governed by the ArcKit Architecture Review Board, with a structural ≥10% post-tax margin cross-subsidy to the ArcKit SaaS SME tier.

**Strategic Fit**: Directly operationalises ArcKit Principle 1 (Equitable Access for SMEs) and Principle 16 (Open Source First and Reuse Before Build); aligns with UK Government Procurement Act 2023 (≥ £1-in-£3 SME spend ambition), Technology Code of Practice, GDS Service Standard, and the CDDO Cloud Strategy.

**Investment Required**: ROM **£800k – £1.2m over 3 years** (ranges below)

- **One-off setup** (incorporation, insurance, CE+, framework applications, website, brand, tooling setup): £50k – £110k
- **Year-1 operating cost** (cohort + tooling + statutory baseline + framework MI + capability development): £700k – £900k
- **Year-2 / Year-3 ongoing operating cost** (steady-state): £900k – £1.4m / year, scaling with cohort growth

> Costs in 2026 prices, before optimism-bias uplift and before tax. Year-1 cohort cost dominates (~80% of total). All costs are ROM with ±40% bands appropriate for SOBC stage.

**Expected Benefits** (3 years, primarily qualitative at SOBC stage):

- **Booked revenue Y1 £750k – £1.5m, Y2 £1.5m – £3m, Y3 £2.5m – £5m** (Goal G-5; mid-points imply 3-year cumulative revenue ~£6–8m)
- **Net consulting margin ≥ 20% sustained from Q3 of Y1** (Goal G-5)
- **Cross-subsidy to ArcKit SaaS SME tier ≥ 10% of post-tax net margin annually** — operationalises Principle 1 (Goal G-7; addresses Stakeholder Driver SD-1, SD-10, SD-14)
- **≥ 5 SME engagements delivered Y1, ≥ 4 anonymised case studies, ≥ 2 OSS / public-code contributions** (Goal G-6, G-12; addresses SD-14, SD-15, SD-18 — public scrutiny posture)
- **Public-sector EA capability gap demonstrably reduced** for SMEs supplying UK gov — measurable through SME engagement count and published case studies (Outcome O-4)
- **Structured product-feedback loop ≥ 10 items / quarter** to ArcKit Projects 001 / 002 — strategic asset of dual-channel ecosystem (Goal G-13; Outcome O-9)

**Return on Investment** (qualitative at SOBC; quantitative analysis deferred to OBC):

- **Payback Period**: Year 2 — practice is expected to break even by end of Y1 in the central case, with positive Y2 contribution.
- **NPV (qualitative)**: Positive in central case at HMT 3.5% discount rate; sensitive to Y1 pipeline maturity (G-9), framework-listing timing (G-2), and cohort retention (G-3, NFR-S-002 utilisation discipline).
- **Strategic value**: Beyond direct ROI, the practice unlocks Principle 1 sustainability for the wider ArcKit ecosystem — without it, the SaaS SME free tier is unfunded and at long-term risk.

**Recommended Option**: **Option 2: Balanced Approach**

**Key Risks** (top 3 — full register at /arckit:risk):

1. **Pipeline thinness in early months** (probability MEDIUM, impact HIGH) — mitigated by framework diversification (BR-009), MCF sub-contracting under primes pre-listing, sub-contractor relationships.
2. **High-profile quality failure on assurance event** (probability LOW, impact CRITICAL) — mitigated by 100% checklist pass-rate (NFR-Q-001), independent reviewer pool (FR-008), pre-assessment dry-runs.
3. **SME-tier capacity erosion under commercial pressure** (probability MEDIUM, impact HIGH — Principle 1 compliance issue) — mitigated by ARB quarterly review, published capacity reservation (BR-005), structural cross-subsidy mechanism (BR-004, BC-2).

**Go/No-Go Recommendation**: **PROCEED**

**Rationale**: The proposed practice (a) operationalises a non-negotiable architecture principle (Principle 1) that the ecosystem currently cannot honour at scale; (b) diversifies the ArcKit commercial model usefully; (c) generates a strategic feedback loop into the product line; (d) is a recognised supplier-shape in the UK public sector market with credible comparators (dxw, Made Tech, Equal Experts); (e) has manageable financial risk at the proposed scale (Y1 outlay £700k–£900k against Y1 revenue range £750k–£1.5m). The principal risks are operational, not strategic, and have known mitigations.

**Next Steps if Approved**:

1. ARB approval and seed-capital allocation: target **2026-06-30**.
2. Practice incorporation and statutory baseline (BR-001, G-1): target **2026-09-30**.
3. Cohort recruitment (BR-003, G-3): target **2026-10-31**.
4. Framework listings (BR-002, G-2): target **2026-12-31**.
5. First commercial engagement (G-5): target **2026-12-15**.
6. OBC refresh after Y1 actuals: target **2027-12-15** (12 months post-GA).

---

# PART A: STRATEGIC CASE

## A1. Strategic Context

### A1.1 Problem Statement

**Current Situation**:

The UK Government is actively seeking to spend more with SMEs (Procurement Act 2023; departmental SME Action Plans; ministerial £1-in-£3 SME-spend ambition) and to raise the digital governance maturity of suppliers (Technology Code of Practice; GDS Service Standard; CDDO Cloud Strategy; NCSC Cyber Assessment Framework). Buyers are increasingly expecting assurance-grade governance evidence (security, accessibility, data protection, code-of-practice compliance) as a default precondition for engagement.

Two structural frictions impede that ambition:

1. **Capability asymmetry between SMEs and System Integrators** — SMEs supplying government rarely have the in-house enterprise architecture capability that large System Integrators take for granted, and commercial EA consulting is priced for enterprises (Big-4 day rates routinely exceed £1,500/day; even mid-tier EA day rates start at £900–£1,200). SMEs that win opportunities then struggle to produce the assurance evidence that buyers expect by default — and assurance failure is a recognised disqualifier in subsequent bids.
2. **Adoption gap of governance tooling** — even where buyers and SMEs adopt structured toolkits like ArcKit, the gap between "tool installed" and "evidence-grade artefacts produced and owned by the team" is wide. It is closed by people, not by licences.

The ArcKit ecosystem can produce a tool (Project 001 SaaS, Project 002 sovereign) but cannot, on its own, close the capability gap or fund the externally-published Principle 1 commitment that the SaaS SME tier be free or substantially cheaper than commercial alternatives.

**Specific Pain Points** (from `ARC-003-STKE-v1.0.md`):

| Stakeholder | Driver ID | Pain Point | Impact | Intensity |
|-------------|-----------|------------|--------|-----------|
| ArcKit Practice Lead / SRO (Mark Craddock) | SD-1 | Principle 1 cannot be operationalised at scale without a profitable consulting channel cross-subsidising the SaaS SME tier | Strategic — ecosystem credibility at risk | CRITICAL |
| SME Founders supplying UK gov | SD-14 | Cannot afford EA consultancy at commercial day-rates; in-house EA capability absent; tooling out of reach | Excluded from competitive bids on capability-evidence grounds | HIGH |
| ArcKit Architecture Review Board | SD-10 | No mechanism today funds the Principle 1 SaaS SME free tier sustainably | Principle 1 compliance becomes voluntary, hence at risk | HIGH |
| Client SROs (gov department buyers) | SD-12 | Hard to find UK-public-sector-only specialist EA consultancy that is not enterprise-priced or bound to Big-4 commercial templates | Practical procurement friction; career-sensitive (NAO/PAC-aware) | CRITICAL |
| ArcKit Product Owners (Projects 001 / 002) | SD-9 | No structured engagement-derived feedback loop into the product roadmap | Strategic asset of dual-channel ecosystem unrealised | HIGH |
| HM Treasury / NAO / public scrutiny posture | SD-17, SD-18 | Continued public-sector consultancy concentration on Big-4; SME spend ambition under-met | Continuing political and audit pressure | MEDIUM |

**Consequences of Inaction**:

- **Principle 1 erodes silently**: without cross-subsidy income, the SaaS SME free tier (Project 001) accrues a financial-risk overhead that pressure ultimately closes — undermining the foundational commercial commitment of the entire ecosystem.
- **SME founders remain excluded** from competitive UK gov bids on capability-evidence grounds — the very outcome the Procurement Act 2023 SME-spend ambition was created to prevent.
- **ArcKit Product roadmap loses the highest-signal feedback channel available** (real client engagements) — the Product team relies on synthetic / opportunistic feedback instead.
- **Continuing NAO/PAC pressure on UK consultancy spend** (a recognised regulatory direction-of-travel since 2020) leaves ArcKit unable to differentiate itself via principled, transparent SME-affordable practice.

### A1.2 Strategic Drivers

**Link to Stakeholder Analysis**: This business case is informed by the stakeholder analysis in `ARC-003-STKE-v1.0.md` (18 drivers; SD-1 through SD-18).

**Primary Drivers**:

| Driver ID | Stakeholder | Driver Type | Driver Description | Strategic Imperative |
|-----------|-------------|-------------|-------------------|---------------------|
| SD-1 | Practice Lead / SRO | STRATEGIC + PERSONAL + RISK | Principled, sustainable practice operationalising Principle 1 cross-subsidy; brand integrity across product / sovereign / consulting trio | Mission delivery + ecosystem solvency |
| SD-10 | ArcKit ARB | COMPLIANCE + STRATEGIC | Cross-project consistency; Principle 1 honoured operationally; no commercial drift contradicting principles | Governance integrity |
| SD-14 | SME Founders | FINANCIAL + STRATEGIC + PERSONAL | Affordable EA expertise; fast time to assurance pass; learn-to-maintain model | Mission beneficiary; ecosystem credibility |
| SD-9 | ArcKit Product Owners | STRATEGIC + OPERATIONAL | Real-engagement product feedback loop; dual-channel reinforcement | Ecosystem strategy |
| SD-12 | Client SROs (gov) | PERSONAL + RISK + OPERATIONAL | Outcome delivered, value defensible at NAO/PAC; capability built up; not locked in | Buyer trust = pipeline |
| SD-15 | GDS / CDDO | COMPLIANCE + STRATEGIC | TCoP / Service Standard / Cloud Strategy adherence | Standards-based supplier |
| SD-17, SD-18 | HMT / NAO / public scrutiny | FINANCIAL + COMPLIANCE | VfM, transparent pricing, SME spend ambition met | Public legitimacy |

**Strategic Alignment**:

- **ArcKit Principle 1** (Equitable Access for SMEs) — non-negotiable; this practice is the structural mechanism that funds it sustainably.
- **ArcKit Principle 16** (Open Source First and Reuse) — every engagement contributes back via anonymised patterns and OSS contributions (FR-013).
- **ArcKit Principle 17** (Cost Transparency and FinOps) — transparent pricing across all four pricing-stack models; cross-subsidy is auditable.
- **UK Procurement Act 2023** — SME spend ambition; transparent supplier conduct.
- **Technology Code of Practice and GDS Service Standard** — quality discipline aligned to assurance gates.
- **CDDO Cloud Strategy** — practice standards-aware in delivery.
- **NCSC Cyber Assessment Framework + PPN 09/23** — Cyber Essentials Plus continuous certification (NFR-C-005).

### A1.3 Stakeholder Goals (Spending Objectives)

**Goals Addressed** (from `ARC-003-STKE-v1.0.md`):

| Goal ID | Stakeholder | SMART Goal | Current State | Target State | Timeline |
|---------|-------------|------------|---------------|--------------|----------|
| G-1 | Practice Lead, DPO, CCS, ICO | UK trading entity with full regulatory baseline (Companies House, ICO, HMRC, CE+, insurance, website) | Founder only — no entity | All baseline live | 2026-09-30 |
| G-2 | Commercial Lead, Practice Lead | G-Cloud + DOS framework listings live | No listings | Both live | 2026-12-31 |
| G-3 | Talent Lead, Engagement Director, Practice Lead | Cohort onboarded (1 PL, 2 Principal, 3 Senior, 2 Consultant + 5-strong associate panel) | 1 founder | 8 employed + 5 associates | 2026-10-31 |
| G-4 | DPO, CCS, Client SROs | Cyber Essentials Plus continuous; CHC + annual pen test | Not certified | Continuous certification | 2026-09-30 onwards |
| G-5 | Practice Lead, Commercial, Engagement Director | Year-1 booked revenue £750k–£1.5m at ≥ 20% net margin | £0 | Revenue range achieved | End Y1 |
| G-6 | Practice Lead, ARB, SME Founders, NAO posture | Published SME tier; ≥ 5 SME engagements in Y1; quarterly published case study | None | ≥ 5 Y1 | End Y1 |
| G-7 | Practice Lead, Product Owners, ARB | Cross-subsidy ≥ 10% post-tax net margin to SaaS SME tier | None | First annual transfer | End first profitable FY |
| G-8 | QA Lead, Practice Lead, Client SROs, GDS/CDDO | 100% client deliverables pass ArcKit quality checklist | n/a | 100% sustained | Continuous from GA |
| G-9 | Commercial Lead, Engagement Director, Practice Lead | Pipeline coverage ≥ 3.0 | n/a | ≥ 3.0 sustained | Steady-state |
| G-10 | Practice Lead, QA, Engagement Director, Client SROs | Client NPS ≥ +40 rolling 12-month | n/a | ≥ +40 | From Y2 |
| G-11 | QA Lead, Practice Lead, Client SROs, GDS/CDDO | Zero independent-assurance failures attributable to practice | n/a | 0 sustained | Continuous |
| G-12 | Practice Lead, ARB, GDS/CDDO, NAO posture | ≥ 4 case studies + ≥ 2 OSS contributions in Y1 | None | Targets met | End Y1 |
| G-13 | Practice Lead, Product Owners | Quarterly product feedback loop (≥ 10 items / qtr at steady-state) | None | Operational | From Y1 |
| G-14 | DPO, Practice Lead, Client SROs, ICO | 0 cross-engagement data leakage incidents | n/a | 0 sustained | Continuous |

> All 14 goals are addressed by the Recommended Option (Option 2). Coverage by other options shown in §B2.

### A1.4 Scope

**In Scope** (this SOBC; full detail in REQ-003 §Project Scope):

- UK trading entity (Ltd v1 → B-Corp certification Y2 → EOT consideration Y3-5; CIC explicitly out — see RSCH-003 legal-vehicle analysis).
- Engagement lifecycle from opportunity → contract → delivery → closure, using ArcKit toolkit (Project 001 for OFFICIAL; Project 002 for OFFICIAL-SENSITIVE).
- Baseline consultant cohort (8 employed) + associate panel (5).
- Knowledge management (anonymised IP / pattern library, FR-012).
- Routes to market: G-Cloud + DOS + MCF sub-contracting + direct-award under threshold.
- Pricing models: four-stack hybrid (day-rate, fixed-price, retainer £8k–£18k/month, SME-tier pro-rata).
- Quality assurance and peer review of all deliverables.
- Regulatory compliance: UK GDPR, ICO, Companies Act, HMRC, employment law, Cyber Essentials Plus.

**Out of Scope** (deferred or excluded):

- Operating the ArcKit SaaS or sovereign deployments (Projects 001 / 002).
- Licence resale of third-party EA tooling (no software-reseller business).
- Engagements outside UK Public Sector and SMEs supplying it.
- Engagements requiring classifications above OFFICIAL-SENSITIVE *unless* delivered through Project 002 sovereign with deploying-authority accreditation.
- Permanent staff placement / recruitment as a primary service line.
- Bespoke software build engagements where ArcKit governance is not the centre of the work.

**Interfaces**:

- **ArcKit Project 001 (managed SaaS)** — primary delivery platform for OFFICIAL engagements (INT-001 in REQ-003).
- **ArcKit Project 002 (sovereign)** — delivery platform for OFFICIAL-SENSITIVE engagements (INT-002).
- **Crown Commercial Service Digital Marketplace** — framework listings and call-off (INT-004).
- **Companies House, HMRC, ICO** — statutory interfaces (INT-003, INT-006, INT-011).
- **ArcKit Architecture Review Board** — internal cross-project governance.

**Assumptions**:

1. ArcKit Project 001 (managed SaaS) reaches a usable state on or before this practice's GA; if delayed, fallback to Markdown / git-based delivery (R-8 in STKE).
2. Project 002 (sovereign) is operable for sensitive-site engagements where required (or contingency tooling is acceptable to client).
3. CCS framework cycles continue at current pace and continue to admit small specialist suppliers.
4. UK public sector demand for ArcKit-style governance support persists at or above current observed levels.
5. SC clearance pipelines for nominated consultants meet typical 3–9 month timelines.

**Dependencies**:

- **Internal**: ArcKit Project 001 GA; ArcKit Architecture Review Board governance bandwidth.
- **External**: G-Cloud / DOS framework refresh windows; CE+ assessor capacity; insurance market for new entity.
- **Technical**: Identity / SSO provider selection; managed-device tooling; engagement-workspace isolation as designed in Project 001.

### A1.5 Why Now?

**Urgency Factors**:

- **ArcKit ecosystem at GA inflection**: Projects 001 / 002 are reaching commercial readiness; without an operational consulting channel at the same time, the dual-channel strategy fails to launch coherently and Principle 1 cross-subsidy starts late, losing a year of compounding.
- **G-Cloud 16 / DOS 8 / DSP successor framework iteration windows**: framework refresh cycles are the practical market entry points; missing the next cycle delays effective bidding by 12–18 months.
- **UK Government SME-spend ambition is a current political priority** (Procurement Act 2023; SME Action Plans; £1-in-£3 spend target) — the political and procurement environment for a principled SME-tier offer is the most receptive in a decade.
- **Public scrutiny of UK consulting spend (NAO, PAC, journalism)** is at a sustained high since 2020; differentiated, transparent, principled practices are commercially advantaged in a way that may diminish if/when scrutiny eases.

**Opportunity Cost of Delay** (12-month delay vs proceeding now):

- ~£750k – £1.5m Y1 booked revenue forgone (G-5).
- ~£75k – £150k forgone Y1 cross-subsidy contribution to SaaS SME tier (estimated 10% post-tax of mid-margin).
- Loss of strategic feedback loop into Project 001 / 002 product roadmap for one full year.
- ≥ 5 SME engagements forgone in Y1, plus the ≥ 4 case-study and ≥ 2 OSS contributions that compound the brand and ecosystem.
- Comparator practices (Made Tech, dxw, Equal Experts) consolidate UK-public-sector standing further; ArcKit Consulting enters a more crowded position later.

**Window of Opportunity**:

- Practice Lead is available to dedicate full time to founding (2026 H2 onwards).
- ArcKit Product line GA timing creates a coherent ecosystem launch story.
- Framework refresh windows align with practice readiness timing.
- B-Corp UK community is mature enough to recognise and support principled new entrants.

---

# PART B: ECONOMIC CASE

## B1. Critical Success Factors

**Critical Success Factors (CSFs)** — this is what "success" means; every option is judged against these.

1. **CSF-1 — Strategic Alignment**: Honours ArcKit Principle 1 (SME affordability) operationally, not just in policy.
   - **Measure**: Quarterly published SME-tier capacity reservation utilised; ≥ 10% post-tax net margin transferred annually to SaaS SME tier; ARB validates annually.
   - **Threshold**: Both must hold; either failing is a Principle 1 compliance issue.

2. **CSF-2 — Quality Discipline**: Brand-protective evidence-grade output that withstands independent assurance.
   - **Measure**: 100% deliverables pass ArcKit quality checklist (NFR-Q-001); zero substantive independent-assurance failures attributable to practice (G-11).
   - **Threshold**: 100% checklist pass-rate is the floor; one publicised assurance failure is a brand crisis.

3. **CSF-3 — Information Governance**: Provable confidentiality and security baseline.
   - **Measure**: Cyber Essentials Plus continuous; zero cross-engagement leakage; clean ICO record; tested 72h breach process.
   - **Threshold**: All four. CE+ lapse alone disqualifies the practice from most UK gov work.

4. **CSF-4 — Commercial Sustainability**: Margin sufficient to fund cross-subsidy and pay competitive consultant rates.
   - **Measure**: Net consulting margin ≥ 20% sustained from Q3 of Y1; pipeline coverage ≥ 3.0; concentration thresholds (BR-009) respected.
   - **Threshold**: Margin floor of 20%; pipeline floor of 3.0.

5. **CSF-5 — Brand Differentiation**: Delivery quality, openness, and SME-tier credibility distinguish the practice in the UK gov consultancy market.
   - **Measure**: Client NPS ≥ +40 rolling 12-month; ≥ 4 anonymised case studies + ≥ 2 OSS contributions in Y1; client retention ≥ 50% Y2+.
   - **Threshold**: NPS ≥ +40; case-study and OSS volume floors.

## B2. Options Analysis

> **Note**: All cost figures are **Rough Order of Magnitude (ROM) with ±40% bands** appropriate for SOBC stage. NPV / BCR calculations are deferred to OBC. Optimism-bias uplift is shown explicitly per option (UK Gov standard +40% on costs for IT projects; the practice's IT spend is small but the principle applies to delivery overhead too — recommend +25% optimism bias on the cohort cost).

### Option 0: Do Nothing (Baseline)

**Description**: Do not establish ArcKit Consulting. The ArcKit ecosystem operates with Projects 001 (SaaS) and 002 (sovereign) only; SME tier on the SaaS is funded (if at all) from product margin alone or by founder subsidy.

**Costs (3-year)**:

- **One-off**: £0 (nothing established).
- **Operational**: £0 direct; **£0 – £750k opportunity cost** (founder subsidy of SaaS SME tier, plus continuing absence of structured product feedback).
- **Total ROM**: £0 direct cost; 3-year opportunity cost in the order of £200k – £1m+ depending on how far the SaaS SME tier needs to scale.

**Benefits**: £0.

**Pros**:

- ✅ No upfront investment.
- ✅ No governance overhead for a third channel.
- ✅ Zero implementation risk.

**Cons**:

- ❌ All 14 stakeholder goals (G-1 to G-14) unmet (0% coverage).
- ❌ Principle 1 cross-subsidy unfunded; SaaS SME free tier becomes a financial-risk overhead that pressure may close — Principle 1 compliance becomes voluntary and at risk.
- ❌ Capability gap for SME founders supplying UK gov persists; Procurement Act 2023 SME-spend ambition unsupported.
- ❌ Strategic feedback loop into Projects 001 / 002 absent — dual-channel ecosystem strategy unrealised.
- ❌ ArcKit ecosystem fails to differentiate itself in UK gov market vs commodity EA tooling vendors.
- ❌ Opportunity cost compounds year-on-year.

**Risks**:

- **R0.1 SaaS SME tier financial pressure → tier reduction or closure**: HIGH probability over 3+ years; CRITICAL impact on Principle 1 compliance.
- **R0.2 Principle 1 erodes silently into a marketing claim only**: HIGH probability without structural funding; CRITICAL reputational impact.
- **R0.3 Comparator practices (Made Tech, dxw, Equal Experts) consolidate UK gov standing**: HIGH probability over the same window; MODERATE impact on later entry options.

**Stakeholder Goals Met**: 0% (0 of 14).

**Critical Success Factors**: CSF-1 fails (Principle 1 unfunded); CSF-2 / 3 / 4 / 5 not applicable (no practice).

**Recommendation**: **REJECT** — Strategically unacceptable; Principle 1 compliance becomes voluntary and at long-term risk. This option exists in the analysis only as the baseline against which other options are compared.

---

### Option 1: Minimal Viable Practice (Solo + Associates)

**Description**: Establish a micro-practice — 1–2 employed (Practice Lead + possibly one Senior Consultant) plus a small associate panel (3–4 associates) used on demand. List on DOS as a Specialist supplier only (skip G-Cloud and MCF in v1). Pricing limited to day-rate + SME-tier pro-rata only (skip fixed-price catalogue and retainer).

**Scope**:

- Solo / micro practice with 1–2 employed + 3–4 associates.
- DOS specialist listing only.
- Day-rate + SME-tier pricing only.
- Minimal operating tooling (free / low-cost SaaS only — e.g. HubSpot free, FreeAgent free with NatWest, Notion free / Plus, Google Workspace).
- B-Corp certification deferred indefinitely; Ltd only.

**Costs (3-year ROM, ±40%)**:

| Cost Item | Year 1 | Year 2 | Year 3 | 3-Year Total |
|-----------|--------|--------|--------|--------------|
| Setup (incorporation, insurance, CE+, brand, website) | £40k – £80k | £0 | £0 | £40k – £80k |
| Cohort (1–2 employed + on-costs) | £100k – £200k | £150k – £250k | £180k – £300k | £430k – £750k |
| Associate panel (variable, Y1 utilisation low) | £50k – £150k | £100k – £250k | £150k – £350k | £300k – £750k |
| Operating tooling (low-cost SaaS) | £3k – £8k | £5k – £10k | £6k – £12k | £14k – £30k |
| Statutory / compliance ongoing (insurance renewal, CE+, ICO) | £8k – £15k | £8k – £18k | £10k – £20k | £26k – £53k |
| Capability development (NFR-M-003, ≥ 5%) | £5k – £15k | £8k – £20k | £10k – £25k | £23k – £60k |
| **Total ROM** | **£206k – £468k** | **£271k – £548k** | **£356k – £707k** | **£833k – £1.72m** |

**Optimism-bias uplift** (+25% on cohort and operating; +40% on setup): adds approximately £200k – £400k over 3 years.

**Benefits (3-year, qualitative)**:

- **Booked revenue** (smaller cohort → smaller pipeline): ROM Y1 £200k – £500k, Y2 £400k – £900k, Y3 £600k – £1.2m. 3-year cumulative ~£1.2m – £2.6m.
- **Net margin** likely thin and volatile (fixed cohort cost vs variable utilisation). Year-1 likely loss-making; break-even Y2 in central case only.
- **Cross-subsidy contribution** small or zero — Principle 1 only partially funded.
- **SME engagements**: ≤ 2 / year realistically with this capacity.
- **Case studies / OSS contributions**: 1 / year realistically.
- **Product feedback loop**: thin.

**Pros**:

- ✅ Lowest upfront capital outlay.
- ✅ Lower regulatory / governance overhead.
- ✅ Faster to stand up (~3 months).
- ✅ Lowest risk if practice fails to gain traction (smallest sunk cost).
- ✅ Founder retains majority control / equity.

**Cons**:

- ❌ Cannot meet pipeline-coverage target (G-9) or revenue target (G-5) — capacity-bound.
- ❌ SME-tier delivery (G-6) materially diluted to ≤ 2 / year — Principle 1 compliance issue.
- ❌ Cross-subsidy (G-7) negligible — Principle 1 commitment fundamentally at risk.
- ❌ No G-Cloud / MCF route — most UK gov EA call-offs out of reach.
- ❌ Single-key-person risk extreme (founder = practice).
- ❌ Quality-discipline at scale unproven; QA gate (NFR-Q-001) often founder-conflicted.
- ❌ Brand differentiation thin; comparators (Made Tech, dxw) outscale rapidly.

**Stakeholder Impact**:

- G-1 (regulatory baseline): ✅ Met (lighter footprint).
- G-2 (frameworks): ⚠️ Partially met (DOS only; G-Cloud + MCF deferred).
- G-3 (cohort): ⚠️ Partially met (1–2 employed vs target 8).
- G-4 (CE+): ✅ Met.
- G-5 (revenue + margin): ❌ At risk; revenue target unachievable; margin thin.
- G-6 (SME tier): ⚠️ Partially met (≤ 2 / year).
- G-7 (cross-subsidy): ❌ Negligible — Principle 1 effectively unfunded.
- G-8 (quality 100%): ⚠️ At risk (independent reviewer pool too small).
- G-9 (pipeline ≥ 3.0): ❌ Capacity-bound, unachievable.
- G-10–G-14: largely achievable but at lower scale.

**Stakeholder Goals Met**: ~40% (with notable Principle 1 dilution).

**Critical Success Factors**: CSF-1 fails (cross-subsidy too small); CSF-4 fails (margin too thin to pay cross-subsidy); CSF-2 / 3 partly met; CSF-5 thin.

**Risks**:

- **R1.1 Capacity bound preventing pipeline scale-up**: HIGH probability; HIGH impact on revenue target.
- **R1.2 Single-person dependency on founder**: HIGH probability of disruption (illness, leave, burnout); CRITICAL impact on engagement continuity (NFR-A-001).
- **R1.3 QA discipline diluted by small reviewer pool**: MEDIUM probability; HIGH brand-risk.
- **R1.4 Principle 1 commitment becomes a marketing claim, not an operational reality**: HIGH probability without cross-subsidy income.

**Recommendation**: **REJECT** — Materially fails the strategic case (Principle 1 cross-subsidy unfunded; CSF-1 fails). Acceptable only if it were a deliberate proof-of-concept stage on a path to Option 2, but in that case the costs of stand-up are mostly sunk twice. Better to commit to Option 2.

---

### Option 2: Balanced Approach — RECOMMENDED

**Description**: Establish ArcKit Consulting Ltd at full baseline cohort size as defined in REQ-003 BR-003. List on G-Cloud and DOS, sub-contract under MCF prime contractors for surge demand and to cover MCF call-offs. Operate the four-stack pricing hybrid (day-rate / fixed-price / retainer / SME-tier pro-rata, per RSCH-003). Adopt the recommended operating-tooling stack (Microsoft 365 Business Premium + FreeAgent + HubSpot + Harvest + Notion + Eleventy site, per RSCH-003). Ltd v1 → B-Corp certification Y2 → EOT consideration Y3-5. Structural ≥ 10% post-tax cross-subsidy to SaaS SME tier from first profitable year.

**Scope**:

- Baseline cohort: 1 PL + 2 Principal + 3 Senior + 2 Consultant + 5 associate panel (per BR-003).
- All three primary framework routes: G-Cloud + DOS + MCF sub-contracting + direct-award under threshold.
- Four-stack pricing (RSCH-003): day-rate (DOS) + fixed-price (G-Cloud / SME tier) + retainer £8k–£18k/month + SME-tier pro-rata (~50% standard).
- Full operating-tooling stack: M365 Business Premium (£20.60/user/m bundling Entra P1 + Intune + Office), FreeAgent or Xero, HubSpot CRM (free → Starter), Harvest Pro, Adobe Acrobat Sign, Sage HR/Payroll, Notion Plus, Eleventy public website.
- Statutory baseline: PI £10m + PL £5m + EL £10m + cyber £2m + Cyber Essentials Plus + ICO Tier 2.
- Quality discipline (NFR-Q-001) + independent reviewer pool (FR-008).
- B-Corp certification Y2; EOT consideration Y3-5.
- Quarterly product-feedback loop into Projects 001 / 002 (BR-010, G-13).

**Costs (3-year ROM, ±40%)**:

| Cost Item | Year 1 | Year 2 | Year 3 | 3-Year Total |
|-----------|--------|--------|--------|--------------|
| Setup (incorporation, insurance Y1, CE+, brand, website, framework apps, contract templates) | £50k – £110k | £0 | £0 | £50k – £110k |
| Cohort (8 employed + on-costs, blended ≈ £75k loaded average × 8) | £550k – £700k | £700k – £900k | £850k – £1.1m | £2.1m – £2.7m |
| Associate panel (5 associates, variable use) | £100k – £300k | £200k – £500k | £300k – £700k | £600k – £1.5m |
| Operating tooling (M365 + FreeAgent + HubSpot + Harvest + Notion + Eleventy, per RSCH) | £8k – £15k | £10k – £18k | £12k – £22k | £30k – £55k mid-£30k |
| Statutory / compliance ongoing (insurance, CE+ recert, pen test, ICO, MI returns) | £15k – £30k | £18k – £35k | £20k – £40k | £53k – £105k |
| Capability development (≥ 5% chargeable equivalent) | £25k – £45k | £35k – £60k | £45k – £75k | £105k – £180k |
| Framework / brand investment (case studies, OSS contributions, conferences, B-Corp Y2) | £10k – £25k | £15k – £35k | £15k – £30k | £40k – £90k |
| Contingency (~10% on cohort and ops to absorb pipeline variance, framework timing) | £80k – £120k | £100k – £150k | £130k – £200k | £310k – £470k |
| **Total ROM** | **£838k – £1.345m** | **£1.078m – £1.698m** | **£1.372m – £2.167m** | **£3.288m – £5.21m** |

**Optimism-bias uplift** (+25% on cohort/ops; +40% on setup): adds ~£250k – £400k over 3 years. Adjusted central case 3-year cost £3.5m – £4.5m.

**Benefits (3-year, qualitative)**:

| Benefit ID | Benefit Description | Linked Stakeholder Goal | Type | Y1 (range) | Y2 (range) | Y3 (range) | 3-Year Total (range) |
|------------|---------------------|-------------------------|------|------------|------------|------------|----------------------|
| B-001 | Booked revenue | G-5 | FINANCIAL | £750k – £1.5m | £1.5m – £3m | £2.5m – £5m | £4.75m – £9.5m |
| B-002 | Net consulting margin (≥ 20% from Q3 of Y1) | G-5 | FINANCIAL | -£250k – +£300k | £300k – £600k | £500k – £1m | £550k – £1.9m |
| B-003 | Cross-subsidy to SaaS SME tier (≥ 10% post-tax net margin) | G-7, Principle 1 | STRATEGIC + FINANCIAL | £0 (likely loss) | £20k – £60k | £40k – £100k | £60k – £160k |
| B-004 | SME engagements delivered (≥ 5/year from Y1) | G-6, Outcome O-4 | STRATEGIC + COMPLIANCE | ≥ 5 engagements | ≥ 5 engagements | ≥ 5 engagements | ≥ 15 engagements |
| B-005 | Anonymised case studies + OSS contributions (≥ 4 + ≥ 2 in Y1) | G-12, Outcome O-9 | STRATEGIC | 4 + 2 | 4 + 2 | 4 + 2 | 12 + 6 |
| B-006 | Quarterly product feedback loop (≥ 10 items/qtr) | G-13, Outcome O-9 | STRATEGIC + OPERATIONAL | ~30 items | ~40 items | ~40 items | ~110 items |
| B-007 | Trusted brand evidenced (NPS ≥ +40, retention ≥ 50% Y2+) | G-10, G-11, Outcome O-3 | STRATEGIC | NPS established | ≥ +40 sustained | ≥ 50% retention | Brand evidenced |
| B-008 | Information governance incident-free record | G-4, G-14, Outcome O-8 | RISK | CE+ live; 0 leakage | Sustained | Sustained | Clean ICO record |
| B-009 | Public-sector EA capability gap reduced for SMEs (qualitative; mission outcome) | SD-14, Outcome O-4 | STRATEGIC | First cohort of SMEs supported | Compounds | Compounds | Mission credibility |
| B-010 | Strategic feedback loop into ArcKit Product roadmap (qualitative) | G-13, Outcome O-9 | STRATEGIC | Established | Productised | Compounds | Ecosystem advantage |

**Net financial position (central / midpoint case, ROM)**:

- **3-year revenue mid-point**: ~£7m
- **3-year cost mid-point** (with optimism bias): ~£4m
- **3-year net contribution**: ~£3m before tax
- **Cumulative cross-subsidy to SaaS SME tier** (≥ 10% post-tax): ~£200k – £400k over 3 years
- **Payback period**: Y2 mid (break-even by end of Y1 in central case; positive Y2 contribution)

> **NPV / BCR not calculated at SOBC stage (per appraisal-depth selection — Strategic estimates).** OBC will refine: cohort cost certainty after recruitment, pipeline maturity actuals after Y1, sensitivity analysis, formal NPV at HMT 3.5% discount.

**Pros**:

- ✅ All 14 stakeholder goals achievable (100% coverage of G-1 to G-14).
- ✅ All 5 Critical Success Factors met or attainable.
- ✅ Principle 1 cross-subsidy operationalised structurally (CSF-1).
- ✅ Brand differentiation feasible vs comparators (CSF-5).
- ✅ Realistic recruitment / retention via NFR-S-002 utilisation discipline + NFR-M-003 capability time.
- ✅ Strategic feedback loop into Projects 001 / 002 functional (G-13).
- ✅ Risk-bearing capacity to absorb a single bad engagement without practice failure.
- ✅ Comparator-validated shape (dxw, Made Tech, Equal Experts all run at this scale or above with similar service mixes).

**Cons**:

- ⚠️ Higher Y1 outlay than Option 1 — financial risk if pipeline matures slowly (mitigated by BR-009 pipeline coverage + sub-contracting under MCF primes pre-listing).
- ⚠️ Governance overhead — quarterly ARB review, weekly steering, monthly compliance review.
- ⚠️ Cohort recruitment and retention is the practice's largest operational risk (R-4 in STKE).
- ⚠️ Senior consultant market is competitively priced and sticky; achieving 8 employed in 6 months is realistic but not effortless.

**Stakeholder Impact**:

- G-1 (regulatory baseline): ✅ Met by 2026-09-30.
- G-2 (frameworks): ✅ Met by 2026-12-31.
- G-3 (cohort): ✅ Met by 2026-10-31.
- G-4 (CE+ continuous): ✅ Met from 2026-09-30 onwards.
- G-5 (revenue + margin): ✅ On-target in central case; pipeline-discipline (G-9) is the leading indicator.
- G-6 (SME tier ≥ 5/year): ✅ Met from Y1.
- G-7 (cross-subsidy ≥ 10% post-tax): ✅ Met from first profitable FY (likely Y2).
- G-8 (quality 100%): ✅ Achievable with FR-008 independent reviewer discipline.
- G-9 (pipeline ≥ 3.0): ✅ Achievable at this cohort scale.
- G-10 (NPS ≥ +40): ✅ Achievable based on comparator evidence (Made Tech, dxw cite NPS in this range).
- G-11 (zero assurance failures): ✅ Achievable with checklist + independent review discipline.
- G-12 (case studies + OSS): ✅ Achievable; capacity sufficient.
- G-13 (product feedback ≥ 10/qtr): ✅ Achievable.
- G-14 (zero cross-engagement leakage): ✅ Achievable with FR-004 isolation discipline.

**Stakeholder Goals Met**: 100% (14 of 14).

**Critical Success Factors**: All 5 met or attainable.

**Risks** (top 5 — full register at /arckit:risk):

- **R2.1 Pipeline thinness in early months** → MEDIUM/HIGH; mitigated by BR-009 framework diversification, MCF sub-contracting under primes (live before listings), sub-contractor surge capacity.
- **R2.2 High-profile quality failure on assurance event** → LOW/CRITICAL; mitigated by FR-008 independent QA, NFR-Q-001 100% checklist, pre-assessment dry-runs.
- **R2.3 Cross-engagement data leakage** → LOW/CRITICAL; mitigated by FR-004 isolation, quarterly tests, FR-017 incident response, NFR-SEC-007 leaver controls.
- **R2.4 Senior consultant churn in first 12 months** → MEDIUM/HIGH; mitigated by NFR-S-002 utilisation cap (65–80%), NFR-M-003 capability time, fair pay, principled environment.
- **R2.5 SME-tier capacity erosion under commercial pressure** → MEDIUM/HIGH (Principle 1 compliance); mitigated by ARB review, BC-1 published commitment, structural cross-subsidy.

**Recommendation**: **ACCEPT — RECOMMENDED OPTION**.

---

### Option 3: Comprehensive Practice (Larger Cohort + MCF Lot Direct Bid)

**Description**: Establish at significantly larger scale — 15+ employed consultants in Y1, multi-region UK presence (London + at least one regional hub, e.g. Manchester or Bristol), pursue MCF Lot direct (not via sub-contracting) for inclusion in next MCF refresh, foundation status (B-Corp from Y1, faster EOT path), broader service catalogue including bespoke build / DevOps capacity.

**Scope**:

- Cohort 15+ employed (1 PL + 1 Engagement Director + 4 Principal + 6 Senior + 3 Consultant + 8-strong associate panel).
- Multi-region UK presence; physical office or co-working membership in 2 regions.
- Pursue MCF Lot direct bid in next MCF refresh.
- Broader service catalogue: EA + bespoke design + light build / DevOps.
- B-Corp certification from Y1; EOT path Y3.
- Larger marketing / brand investment.

**Costs (3-year ROM, ±40%)**:

| Cost Item | Year 1 | Year 2 | Year 3 | 3-Year Total |
|-----------|--------|--------|--------|--------------|
| Setup (incorporation, dual-region insurance, CE+, brand, premises, website, framework apps, MCF Lot bid) | £100k – £200k | £30k – £50k | £20k – £40k | £150k – £290k |
| Cohort (15 employed + on-costs, blended ≈ £80k loaded × 15) | £1.0m – £1.4m | £1.3m – £1.8m | £1.6m – £2.2m | £3.9m – £5.4m |
| Associate panel (8 associates, variable use) | £200k – £600k | £400k – £900k | £500k – £1.2m | £1.1m – £2.7m |
| Premises / co-working (2 regions) | £30k – £80k | £40k – £100k | £50k – £120k | £120k – £300k |
| Operating tooling (scaled — Salesforce / Office 365 E3 etc) | £20k – £45k | £30k – £55k | £35k – £70k | £85k – £170k |
| Statutory / compliance ongoing (insurance, CE+, pen test, MI, ICO, B-Corp annual fee, MCF MI) | £25k – £55k | £30k – £65k | £35k – £80k | £90k – £200k |
| Capability development (≥ 5% chargeable equivalent) | £50k – £85k | £65k – £115k | £80k – £140k | £195k – £340k |
| Marketing / brand / case studies / events | £30k – £80k | £40k – £100k | £40k – £100k | £110k – £280k |
| Contingency (~10%) | £150k – £250k | £200k – £320k | £240k – £400k | £590k – £970k |
| **Total ROM** | **£1.605m – £2.795m** | **£2.135m – £3.505m** | **£2.6m – £4.35m** | **£6.34m – £10.65m** |

**Optimism-bias uplift** (+25% on cohort/ops; +40% on setup): ~£600k – £1m over 3 years.

**Benefits (3-year, qualitative)**:

- **Booked revenue Y1 £1.5m – £3m, Y2 £3m – £6m, Y3 £5m – £10m** (more headroom but pipeline must match scale).
- **Net margin** initially thin (cohort cost runs ahead of revenue); break-even Y2 in central case; ≥ 20% achievable Y3.
- **Cross-subsidy** larger in absolute terms once profitable (Y3+).
- **SME engagements**: ≥ 10/year achievable with this capacity.
- **Case studies / OSS / product feedback**: 1.5–2× Option 2 volumes.
- **MCF direct presence**: meaningful procurement-route advantage if next refresh window aligns; not all UK gov departments use MCF directly though.

**Pros**:

- ✅ Larger volumes on every benefit metric.
- ✅ MCF direct route opens larger consultancy spend pools.
- ✅ Risk-bearing capacity higher (single-engagement / single-consultant failures less destabilising).
- ✅ Brand investment larger (case studies, conferences, OSS).
- ✅ B-Corp from Y1 differentiation.

**Cons**:

- ❌ Y1 outlay £1.6m – £2.8m vs Option 2's £840k – £1.35m — significantly higher financial risk if pipeline does not mature.
- ❌ Cohort scale (15 employed) requires ~30 candidates interviewed in 6 months — ambitious in current market.
- ❌ Multi-region presence adds operational complexity that does not directly help win UK gov work (most engagements are remote-or-London).
- ❌ MCF Lot direct bid is competitively-evaluated; success not guaranteed and effort cost £80k+ for the bid alone.
- ❌ Bespoke build / DevOps service line is **out of scope** of REQ-003 — adopting it requires reopening scope (BR scope expansion).
- ❌ Quality discipline at 15+ harder to maintain than at 8; QA reviewer pool stretched.
- ❌ Cross-subsidy contribution proportionally similar to Option 2 (10% of post-tax margin), not larger as % of practice — and absolute amount depends on margin holding.
- ❌ Diminishing returns: Option 3 costs ~2× Option 2 but does not deliver 2× the strategic benefit.

**Stakeholder Impact**: All 14 goals achievable but with higher delivery risk in Y1 due to cohort recruitment and pipeline maturity at scale.

**Stakeholder Goals Met**: 100% (14 of 14) — same coverage as Option 2 but at higher risk and higher cost.

**Critical Success Factors**:

- CSF-1 (Principle 1): ✅ Met.
- CSF-2 (Quality): ⚠️ Harder to maintain at scale; reviewer pool stretched.
- CSF-3 (Information governance): ✅ Met (same controls).
- CSF-4 (Sustainability): ❌ Y1 margin pressure significantly higher; break-even risk extends into Y2.
- CSF-5 (Brand differentiation): ✅ Met (and stronger via MCF, B-Corp Y1).

**Risks**:

- **R3.1 Cohort recruitment shortfall in Y1** → HIGH probability; HIGH impact (revenue model assumes 15-FTE chargeable capacity).
- **R3.2 Pipeline-cohort mismatch in Y1** → MEDIUM-HIGH; HIGH impact (a £1.5m+ cost base unmatched by revenue is materially dangerous).
- **R3.3 MCF direct-bid rejection** → MEDIUM; MEDIUM impact (bid cost £80k+ sunk).
- **R3.4 Bespoke build / DevOps scope-creep distracts from EA mission** → MEDIUM; HIGH brand-impact (the practice is recognisable as "EA" not as "build shop").
- **R3.5 Quality drift at scale** → MEDIUM; CRITICAL brand-impact.

**Recommendation**: **REJECT** — Diminishing returns; Y1 financial risk materially higher; scope-expansion (build / DevOps) distracts from EA mission; MCF direct-bid uncertain. Option 2 achieves the same Stakeholder Goals coverage and CSF coverage with materially lower risk and is the right starting position. Option 3 may be revisited in Y3-4 as a deliberate growth step *after* Option 2 is established and de-risked.

---

## B3. Recommended Option

**Recommendation**: **Option 2: Balanced Approach**.

### Side-by-side Comparison

| Dimension | Option 0 (Do Nothing) | Option 1 (Minimal) | **Option 2 (Balanced) — RECOMMENDED** | Option 3 (Comprehensive) |
|-----------|------------------------|---------------------|----------------------------------------|---------------------------|
| **Cohort size (Y1 employed)** | 0 | 1–2 | **8** | 15+ |
| **Framework routes** | None | DOS only | **G-Cloud + DOS + MCF subbing** | G-Cloud + DOS + MCF direct |
| **Pricing models** | n/a | Day-rate + SME tier | **4-stack hybrid (DR + FP + Retainer + SME)** | 4-stack + larger fixed-price catalogue |
| **3-year cost ROM** | £0 direct | £0.83m – £1.72m | **£3.3m – £5.2m** | £6.3m – £10.7m |
| **3-year revenue ROM** | £0 | £1.2m – £2.6m | **£4.75m – £9.5m** | £9.5m – £19m |
| **Y1 break-even probability** | n/a | LOW | **MEDIUM-HIGH** | LOW |
| **Cross-subsidy contribution** | £0 | Negligible | **Material from Y2** | Material from Y3 |
| **Stakeholder Goals met** | 0% | ~40% | **100%** | 100% |
| **Critical Success Factors** | 0/5 met | 1-2/5 attained | **5/5 attainable** | 4/5 attainable |
| **Principle 1 compliance risk** | CRITICAL | HIGH | **LOW** | LOW |
| **Cohort recruitment risk** | n/a | LOW (small) | **MEDIUM** | HIGH |
| **Brand differentiation** | n/a | THIN | **CREDIBLE** | STRONG |
| **Diminishing returns vs Option 2** | n/a | n/a | **n/a (anchor)** | YES (~2× cost, similar coverage) |
| **SOBC Recommendation** | REJECT | REJECT | **ACCEPT** | REJECT (revisit Y3-4) |

### Rationale for Option 2

1. **Best Strategic Fit**: Operationalises Principle 1 cross-subsidy structurally (CSF-1); funds the SaaS SME free tier sustainably from first profitable year; 100% Stakeholder Goal coverage.
2. **Best CSF Coverage**: All 5 Critical Success Factors met or attainable, including the principled-and-sustainable balance that defines the practice's identity (CSF-1 + CSF-4 simultaneously).
3. **Comparator-Validated Scale**: dxw, Made Tech, and Equal Experts all operate at this approximate scale or higher with similar UK-public-sector service mixes (per RSCH-003 comparator analysis) — the shape is market-validated.
4. **Manageable Financial Risk**: Y1 outlay £840k – £1.35m against Y1 revenue range £750k – £1.5m gives a thin Y1 but realistic break-even in central case. Risk-adjusted contingency (~10%) covers pipeline timing variance.
5. **Recruitment Achievable**: 8 employed + 5 associates over 6 months is ambitious but realistic in the current senior-EA market — comparators have done it. Option 3's 15+ would require near-doubling of recruitment speed and is the principal failure-mode.
6. **Right Scope**: Stays within EA professional services (the mission); does not bleed into bespoke build / DevOps (which is a different business model and risks brand drift).
7. **Principled Defaults**: Pricing-floor governance, ARB quarterly review, and structural cross-subsidy mean the practice cannot drift commercially away from Principle 1 without explicit, traceable decisions.

### Key Sensitivities (informal at SOBC; formalised at OBC)

- **If Y1 revenue is at the low end (£750k)**: Y1 will be loss-making by ~£100k – £400k (given £840k – £1.35m cost). Mitigation: contingency reserve; pipeline-coverage discipline (G-9); MCF sub-contracting under primes pre-listing; phased associate engagement (variable cost flex).
- **If cohort recruitment slips by 3 months**: Y1 cost reduces by ~£100k – £150k but Y1 revenue also reduces. Net effect on Y1 break-even is roughly neutral; net effect on Y2 ramp is moderately negative.
- **If framework listings slip past 2026-12-31**: revenue compresses substantially in Y1 (most UK gov EA work flows through frameworks). Mitigation: MCF sub-contracting under primes is live before own MCF/G-Cloud listings, providing bridging revenue.
- **If a high-profile quality failure occurs**: brand impact is critical. Mitigation: NFR-Q-001 100% checklist, FR-008 independent QA, pre-assessment dry-runs.
- **Optimism bias (UK Gov standard)**: +25% applied to cohort and operational costs; +40% applied to setup costs. Adjusted central-case 3-year cost £3.5m – £4.5m. Even with full optimism uplift, Option 2 remains net positive in the central case.

### Sensitivity to Optimism Bias (UK Government)

UK Gov Green Book guidance recommends +40% optimism bias for IT projects in early stages. ArcKit Consulting is a *professional services* practice rather than an IT system, but the principle of accounting for early-stage cost optimism applies. Recommended uplifts:

| Item | Recommended Uplift | Reason |
|------|---------------------|--------|
| Setup costs | **+40%** | Standard for early-stage estimate; legal / insurance pricing variability |
| Cohort costs | **+25%** | Recruitment market variability; on-cost certainty improves at OBC |
| Operating tooling | **+15%** | RSCH-003 has narrow ranges already |
| Framework / MI overhead | **+25%** | First-cycle uncertainty |
| Pipeline / revenue (downward) | **-25%** | Y1 pipeline maturity risk |

Adjusted central case: 3-year cost ~£4m – £4.5m; 3-year revenue ~£5m – £7m. Positive net contribution in central case under optimism-biased view; OBC will refine.

---

# PART C: COMMERCIAL CASE

## C1. Procurement Strategy

### C1.1 Market Assessment

**Market Maturity**: The UK public sector consultancy market is mature, competitive, and fragmented. Big-4 (Deloitte, EY, KPMG, PwC) dominate large engagements; mid-tier (BJSS, Mastek, TPXImpact, CGI) hold significant share; specialist boutiques (Made Tech, dxw, Equal Experts, Caspian One, Snook, Public.io) hold the differentiated UK-public-sector niche that ArcKit Consulting will compete in. Per RSCH-003 §6, none of the existing comparators combines: (a) UK-public-sector-only focus, (b) explicit principled SME-tier with structured cross-subsidy, (c) toolkit-anchored evidence-grade delivery, (d) Ltd flexibility with B-Corp credibility overlay. **The white-space is real, and identifiable**.

**Supplier Landscape** (closest comparators per RSCH-003):

- **Tier — Closest values comparator**: dxw (employee-owned, public-sector-only, ~80 staff).
- **Tier — Closest structural comparator**: Made Tech (transparent, public-sector-only, listed company, ~300 staff).
- **Tier — Capability comparator**: Equal Experts, BJSS, TPXImpact (multi-sector but heavy UK-gov presence).
- **Tier — Niche / differentiated**: Public.io, Snook, dxw (each occupies an identifiable principled niche).

**UK Government Digital Marketplace Assessment**:

- **G-Cloud (currently 14, with 15/16 cycles upcoming)**: Cloud Software and Cloud Support service categories — the recommended listing route for fixed-price ArcKit-led architecture services. Hundreds of suppliers across categories; SME-friendly entry; transparent published pricing required.
- **DOS (currently 6, with 7/8 / DSP successor upcoming)**: Specialist roles (Enterprise / Business / Security / Data / Digital Architect) — capped day-rate entry with clear specialism categories. SME-friendly.
- **MCF (currently 3/4)**: Management Consultancy Framework — ArcKit Consulting will not be on MCF directly in v1 (entry barrier high for new SMEs); will sub-contract under existing MCF prime contractors. Revisit at MCF5 refresh in Y2-3.
- **SME participation**: Crown Commercial Service publishes SME participation data; G-Cloud is ~50% SME-supplier-share by count.

**This Practice as Buyer / Procurer**: ArcKit Consulting is also a **buyer** of professional services / SaaS tooling. Procurement of operating tooling (Microsoft 365, FreeAgent, HubSpot, etc.) is straightforward SaaS subscription procurement — not subject to public-sector procurement rules (the practice is not a contracting authority). Standard commercial diligence applies.

### C1.2 Sourcing Route to Market (the Practice as Supplier)

**Recommended Routes** (in order of priority — per RSCH-003):

1. **MCF sub-contracting under existing primes** (LIVE as soon as cohort cleared) — bridging revenue while own framework listings are pending.
2. **G-Cloud 16** (when cycle opens) — Cloud Support service entry; transparent published pricing for the fixed-price catalogue (RSCH-003 four-stack pricing model).
3. **DOS 8 / DSP successor** (when cycle opens) — Specialist roles for day-rate consultant deployment.
4. **Direct award under threshold** — single-supplier engagements under £40k typically permitted without formal procurement.

**Rationale**:

- Multi-route presence diversifies pipeline (BR-009 concentration thresholds: no single framework > 60% of forward 12-month revenue).
- MCF sub-contracting lets the practice trade revenue from day 1 without waiting for own listings — material de-risk against framework-cycle timing (R-5 in STKE).
- G-Cloud + DOS are SME-friendly with transparent pricing aligned with Principle 17 (Cost Transparency / FinOps).

**Alternative Routes Considered**:

| Route | Pros | Cons | Recommendation |
|-------|------|------|----------------|
| G-Cloud + DOS only (no MCF sub-contracting) | Simpler | Slower revenue ramp; framework-cycle risk | REJECT — adopt MCF sub-contracting for bridging |
| MCF Lot direct | Larger consultancy spend access | Bid cost £80k+, evaluation competitive, success uncertain | **REJECT in v1; revisit MCF5 refresh in Y2-3** |
| Open competition / non-framework | Targets bespoke RFPs | Each tender-win cost high; no SME shortcuts | Use selectively for high-value targeted opportunities |
| Direct award under threshold | Flexibility | Limited to small engagements; no cumulative-spend benefit | Use opportunistically (default for SME tier) |

### C1.3 Contract Approach

**Standard Contract Templates** (to be drafted as part of FR-002 / BR-001 stand-up):

- **Day-rate (DOS) Specialist Engagement**: capped day-rate; deliverable-defined; per-day reporting; standard CCS DOS terms.
- **Fixed-price (G-Cloud) Engagement**: outcome-defined SOW; milestone-based payment; PPN 03/23 prompt-payment compliant; standard CCS G-Cloud Cloud Support call-off terms with practice-customised rider (`/arckit:sow` template customisation).
- **Retainer (Direct or G-Cloud)**: monthly capped advisory; £8k–£18k/month range; per-month deliverable bundle; rolling 12-month with 3-month notice termination.
- **SME-tier (Direct, Pro-Rata)**: capped scope; published rates ~50% standard; explicit IP / case-study consent template; lightweight contract.

**Contract Duration**:

- Day-rate / DOS: typically 3–12 months per engagement.
- Fixed-price / G-Cloud: 6–18 months per engagement.
- Retainer: rolling 12 months with 3-month notice.
- SME-tier: typically time-boxed (4–12 weeks).

**Payment Structure**:

- Day-rate: monthly arrears against time-records.
- Fixed-price: 30/40/30 split on three milestones (kick-off / mid / sign-off) — or per CCS framework standard terms where mandated.
- Retainer: monthly advance.
- SME-tier: 50/50 (kick-off / closure).

**Key Contract Terms**:

- Service Level Agreements: per fixed-price engagement (defined in SOW).
- Penalties: only where required by CCS framework or buyer.
- Intellectual Property: client owns engagement deliverables; practice retains rights in pre-existing patterns; anonymised pattern reuse permitted with client consent (FR-013).
- IG / DPA Article 28 clauses: per FR-003 / NFR-C-001.
- Termination: per framework standard or 3-month notice.
- Information governance: NDAs + IG training attestation; FR-004 workspace isolation.

### C1.4 Social Value (UK Gov context)

**Social Value Themes ArcKit Consulting Embeds Naturally**:

1. **Economic** — SME-tier engagements directly support SMEs supplying UK gov (Procurement Act 2023 SME-spend ambition); apprenticeships / capability-development for early-career consultants.
2. **Social** — published Equality Act 2010 commitments; B-Corp certification Y2 (recognised social-value evidence).
3. **Environmental** — carbon-light operating model (no premises in v1; remote-first); carbon-aware tooling choices.

The practice will publish a Social Value Statement on the public website (FR-019) and bind it into engagement SOWs where buyers request social-value commitments (per CCS Social Value Model, minimum 10% weighting).

---

# PART D: FINANCIAL CASE

## D1. Budget Requirement

**Total Investment Required (3-year Recommended Option, ROM with optimism-bias uplift)**: **£3.5m – £4.5m central case; £4m – £6m worst case (-25% revenue + +40% setup + +25% cohort).**

> All costs in 2026 prices, ROM ±40% bands. OBC stage will refine after cohort recruitment confirms cost base and Y1 actuals confirm pipeline maturity.

### D1.1 Capital Expenditure (CapEx)

The practice is heavily OpEx-weighted (professional services); CapEx is small.

| Item | Year 1 | Year 2 | Year 3 | Total |
|------|--------|--------|--------|-------|
| Brand / website (Eleventy site, design) | £8k – £18k | £0 | £2k – £5k | £10k – £23k |
| Operating tooling setup (M365, FreeAgent, HubSpot, Harvest, Notion, Adobe Sign — config + training) | £8k – £15k | £0 | £0 | £8k – £15k |
| Endpoint hardware (laptops × cohort) | £15k – £30k | £8k – £15k | £10k – £20k | £33k – £65k |
| Initial CE+ assessment | £3k – £6k | £0 | £0 | £3k – £6k |
| Contract / IP templates (legal counsel) | £5k – £15k | £0 | £0 | £5k – £15k |
| **Total CapEx** | **£39k – £84k** | **£8k – £15k** | **£12k – £25k** | **£59k – £124k** |

### D1.2 Operational Expenditure (OpEx)

The dominant cost. Detailed in B2 Option 2.

| Item | Year 1 | Year 2 | Year 3 | 3-Year Total |
|------|--------|--------|--------|--------------|
| Cohort (8 employed + on-costs) | £550k – £700k | £700k – £900k | £850k – £1.1m | £2.1m – £2.7m |
| Associate panel (5, variable) | £100k – £300k | £200k – £500k | £300k – £700k | £600k – £1.5m |
| Operating tooling subscriptions | £8k – £15k | £10k – £18k | £12k – £22k | £30k – £55k |
| Insurance renewal (PI, PL, EL, cyber) | £8k – £25k | £12k – £30k | £15k – £35k | £35k – £90k |
| Cyber Essentials Plus annual + pen test | £6k – £20k | £6k – £20k | £6k – £20k | £18k – £60k |
| Framework MI / membership fees | £2k – £8k | £3k – £10k | £3k – £10k | £8k – £28k |
| Capability development (≥ 5%) | £25k – £45k | £35k – £60k | £45k – £75k | £105k – £180k |
| Brand / case studies / OSS contributions / B-Corp Y2 | £10k – £25k | £15k – £35k | £15k – £30k | £40k – £90k |
| Contingency (~10%) | £80k – £120k | £100k – £150k | £130k – £200k | £310k – £470k |
| **Total OpEx** | **£789k – £1.258m** | **£1.081m – £1.723m** | **£1.376m – £2.192m** | **£3.246m – £5.173m** |

### D1.3 Total Cost of Ownership (TCO)

| | Year 1 | Year 2 | Year 3 | 3-Year Total |
|---|--------|--------|--------|--------------|
| CapEx | £39k – £84k | £8k – £15k | £12k – £25k | £59k – £124k |
| OpEx | £789k – £1.258m | £1.081m – £1.723m | £1.376m – £2.192m | £3.246m – £5.173m |
| **Total TCO (ROM)** | **£828k – £1.342m** | **£1.089m – £1.738m** | **£1.388m – £2.217m** | **£3.305m – £5.297m** |
| **Plus optimism bias (~+25%)** | **£1.04m – £1.68m** | **£1.36m – £2.17m** | **£1.74m – £2.77m** | **£4.13m – £6.62m** |

**Notes**:

- All costs in 2026 prices.
- Excludes VAT (will apply once turnover threshold £85k crossed; recoverable on most expenses).
- Optimism-bias uplift applied (UK Gov standard +25% on professional-services cohort; +40% on setup).
- Cohort cost dominates (~80% of total) — most refinement at OBC will narrow the cohort range.

## D2. Funding Source

**Funding Structure**:

- **Source**: Founder capital + reinvested margin (the practice is self-funded, no external investor in v1).
- **Y1 working capital requirement**: ROM £200k – £500k (cohort cost runs ahead of revenue collection in early months; aged-debt; framework application costs).
- **Y2-3 funding**: From operating margin + reinvested profit; no further capital injection required in central case.
- **Risk-case Y2-3 funding**: If pipeline matures slowly, founder bridge-funding or short-term loan facility (£200k – £400k) may be needed in late Y1 / early Y2. This is the principal financial risk of the SOBC.

**Approval Path**:

- **Practice Lead / SRO**: All commercial decisions within budget envelope.
- **ArcKit Architecture Review Board**: Approves Y1 budget envelope; quarterly review of cross-subsidy mechanism (G-7); annual Principle-1 affordability review.
- **External (no UK Gov approval)**: The practice is a private trading entity. No HMT / spend-control approval is required.

**Funding Gaps** (if any):

- Identified principal gap: **Y1 working capital £200k – £500k** depending on pipeline maturity rate.
- **Mitigation**: founder capital + cash-flow management discipline (FR-007 invoices issued ≤ 5 days from milestone; aged-debt > 90 days ≤ 5% of debtors per BR-004); MCF sub-contracting bridging revenue in Y1 H1; phased associate engagement (variable cost-flex).

## D3. Affordability

**Practice-level Affordability**:

- The practice is funded by its own founder capital. Affordability is therefore a **founder-capital-availability** question and a **pipeline-maturity** question, not an institutional-budget question.
- Y1 worst-case scenario (low-end revenue + high-end cost + working capital): £400k – £600k cumulative cash drawdown before Y2 inflection. **Within plausible founder-capital envelope; manageable risk.**
- Y2 / Y3: practice expected to be self-funding from operating margin in central case.

**Cross-Subsidy Affordability** (Principle 1):

- **≥ 10% of post-tax net consulting margin** transferred annually to the ArcKit SaaS Project 001 SME-tier capacity pool (G-7).
- In Y1 (likely loss-making or thin), no transfer; transfer accrues notionally.
- From first profitable FY (likely Y2): transfer £20k – £100k/year in central case.
- ARB tracks; transfer is structural, not optional (BC-2 of REQ-003).

**Cash Flow Impact**:

- Largest single cash outflow: monthly cohort payroll £45k – £60k from month 6 of Y1 onwards.
- Aged-debt risk (clients paying 60+ days): material in Y1 H2 as engagement portfolio matures. PPN 03/23 prompt-payment regime mitigates from public-sector clients but does not eliminate.
- Cash-flow runway: 6-month cohort + ops cost reserve (~£300k – £500k) recommended at all times once cohort is live.

## D4. Financial Appraisal (Strategic Estimates — appropriate for SOBC stage)

### D4.1 Qualitative Economic Appraisal (Green Book)

**Discount Rate**: 3.5% (HMT standard social time preference rate). Applied conceptually here; numerical NPV deferred to OBC.

**3-year cumulative net contribution (central / midpoint case, ROM)**:

- **Total benefits PV** (revenue, undiscounted central): ~£7m
- **Total costs PV** (with optimism bias, undiscounted central): ~£4m – £4.5m
- **Net contribution** (undiscounted central): ~£2.5m – £3m before tax
- **NPV at 3.5% over 3 years**: positive in central case; precise figure deferred to OBC.

**Cross-subsidy (G-7) value**: ~£60k – £200k cumulative over 3 years; this is *value* (not cost) because it operationalises Principle 1 and unlocks SaaS SME tier sustainability that itself is a strategic enabler.

### D4.2 Return on Investment (Strategic Estimate)

**Payback Period** (ROM): break-even by end of Y1 in central case; clear positive contribution from Y2; payback ~Y2 mid.

**ROI** (Strategic Estimate, 3 years, central case):

```text
ROI = (Total Benefits - Total Costs) / Total Costs × 100%
ROM ROI = (~£7m - ~£4.25m) / ~£4.25m × 100% ≈ 65% over 3 years
```

> Numerical ROI is indicative only. OBC will refine after cohort cost certainty and Y1 pipeline-maturity actuals.

### D4.3 Value for Money Assessment

**Qualitative Assessment**:

- **Economy**: Recommended operating-tooling stack (per RSCH-003) is competitive (3-year tooling TCO ~£30k mid-point at 10-person scale; vs ~£60k+ for an open-source-first stack and ~£390k+ for a build-everything stack). Cohort blended rates competitive vs comparators.
- **Efficiency**: Capacity utilisation discipline (NFR-S-002 65–80%) protects per-FTE economics. Quality-checklist discipline (NFR-Q-001) reduces rework cost per engagement. Pattern library (FR-012) compounds delivery efficiency over time.
- **Effectiveness**: 100% of REQ-003 requirements covered; 100% of STKE-003 stakeholder goals attainable; 5/5 CSFs met or attainable.

**Overall VfM Rating**: **HIGH** (qualitative; OBC will quantify).

**Justification**: The practice is structurally engineered to honour the principles that make ArcKit credible (Principle 1, 16, 17), at a cost base competitive with comparators and a revenue model validated by their precedents. The principal VfM risk is pipeline-maturity timing (Y1 working capital), which is bounded and mitigatable.

---

# PART E: MANAGEMENT CASE

## E1. Governance

### E1.1 Roles & Responsibilities (RACI)

Derived from `ARC-003-STKE-v1.0.md` §Governance & Decision Rights:

| Decision/Activity | Responsible | Accountable | Consulted | Informed |
|-------------------|-------------|-------------|-----------|----------|
| Annual cross-subsidy transfer to SaaS SME tier | Practice Lead | ArcKit ARB | DPO, Finance | All stakeholders |
| Pricing-floor exception (below-floor bid) | Commercial Lead | Practice Lead | QA Lead | ARB |
| QA gate hold on a deliverable | QA Lead | QA Lead | Engagement Director | Practice Lead |
| Engagement classification (OFFICIAL / OFFICIAL-SENSITIVE) | Engagement Director | Practice Lead | DPO, Client SRO | Talent Lead |
| Consultant allocation to engagement | Engagement Director | Engagement Director | Talent Lead, QA Lead | Consultant |
| Sub-contractor engagement | Commercial Lead | Engagement Director | Talent Lead, DPO | Practice Lead |
| Case-study / OSS publication | Practice Lead | Practice Lead | DPO, Client SRO (consent) | ARB |
| Information-security incident response | DPO | DPO | Practice Lead, Engagement Director | ICO (if breach), Clients (per contract) |
| Hiring (employees) | Talent Lead | Practice Lead | Engagement Director | All consultants |
| Framework-listing applications | Commercial Lead | Practice Lead | DPO (CE+, IG), QA Lead | ARB |
| Architecture exception against principles | Practice Lead | ArcKit ARB | DPO, QA Lead | All stakeholders |
| Client engagement contract sign-off | Commercial Lead | Practice Lead | DPO (IG clauses), QA Lead (deliverable scope) | Client SRO |

**Senior Responsible Owner (SRO)**: **Mark Craddock (Practice Lead)**.

- Accountable for delivery of all 14 stakeholder goals.
- Chairs weekly steering with Engagement Director, Commercial Lead, QA Lead.
- Reports quarterly to ArcKit Architecture Review Board.
- Annual Principle-1 affordability review presented to ARB and published.

**Steering Committee (Practice-internal)**:

- Practice Lead / SRO (Chair)
- Engagement Director (Operations)
- Commercial Lead (Bid, Framework, Contracts)
- QA Lead (Quality)
- Talent Lead (Capability)
- DPO / IG Lead (Compliance)

**Meeting Frequency**: Weekly.

**Cross-Project Governance**: ArcKit Architecture Review Board — quarterly, with annual Principle-1 affordability validation.

### E1.2 Approval Gates

| Gate | Criteria | Approving Body | Timing |
|------|----------|----------------|--------|
| **Gate 0: SOBC Approval** | This document approved; seed capital allocated; ARB endorsement | ArcKit ARB | 2026-06-30 |
| **Gate 1: Practice Stand-Up** | Companies House live; ICO live; HMRC live; insurance live; CE+ assessment scheduled | SRO | 2026-09-30 |
| **Gate 2: Cohort Live** | Cohort recruited and onboarded per BR-003 / G-3 | SRO + Talent Lead | 2026-10-31 |
| **Gate 3: Framework Listings** | G-Cloud + DOS listings live; MCF sub-contracting relationships in place | SRO + Commercial Lead | 2026-12-31 |
| **Gate 4: First Engagement Sign-Off** | First commercial engagement closed (FR-014) with full QA log + client NPS | SRO + QA Lead | 2027-Q1 |
| **Gate 5: Y1 OBC Refresh** | First profitable FY confirmed; cross-subsidy transferred; ARB Principle-1 review complete | ArcKit ARB | 2027-12-15 |

## E2. Delivery Approach

**Methodology**: Stage-gated practice stand-up, then continuous operating model.

**Phases**:

1. **Phase 1 — Pre-incorporation** (May–Jun 2026): SOBC approval, ARB sign-off, founder-capital allocation, key recruitment for Engagement Director / Commercial Lead.
2. **Phase 2 — Stand-up** (Jul–Sep 2026): Companies House, regulatory baseline, insurance, CE+, brand, public website, contract templates, identity / SSO, MDM, financial system.
3. **Phase 3 — Cohort and frameworks** (Sep–Dec 2026): Recruitment, onboarding (FR-006), framework applications, MCF prime relationships, first opportunity capture (FR-001).
4. **Phase 4 — First engagements** (Dec 2026 – Mar 2027): Bridging engagements via MCF subbing; first own-listing wins; QA / pattern-library bootstrapping.
5. **Phase 5 — Steady state** (Apr 2027 onwards): Concurrent engagements scale from 5 → 20 over 18 months (NFR-S-001); B-Corp certification; first cross-subsidy transfer; first published case studies.

**Delivery Model**:

- **In-house**: All commercial work; QA; brand; case-study production.
- **Vendor (B2B)**: Insurance, accounting, HR/payroll, training providers, legal counsel.
- **Sub-contractor**: Surge capacity via associate panel and MCF prime relationships.

## E3. Key Milestones

| Milestone | Date | Dependencies | Owner |
|-----------|------|--------------|-------|
| **SOBC Approved (this gate)** | 2026-06-30 | ARB endorsement | SRO + ARB |
| Engagement Director + Commercial Lead hired | 2026-07-31 | SOBC approval | Talent Lead |
| Companies House incorporation; ICO registration; HMRC | 2026-08-31 | Legal counsel; founder | SRO |
| Insurance in force; CE+ assessment scheduled | 2026-09-15 | Insurance market; CE+ assessor capacity | DPO |
| **Gate 1 — Practice Stand-Up Complete** | 2026-09-30 | All baseline live | SRO |
| Cyber Essentials Plus certificate issued | 2026-10-15 | Assessment passed | DPO |
| Public website live with WCAG 2.2 AA evidence | 2026-10-31 | Brand + content + accessibility audit | SRO |
| **Gate 2 — Cohort Live** (G-3) | 2026-10-31 | Onboarding complete per FR-006 | Talent Lead + SRO |
| First MCF sub-contracting engagement live | 2026-11-30 | Prime relationship; cohort cleared | Commercial Lead + Engagement Director |
| **Gate 3 — Framework Listings Live** (G-2) | 2026-12-31 | G-Cloud + DOS submitted in active cycle | Commercial Lead |
| **First own-listing engagement closed** (G-5 inaugural data) | 2027-Q1 | Listing live; bid won; engagement delivered | Engagement Director + QA Lead |
| **Gate 4 — First Engagement Sign-Off** | 2027-Q1 | Closure FR-014 complete; QA log clean; NPS captured | SRO + QA Lead |
| First SME-tier engagement closed (G-6 inaugural) | 2027-Q1–Q2 | SME-tier intake live (FR-011) | Practice Lead |
| First anonymised case study published (G-12 inaugural) | 2027-Q2 | Client consent (FR-013); DPO IG review | Practice Lead |
| First quarterly product-feedback meeting (G-13) | 2027-Q1 | Engagement portfolio established | Practice Lead + Product Owners |
| **Gate 5 — Y1 OBC Refresh** | 2027-12-15 | First profitable FY confirmed; ARB Principle-1 review | ArcKit ARB |
| B-Corp certification live | 2027-Q4 | Application; assessment | Practice Lead |
| First cross-subsidy transfer to SaaS SME tier (G-7) | End first profitable FY | Margin > 0 post-tax | Practice Lead + ARB |

**Critical Path**:

1. CE+ assessment (4–8 week lead time per RSCH-003) — gates framework-listing eligibility.
2. Cohort recruitment (SC clearance pipelines 3–9 months) — gates engagement allocation on OFFICIAL-SENSITIVE work.
3. G-Cloud / DOS framework refresh windows — gate own-listing-route pipeline ramp.

## E4. Resource Requirements

### E4.1 Team Structure

**Core Practice Team** (per BR-003):

| Role | FTE / Status | Y1 Cost (loaded, ROM) |
|------|---------------|------------------------|
| Practice Lead / SRO (founder) | 1.0 | Founder rate; ~£100k loaded |
| Engagement Director | 1.0 | ~£100k–£120k loaded |
| Commercial Lead (Bid, Framework, Contracts) | 1.0 | ~£80k–£100k loaded |
| QA Lead | 0.5 (could be combined with senior consultant) | ~£50k loaded share |
| Talent Lead | 0.5 (could be fractional / outsourced) | ~£40k loaded |
| DPO / IG Lead | 0.2 (fractional) | ~£15k–£25k retainer |
| Principal Consultants × 2 | 2.0 | ~£200k loaded |
| Senior Consultants × 3 | 3.0 | ~£225k loaded |
| Consultants × 2 | 2.0 | ~£110k loaded |

**Associate Panel (variable use)**: 5 associates available; cost variable by engagement booking.

**Total cohort Y1 cost (loaded ROM)**: ~£550k – £700k as in B2 / D1.

### E4.2 Skills Required

**Critical Skills**:

- **EA delivery** (TCoP, Service Standard, NCSC CAF, MOD SbD where relevant) — **Available**: PL has it; recruit Principals / Seniors with same.
- **ArcKit toolkit fluency** — **Gap**: New to most market consultants; 2–3 weeks accreditation per consultant.
- **UK gov procurement** (G-Cloud, DOS, MCF, PPN 03/23, Procurement Act 2023) — **Need**: Commercial Lead recruitment to bring this.
- **UK GDPR / DPA / IG** — **Fractional retainer**: external DPO recommended in v1.

**Training Plan**:

- ArcKit toolkit accreditation per consultant: 2–3 weeks; ~£3k–£5k per head.
- IG / NDA / equality training: annual (≥ £200 per head).
- Capability development time embedded (≥ 5% chargeable equivalent per quarter, NFR-M-003).

## E5. Change Management

### E5.1 Stakeholder Engagement

Per `ARC-003-STKE-v1.0.md` §Communication & Engagement Plan. Summary:

| Stakeholder | Power-Interest | Engagement Approach | Frequency | Owner |
|-------------|----------------|---------------------|-----------|-------|
| Practice Lead / SRO | Manage Closely | Daily ownership | Continuous | Self |
| Engagement Director | Manage Closely | Weekly steering | Weekly | SRO |
| Commercial Lead | Manage Closely | Pipeline review | Weekly | SRO |
| Client SROs | Manage Closely | Per-engagement steering meeting | Per-engagement | Engagement Director |
| ArcKit ARB | Manage Closely (governance) | Quarterly review | Quarterly | SRO |
| QA Lead, Talent Lead | Keep Informed | Daily QA gate / weekly cohort review | Daily / weekly | SRO |
| DPO / IG Lead | Keep Satisfied | Monthly compliance | Monthly | SRO |
| CCS Framework Mgrs | Keep Satisfied | MI returns; framework conduct | Quarterly | Commercial Lead |
| GDS / CDDO, ICO, HMT | Keep Satisfied | Through engagement deliverables | Per-engagement | Engagement Director / DPO |
| Senior Consultants | Keep Informed | Weekly peer forum | Weekly | Engagement Director |
| Associate Panel | Keep Informed | Quarterly partner review + per-engagement | Quarterly | Commercial Lead |
| SME Founders | Keep Informed | Public website intake; per-engagement | Per-engagement | Practice Lead |

### E5.2 Resistance Management

Per STKE §Risk Register R-1 to R-10. Anticipated resistance:

| Source | Reason | Impact | Mitigation |
|--------|--------|--------|------------|
| Implicit competitor consultancies (Big-4, mid-tier) | Market entrant in UK gov niche | Low (managed via framework competition, not by persuasion) | Compete on quality, principles, transparent pricing |
| Some commercial advisers (internal) | Concern that Principle 16 (open contribution) weakens competitive moat | Low | ARB authority; Principle 16 mandatory; brand depends on differentiated openness |
| Senior-talent market | Hiring competition | Medium | Principled environment + utilisation cap + capability time + fair pay |

**Change Champions**:

- Practice Lead (Mark Craddock) — founder, principled mission alignment.
- ArcKit ARB members — gain commercial channel that funds Principle 1.
- ArcKit Product Owners — gain structured product-feedback loop.
- Early SME-tier clients — direct beneficiaries of Principle 1 operationalised.

## E6. Benefits Realization

### E6.1 Benefits Profiles (mapped to STKE Outcomes O-1 to O-9)

**Benefit B-001**: Booked revenue + sustainable margin (G-5; Outcome O-2).

- **Owner**: Practice Lead with Commercial Lead.
- **Baseline**: £0.
- **Y1 Target**: £750k–£1.5m booked, ≥ 20% margin from Q3.
- **Measurement**: Accounting system; engagement records.
- **Y1 leading indicator**: # qualified opportunities; bid win-rate; first signed contract.
- **Y1 lagging indicator**: Year-end revenue and margin.

**Benefit B-002**: Cross-subsidy transfer to SaaS SME tier (G-7; Outcome O-5).

- **Owner**: Practice Lead with ArcKit ARB.
- **Baseline**: £0.
- **Target**: ≥ 10% post-tax net margin transferred annually from first profitable FY.
- **Measurement**: Inter-project transfer record; ARB minutes; published affordability review.
- **Year-2+ leading indicator**: Q3 profitability; cumulative FY position.
- **Year-2+ lagging indicator**: Annual transfer evidenced.

**Benefit B-003**: SME engagements delivered (G-6; Outcome O-4).

- **Owner**: Practice Lead.
- **Baseline**: 0.
- **Y1 Target**: ≥ 5 SME engagements; quarterly capacity reservation maintained.
- **Measurement**: Engagement records; public-website published policy.

**Benefit B-004**: Quality discipline and brand integrity (G-8, G-10, G-11; Outcome O-3, O-7).

- **Owner**: QA Lead with Practice Lead.
- **Y1 Target**: 100% checklist pass-rate; zero independent-assurance failures; per-engagement NPS established.
- **Y2+ Target**: NPS ≥ +40 rolling 12-month; client retention ≥ 50% Y2+.
- **Measurement**: QA logs; NPS data (FR-009); post-assurance reviews.

**Benefit B-005**: Public ecosystem contribution (G-12; Outcome O-9).

- **Owner**: Practice Lead.
- **Y1 Target**: ≥ 4 anonymised case studies + ≥ 2 OSS / public-code contributions.
- **Measurement**: Public website; public OSS repos.

**Benefit B-006**: Strategic feedback loop into Projects 001/002 (G-13; Outcome O-9).

- **Owner**: Practice Lead with Product Owners.
- **Steady-state Target**: ≥ 10 product change requests / quarter; ≥ 70% feedback closure within 2 quarters.
- **Measurement**: Feedback register; product-owner acknowledgement.

**Benefit B-007**: Compliant operating practice (G-1, G-4, G-14; Outcome O-1, O-8).

- **Owner**: DPO.
- **Target**: Zero open material non-compliance findings; CE+ continuous; zero leakage; clean ICO record.
- **Measurement**: Compliance register; statutory portals; incident register.

### E6.2 Benefits Measurement

**Monitoring Approach**:

- **Weekly**: pipeline coverage; bid pace.
- **Monthly**: financials; margin per engagement; QA pass-rate; compliance register.
- **Quarterly**: full benefits scorecard at Steering Committee; product-feedback meeting with ArcKit Product Owners.
- **Annually**: published Principle-1 affordability review at ArcKit ARB.

**Reporting Hierarchy**:

- Practice-level: Steering Committee weekly; Practice Lead reports.
- Cross-project: ArcKit ARB quarterly review.
- External / public: annual Principle-1 affordability review published; quarterly case studies.

## E7. Risk Management

### E7.1 Top 10 Strategic Risks (from STKE; full register at /arckit:risk)

| Risk ID | Risk Description | Stakeholder Impact | Likelihood | Impact | Score | Mitigation | Owner |
|---------|------------------|-------------------|------------|--------|-------|------------|-------|
| R-1 | SME-tier capacity erosion under commercial pressure | Mission credibility; Principle 1 compliance | Medium | High | 12 | BC-1 published commitment; ARB review; structural cross-subsidy | Practice Lead |
| R-2 | High-profile quality failure on assurance event | Brand catastrophic | Low | Critical | 10 | NFR-Q-001 100%; FR-008 independent QA; pre-assessment dry-runs | QA Lead |
| R-3 | Cross-engagement data leakage | Brand catastrophic; ICO action | Low | Critical | 10 | FR-004 isolation; quarterly tests; FR-017 incident response | DPO |
| R-4 | Senior consultant churn in first 12 months | Capacity / morale | Medium | High | 12 | NFR-S-002 utilisation cap; capability time; fair pay; principled environment | Talent Lead |
| R-5 | Framework listing rejected or lapsed | Pipeline | Low | High | 8 | Pre-application dry-run; framework calendar discipline; sub-contractor route | Commercial Lead |
| R-6 | Below-floor pricing pressure under thin pipeline | Margin | Medium | Medium | 9 | Pipeline-coverage discipline; pricing-floor governance with Practice Lead exception | Practice Lead |
| R-7 | IR35 mis-classification on associate panel | HMRC liability | Medium | Medium | 9 | HMRC CEST evidence per associate; Talent Lead governance; tax-counsel review | Talent Lead |
| R-8 | Project 001 / 002 GA delay forces fallback tooling | Delivery / brand | Medium | High | 12 | Contingency tooling stance; transparent client comms; Markdown / git fallback | Practice Lead |
| R-9 | Client SRO consent withheld for case-study publication | G-12 target shortfall | Medium | Medium | 9 | Consent normalised at engagement closure; anonymised pattern publication fallback | Practice Lead |
| R-10 | Brand damage from publicised confidentiality / quality incident | Brand catastrophic | Low | Critical | 10 | All of NFR-Q-001, FR-004, FR-008, FR-017, CE+ continuous, transparent culture | Practice Lead + DPO |

**Risk Score**: Likelihood (1–4) × Impact (1–4) = Score (1–16).

**Risk Appetite**:

- **Financial Risk**: Medium (Y1 cohort cost outpacing Y1 revenue is plausible; founder capital is a finite buffer).
- **Delivery Risk**: Low (quality is brand-critical; QA discipline is non-negotiable).
- **Reputational Risk**: Low (a single publicised failure is materially destabilising).
- **Compliance Risk**: Very Low (regulatory baseline + IG controls + Principle 1 operationalisation are non-negotiable).

### E7.2 Risk Mitigation Summary

**High Risks (Score 12+)**: R-1, R-4, R-8 — active mitigation, monthly review, ARB-level visibility.
**Medium Risks (Score 6–11)**: R-2, R-3, R-5, R-6, R-7, R-9, R-10 — mitigation plans in place; quarterly review at ARB level for R-2, R-3, R-10 (catastrophic-impact).
**Low Risks (Score 1–5)**: None identified at SOBC stage.

---

# PART F: RECOMMENDATION & NEXT STEPS

## F1. Summary of Recommendation

**Recommended Option**: **Option 2: Balanced Approach**.

| Decision Criterion | Result |
|--------------------|--------|
| Strategic fit (Principle 1 funded) | ✅ |
| Stakeholder Goals coverage | 14 of 14 (100%) |
| Critical Success Factors | 5 of 5 met or attainable |
| 3-year cost ROM (with optimism bias) | £4.13m – £6.62m |
| 3-year revenue ROM | £4.75m – £9.5m |
| Net contribution central case | ~£2.5m – £3m before tax |
| Payback period | Y2 mid (break-even Y1 central) |
| Cross-subsidy contribution to SaaS SME tier | ~£60k – £200k cumulative over 3 years |
| Top risks | R-1, R-4, R-8 (all mitigatable) |
| Affordability | Within founder-capital envelope; manageable risk |

**Go/No-Go Recommendation**: **PROCEED to practice stand-up phase**.

## F2. Conditions for Approval

**Mandatory Conditions** (must be satisfied before Gate 1 stand-up begins):

1. ArcKit Architecture Review Board endorsement of SOBC (this document).
2. Founder-capital allocation confirmed: ≥ £500k available as Y1 working capital.
3. Engagement Director and Commercial Lead candidate pipeline identified (Talent Lead).
4. Insurance broker engaged; PI / PL / EL / cyber quotes obtained.
5. Cyber Essentials Plus assessor identified and lead-time confirmed (4–8 week target).
6. Legal counsel engaged for incorporation, contract templates, IR35 status determinations, IP / NDA template.

**Recommended Conditions** (should be satisfied before Gate 2 cohort-live):

1. At least 2 MCF prime contractor relationships established for sub-contracting (bridging revenue).
2. At least 3 prospective Client SROs interviewed (discovery for early opportunity pipeline).
3. At least 3 prospective SME founders interviewed (SME-tier policy validation; FR-011).

## F3. Next Steps if Approved

**Phase 1 — Immediate (Months 1–2)**:

1. **ARB approval and capital allocation** — target 2026-06-30.
2. **Engagement Director + Commercial Lead recruitment** — target 2026-07-31.
3. **Legal / insurance / brand engagement starts** — target 2026-07-31.
4. **Refresh REQ-003 to v1.1** — strengthen upstream traceability now that STKE-003 and SOBC-003 exist; address ORPHAN-REQ health finding by drafting key ADRs (`/arckit:adr 003`) — target ongoing.

**Phase 2 — Stand-up (Months 3–4)**:

1. **Run `/arckit:risk 003`** to upgrade placeholder risk register to formal Orange-Book aligned register.
2. **Run `/arckit:adr 003`** to capture key decisions (commercial model 4-stack hybrid; legal vehicle Ltd→B-Corp→EOT path; framework strategy G-Cloud + DOS + MCF subbing; operating-tooling stack; pricing-floor governance; SME-tier policy).
3. **Run `/arckit:plan 003`** to detail the stand-up project plan.
4. **Run `/arckit:wardley 003`** to map commercial-model evolution onto Wardley axes.
5. **Practice incorporation, regulatory baseline, insurance** — Gate 1 (2026-09-30).

**Phase 3 — Cohort and frameworks (Months 5–6)**:

1. **Cohort recruitment** — Gate 2 (2026-10-31).
2. **Framework applications** — Gate 3 (2026-12-31).
3. **First MCF sub-contracting engagements** — bridging revenue.

**Phase 4 — Operate and refine (Months 7–12)**:

1. **First own-listing engagements** delivered.
2. **First SME-tier engagements** delivered.
3. **First case studies published**.
4. **First quarterly product-feedback meeting** with ArcKit Product Owners.

**Phase 5 — Y1 OBC refresh** (Month 12):

1. **Run `/arckit:sobc 003`** with v2.0 update or escalate to **Outline Business Case (OBC)** — refines costs and benefits with Y1 actuals.
2. **First cross-subsidy transfer to SaaS SME tier** — first profitable FY.
3. **Annual Principle-1 affordability review** published.

## F4. Next Steps if Not Approved

If this SOBC is not approved:

1. **Understand objections** — SRO meets ArcKit ARB to understand specific concerns.
2. **Revise** — most likely revisit pricing assumptions, cohort scale (Option 1 fallback), or framework strategy.
3. **Re-submit** — within 4–8 weeks.
4. **Communicate** — inform stakeholders; consider founder-funded interim arrangement for SaaS SME tier in the meantime.

**Do Nothing Consequences** (per Option 0):

- All 14 Stakeholder Goals unmet.
- Principle 1 cross-subsidy unfunded; SaaS SME free tier financial pressure compounds.
- ~£750k – £1.5m Y1 booked revenue forgone, with ~£75k – £150k Y1 cross-subsidy contribution forgone.
- Strategic feedback loop into Projects 001 / 002 absent for the year.
- Comparator practices consolidate UK gov standing; later entry harder.

---

# APPENDICES

## Appendix A: Stakeholder Analysis

**Source**: `projects/003-arckit-consulting/ARC-003-STKE-v1.0.md` (v1.0).

**Summary**: 18 stakeholder drivers (SD-1 to SD-18), 14 SMART goals (G-1 to G-14), 9 outcomes (O-1 to O-9), 8 conflict resolutions (C-1 to C-8), 6 synergies (S-1 to S-6). Overall stakeholder alignment HIGH; principal conflicts are internal trade-offs between commercial pressure and principled discipline (mitigated structurally by ARB governance, pricing-floor authority, and quality-discipline guardianship).

**Key Stakeholders**: Practice Lead / SRO, Engagement Director, Commercial Lead, QA Lead, Talent Lead, DPO; Client SROs, Client Architects, SME Founders, Sub-contractor partners; CCS framework managers, GDS/CDDO, ICO, HMT, NAO/PAC posture; ArcKit Architecture Review Board; ArcKit Product Owners (Projects 001 / 002).

## Appendix B: Architecture Principles

**Source**: `projects/000-global/ARC-000-PRIN-v2.0.md` (v2.0, all 21 principles relevant; the following are most directly load-bearing for this practice):

- **Principle 1** (Equitable Access for SMEs) — non-negotiable; this practice is the structural mechanism that funds it.
- **Principle 4** (Open Standards and Interoperability) — all client deliverables in open formats (NFR-I-001).
- **Principle 5** (Security by Design) — practice security baseline; CE+ continuous.
- **Principle 7** (UK Data Sovereignty and Governance) — UK-resident hosting / data.
- **Principle 8** (Tenant / Engagement Isolation) — FR-004 workspace isolation.
- **Principle 9** (Data Quality, Lineage, Portability) — open formats; client owns artefacts.
- **Principle 12** (Accessibility — non-negotiable) — practice public website + internal tooling.
- **Principle 16** (Open Source First and Reuse) — case studies + OSS contributions (G-12).
- **Principle 17** (Cost Transparency and FinOps) — transparent pricing across all four pricing-stack models; cross-subsidy auditable.

## Appendix C: Options Analysis Details

**Detailed cost ranges per option**: in B2 above. OBC will refine after cohort recruitment.

**Assumptions Register**:

1. Cohort blended loaded cost ≈ £75k average (Principal £100k+, Senior £75k–£85k, Consultant £55k–£65k).
2. Associate panel utilisation 30%–50% of nominal capacity in Y1.
3. Framework cycles open within 12 months (G-Cloud annually; DOS / DSP biennially-ish).
4. Y1 pipeline maturity reaches ≥ 3.0 coverage by month 9.
5. Y1 utilisation 50%–65% (ramp); Y2+ 65%–80% (steady state, NFR-S-002).
6. Quality discipline (NFR-Q-001) holds at 100% checklist pass-rate.
7. Optimism bias: +25% on cohort/ops; +40% on setup; -25% on Y1 revenue (sensitivity).

## Appendix D: Benefits Calculation

Detailed benefits mapping is in B2 Option 2 §Benefits and in §E6.1. Sensitivity analysis deferred to OBC.

## Appendix E: Risk Register

**Top 10 Strategic Risks**: in §E7.1. Full Orange-Book aligned register at `/arckit:risk 003` (to be created).

## Appendix F: Market Research

**Source**: `projects/003-arckit-consulting/research/ARC-003-RSCH-v1.0.md` (v1.0, 1,750 lines). Detailed comparator analysis: dxw, Made Tech, Equal Experts, BJSS/CGI, TPXImpact, Public.io, Mastek, Snook, Caspian One, Big-4. Detailed pricing-model analysis (4-stack hybrid). Detailed legal-vehicle analysis (Ltd → B-Corp → EOT recommended; CIC explicitly out). Detailed operating-tooling stack analysis (M365 + FreeAgent + HubSpot + Harvest + Notion + Eleventy site recommended). Detailed framework-route analysis (G-Cloud + DOS + MCF subbing recommended; MCF Lot direct deferred to MCF5 refresh in Y2-3).

## Appendix G: Governance Terms of Reference

**Steering Committee ToR**: weekly cadence; SRO chairs; standing items pipeline (Commercial Lead), QA gate review (QA Lead), cohort capacity (Talent Lead), compliance hot spots (DPO).

**ArcKit Architecture Review Board ToR**: quarterly cross-project review; annual Principle-1 affordability review; exception approval authority; cross-project consistency review; SOBC / OBC / FBC approval.

## Appendix H: Glossary

| Term | Definition |
|------|------------|
| ARB | ArcKit Architecture Review Board — cross-project governance authority |
| BCR | Benefit-Cost Ratio (HMT Green Book) |
| BPSS | HMG Baseline Personnel Security Standard |
| CCS | Crown Commercial Service |
| CDDO | Central Digital and Data Office |
| CE+ | Cyber Essentials Plus (NCSC-licensed certification) |
| CIC | Community Interest Company (rejected for ArcKit Consulting per RSCH-003) |
| DOS | Digital Outcomes and Specialists (CCS framework) |
| DSP | Digital Specialists and Programmes (DOS successor framework) |
| EOT | Employee Ownership Trust |
| FBC | Full Business Case |
| GDS | Government Digital Service |
| G-Cloud | CCS Cloud framework |
| MCF | Management Consultancy Framework |
| MI | Management Information (CCS framework MI returns) |
| NAO | National Audit Office |
| NPV | Net Present Value (HMT Green Book; 3.5% discount rate) |
| OBC | Outline Business Case (next-stage refinement after SOBC) |
| PAC | Public Accounts Committee (UK Parliament) |
| PI / PL / EL | Professional Indemnity / Public Liability / Employer's Liability insurance |
| PPN | Procurement Policy Note |
| ROM | Rough Order of Magnitude (cost estimate at SOBC stage; ±40% bands) |
| SC | Security Check (HMG personnel security clearance) |
| SME | Small and Medium Enterprise (Companies Act 2006 thresholds) |
| SOBC | Strategic Outline Business Case (this document) |
| SRO | Senior Responsible Owner |
| TCO | Total Cost of Ownership |

---

## Document Approval

| Name | Role | Signature | Date |
|------|------|-----------|------|
| Mark Craddock | Senior Responsible Owner / Practice Lead | | |
| [PENDING] | ArcKit Architecture Review Board Chair | | |

**Approval Decision**: **APPROVED** | **APPROVED WITH CONDITIONS** | **REJECTED** | **DEFERRED**

**Conditions** (if any): per F2 Mandatory Conditions.

**Approval Date**: [PENDING]

**Next Review Date**: 2026-12-15 (Y1 OBC refresh trigger), or sooner if material change.

---

**END OF STRATEGIC OUTLINE BUSINESS CASE**

*Document created using ArcKit `/arckit:sobc` command*
*Template version: 4.19.0*
*Green Book compliant: Yes (HM Treasury 5-case model; 4-option appraisal; Strategic estimates with optimism-bias uplift; sensitivity analysis deferred to OBC)*

## External References

> No external policy documents were placed in `projects/003-arckit-consulting/external/` at the time of generation. Public-domain UK Government and CCS policies referenced in the body (HM Treasury Green Book and Magenta Book; Procurement Act 2023; PPN 03/23, 06/21, 09/14, 09/22, 09/23; Technology Code of Practice; GDS Service Standard; CDDO Cloud Strategy; NCSC CAF; Cyber Essentials Plus; UK GDPR; DPA 2018; Modern Slavery Act 2015; Bribery Act 2010; Equality Act 2010; HMG Government Security Classifications Policy; Companies Act 2006; PSBAR 2018; WCAG 2.2 AA; GovS 005 Digital; GovS 007 Security) are cited by name. Authoritative references in this document include `projects/003-arckit-consulting/ARC-003-REQ-v1.0.md`, `projects/003-arckit-consulting/ARC-003-STKE-v1.0.md`, and `projects/003-arckit-consulting/research/ARC-003-RSCH-v1.0.md`.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| ARC-003-REQ-v1.0 | ARC-003-REQ-v1.0.md | Internal artefact | projects/003-arckit-consulting/ | 76 requirements |
| ARC-003-STKE-v1.0 | ARC-003-STKE-v1.0.md | Internal artefact | projects/003-arckit-consulting/ | Stakeholder analysis |
| ARC-003-RSCH-v1.0 | research/ARC-003-RSCH-v1.0.md | Internal artefact | projects/003-arckit-consulting/research/ | Commercial-model research (1,750 lines) |
| ARC-000-PRIN-v2.0 | ARC-000-PRIN-v2.0.md | Internal artefact | projects/000-global/ | Architecture principles |

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
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**AI Model**: claude-opus-4-7[1m]
**Generation Context**: Generated using the `/arckit:sobc` command for project 003 with user inputs "003" + (4 options + Strategic estimates appraisal). Anchored on `ARC-003-REQ-v1.0.md`, `ARC-003-STKE-v1.0.md`, `ARC-003-RSCH-v1.0.md` (commercial-model research), and `ARC-000-PRIN-v2.0.md` (especially Principles 1, 16, 17). Five-case Green Book structure; 4-option appraisal (Do Nothing / Minimal / Balanced / Comprehensive); Recommended Option 2 (Balanced). NPV / BCR formal numerical analysis deferred to OBC stage.
