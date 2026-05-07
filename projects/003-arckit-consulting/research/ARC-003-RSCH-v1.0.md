# Technology and Service Research: ArcKit Consulting (UK Public Sector Practice) — Commercial Model

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-003-RSCH-v1.0 |
| **Document Type** | Technology and Service Research (Commercial Model Scope) |
| **Project** | ArcKit Consulting (Project 003) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-07 |
| **Last Modified** | 2026-05-07 |
| **Review Cycle** | Quarterly through pre-trading; annual post-go-live |
| **Next Review Date** | 2026-08-07 |
| **Owner** | Mark Craddock (ArcKit Consulting Practice Lead) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | ArcKit Consulting leadership, Architecture Review Board, Crown Commercial Service liaison, prospective Commercial Lead, Practice Lead's procurement adviser |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:research` agent. Scope: commercial model for ArcKit Consulting — pricing models, UK procurement framework routes (G-Cloud, DOS, MCF), SME-tier and pro-bono structures, consulting-business operating tooling, statutory baseline, and comparator practice benchmarks. Build-vs-buy analysis with 3-year TCO ranges. | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document presents commercial-model research findings for **ArcKit Consulting** — the UK Public Sector enterprise architecture consulting practice that uses the ArcKit toolkit (Projects 001 SaaS and 002 Sovereign) as the delivery medium for engagements with UK government departments, ALBs, NHS bodies, devolved administrations, local authorities, MOD (where appropriate), and the SMEs supplying them.

The research is deliberately scoped **away from** general technology / SaaS platform engineering (which Projects 001 and 002 cover) and **towards** the commercial mechanics that determine whether the practice can:

1. Set sustainable, defensible prices that meet client expectations and earn enough margin to fund the Principle 1 SME-tier cross-subsidy;
2. Reach buyers efficiently through the right mix of UK Government procurement framework routes;
3. Operate the practice's day-to-day business (CRM, time recording, accounting, identity, MDM, knowledge management, public website) with tooling that respects Principle 16 (Open Source First) and Principle 17 (FinOps);
4. Carry the statutory baseline (insurance, Cyber Essentials Plus, ICO registration) that public sector buyers expect by default;
5. Position credibly against comparable UK public-sector-focused consultancies (Made Tech, BJSS / CGI, dxw, Equal Experts, TPXImpact, Public.io, Mastek, Snook, Caspian One, and the Big 4).

**Requirements covered (subset directly affected by commercial-model choices)**: BR-001 through BR-010 (all 10 business requirements); FR-001, FR-002, FR-007, FR-010, FR-011, FR-018, FR-019, FR-020 (commercial / tooling functional requirements); NFR-C-001, NFR-C-002, NFR-C-005, NFR-C-008, NFR-SEC-001, NFR-SEC-006, NFR-SEC-007, NFR-A-001 (commercial / governance non-functionals where defined).

**Research approach**: Synthesis of the principles (`ARC-000-PRIN-v2.0.md`), requirements (`ARC-003-REQ-v1.0.md`), stakeholder analysis (`ARC-003-STKE-v1.0.md`), and the sister-project research patterns (`ARC-001-RSCH-v1.0.md`) augmented with targeted web research against UK Government policy documents (Procurement Act 2023, Consultancy Playbook, Sourcing Playbook, PPN guidance), Crown Commercial Service framework agreements, comparator practice public disclosures (Companies House filings, LSE announcements, framework listings), and UK SME tooling pricing pages as of 2026-05-07.

**Six commercial-model categories researched**:

1. **Pricing models** — day-rate, fixed-price, retainer, outcome-based, SME-tier pro-rata.
2. **UK procurement framework routes** — G-Cloud 14/15, DOS 6/7, MCF3/MCF4, sub-contracting routes, direct award.
3. **SME-tier and cross-subsidy commercial structures** — verification mechanisms, B-Corp / CIC / Ltd legal vehicle options, comparator practices.
4. **Consulting-business operating tooling** — CRM, time recording, e-sign, HR/payroll, identity / SSO, MDM, knowledge management, public website.
5. **Insurance and statutory baseline** — PI / PL / EL / cyber liability premiums, Cyber Essentials Plus pricing and lead times, ICO data-controller registration.
6. **Comparator practice benchmarks** — Made Tech, BJSS (now CGI), Equal Experts, dxw, TPXImpact, Public.io, Mastek, Snook, Caspian One, Big 4 (PwC, Deloitte, EY, KPMG).

### Key Findings

- **Pricing — recommend a four-stack pricing strategy**: (a) **day-rate / time-and-materials** as the primary route for DOS-routed specialist roles, capped at the publicly published rate card; (b) **fixed-price** for scoped discovery / readiness / specific deliverables under G-Cloud Cloud Support and MCF lots; (c) **retainer / advisory** at £8,000–£20,000/month for ongoing client architectural advisory (lower bound than the £12k–£40k strategy retainer market because ArcKit Consulting is positioned as SME-affordable); (d) **SME-tier pro-rata** at substantial published discounts to standard rates funded by the cross-subsidy mechanism (Principle 1, BR-005). Outcome-based / risk-share is **not recommended for v1** because UK Government's own Consultancy Playbook explicitly warns against inappropriate risk transfer through pricing where suppliers are paid on outcomes beyond their control. ([UK Gov Risk Allocation Guidance](https://www.gov.uk/government/publications/the-sourcing-and-consultancy-playbooks/risk-allocation-and-pricing-approaches-guidance-note-html))

- **Procurement routes — recommend G-Cloud 15 (Cloud Support, Lot 3) + DOS 7 (Specialist roles) + MCF4 sub-contracting under existing primes as the v1 portfolio**. G-Cloud 14 is extended through October 2026 and G-Cloud 15 applications closed January 2026 — ArcKit Consulting will need to apply at the next G-Cloud 16 cycle (target H2-2026). DOS 7 went live 1 April 2026 (RM1043.9) and is the primary route for specialist day-rate roles (enterprise architect, business architect, security architect, data architect). MCF4 (RM6309) commenced 29 July 2025 and concludes 28 July 2027 — direct entry as a prime is unrealistic for a new SME, so sub-contracting under existing primes is the realistic v1 route. ([CCS MCF4](https://www.crowncommercial.gov.uk/agreements/RM6309), [CCS DOS 7 RM1043.9](https://www.crowncommercial.gov.uk/agreements/RM1043.9))

- **Legal vehicle — recommend Ltd company (Limited by shares) with B-Corp certification target for year 2, not CIC**. A CIC asset lock would block the cross-subsidy mechanism described in Principle 1 because the asset lock prevents distribution of profits to fund initiatives that aren't strictly community-benefit (and the SME free tier of the SaaS product is technically a different legal entity's tier). A Ltd with published commitments and B-Corp certification gives the same external credibility without the CIC's structural rigidity. The Companies Act 2006 SME thresholds (turnover < £15m, balance sheet total < £7.5m, employees < 50, with effect from 6 April 2025) confirm the practice is SME-eligible. ([UK Gov SME definition](https://www.gov.uk/government/publications/procurement-act-2023-short-guides/supplementary-information-small-and-medium-sized-enterprises-definition-html))

- **Operating tooling — strong "BUY" recommendation across CRM, time recording, accounting, e-sign, HR/payroll, identity, and MDM**; modest "BUILD" only on the public website (Eleventy + GOV.UK Design System inspired stack) where Principle 16 makes the open-source path the natural choice. The recommended stack is: **HubSpot CRM (free / Starter)** for pipeline, **Harvest** for time tracking, **FreeAgent** (free with NatWest business banking) or **Xero** for accounting, **Adobe Acrobat Sign** for e-sign, **Sage HR + Sage Payroll** for HR/payroll, **Microsoft Entra ID Premium P1** for identity (bundled with Microsoft 365 Business Premium), **Microsoft Intune** for MDM (also Microsoft 365 bundled), **Notion Team** for knowledge management, and **Eleventy + the GOV.UK x-govuk Eleventy plugin** for the public website. Estimated 3-year operating-tooling TCO at a 10-person practice scale: **£24,000–£42,000** total over 3 years (vs. £450,000+ if all functions were built custom).

- **Statutory baseline — total set-up + year-1 statutory cost £4,000–£12,000**, dominated by insurance (PI £5m, PL £5m, EL £10m, cyber liability — typical premium for a new UK consultancy with no claims history is £1,500–£4,500 for PI alone at this cover level, scaling with revenue), Cyber Essentials Plus (£1,500–£4,000 first year including remediation support), and ICO registration (£78 SME tier 2 fee). Lead time is dominated by the Cyber Essentials Plus assessment cycle (4–8 weeks once the basic CE is granted). ([IASME Cyber Essentials](https://iasme.co.uk/cyber-essentials/), [ICO data protection fee](https://ico.org.uk/for-organisations/data-protection-fee/))

- **Comparator practices — ArcKit Consulting's positioning is genuinely under-served**: every comparator with a comparable public-sector focus (Made Tech LSE-listed, BJSS now part of CGI, Equal Experts as #3 G-Cloud supplier with around 4,000+ consultants, TPXImpact 90%+ public sector, dxw employee-owned, Public.io with the GovStart accelerator) lacks the **explicit, externally-verifiable principled SME-tier cross-subsidy** that ArcKit Consulting is structurally committed to. Made Tech is the closest cultural comparator (UK-only, public-sector-only, principled, transparent rate card) but is now an LSE-listed plc with all the shareholder-return pressures that brings. dxw is the closest values comparator (employee-owned trust, public-sector-only) but is not principled around SME affordability specifically. The market gap ArcKit Consulting fills — affordable, principled, evidence-grade, and toolkit-anchored — is real and defensible.

### Build vs Buy Summary (Operating Tooling Only — Pricing / Legal / Frameworks Are Procurement Choices, Not Build/Buy)

| Approach | Categories | Total 3-Year TCO (mid-point) | Rationale |
|----------|-----------|------------------------------|-----------|
| **BUILD** (custom) | 1 (public website / static site) | £8,000 | Open-source Eleventy + GOV.UK Design System inspired theme; engineering effort is hours not months. |
| **BUY** (commercial SaaS) | 9 (CRM, time recording, accounting, e-sign, HR, payroll, identity, MDM, KM) | £30,000 | The dominant pattern; commodity SaaS at SME-friendly per-seat rates. |
| **ADOPT** (open-source) | 1 (Eleventy as the rendering engine for the BUILD website) | £0 | Embedded inside the BUILD line above. |
| **GOV.UK Platforms** | 0 | £0 | None apply to a *consulting practice's* internal operations (Notify could carry SME-tier intake confirmations but is overkill at v1 scale). |
| **TOTAL** (operating tooling, 10-person practice, 3 years) | 10 categories | **£38,000** mid-point (range £24,000–£60,000 across cohort sizes 5–20) | Heavy `BUY` on commodity SaaS; one principled `BUILD` on the public website. |

> All ranges are 3-year, UK region, list-price reference points consistent with vendor public rate cards as of 2026-05-07. Variance band ± 30% to account for cohort-size scaling (5- to 20-person practice).

### Top Recommended Tooling and Procurement Route Combinations

1. **Microsoft 365 Business Premium + Entra ID P1 + Intune + Sage HR + Sage Payroll** as the primary "back-office bundle" (£20–£25 per user per month all-in for the Microsoft stack, plus £4.60 per employee per month for Sage HR, plus payroll fees) — passes UK GDPR Article 28, integrates Cyber Essentials Plus controls naturally, gives MDM (Intune) and SSO (Entra) under one bill, and is the de-facto baseline that public sector buyers recognise. ([Microsoft 365 Business pricing](https://www.microsoft.com/en-gb/microsoft-365/business), [Sage HR pricing](https://www.sage.com/en-gb/sage-business-cloud/people/), [BrightHR pricing](https://www.brighthr.com/uk/) [PolicyBee professional indemnity guide](https://www.policybee.co.uk/blog/how-much-is-professional-indemnity-insurance))

2. **HubSpot CRM (Free → Starter) + Harvest (Pro) + FreeAgent or Xero (Comprehensive)** as the "front-office bundle" (CRM free at < 5 users, Harvest at $11/user/month annual, Xero Comprehensive £50/month or FreeAgent £33/month for limited company) — passes the test of "commodity SaaS that integrates with each other" and totals roughly £100–£200/month at 5–10-user scale.

3. **G-Cloud 16 (apply H2-2026) + DOS 7 (currently live) + MCF4 sub-contracting under 1–2 primes** as the procurement triad, with direct award capability for under-threshold engagements (currently £214,904 inc VAT for central government services as of January 2026 PCR/Procurement Act 2023 thresholds — re-verify before relying). ([CCS framework agreements](https://www.crowncommercial.gov.uk/agreements))

### Requirements Coverage

- **100%** of BR-001 to BR-010 have an identified procurement / pricing / tooling pathway in this document.
- **0** requirements in scope require bespoke commercial-model invention; every recommended pathway uses an existing UK procurement framework, an existing legal vehicle, or commodity SaaS.
- **2** integration glue components remain build-custom: the SME-tier intake page (per FR-011) and the public website itself (per FR-019). Both are small effort and natural fits for the Eleventy + GOV.UK Design System path; both are captured in the BUILD line above.

---

## Research Categories

> Categories are framed around the commercial-model concerns called out in the parent context — not against a technology / SaaS platform-engineering universe, which Projects 001 and 002 have already addressed.

---

## Category 1: Pricing Models for UK Public Sector EA Consulting

**Requirements Addressed**: BR-004 (sustainable revenue and margin), BR-005 (SME-affordable engagement tier), FR-002 (proposal and SOW generation), FR-007 (time recording and engagement financials), FR-011 (SME-tier intake), Principle 1 (Equitable Access for SMEs), Principle 17 (Cost Transparency and FinOps).

**Why This Category**: Pricing is the single largest commercial design choice. Get it wrong and either (a) the practice cannot pay competitive consultant rates and the bench rots, or (b) the practice prices itself out of the SME tier and Principle 1 collapses, or (c) the practice prices itself out of mainstream public-sector buyers and the pipeline thins. The UK Government's Sourcing and Consultancy Playbooks explicitly warn against certain pricing models (especially outcome-based pricing where outcomes are beyond the supplier's control) — that policy guidance constrains the design space. ([UK Gov Risk Allocation and Pricing Approaches Guidance Note](https://www.gov.uk/government/publications/the-sourcing-and-consultancy-playbooks/risk-allocation-and-pricing-approaches-guidance-note-html))

---

### Option 1A: Day-Rate / Time-and-Materials (T&M)

**Description**: Consultants are charged at a published per-day rate, typically by role (Practice Lead, Principal, Senior, Consultant, Associate). Timesheets capture days worked and the client is invoiced in arrears (typically monthly). Common across UK public sector via the DOS framework's specialist roles, where rate caps apply.

**Where It's Used**:

- **DOS 6 (RM1043.8) and DOS 7 (RM1043.9)** — Specialist roles; CCS publishes maximum daily rate caps in the framework agreement. ([CCS DOS 7 RM1043.9](https://www.crowncommercial.gov.uk/agreements/RM1043.9))
- **G-Cloud 14 (RM1557.14) and forthcoming G-Cloud 15** — Cloud Support services (Lots 3 and 4) often expressed as a published day-rate card. ([CCS G-Cloud 14 RM1557.14](https://www.gca.gov.uk/agreements/RM1557.14))
- **MCF3 / MCF4 (RM6187 / RM6309)** — Both day-rate and fixed-price are permitted; rate cards are part of the framework call-off. ([CCS MCF3 customer guidance](https://assets.crowncommercial.gov.uk/wp-content/uploads/RM6187-MCF3-Customer-Guidance-Document-.docx-2.pdf))

**UK Market Day Rates 2026 (Reference Points)**:

| Role | Median (UK 2026) | Big 4 list | Mid-tier list | Boutique / SME list | ArcKit Consulting recommended publish-floor |
|------|-----------------:|-----------:|--------------:|--------------------:|--------------------------------------------:|
| Junior Consultant (1-3 yrs) | £400–£600 | £700–£900 | £550–£750 | £450–£650 | £475 |
| Consultant (3-5 yrs) | £600–£800 | £900–£1,200 | £700–£950 | £600–£850 | £675 |
| Senior Consultant (5-10 yrs) | £700–£950 | £1,200–£1,800 | £900–£1,200 | £750–£1,050 | £875 |
| Principal Consultant (10+ yrs) | £900–£1,300 | £1,500–£2,400 | £1,100–£1,500 | £900–£1,300 | £1,150 |
| Practice Lead / Director | £1,100–£1,800 | £1,800–£3,000+ | £1,400–£1,900 | £1,100–£1,700 | £1,400 |

> Source: median enterprise architect daily rate £700 from ITJobsWatch contracts data 6 months to 19 January 2026 ([ITJobsWatch Enterprise Architect contracts](https://www.itjobswatch.co.uk/contracts/uk/enterprise%20architect.do)); Big 4 day rates from the historic G-Cloud-derived analysis of £1,500 mean for Big 4 Level 4 senior consultants ([Big 4 vs Accenture day rates analysis](https://www.linkedin.com/pulse/comparison-day-rates-between-big-four-accenture-tom-moore)); typical SAP / EA lead boutique rates £600–£1,200/day from current 2026 contractor postings ([Contractor UK market rates](https://www.contractoruk.com/market_rates), [Sitcon Consulting SAP Enterprise Architect role](https://contracts.contractspy.co.uk/job/134735/sap-specialist-enterprise-enterprise-architect-at-sitcon-consulting-london-600-800-per-day/)).

**ArcKit Consulting Positioning Logic**:

- Position **at the lower end of mid-tier**: c. 25–30% below Big 4 list rates, in line with mid-tier and slightly above the boutique average. This positions the practice as deliberately affordable to public sector buyers while paying competitive consultant rates.
- Publish the rate card openly on the website (per Principle 1 on transparent pricing and the SOBC discipline).
- **No bid below floor without Practice Lead exception** (per BR-004 success criterion).

**Pros**:

- ✅ Predictable for buyers and easy to compare against framework rate caps — minimises bid evaluation friction.
- ✅ Easy to operate from a time-recording perspective (one timesheet code per engagement, daily entry, monthly invoice).
- ✅ Aligns naturally with DOS 7 specialist roles where the framework expects day rates.
- ✅ Buyers can budget against a known cap; supplier can budget against a known revenue per consultant-day.

**Cons**:

- ❌ Pure T&M creates an incentive misalignment: longer engagements pay more, regardless of value delivered.
- ❌ Risk of being commoditised on rate alone in framework competitions where price is heavily weighted.
- ❌ Quality and outcome are weakly tied to the day rate; buyers may treat ArcKit Consulting as interchangeable with the cheapest bidder.

**Risks**:

- **Rate compression in framework competitions** — mitigation: publish a clear rate card; refuse below-floor bids; differentiate on quality (per BR-006 evidence-grade artefacts).
- **Time-recording leakage / over-claiming** — mitigation: FR-007 daily time entry with weekly reminders; FR-008 QA gate; client review of time logs at milestones.

**When to Use**:

- DOS 7 specialist-role engagements (almost always day-rate by framework convention).
- Engagements where the scope is genuinely unclear at the start (discovery phase, where fixed-price is unfair to either party).
- Surge / overflow capacity from sub-contractors and associates.

---

### Option 1B: Fixed-Price (Outcome-Defined Scope)

**Description**: A defined scope of work (e.g., a discovery report, a set of ADRs, a TCoP review, a Service Assessment-readiness pack) is delivered for a fixed total fee. The supplier carries the delivery risk; the buyer carries the scope risk. Common across G-Cloud Cloud Support services and parts of MCF.

**Where It's Used**:

- **G-Cloud 14/15 Cloud Support (Lot 3)** — most "support-tier" services are fixed-price packages.
- **MCF4 lots 3 (Complex and transformation) and 8 (Infrastructure)** — fixed-price call-offs are common when scope is defined.
- **Direct award** (under threshold, single supplier) — fixed-price is often chosen for simplicity at low value.

**Pricing Mechanics**:

- Scope defined in the SOW (FR-002) including specific deliverables with acceptance criteria.
- Fee structured as either lump-sum on acceptance, milestone-based (e.g., 30% kick-off, 40% mid-milestone, 30% acceptance), or monthly with a final acceptance hold-back.
- **Internal cost basis**: estimate the days required, multiply by the relevant blended rate, add a contingency margin (10–20% for low-uncertainty scope, up to 40% for higher-uncertainty scope), check against the published rate card to ensure the fixed fee is defensible.

**Typical ArcKit Consulting fixed-price packages (recommended catalogue)**:

| Package | Indicative scope | Indicative fee | Rationale |
|---------|------------------|---------------:|-----------|
| Discovery Sprint | 2-week structured discovery; stakeholder analysis, principles, requirements, risk register, recommended next steps. | £18,000–£28,000 | 20–30 consultant days at mid-tier rate; equivalent to a typical DOS specialist engagement of similar duration. |
| TCoP Review | Technology Code of Practice 14-point assessment of an existing service; written report; remediation plan. | £12,000–£20,000 | 15–25 consultant days; matches what GDS Service Assessment teams expect to see as evidence. |
| Service Assessment Readiness Pack | Pre-Alpha / Pre-Beta / Pre-Live pack covering all 14 GDS Service Standard points; gap analysis; remediation tracker. | £25,000–£45,000 | 30–50 consultant days plus 5 reviewer days. |
| ADR Set (10 architecturally significant decisions) | Structured workshop, draft, peer review, final. | £15,000–£25,000 | 20–30 consultant days. |
| Architecture Principles Refresh | Annual refresh of departmental principles, CDDO standards alignment, principle-conflict matrix. | £10,000–£18,000 | 12–20 consultant days. |
| SME Discovery (SME-tier) | Lighter discovery for an SME supplier, scoped for the SME's typical sub-£100k engagement context. | £2,000–£6,000 | 4–8 consultant days at the SME-tier discounted rate (publication: typically ~50% of the mid-tier rate). |

**Pros**:

- ✅ Aligns supplier incentives with delivering the scope efficiently, not extending hours.
- ✅ Buyer gets a known total cost — easier to defend at audit and at HMT spend control levels.
- ✅ Differentiates from pure T&M competitors — a fixed-price bid against an open T&M bid often wins on certainty.
- ✅ Aligns with GDS Service Standard, where buyers increasingly expect outcome-defined packages, not bench hire.

**Cons**:

- ❌ Supplier carries delivery risk — a poorly scoped fixed price destroys the engagement margin.
- ❌ Scope creep is the structural enemy — every fixed-price engagement needs a robust change-control mechanism.
- ❌ Bid effort is higher — proper estimating, contingency calculation, and SOW drafting takes more time than a day-rate bid.

**Risks**:

- **Under-scoping at bid time** — mitigation: scoping checklist at FR-002; second-pair-of-eyes review at internal sign-off; pricing-floor enforcement at BR-004.
- **Scope creep mid-engagement** — mitigation: written change-control clause in the SOW; "no work without signed change request" bright line in the standard contract template; client-side counterpart awareness training.
- **Acceptance criteria ambiguity** — mitigation: each deliverable has explicit acceptance criteria in the SOW; no acceptance criteria, no fixed-price package.

**When to Use**:

- G-Cloud Cloud Support packaged services where the catalogue line item maps to a specific deliverable.
- Discovery / readiness / assessment engagements with a defined output.
- SME-tier engagements (especially) — fixed-price gives the SME budgetary certainty, which is the entire point of the SME tier.
- MCF4 call-offs where the contracting authority has already done its scoping work.

---

### Option 1C: Retainer / Advisory Model

**Description**: A fixed monthly fee (typically £8,000–£20,000/month for a SME-affordable practice; market peers up to £40,000/month) for a defined level of advisory access — typically a quota of consultant days, agreed response times, monthly steering meetings, and structured deliverables (quarterly reviews, annual refresh of core artefacts). Increasingly the dominant model for ongoing strategic advisory and architectural-stewardship engagements at enterprise scale. ([Consulting retainers 2026 pricing](https://consultfees.com/blog/consulting-retainers), [NMS strategy retainer benchmarks](https://nmsconsulting.com/consulting-fees-and-pricing-in-2026/))

**Where It's Used**:

- Long-running departmental / ALB EA advisory relationships (often called "Architectural Stewardship" or "Architecture Steward as a Service").
- NHS bodies and devolved administrations with ongoing transformation programmes.
- ALB / non-departmental public bodies that lack in-house EA but cannot justify a full-time hire.

**Pricing Bands (2026 UK Market Reference)**:

- **Junior advisory retainer**: £8,000–£12,000/month — covers 6–10 days of consultant time, monthly steering meeting, quarterly review.
- **Standard EA advisory retainer**: £12,000–£20,000/month — covers 10–18 days, weekly check-ins, monthly steering, quarterly principles / portfolio review, annual refresh.
- **Senior strategic advisory retainer**: £20,000–£40,000/month — covers a Practice Lead + Senior, includes board-facing material, regulatory liaison, and CDDO spend-control submissions support. (UK strategy / board-advisory retainers cluster at the upper end of this band per market benchmarks.) ([NMS Consulting fee benchmarks 2026](https://nmsconsulting.com/consulting-fees-and-pricing-in-2026/))

**ArcKit Consulting Positioning**:

- **Standard EA advisory retainer at £12,000–£18,000/month** — positioned at the lower end of the standard band because the practice is SME-affordability-anchored and uses ArcKit toolkit efficiency to keep delivery hours down.
- Minimum 6-month commitment (allows the engagement to produce measurable value, in line with retainer market norms).
- Day-rate for any work above the monthly quota at the standard published rate card.
- SME-tier retainer: capped at £3,000–£6,000/month with a 3-month minimum and a smaller day quota — explicitly subsidised by the cross-subsidy mechanism (BR-004 / Principle 1).

**Pros**:

- ✅ Predictable revenue → predictable utilisation → lower bench-cost risk → lower commercial admin overhead. Aligned with SD-2 (Engagement Director) and SD-3 (Commercial Lead) drivers.
- ✅ Strategic depth — retainer engagements compound knowledge of the client's context, leading to higher-quality decisions.
- ✅ Supports BR-009 (pipeline diversity) by reducing the single-engagement concentration risk.

**Cons**:

- ❌ Setup effort to define the monthly quota / scope is non-trivial; under-quoting it bleeds margin.
- ❌ Risk of being treated as "always available" by the client, blurring the day quota.
- ❌ Some procurement routes (DOS specialist day rate) don't naturally accommodate the retainer model; an MCF4 or G-Cloud Cloud Support pathway is usually needed.

**When to Use**:

- Long-running departmental advisory relationships post-discovery.
- Where the client is investing in their own capability and needs structured support over a 12–24 month horizon.
- Where the engagement spans multiple programmes / projects — the retainer becomes the architectural-stewardship layer.

---

### Option 1D: Outcome-Based / Risk-Share Pricing

**Description**: All or part of the supplier fee is contingent on achieving defined outcomes — often expressed as gain-share (supplier shares in upside if the outcome is exceeded) or pay-on-outcome (supplier paid only on outcome attainment).

**UK Government policy context**: The Sourcing and Consultancy Playbooks **explicitly warn against inappropriate use of outcome-based pricing**. The guidance states: "in several high-profile contracts, risk transfer has been inappropriately transferred through the pricing mechanism where suppliers were inappropriately paid on outcomes, with payment linked to factors beyond their control and leaving suppliers exposed to the risk of not being paid for their services where desired outcomes were not achieved." ([Risk Allocation and Pricing Approaches Guidance Note](https://www.gov.uk/government/publications/the-sourcing-and-consultancy-playbooks/risk-allocation-and-pricing-approaches-guidance-note-html))

The same guidance recommends "risk pots" — explicitly priced and visible — rather than implicit risk transfer through outcome pricing.

**Pros (in principle)**:

- ✅ Aligns supplier and buyer incentives where outcomes are within the supplier's control.
- ✅ Differentiates the practice on confidence in the outcome.
- ✅ Can yield higher gross fees on successful engagements.

**Cons (in practice)**:

- ❌ Most public sector outcomes (citizen take-up, internal capability uplift, service-assessment pass rates) are partially outside the supplier's control — the buyer's organisational behaviour and political context are usually decisive. UK Government policy explicitly warns against this pattern.
- ❌ Cash-flow risk: revenue recognition and DSO worsen materially.
- ❌ Audit complexity: NAO and HMT scrutiny of outcome-based fees is high; the supplier must demonstrate the link between fee and outcome.
- ❌ Definition complexity: drafting a measurable, attributable outcome metric is genuinely hard for EA work.

**Recommendation for ArcKit Consulting v1**: **Do not adopt outcome-based or risk-share pricing for v1**. Revisit at year-3 review when the practice has 20+ engagements of historical evidence and a portfolio mature enough to understand what outcomes are within its control. In the meantime, where buyers ask for outcome alignment, offer a small acceptance hold-back (e.g., 10% of fee released on milestone acceptance) within a fixed-price model — this gives outcome-alignment without the structural risk-transfer pattern UK Government warns against.

---

### Option 1E: SME-Tier Pro-Rata Pricing

**Description**: For verified SMEs (per BR-005 and Principle 1), a published, externally-verifiable discount applied to the standard rate card or fixed-price packages. The SME tier is **not** a discretionary discount — it is a structured, published tier with eligibility criteria and a quarterly capacity reservation, funded by the cross-subsidy from the standard / large-engagement tiers.

**Eligibility criteria (per BR-005, mirroring Principle 1)**:

- UK-incorporated company (verifiable on Companies House).
- Companies Act 2006 SME thresholds met (turnover ≤ £15m, balance sheet total ≤ £7.5m, headcount ≤ 50; effective from 6 April 2025). ([UK Gov SME definition](https://www.gov.uk/government/publications/procurement-act-2023-short-guides/supplementary-information-small-and-medium-sized-enterprises-definition-html))
- Supplying or seeking to supply UK government services (self-declared with reasonable evidence — e.g., framework application, sub-contracting relationship, active bid).
- Not a captive SME of a larger non-SME enterprise (e.g., a pass-through subsidiary).

**Pricing Mechanics**:

- **Day rate**: typically 50% of the standard rate card. E.g., a Senior Consultant at standard £875/day → SME tier £437/day (rounded to £450).
- **Fixed-price packages**: typically 50–60% of the standard package fee. E.g., a Discovery Sprint at standard £24,000 → SME tier £12,000–£14,000.
- **Pro-bono engagements**: a small pool (target: ~5 per year per BR-005) of fully-funded discovery / readiness engagements for early-stage SMEs at zero fee, with a bounded scope (typically ≤ 5 consultant days).

**Cross-Subsidy Funding Mechanism**:

- Per BR-004: ≥10% of post-tax net margin earmarked annually as cross-subsidy.
- This funds the gap between SME-tier pricing and the practice's underlying cost-to-serve.
- The cross-subsidy is **published** in the practice's transparency report, alongside the count of SME-tier engagements delivered.

**Comparator practice precedents (closest external analogues)**:

- **Made Tech** has historically maintained transparent rate cards on G-Cloud and a public-sector-only focus. ([Made Tech Frameworks](https://www.madetech.com/frameworks/)) The closest market analogue, but not principled around SME affordability.
- **dxw** is employee-owned and public-sector-focused, with explicit values commitments. ([dxw employee-owned](https://www.dxw.com/employee-owned/)) The closest values comparator but not specifically SME-tier-anchored.
- **Public.io** runs the GovStart accelerator providing structured support to GovTech SMEs (not pricing-tier discounts but capability uplift). ([PUBLIC GovStart](https://www.public.io/case-study/govstart))
- **ThoughtWorks** historically ran a "Social Impact" practice cross-subsidising third-sector engagements from commercial revenue (broader than SME-only).
- **Co-op Digital / Co-op Innovation Lab** has historically offered low-cost / pro-bono partnerships with mission-aligned SMEs and charities.

**No comparator currently combines all three of**: published transparent rate card, explicit SME-tier discount, and externally-verifiable cross-subsidy reporting. ArcKit Consulting's positioning is genuinely under-served.

**Pros**:

- ✅ Operationalises Principle 1 in the consulting practice (mirroring the SaaS Principle 1 commitment).
- ✅ Demonstrates the principles publicly — strong PR / brand value, especially with CCS, GDS, and HMT scrutiny stakeholders (per stakeholder analysis SD-1, SD-4).
- ✅ Builds a future client pipeline: SMEs that are sub-£500k revenue today are sometimes £5m+ revenue in 3 years; the SME tier is also a long-horizon business development investment.
- ✅ Generates SME case studies (per BR-005, BR-007), feeding the marketing flywheel.

**Cons**:

- ❌ Reduced gross margin per SME-tier consultant-day — must be recovered elsewhere in the portfolio mix.
- ❌ Operational overhead of eligibility verification (per FR-011).
- ❌ Risk of "discount creep" if the SME tier becomes a backdoor for non-SME clients with weak verification.
- ❌ Capacity reservation cost when SME demand is lumpy (quarterly capacity may be under-utilised in a soft quarter).

**Mitigations**:

- FR-011 verification process: Companies House lookup, self-declaration, lightweight evidence requirement.
- Annual review of SME tier delivery against the BR-005 success criterion (≥5 engagements / year).
- Quarterly capacity reservation expressed as a percentage of practice capacity (e.g., 5–8%), reviewed against pipeline pressure.

---

### Option 1F: Hybrid (Recommended Strategy)

**Recommendation**: ArcKit Consulting should adopt a **four-stack hybrid pricing strategy**:

1. **Day-rate / T&M** as the primary route for DOS 7 specialist-role engagements and surge / overflow capacity. Published rate card, no below-floor without Practice Lead exception.
2. **Fixed-price packages** as the primary route for G-Cloud Cloud Support catalogue items, MCF4 call-offs with defined scope, and SME-tier discovery / readiness engagements. Published catalogue with acceptance criteria.
3. **Retainer / advisory model** as the primary route for ongoing departmental / ALB / NHS-body relationships at £8,000–£18,000/month. Minimum 6-month commitment.
4. **SME-tier pro-rata** as the explicit, externally-verifiable affordability tier for verified UK SMEs. Combination of discounted day-rate, discounted fixed-price packages, and a small pool of fully-funded pro-bono engagements. Funded by the BR-004 cross-subsidy mechanism.

**Outcome-based / risk-share pricing**: **Not adopted in v1**. Revisit at year-3 review.

**Pricing Strategy Summary Table**:

| Pricing Model | When Used | Procurement Route Most Suited | Year-1 Revenue Mix Target | Key Risk |
|---------------|-----------|-------------------------------|---------------------------|----------|
| Day-rate / T&M | Specialist roles, surge | DOS 7, MCF4 day-rate call-offs | 35–45% | Rate compression |
| Fixed-price | Defined deliverables | G-Cloud, MCF4 fixed-price call-offs | 25–35% | Under-scoping |
| Retainer / advisory | Ongoing advisory | MCF4, G-Cloud Cloud Support | 15–25% | Quota leakage |
| SME-tier pro-rata | Verified SMEs | Direct or G-Cloud SME-flagged | 5–10% (target ≥5 engagements per BR-005) | Discount creep |
| Outcome-based | Not adopted v1 | n/a | 0% | Out-of-control outcome risk |

---

## Category 2: UK Procurement Framework Routes to Market

**Requirements Addressed**: BR-002 (List on relevant UK public sector procurement frameworks), BR-009 (Build a qualified opportunity pipeline), FR-001 (Opportunity capture), FR-002 (Proposal and SOW generation), Principle 1 (Procurement routes inclusive of G-Cloud).

**Why This Category**: The vast majority of UK public-sector EA work is awarded through framework call-off, not open tender. Without framework listings, ArcKit Consulting is effectively excluded from the addressable market. Framework standing is also evidence to clients of basic supplier standing — passing the framework's selection criteria signals corporate maturity.

This category covers the four major routes: **G-Cloud**, **DOS**, **MCF**, and **sub-contracting / direct award**. Other frameworks may be relevant later (e.g., NHS LPP DTCS for NHS-specific work, education / local-government framework variants, the various Spark / Vertical Application Solutions frameworks), but the four covered here are the dominant national-scale routes for EA consulting services.

---

### Option 2A: G-Cloud (Cloud Software / Cloud Support)

**Description**: G-Cloud is CCS's framework for cloud-based services, including Cloud Hosting (Lot 1), Cloud Software (Lot 2), Cloud Support (Lot 3), and Cloud Support — Further Competition Only (Lot 4). EA consultancy services typically list under Cloud Support (Lot 3) — the catalogue that covers cloud-related professional services including architecture, design, and assurance. ([UK Government G-Cloud — Wikipedia](https://en.wikipedia.org/wiki/UK_Government_G-Cloud))

**Current Status (as of 2026-05-07)**:

- **G-Cloud 14 (RM1557.14)** — currently live, originally 18-month term ending April 2026, **extended for 6 months until October 2026**. ([CCS G-Cloud 14 RM1557.14](https://www.gca.gov.uk/agreements/RM1557.14), [Computer Weekly G-Cloud 15 explainer](https://www.computerweekly.com/feature/UK-governments-G-Cloud-15-framework-Everything-you-need-to-know))
- **G-Cloud 15** — applications closed January 2026; framework expected go-live in 2026.
- **G-Cloud 16** — next available application window for new entrants. Target: H2-2026 onwards (re-verify with CCS — exact timing depends on G-Cloud 15 award outcomes).

**Implication for ArcKit Consulting**: cannot enter G-Cloud 14 (closed); cannot enter G-Cloud 15 (closed). Must wait for the G-Cloud 16 application window.

**Application Process**:

- Self-service supplier application on [Apply to Supply](https://www.applytosupply.digitalmarketplace.service.gov.uk/) ahead of each framework iteration.
- New for G-Cloud 14: economic and financial standing assessments of prospective suppliers to the selection process for Lots 1–3. ([G-Cloud 14 Lots 1-3 Supplier Guidance v1.0](https://www.contractsfinder.service.gov.uk/Notice/Attachment/72f479d9-9d4e-46f8-9557-be9200cab135))
- Mandatory information: company details, services offered with descriptions, transparent published pricing, service definitions, terms and conditions, sub-processor / supply chain disclosures.
- Service offers and pricing must remain **fixed for the duration of the framework** and cannot be materially changed or negotiated. Suppliers are allowed no price increases, only reductions (which can be permanent or time limited). ([Computer Weekly G-Cloud 15 explainer](https://www.computerweekly.com/feature/UK-governments-G-Cloud-15-framework-Everything-you-need-to-know))
- The framework is uncapped, so any compliant application can join.

**Fees / Costs to Suppliers**:

- **Framework fee**: 1% of revenue invoiced through G-Cloud (paid to CCS quarterly). This is a published management charge.
- **MI returns**: monthly / quarterly Management Information returns to CCS detailing all G-Cloud-derived sales.
- **Listing maintenance**: each framework iteration requires re-application and re-listing.
- **Internal effort**: typical first-time application 5–15 person-days of effort to prepare service definitions, pricing, and supporting documentation.

**Buyer Behaviour**:

- Buyers search the [Digital Marketplace](https://www.digitalmarketplace.service.gov.uk/) catalogue of services.
- Lot 3 services typically called off without further competition for sub-£100k engagements (direct award based on rate card and service definition).
- Lot 4 used for larger services where the buyer runs a further competition across the catalogue.

**Pros**:

- ✅ Most-used UK public-sector route for cloud-related consulting; high addressable-market exposure.
- ✅ Direct-award path for sub-threshold engagements means low buyer friction.
- ✅ Transparent published pricing aligns naturally with Principle 1 (transparent rates) and ArcKit Consulting's positioning.
- ✅ SME-friendly application process; CCS publishes SME spend statistics that include G-Cloud as a positive case study.

**Cons**:

- ❌ Listing is a "set and forget" exercise — pricing locked for the framework duration, no dynamic adjustment.
- ❌ The catalogue is crowded (4,000+ suppliers, 46,000+ services on G-Cloud 14) — visibility / discovery is the practical constraint, not eligibility.
- ❌ Framework refresh cycles require re-listing effort every 18–24 months.
- ❌ Cannot apply mid-cycle — the next open window is G-Cloud 16, with timing dependent on CCS schedule.

**Risks**:

- **Application rejection** — mitigation: hire a specialist framework adviser (Advice Cloud, Frameworker, or similar) for first-time application; budget c. £3,000–£8,000 for application support.
- **Framework lapse during transition** — mitigation: apply at every iteration without skipping; CCS publishes pre-market engagement notices well in advance.

**Recommendation for ArcKit Consulting**:

- **Apply to G-Cloud 16** at the next open window (target H2-2026; actual timing to be confirmed via CCS pre-market engagement).
- **Service catalogue**: 3–5 Cloud Support listings (Discovery Sprint, TCoP Review, Service Assessment Readiness Pack, ADR Set, Architecture Principles Refresh) plus 1 day-rate listing covering the consultant role catalogue.
- **Pricing**: published rate card + fixed-price packages + SME-tier flag on each listing.
- **Application support**: budget £5,000 for first-time application support if internal capacity is constrained (Commercial Lead may absorb internally if available).

---

### Option 2B: Digital Outcomes and Specialists (DOS 6 / DOS 7)

**Description**: DOS is CCS's framework for procuring agile digital and design services. Two major variants are in scope:

- **DOS 6 (RM1043.8)** — currently being phased out; extended to 27 June 2026.
- **DOS 7 (RM1043.9)** — went live 1 April 2026; replaces DOS 6 and is now the active framework.

The framework supports two main routes:
- **Digital Outcomes**: bespoke teams (developers, researchers, designers, delivery leaders) — capacity hire mode.
- **Digital Specialists**: individual specialist roles, often day-rate.

ArcKit Consulting's primary fit is **Digital Specialists**: enterprise architect, business architect, security architect, data architect, digital architect roles — all on day-rate basis with role-specific rate caps published in the framework agreement. ([CCS DOS 7 RM1043.9](https://www.crowncommercial.gov.uk/agreements/RM1043.9), [Find a Tender DOS 7 Notice](https://www.find-tender.service.gov.uk/Notice/004688-2026), [DOS 7 guide 2026](https://www.gend.co/blog/dos7-digital-outcomes-specialists-guide))

**Application Process**:

- Self-service application on [Apply to Supply](https://www.applytosupply.digitalmarketplace.service.gov.uk/) at each framework iteration.
- DOS 7 applications closed pre-1 April 2026 launch; next open window will be DOS 8 (or a successor framework — CCS has historically considered Digital Specialists & Programmes (DSP, RM6263) as a parallel option). ([techUK DSP framework](https://www.techuk.org/resource/new-digital-specialists-programmes-framework-for-the-public-sector.html))
- Implication for ArcKit Consulting: cannot enter DOS 7 mid-cycle. Must wait for DOS 8 / DSP application window.

**SME Friendliness**:

- 33% of the £6 billion+ that has historically passed through the DOS framework was with SME providers. ([Bramble Hub DOS 6 framework guide](https://www.bramblehub.co.uk/frameworks/ccs-digital-outcomes-and-specialists-6-framework-dos6/))
- SME share has been a CCS priority indicator; the framework is generally regarded as SME-accessible relative to MCF.

**Day-Rate Caps**:

- DOS publishes maximum daily rate caps per specialist role. The caps vary by role and sometimes by region (London / non-London). Caps are typically reviewed at framework iteration.
- Rate caps are **maxima**, not floors — suppliers can bid below the cap and many do. SME suppliers often bid materially below the cap.
- Specific 2026 cap figures should be re-verified against the current DOS 7 framework agreement; the framework PDFs on CCS list the role-specific caps.

**Buyer Behaviour**:

- Buyers post a **request** on Digital Marketplace covering the role, duration, location, and essential / nice-to-have skills.
- All eligible suppliers are notified; suppliers respond with a CV-equivalent specialist profile and a rate.
- Buyer shortlists, interviews, and selects.
- Award is typically a single-supplier engagement at the agreed rate.

**Pros**:

- ✅ Primary UK public-sector route for specialist day-rate work — directly fits ArcKit Consulting's Discovery / advisory engagement profile.
- ✅ SME-friendly: market share for SME suppliers has historically been around 33%, demonstrating viable pipeline access.
- ✅ Buyer expectation of day-rate makes ArcKit Consulting's published rate card easy to align.
- ✅ Lower bid effort than fixed-price competitive tenders — typical bid is a CV + rate + capability statement.

**Cons**:

- ❌ Pure specialist hire mode means the practice can be commoditised — buyer treats the specialist as a body-shop hire rather than as an outcome partner.
- ❌ Framework refresh cycles (every 18–24 months) require re-listing effort.
- ❌ Cannot apply mid-cycle.
- ❌ Day-rate caps create downward pressure on rates; SMEs bidding below the cap can compress the practice's positioning.

**Risks**:

- **Rate compression at the cap** — mitigation: differentiate on capability statement and named consultant profile; refuse below-floor bids; rely on retainer / fixed-price pathways for higher-margin work.
- **Body-shop drift** — mitigation: aim each DOS engagement at producing a specific evidence-grade artefact, not just consultant hours; QA gate (FR-008) applies regardless.

**Recommendation for ArcKit Consulting**:

- **Apply to DOS 8 / DSP successor framework** at the next open window (post DOS 7's mid-cycle, or whenever CCS announces the successor — likely 2027 onwards).
- **Specialist role catalogue**: enterprise architect, business architect, security architect, data architect, digital architect, technical architect (8 roles minimum, mapped to the practice's capability matrix per FR-005).
- **Each role** has a CV template, capability statement, and published day rate (at the published floor, not at the framework cap).

---

### Option 2C: Management Consultancy Framework (MCF3 / MCF4)

**Description**: MCF is CCS's framework for management consultancy services, covering business, strategy and policy, complex and transformation, finance, HR, procurement and supply chain, health/social care, infrastructure, environment and sustainability, and restructuring and insolvency.

**Current Status**:

- **MCF3 (RM6187)** — currently live, extended; to be replaced by MCF4.
- **MCF4 (RM6309)** — commenced 29 July 2025, scheduled to conclude 28 July 2027. ([CCS MCF4 RM6309](https://www.crowncommercial.gov.uk/agreements/RM6309), [Thornton & Lowe MCF4 guide](https://thorntonandlowe.com/understanding-mcf4/), [D3 Tenders MCF4 contract](https://d3tenders.com/contract/?ocid=ocds-b5fd17-f72d46c7-ca51-470f-aae3-abbc579ef2e1))

**MCF4 Lots**:

| Lot | Description | ArcKit Consulting fit |
|-----|-------------|----------------------|
| Lot 1 | Business | Tangential (general business advisory) |
| Lot 2 | Strategy and policy | Strong fit (strategic EA advisory at policy level) |
| Lot 3 | Complex and transformation | **Primary fit** (transformation-grade EA practice) |
| Lot 4 | Finance | Out of scope |
| Lot 5 | HR | Out of scope |
| Lot 6 | Procurement and supply chain | Out of scope |
| Lot 7 | Health, social care and community | Possible (NHS bodies) |
| Lot 8 | Infrastructure | Strong fit (technology infrastructure transformation) |
| Lot 9 | Environment and sustainability | Tangential |
| Lot 10 | Restructuring and insolvency | Out of scope |

**Implication for ArcKit Consulting**: Lot 3 (Complex and transformation) and Lot 8 (Infrastructure) are the primary lots. Lot 2 (Strategy and policy) and Lot 7 (Health and social care) are secondary.

**SME Standing in MCF**:

- MCF4 "offers expansive opportunities for SMEs and VCSEs, demonstrating continued support for smaller enterprises in the 2026 framework landscape." ([Thornton & Lowe MCF4 guide](https://thorntonandlowe.com/understanding-mcf4/))
- MCF3 was suitable for SMEs but practical entry as a prime is challenging — most SMEs sub-contract under existing primes.
- The framework is multi-Lot, multi-supplier; primes are typically large consultancies (PwC, Deloitte, EY, KPMG, Accenture, Capgemini, BCG, McKinsey, Bain, plus mid-tier firms), with SMEs often on the supplier list as smaller-tier suppliers.

**Application Process**:

- Multi-stage selection process (financial standing, technical capability, references, lot-specific evidence).
- Significantly higher bar than DOS / G-Cloud — typical first-time application 30–60 person-days of effort.
- MCF4 applications closed pre-29 July 2025 commencement; next open window will be MCF5 in 2027.
- Direct prime entry as a new SME is unrealistic for a startup practice. Sub-contracting under existing primes is the realistic v1 route.

**Sub-Contracting Pathways**:

- Many MCF primes maintain associate / sub-contractor panels.
- ArcKit Consulting can register interest with prime suppliers in lots 2, 3, 7, and 8 in MCF4 — typical commercial arrangement is a sub-contractor agreement plus per-engagement work order.
- Prompt payment cascade: PPN 03/23 / Section 73(1) Procurement Act 2023 implies 30-day payment terms into every public sub-contract. ([UK Gov prompt payment policy](https://www.gov.uk/guidance/prompt-payment-policy))

**Pros**:

- ✅ Primary UK public-sector route for consultancy work generally; complements DOS specialist roles with consultancy outcomes work.
- ✅ Sub-contracting opens the addressable market without the prime-application overhead.
- ✅ MCF4's SME-friendly intent (per CCS guidance) supports sub-contracting relationships.
- ✅ Many MCF primes proactively seek SME sub-contractor capacity for transformation engagements.

**Cons**:

- ❌ Direct prime entry as a new SME is effectively impossible (no track record, financial standing, references).
- ❌ Sub-contracting under primes means margin compression (prime takes a margin layer; ArcKit Consulting's effective rate is below standard published rate).
- ❌ Sub-contracting also means brand attenuation — the engagement is delivered "by Prime X with ArcKit Consulting as sub-contractor".
- ❌ Conflict-of-interest checks (FR-016) more complex when working under prime relationships.
- ❌ Ministerial sign-off required for any consultancy spend over £600,000 or contracts lasting more than nine months as part of new controls; spending over £100,000 lasting more than three months will need permanent secretary sign-off. ([UK Gov consultancy spend controls](https://www.gov.uk/government/news/new-controls-across-government-to-curb-consultancy-spend-and-save-over-12-billion-by-2026))

**Risks**:

- **Prime non-payment / late payment** — mitigation: PPN 03/23 prompt payment compliance verified at sub-contract sign; payment-spot-check rights under PPN 021. ([PPN 021 payment spot checks](https://www.gov.uk/government/publications/ppn-021-payment-spot-checks-in-public-sub-contracts/ppn-021-payment-spot-checks-in-public-sub-contracts-html))
- **Conflict of interest** — mitigation: FR-016 CoI check at engagement creation; transparent declaration of all prime relationships.

**Recommendation for ArcKit Consulting**:

- **Sub-contracting pathway under MCF4** as the primary v1 route — establish relationships with at least 2 primes in lots 2, 3, 7, 8 in year 1 (per BR-002 success criterion).
- **MCF5 application** as the year-3+ horizon for direct prime entry once track record, financial standing, and references support it.
- **Conflict-of-interest discipline**: never sub-contract under more than one prime on the same engagement; declare all prime relationships transparently; disengage from prime relationships that compromise ArcKit Consulting's brand.

---

### Option 2D: Direct Award (Under Threshold, Single Supplier)

**Description**: For engagements below the public procurement threshold, contracting authorities can award directly to a single supplier without competitive tender or framework call-off, subject to internal procurement governance.

**Threshold Reference (2026, Procurement Act 2023)**:

- Central Government services threshold: £213,477 (excluding VAT) / £214,904 (including VAT) as of January 2026 — re-verify with [Find a Tender](https://www.find-tender.service.gov.uk/) before relying.
- Sub-Central / NHS / Education / Local Authority threshold: £329,083 (excluding VAT).
- Below threshold, contracting authority's internal procurement rules apply (typically 3-quote competition or single supplier under a delegated authority limit, e.g., £25,000–£100,000).

**Where it's used**:

- Discovery / readiness engagements at modest fees (£10,000–£100,000).
- SME-tier engagements (often well below any threshold).
- Repeat business with a known supplier (subject to CoI controls).
- Specialist work where the contracting authority can demonstrate single-supplier rationale.

**Pros**:

- ✅ Lowest buyer friction — no framework call-off, no tender process.
- ✅ Best fit for SME-tier engagements.
- ✅ Can move from referral to engagement quickly (days, not months).

**Cons**:

- ❌ Limited to sub-threshold engagements.
- ❌ Buyer's internal procurement may still require multiple-quote evidence, even below threshold.
- ❌ No framework "warm intro" — relationship-building from a cold start.
- ❌ CCS controls on consultancy spend (£100,000 / 3-month threshold for permanent secretary sign-off) bite even on direct awards.

**Recommendation for ArcKit Consulting**: Use direct award as the primary route for sub-threshold engagements (especially SME-tier), but rely on G-Cloud and DOS as the dominant pipeline routes once frameworks are listed.

---

### Procurement Strategy Summary

| Route | Status v1 (2026) | Year 1 Target | Year 2 Target | Year 3 Target |
|-------|-----------------|---------------|---------------|---------------|
| **G-Cloud 16** (apply when window opens) | Pending application window | Listed by Q4 2026 | Active selling | Active selling |
| **DOS 8 / DSP successor** | Pending application window | Listed by mid-2027 | n/a (still pending) | Active selling |
| **MCF4 sub-contracting** | Available now via primes | 2 prime relationships established | 4–6 prime relationships | 8+ prime relationships |
| **MCF5 direct entry** | 2027 application window | n/a | Apply when window opens | Listed |
| **Direct award (under threshold)** | Available now | 60–70% of v1 revenue | 35–45% of revenue | 25–35% of revenue |
| **NHS LPP / sector-specific frameworks** | Future | n/a | Evaluate | Listed where relevant |

---

## Category 3: SME-Tier and Cross-Subsidy Commercial Structures

**Requirements Addressed**: BR-001 (UK trading entity foundations), BR-005 (SME-affordable engagement tier), BR-007 (Curate reusable IP and contribute back), Principle 1 (Equitable Access for SMEs), Principle 17 (Cost Transparency and FinOps).

**Why This Category**: The principled cross-subsidy structure is what makes ArcKit Consulting different from every other UK public-sector EA consultancy. Getting the legal vehicle and structural cross-subsidy mechanism right at incorporation avoids costly restructuring later. UK options include Limited Company (Ltd), Limited Liability Partnership (LLP), Community Interest Company (CIC), and B-Corp certification (which is an overlay on top of Ltd or LLP). Each has structural implications for cross-subsidy capacity, tax treatment, governance, and external credibility.

---

### Option 3A: Limited Company (Ltd) — Standard Form

**Description**: Standard UK company limited by shares, regulated under the Companies Act 2006. Owners are shareholders; directors run the company; profits distributable as dividends or retained for reinvestment.

**Tax / Regulatory Profile**:

- Corporation tax (current main rate 25% for profits over £250,000; 19% small profits rate for profits up to £50,000; marginal relief between).
- VAT registration mandatory above the £90,000 turnover threshold (as of 2026).
- Companies House annual confirmation statement and accounts.
- IR35 / off-payroll working rules applicable from April 2021 for medium / large clients; threshold for "small" client size raised effective 6 April 2026 (turnover up to £15m, balance sheet total up to £7.5m, headcount 50). ([UK Gov off-payroll IR35](https://www.gov.uk/guidance/understanding-off-payroll-working-ir35), [Kingsbridge IR35 thresholds 2026](https://www.kingsbridge.co.uk/blog/contractors/ir35/ir35-small-company-threshold-changes-2026/))

**Cross-Subsidy Mechanism**:

- Cross-subsidy operationalised as a **published voluntary commitment**: ≥10% of post-tax net margin earmarked annually as transfer to ArcKit-as-a-Service (the SaaS product) for SME free-tier capacity (per BR-004 / Principle 1).
- Mechanically: an inter-company licence / service fee or a charitable / capacity grant — exact form to be confirmed with the practice's tax adviser.
- Reported publicly in the practice's annual transparency report.

**Pros**:

- ✅ Most flexible legal vehicle — no asset lock, no governance restrictions specific to social enterprise form.
- ✅ Standard public-sector procurement vehicle (CCS frameworks recognise Ltd companies as default).
- ✅ Shareholder structure can include practice founders and (later) employees through EMI options.
- ✅ Cross-subsidy is a voluntary commitment, easily adjustable if circumstances change (e.g., recession year).

**Cons**:

- ❌ No structural commitment to cross-subsidy — relies on Practice Lead / Board / shareholder discipline.
- ❌ External credibility for the social mission depends entirely on Practice Lead's track record + transparency reporting.
- ❌ Risk of mission drift over founder transition / sale.

**Recommendation**: Default v1 vehicle. Mitigations: published commitment in shareholder agreement and articles of association; transparency reporting; B-Corp certification overlay (see Option 3D) within 18 months.

---

### Option 3B: Community Interest Company (CIC)

**Description**: A form of social enterprise introduced under Part 2 of the Companies (Audit, Investigations and Community Enterprise) Act 2004. CICs are companies (limited by shares or guarantee) that exist to provide community benefit, with statutory provisions to ensure assets are used for that benefit. ([Wikipedia Community Interest Company](https://en.wikipedia.org/wiki/Community_interest_company), [GOV.UK CIC guidance](https://www.gov.uk/government/publications/community-interest-companies-how-to-form-a-cic/community-interest-companies-guidance-chapters))

**Key Features**:

- **Asset Lock**: assets and profits must be used for the benefit of the community the CIC was set up to serve. The asset lock is a fundamental feature of CICs and is enforced by the CIC Regulator.
- **Community Interest Statement**: every CIC must define and publish its community benefit objectives.
- **Dividend cap**: CICs limited by shares can pay dividends, but capped (currently 35% of distributable profits at maximum, with the cap regularly reviewed).
- **Annual community interest report** must be filed, demonstrating community benefit delivered.

**UK Adoption**: As of 2024-2025 financial year, there were 37,081 CICs in existence in the UK — a 12% rise on the previous year. ([Plinth CIC complete guide](https://www.plinth.org.uk/complete-guide/what-is-a-community-interest-company))

**Pros**:

- ✅ Externally-verifiable structural commitment to community benefit.
- ✅ Asset lock prevents mission drift over founder transitions.
- ✅ Strong external credibility for the public-benefit positioning.
- ✅ Public sector buyers familiar with CICs.

**Cons**:

- ❌ **Asset lock is structurally incompatible with the BR-004 cross-subsidy mechanism** as designed. The CIC's assets must be used for the *CIC's* community benefit, not transferred to a separate company (ArcKit-as-a-Service Ltd) for that company's purposes — even if both are public-benefit-aligned.
- ❌ Dividend cap restricts shareholder return, limiting capital-raising and exit options.
- ❌ Annual community interest report is additional reporting overhead.
- ❌ Conversion from CIC to Ltd is materially more complex than the reverse.
- ❌ Some procurement routes / DPAs treat CICs as a niche category requiring additional explanation to buyers.

**Why Not Recommended for ArcKit Consulting**: The asset lock is the structural blocker. The cross-subsidy mechanism described in BR-004 / Principle 1 transfers value from the consulting practice to a separate Ltd entity (ArcKit-as-a-Service). A CIC asset lock prohibits such transfers unless the receiving entity is itself a CIC or charity with aligned community benefit. Restructuring the cross-subsidy to remain inside a CIC would require the SaaS product also to be a CIC, which would in turn restrict the SaaS product's commercial flexibility (large-enterprise tier pricing, eventual exit options).

**Alternative**: A Ltd company with the same external commitment, plus B-Corp certification, achieves the same external credibility without the structural rigidity.

---

### Option 3C: Limited Liability Partnership (LLP)

**Description**: A partnership structure where members (partners) have limited liability. Common in professional services (law, accountancy, some consultancies). Profits flow through to partners and are taxed as personal income; the LLP itself does not pay corporation tax.

**Pros**:

- ✅ Tax transparency — profits taxed once at partner level (no corporation tax).
- ✅ Familiar to professional-services audiences (law firms, accountancy practices).
- ✅ Member-owned governance.

**Cons**:

- ❌ Less flexible for capital-raising and external investment than a Ltd company.
- ❌ Governance complexity around member admission / exit.
- ❌ Less suited to a single-founder practice in v1; LLPs typically need 2+ members at incorporation.
- ❌ Cross-subsidy mechanism is less standard — typically a partner-level commitment rather than an entity-level commitment.
- ❌ Public sector buyers less familiar with LLPs as suppliers (vs Ltd companies).

**Why Not Recommended for ArcKit Consulting v1**: Single-founder practice; capital-raising flexibility preferred for future growth; cross-subsidy mechanism easier to structure inside a Ltd.

---

### Option 3D: B-Corp Certification (Overlay on Ltd or LLP)

**Description**: B-Corp is a third-party certification (administered by B Lab) for companies meeting high standards of social and environmental performance, transparency, and accountability. Certification is an overlay on top of the underlying legal vehicle — a Ltd or LLP can be B-Corp certified.

**Adoption in UK Consulting**:

- Kin and Carta plc was the first company listed on the London Stock Exchange to become certified as a B Corporation. ([LexisNexis B-Corps in the UK](https://www.lexisnexis.co.uk/blog/research-legal-analysis/b-the-best-you-can-b-the-rise-of-b-corps-in-the-uk))
- Investing for Good is B-Corp certified. ([Investing for Good B-Corp announcement](https://www.investingforgood.co.uk/news/24bmd3a9telslwzlww5c2dxl8jlpb9))
- Several UK public-sector-focused consultancies have pursued B-Corp certification (the search did not surface explicit B-Corp status for Made Tech, but B-Corp is an active question across the sector).

**Certification Process**:

- B Impact Assessment: comprehensive questionnaire across governance, workers, community, environment, and customers (typical first-time score required: 80+ out of 200).
- Legal requirement: amend articles of association to commit to consideration of stakeholder interests (not just shareholder primacy).
- External verification by B Lab.
- Re-certification every 3 years.

**Pros**:

- ✅ Externally-verifiable commitment to high standards on social / environmental / governance dimensions.
- ✅ Compatible with both Ltd and LLP — does not require legal restructuring.
- ✅ Buyer recognition is growing, especially in public sector and progressive corporate sectors.
- ✅ Network effect — B-Corp community is itself a business development network.

**Cons**:

- ❌ Certification process takes 6–18 months; not realistic for v1 incorporation.
- ❌ Annual B-Corp certification fee (typically £500–£10,000 depending on revenue).
- ❌ B-Corp's score is broad (worker, community, environment, customer) — does not specifically validate the SME affordability commitment.
- ❌ B Lab's standard for IT services has been tightened repeatedly, raising the bar for certification.

**Recommendation**: Pursue B-Corp certification in **year 2** of the practice (after track record establishes the commitments described in BR-005, BR-007, BR-008 are operationally honoured). Use the year-1 transparency report as evidence in the certification application.

---

### Option 3E: Comparator Practice Cross-Subsidy / Public-Benefit Structures

This section surveys how comparable UK practices structure their public-benefit / cross-subsidy commitments.

**Made Tech (LSE: MTEC)**:

- LSE-listed plc (Ltd company in legal form, publicly traded).
- Public-sector-only focus; revenue largely from CCS frameworks. Recently won £19m contract with GDS as Strategic IT and Security Delivery Partner. ([UK Investor Magazine — Made Tech £19m GDS contract](https://ukinvestormagazine.co.uk/made-tech-lands-19m-contract-with-government-digital-service/))
- Transparent rate cards published on G-Cloud listings.
- No explicit SME-tier cross-subsidy commitment; commercial focus is on departmental transformation engagements.
- **Comparison**: closest structural comparator (UK-only, public-sector-only, transparent), but lacks the SME-tier discipline. PLC pressure on dividends / total shareholder return creates structural tension with deep cross-subsidy commitments.

**BJSS / CGI**:

- BJSS was a Ltd company; acquired by CGI in early 2026.
- Now part of CGI's UK operations, expanding CGI to over 8,500 UK employees post-acquisition. ([CGI completes BJSS acquisition](https://www.cgi.com/en/CGI-completes-acquisition-UK-based-BJSS-deepening-presence-across-key-commercial-industries-public-sector))
- BJSS pre-acquisition: c. 2,400 professionals, $144.3m revenue.
- **Comparison**: large-firm / multinational route; structurally cannot offer SME-tier pricing in the way ArcKit Consulting can.

**Equal Experts**:

- Network-based partnership model with c. 4,000+ consultants across 5 continents.
- Top-3 G-Cloud supplier by revenue. ([Equal Experts top G-Cloud supplier](https://www.equalexperts.com/blog/whats-new/equal-experts-is-a-top-supplier-on-g-cloud/))
- Largest current public-sector engagement: HMRC Multichannel Digital Tax Platform.
- Privately held; no public B-Corp / CIC status visible in public records.
- **Comparison**: globally-distributed, large-scale; structurally not SME-positioned but values-led.

**dxw**:

- Ltd company in employee ownership trust (EOT) structure since 2021.
- c. 80 employees; Leeds and London offices.
- Public-sector-only focus including central government, local authorities, housing associations, healthcare, charities. ([dxw employee-owned](https://www.dxw.com/employee-owned/), [dxw consultancy.uk profile](https://www.consultancy.uk/news/29160/digital-consultancy-dxw-becomes-employee-owned))
- **Comparison**: closest values comparator (employee-owned trust, public-sector-only, principles-led). Not specifically SME-tier-anchored but mission-aligned.

**TPXImpact (LSE: TPX)**:

- LSE-listed plc with c. 90%+ public sector clients.
- Recently raised EBITDA guidance to £7m+ for FY26; year-to-date contract wins exceed £110m.
- Engagements with DEFRA, NHS England, HM Land Registry. ([TPXImpact EBITDA update](https://uk.advfn.com/market-news/article/12078/tpximpact-raises-ebitda-guidance-as-public-sector-contract-wins-exceed-110m), [TPXImpact frameworks](https://www.tpximpact.com/about/frameworks))
- **Comparison**: large UK public-sector specialist; PLC pressure same as Made Tech.

**Public.io (PUBLIC)**:

- Privately held; full-stack digital transformation consultancy with 30+ government client organisations.
- Operates GovStart accelerator: 48 startups supported, £19m public sector contracts won by alumni, £59m investment raised. ([PUBLIC GovStart](https://www.public.io/case-study/govstart))
- **Comparison**: similar mission-led positioning, but the SME support is via accelerator (capability uplift) rather than pricing-tier discounts.

**Mastek**:

- Multinational with significant UK public sector practice; recently named supplier on NHS LPP DTCS framework. ([Mastek NHS DTCS framework](https://www.mastek.com/pressreleases/mastek-named-supplier-nhs-lpp-dtcs-framework-clinical-digital-transformation/))
- **Comparison**: large multinational; structurally cannot offer SME-tier pricing.

**Snook**:

- Service design and digital innovation consultancy with public sector practice. (Limited public information surfaced in search.)
- **Comparison**: niche player, possibly aligned values but not specifically SME-tier-anchored.

**Caspian One**:

- Consultancy with UK public sector practice. (Limited public information surfaced in search; primarily known as a financial services contracting / staffing firm rather than an EA practice.)
- **Comparison**: limited overlap with ArcKit Consulting's positioning.

**Big 4 (PwC, Deloitte, EY, KPMG)**:

- All major MCF / G-Cloud listed.
- UK public sector practices large; partner-led commercial models.
- Day rates typically £700–£3,000+ (Big 4 mean L4 senior consultant rate historically c. £1,500/day from G-Cloud-derived analysis). ([Big 4 vs Accenture day rates analysis](https://www.linkedin.com/pulse/comparison-day-rates-between-big-four-accenture-tom-moore))
- **Comparison**: incumbent competitors at the high-fee end; ArcKit Consulting is positioned 25–30% below Big 4 list rates.

**Comparator Summary**:

| Practice | Legal Form | Public Sector Focus | SME-Tier Commitment | Closest Analogue | Differentiators |
|----------|-----------|--------------------:|---------------------:|------------------|------------------|
| Made Tech | Ltd / LSE plc | 90%+ | None | Yes — closest structural | Plc pressure on dividends |
| BJSS / CGI | Ltd (now multinational) | Mixed | None | No | Multinational scale |
| Equal Experts | Network LLP-style | Strong | None | No | Global distribution |
| dxw | Ltd (EOT) | 100% | None explicitly | Yes — closest values | Employee ownership |
| TPXImpact | Ltd / LSE plc | 90%+ | None | Yes — comparable | Plc pressure |
| Public.io | Ltd | 100% gov | Via accelerator (capability) | Yes — mission-aligned | GovStart capability route |
| Mastek | Multinational | Mixed | None | No | Multinational |
| Big 4 | LLP / Ltd | Mixed | None | No | High-fee incumbent |

**ArcKit Consulting's positioning is genuinely under-served**: no comparator combines (a) UK public-sector-only focus, (b) explicit principled SME-tier with structured cross-subsidy, (c) toolkit-anchored evidence-grade delivery, and (d) Ltd flexibility with B-Corp credibility overlay. The closest combinations are dxw (mission-aligned, employee-owned, but not SME-tier-anchored) and Made Tech (transparent, public-sector-only, but plc-pressured and not SME-tier-anchored).

---

### Recommendation: Legal Vehicle and Cross-Subsidy Structure

**Recommended legal vehicle**: **Limited Company (Ltd) with employee ownership ambition (EOT in year 3-5) and B-Corp certification target in year 2**.

**Rationale**:

- **Ltd v1**: maximum flexibility for cross-subsidy mechanism; standard public-sector procurement vehicle; familiar to all stakeholders.
- **B-Corp year 2**: external verification of social / environmental / governance commitments without the CIC asset-lock rigidity.
- **EOT year 3-5**: optional governance evolution if practice scales; aligns long-term incentives with employees and matches dxw's values comparator.

**Cross-subsidy mechanism (operationalised)**:

- ≥10% of post-tax net margin transferred annually to ArcKit-as-a-Service as licence / service fee or capacity grant (exact form per tax adviser).
- Reported in published annual transparency report alongside SME-tier engagement count.
- Reviewed annually by Architecture Review Board and Practice Lead.
- Adjustable downward only with public explanation (e.g., recession year, founder transition); upward at Practice Lead discretion.

---

## Category 4: Consulting-Business Operating Tooling

**Requirements Addressed**: BR-001 (UK trading entity foundations), BR-008 (Provable confidentiality and information governance), FR-001 (Opportunity capture), FR-005 (Capability matrix), FR-007 (Time recording), FR-018 (Identity and SSO), FR-019 (Public website), Principle 16 (Open Source First), Principle 17 (FinOps).

**Why This Category**: A consulting practice runs on its operating tooling — CRM for pipeline, time tracking for invoicing, accounting for finances, e-sign for contracts, HR/payroll for people, identity for security, MDM for endpoint management, knowledge management for IP curation, and a public website for visibility. The tooling stack is not the differentiator — the engagements and people are — but a poorly-chosen tooling stack creates compounding operational drag that erodes margin and quality.

The Principle 16 (Open Source First and Reuse Before Build) commitment biases the recommendation towards open-source where it meets the operational need; Principle 17 (FinOps) biases towards transparent published per-seat pricing (versus opaque enterprise pricing).

---

### Sub-Category 4.1: CRM / Pipeline Management

**Requirements**: FR-001, BR-009.

**Options**:

| Option | Pricing (UK 2026) | Free Tier | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|-----------|-------------------|-----------|------------|
| **HubSpot CRM** | Free (Forever, basic) → Starter £20/user/month → Professional £105/user/month | Yes (Forever Free) | Multi-region (UK / EU available) | Very strong free tier; integrates with email, website, marketing; large ecosystem | Aggressive upselling at higher tiers; multi-team functionality requires Enterprise |
| **Salesforce** | Starter £25/user/month → Pro £125/user/month → Enterprise £165+/user/month | No (free trial only) | Multi-region (UK Hyperforce available) | De-facto enterprise standard; deep customisation; Service Cloud / Sales Cloud | Setup complexity; high TCO at scale; SME-overkill |
| **Pipedrive** | Essential £14/user/month → Advanced £29/user/month → Professional £49/user/month | No (free trial only) | EU (Frankfurt) — UK access fine | Sales-focused; intuitive UI; pipeline-centric; SME-friendly | Less marketing automation than HubSpot; less customisation than Salesforce |
| **Capsule CRM** | Free (up to 2 users) → Starter £15/user/month → Growth £29/user/month | Yes (free for 2 users) | UK-based company; UK / EU data residency | UK-built; SME-priced; clean simple UI | Smaller ecosystem; fewer integrations |
| **OnePageCRM** | Professional £14/user/month → Business £29/user/month | No (free trial only) | UK / EU | UK-built; action-focused; strong for follow-ups | Less analytics depth than competitors |

> Sources: [Pipedrive vs HubSpot 2026](https://monday.com/blog/crm-and-sales/pipedrive-vs-hubspot/), [HubSpot vs Salesforce vs Pipedrive comparison](https://www.pipedrive.com/en/blog/hubspot-vs-salesforce-vs-pipedrive), [LaGrowthMachine 15 CRM examples 2026](https://lagrowthmachine.com/crm-software-examples-2026/), [Capsule CRM blog Pipedrive pricing comparison](https://capsulecrm.com/blog/pipedrive-crm-pricing/), [Salesflare CRM comparison](https://blog.salesflare.com/compare-salesforce-zoho-hubspot-pipedrive).

**Recommendation**: **HubSpot CRM (Free → Starter)**. The forever-free tier covers v1 needs (up to 1m contacts, basic pipeline, email integration). Starter at £20/user/month adds task automation, custom properties, and removes branding. The upgrade path is generous; the free tier is a genuine working tier (not a trial).

Alternative: **Capsule CRM** (UK-built, SME-priced, free for 2 users) for a more SME-aligned and UK-centric option.

**3-year TCO at 5–10 users**: HubSpot Free → Starter (year 2 onwards): **£0–£2,400** (£0 if staying on Free tier; £100/month at 5 users on Starter). Capsule CRM equivalent: **£0–£2,700**.

---

### Sub-Category 4.2: Time Tracking and Invoicing

**Requirements**: FR-007 (Time recording and engagement financials).

**Options**:

| Option | Pricing (UK 2026) | Free Tier | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|-----------|-------------------|-----------|------------|
| **Harvest** | Free → Pro $11/user/month annual ($13.75 monthly) → Teams $9/user/month annual | Yes (limited) | US-hosted (UK data subject to DPA) | Best-in-class time-to-invoice flow; integrates Xero / QuickBooks; mature | US-hosted — UK GDPR Article 28 needed |
| **Clockify** | Free → Basic $3.99/user/month → Standard $5.49 → Pro $7.99 | Yes (genuine free tier) | EU (Frankfurt) | Cheapest paid tier; generous free tier; basic invoicing | Less polished invoicing flow than Harvest |
| **Toggl Track** | Free → Starter $9/user/month → Premium $18 | Yes | EU | Track-focused; clean UI | Invoicing requires separate Toggl Plan / Track Premium |
| **FreeAgent (built-in time)** | Bundled with FreeAgent accounting (£33/month limited co.) | n/a | UK-hosted | Already in the accounting tool; no separate bill | Less feature-rich than dedicated time trackers |
| **Xero (built-in time)** | Bundled with Xero Comprehensive (£50/month) | n/a | UK / EU | Already in the accounting tool | Limited time tracking compared to Harvest / Clockify |

> Sources: [Harvest pricing 2026](https://costbench.com/software/time-tracking/harvest/), [Clockify vs Harvest 2026](https://www.plutio.com/compare/clockify-vs-harvest), [Capterra Harvest profile](https://www.capterra.com/p/75598/Harvest/), [Harvest invoicing](https://www.getharvest.com/), [TimeSentry Clockify vs Harvest](https://timesentry.ai/compare/clockify-vs-harvest).

**Recommendation**: **Harvest (Pro)**. Harvest is best-in-class for the consultancy "time → invoice" workflow, integrates natively with Xero and QuickBooks (bridging Sub-Category 4.3 below), and has UK GDPR Article 28 DPA available. The Pro tier at $11/user/month annual is the right balance for a 5–15 person practice.

Alternative: **Clockify (Standard)** for a deeper free tier and lower paid tier — recommended if the practice is highly cost-sensitive in v1.

**3-year TCO at 10 users**: Harvest Pro 10 users × $11 × 12 × 3 ≈ £3,200 (at $1.30/£1). Clockify Standard equivalent: £1,600.

---

### Sub-Category 4.3: Accounting and Invoicing

**Requirements**: BR-001 (HMRC registrations, VAT compliance), FR-007 (Engagement financials), Principle 17 (FinOps transparency).

**Options**:

| Option | Pricing (UK 2026) | UK MTD Compliant | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|------------------|-------------------|-----------|------------|
| **FreeAgent** | Sole trader £19/m → Partnership £29/m → Limited Company £33/m. **Free with NatWest / RBS / Ulster Bank business banking**. | Yes | UK-hosted | UK-built; SME-priced; **free with NatWest banking**; designed for small UK businesses | Less suited to multi-entity / complex accounting |
| **Xero** | Ignite £16/m → Grow £37/m → Comprehensive £50/m → Ultimate £65/m | Yes | UK / EU | Strongest UK SME accounting platform; deep integration ecosystem (Harvest, payroll); HMRC-recognised | Pricing rises sharply at scale |
| **QuickBooks Online (UK)** | Simple Start £14/m → Essentials £30/m → Plus £42/m → Advanced £85/m | Yes | UK / EU | Strong UK SME presence; HMRC-recognised | UI less polished than Xero; smaller integration ecosystem in UK |
| **Sage Accounting** | Accounting Start £15/m → Standard £30/m → Plus £39/m | Yes | UK | UK-built; deep payroll integration; familiar to UK accountants | UI less modern; ecosystem more closed than Xero |

> Sources: [E-Accounts Xero vs QuickBooks vs FreeAgent 2026](https://www.e-accounts.co.uk/2025/12/16/xero-vs-quickbooks-vs-freeagent-uk-2026/), [HS Global MTD Software 2026](https://www.hsglobalaccountancy.co.uk/mtd-software-landlords-xero-quickbooks-freeagent/), [FreeAgent pricing](https://www.freeagent.com/pricing/), [Heights Accountancy Xero vs QuickBooks vs FreeAgent service SMEs 2025/26](https://heightsaccountancy.co.uk/2025/10/29/xero-vs-quickbooks-vs-freeagent-uk-service-smes-2025-26/), [TaxCareAcademy FreeAgent vs Xero 2026](https://taxcareacademy.co.uk/freeagent-vs-xero-comparison/).

**Recommendation**: **FreeAgent if banking with NatWest / RBS / Ulster Bank (free) — otherwise Xero (Comprehensive)**.

- FreeAgent free with NatWest / RBS / Ulster Bank business banking is the best deal for a v1 UK Ltd.
- If banking elsewhere (e.g., Starling, Tide, Mettle), Xero Comprehensive at £50/month is the best balance of capability and cost. (Xero is HMRC-recognised, MTD-compliant, integrates natively with Harvest, supports VAT registration tracking, and scales without re-platforming.)

**3-year TCO**: FreeAgent (free with NatWest): **£0**. Xero Comprehensive: **£1,800** (£50 × 36 months).

---

### Sub-Category 4.4: Contracts and E-Signature

**Requirements**: FR-002 (Proposal and SOW), FR-010 (Sub-contractor agreements), FR-006 (Onboarding contracts).

**Options**:

| Option | Pricing (UK 2026) | UK Legal Validity | UK GDPR | Strengths | Weaknesses |
|--------|------------------:|-------------------|---------|-----------|------------|
| **DocuSign** | Personal £10/m → Standard £25/m → Business Pro £40/m | Yes (eIDAS / UK Electronic Communications Act 2000) | Yes (DPA) | Market leader; deep brand recognition; most enterprise integrations | More expensive; SME-overkill |
| **Adobe Acrobat Sign** | Acrobat Standard $12.99/m (individual) → Acrobat Studio for Teams $29.99/user/m (capped 150 transactions/user/year) | Yes | Yes | Bundled with Acrobat for PDF workflow; UK GDPR compliant; common in legal | Transaction caps; pricing-as-bundle confusing |
| **SignNow** | Business £8/user/m → Business Premium £15/user/m → Enterprise £30/user/m | Yes | Yes | Cheapest tier; SME-friendly | Less enterprise-grade than DocuSign / Adobe |
| **HelloSign / Dropbox Sign** | Essentials £15/m → Standard £25/m | Yes | Yes | Integrates Dropbox storage | Smaller market share |

> Sources: [DocuSign UK pricing](https://ecom.docusign.com/plans-and-pricing/esignature), [eSignGlobal UK eSign provider pricing](https://www.esignglobal.com/blog/united-kingdom-docusign-subscription-plans-gbp), [PandaDoc Adobe Sign vs DocuSign 2026](https://www.pandadoc.com/blog/adobe-sign-vs-docusign-comparison/), [Adobe Sign pricing 2026 Signeasy](https://signeasy.com/blog/business/adobe-sign-pricing), [eSign.co.uk best 10 providers UK 2026](https://www.esign.co.uk/resources/news-and-insights/the-top-electronic-signature-providers/), [eSign.ai GDPR-compliant e-signature](https://www.esign.ai/blog/gdpr-compliant-e-signature-eu-clients).

**Recommendation**: **Adobe Acrobat Sign (Acrobat Studio for Teams)**. Bundled with Acrobat (which is needed anyway for proposal / SOW PDF workflow), UK eIDAS / Electronic Communications Act compliant, GDPR-compliant. At small scale (5–10 users, well below 150 transactions/user/year cap) the team plan is cost-effective.

Alternative: **SignNow (Business)** if the practice already uses Adobe through a different licence and wants a cheap stand-alone e-sign tool.

**3-year TCO at 5 users**: Adobe Acrobat Studio for Teams: 5 × $29.99 × 12 × 3 ≈ £4,150. SignNow Business: 5 × £8 × 12 × 3 = £1,440.

---

### Sub-Category 4.5: HR / People and Payroll

**Requirements**: BR-003 (Onboard a baseline cohort of qualified consultants), FR-006 (Consultant onboarding workflow), FR-010 (Sub-contractor and associate management).

**Options**:

| Option | Pricing (UK 2026) | UK Payroll Integration | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|------------------------|-------------------|-----------|------------|
| **BrightHR** | From £2.20/employee/month | Standalone HR; payroll separate (Bright Payroll) | UK | UK-built; SME-priced; HR + payroll bundle option | Less feature-rich than Personio |
| **Sage HR** | From £4.60/employee/month | Sage Payroll (separate, bundled discounted) | UK | UK-built; deep Sage Payroll integration; well-known to UK accountants | Older UI; less polished than Personio |
| **Personio** | From £4/employee/month | Payroll partners (UK) | EU-hosted | European market leader; modern UI; broad HR coverage | Payroll requires separate UK provider |
| **BambooHR** | $10/employee/month (or $250/month flat for ≤ 25 employees) | **No UK payroll** (US-only) | US | Strong HR features; well-known brand | Payroll US-only — disqualifying for UK practice |
| **PeopleHR** | £4/user/month (legacy plan ranges) | UK payroll partners | UK | UK-built | Less modern than Personio |

> Sources: [Stribe HR software for small UK businesses 2026](https://stribehq.com/resources/best-hr-software-small-businesses/), [Zelt 10 best HR software UK 2026](https://zelt.app/blog/best-hr-software-uk/), [BambooHR pricing 2026 Pin](https://www.pin.com/blog/bamboohr-pricing/), [BambooHR official pricing](https://www.bamboohr.com/pricing/), [Theadcompare top 11 HR software UK 2026](https://theadcompare.com/software/hr/), [Zelt best HR software for small business UK 2026](https://zelt.app/blog/best-hr-software-for-small-business-uk/), [BrightHR pricing](https://www.brighthr.com/uk/), [Sage HR pricing](https://www.sage.com/en-gb/sage-business-cloud/people/).

**Recommendation**: **Sage HR + Sage Payroll bundle**. UK-built, MTD-compliant, deep payroll integration, well-known to UK accountants. At 5–10 employees the bundle costs c. £8–£10 per employee / month all-in (HR + Payroll), within SME-friendly range.

Alternative: **BrightHR + Bright Payroll** for a slightly cheaper alternative; similar feature footprint.

BambooHR is **disqualified** because its payroll is US-only.

**3-year TCO at 10 employees**: Sage HR + Sage Payroll bundle: 10 × £10 × 12 × 3 = £3,600. BrightHR + Bright Payroll equivalent: 10 × £8 × 12 × 3 = £2,880.

---

### Sub-Category 4.6: Identity and SSO

**Requirements**: FR-018 (Identity and SSO), NFR-SEC-001, BR-008 (Information governance).

**Options**:

| Option | Pricing (UK 2026) | MFA / Phishing-Resistant | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|--------------------------|-------------------|-----------|------------|
| **Microsoft Entra ID Free** | £0 (bundled with Microsoft 365) | Limited (basic MFA) | UK / EU | Free with Microsoft 365 Business Standard / Premium; ecosystem coverage | Lacks Conditional Access, Privileged Identity Management |
| **Microsoft Entra ID P1** | £6.20/user/month (or bundled with M365 Business Premium) | Yes (Conditional Access, FIDO2, passkeys) | UK / EU | Industry standard for UK public sector; bundled with M365 BP at scale | Cost rises at full P1 |
| **Microsoft Entra ID P2** | £9/user/month | Yes (PIM, Identity Protection) | UK / EU | Most advanced (PIM, identity governance) | Overkill for a small consulting practice |
| **Google Workspace Cloud Identity** | Bundled with Workspace; standalone $6/user/month | Yes | UK / EU | Good if already on Google Workspace | Limited ecosystem outside Google |
| **Okta** | $2/user/m SSO + $3/user/m MFA + $4/user/m Lifecycle | Yes | UK / EU | Best-in-class for heterogeneous SaaS; vendor-neutral | Higher TCO at scale; more setup |
| **JumpCloud** | $9/user/m (device management) → tiered up to enterprise custom | Yes | UK / EU | SME-focused; consolidates IDP / MDM | No free tier post-July 2025; less public sector recognition |

> Sources: [SoftwarePricingGuide Okta vs Entra ID 2026](https://softwarepricingguide.com/okta-vs-microsoft-entra-id-pricing-2026-the-real-cost-of-identity-sso-mfa-and-governance/), [Stabilise UK IAM SSO comparison](https://stabilise.io/blog-pages/blog/identity-management-platform-showdown-which-sso-and-iam-solution-works-best-for-uk-businesses), [JumpCloud pricing 2026](https://checkthat.ai/brands/jumpcloud/pricing), [JumpCloud comparing Entra ID and Intune](https://jumpcloud.com/blog/comparing-jumpcloud-azure-ad-intune), [JumpCloud Google Cloud Identity vs Entra ID](https://jumpcloud.com/blog/google-cloud-identity-azure-active-directory).

**Recommendation**: **Microsoft Entra ID P1, bundled with Microsoft 365 Business Premium**.

- Microsoft 365 Business Premium at £20.60/user/month includes Entra P1, Intune (MDM — Sub-Category 4.7), Defender for Endpoint, and the Office apps suite.
- This is the de-facto baseline that UK public sector buyers recognise; aligns with the dominant tenant landing zone in central-civil and NHS environments.
- Entra P1 supports Conditional Access, FIDO2 / passkeys, and SSO to the rest of the tooling stack.

Alternative: **JumpCloud** if the practice prefers a vendor-neutral SME-focused identity platform.

**3-year TCO at 10 users**: Microsoft 365 Business Premium 10 users × £20.60 × 12 × 3 = £7,416 (this includes Entra P1 + Intune + Defender + Office apps; if the practice already needs M365 for Office apps and email, the marginal cost of Entra P1 + Intune is approximately zero). Standalone Entra P1: 10 × £6.20 × 12 × 3 = £2,232.

---

### Sub-Category 4.7: Endpoint / MDM

**Requirements**: BR-008 (Information governance), NFR-SEC-006 (no BYOD for client data), FR-017 (Incident management — lost device).

**Options**:

| Option | Pricing (UK 2026) | Apple Support | Windows Support | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|---------------|-----------------|-------------------|-----------|------------|
| **Microsoft Intune (standalone)** | £6.20/user/month (or bundled with M365 Business Premium) | Yes | Yes | UK / EU | Bundled with M365 BP; industry standard; integrates Entra | Less polished Apple management than Jamf |
| **Jamf Pro** | $12.50/Mac/month (25-device minimum, billed annually) | Best-in-class | No | US / EU | Best-in-class Apple management; deep MacOS support | 25-device minimum disqualifying for very small practice; Mac-only |
| **Iru (formerly Kandji)** | Quote-based (100-device minimum reported) | Strong | Recently added | US / EU | Modern UI; six-product unified platform (identity, EPM, EDR, vulnerability, compliance, trust centre) | 100-device minimum disqualifying for SME |
| **Hexnode** | From £2/device/month | Yes | Yes | UK / EU | Cheapest MDM | Less feature depth |

> Sources: [Stabilise Jamf Pro vs Intune vs Iru UK 2026](https://stabilise.io/blog/jamf-pro-vs-microsoft-intune-vs-iru-apple-mdm-comparison-2026), [nDuo Apple MDM comparison UK 2026](https://nduo.co.uk/mdm-comparison-uk-2026/), [TechnologyMatch Intune vs Jamf vs Kandji 2026](https://technologymatch.com/blog/intune-vs-jamf-pro-vs-kandji-the-it-leaders-guide-to-apple-management-in-2026), [Connection Technologies best MDM solutions UK 2026](https://connection-technologies.co.uk/blog/mdm-solutions-uk-compared), [Asset Management for Jira Microsoft Intune pricing 2026](https://assetmanagementforjira.com/blog/microsoft-intune-pricing-a-no-nonsense-breakdown), [Costbench Intune pricing 2026](https://costbench.com/software/mdm/microsoft-intune/).

**Recommendation**: **Microsoft Intune, bundled with Microsoft 365 Business Premium** (per the SSO recommendation above). Single-vendor stack; UK-resident; bundled cost.

If the practice is Mac-heavy (5+ Macs) and the client base demands MacOS-first development, evaluate **Jamf Pro** or **Iru** as a paid overlay above Intune for deeper MacOS management.

**3-year TCO**: Already covered by the M365 Business Premium bundle (Sub-Category 4.6). Standalone Intune at 10 users: £2,232 over 3 years.

---

### Sub-Category 4.8: Knowledge / Document Management

**Requirements**: BR-007 (Curate reusable IP), FR-012 (Knowledge / IP curation library), Principle 16 (Open Standards).

**Options**:

| Option | Pricing (UK 2026) | Multi-Tenant for Client Isolation | UK Data Residency | Strengths | Weaknesses |
|--------|------------------:|------------------------------------|-------------------|-----------|------------|
| **Notion** | Free → Plus $8/user/month annual ($10 monthly) → Business $18/user/m → Enterprise custom | Workspace separation; not multi-tenant in true sense | US / EU | Modern UI; flexible blocks model; growing ecosystem; database + wiki + docs unified | Less mature for regulated environments; multi-tenant client isolation needs care |
| **Confluence (Atlassian)** | Standard $5.16/user/m → Premium $9.73/user/m → Enterprise custom (10-user free) | Spaces; not multi-tenant in true sense | UK / EU (data residency) | Mature; integrates Jira; SOC 2, ISO 27001, ISO 27018 | Slower UI than Notion; more template-heavy |
| **SharePoint (M365)** | Bundled with M365 Business Premium | Site collections; multi-tenant capable | UK / EU | Bundled with M365; deep enterprise features; mature for regulated environments | Less modern UI; setup complexity |
| **Google Drive / Workspace** | Bundled with Google Workspace ($6/user/m) | Drive / Shared Drives | UK / EU | Easy collaboration; good for non-technical users | Less structured than Notion / Confluence |

> Sources: [eesel AI Confluence vs Notion vs SharePoint 2026](https://www.eesel.ai/blog/confluence-vs-notion-vs-sharepoint), [Docsie Confluence vs Notion enterprise comparison 2026](https://www.docsie.io/blog/articles/confluence-vs-notion-enterprise-comparison-2026/), [Atlasworkspace 8 best knowledge management tools 2026](https://www.atlasworkspace.ai/blog/best-knowledge-management-software), [Softgile Confluence pricing 2026](https://softgile.com/en/confluence-pricing-2026/), [Costbench Notion pricing 2026](https://costbench.com/software/project-management/notion/).

**Recommendation**: **Notion (Business or Plus) for the IP / pattern library + SharePoint (M365 bundled) for client engagement workspaces**.

- Notion's flexible blocks model and database functionality fit the FR-012 pattern library well; the search / browse UI is the best of the available options for capability-by-engagement-type queries.
- SharePoint (already bundled with M365 Business Premium) provides client engagement workspaces with proper site-collection-based isolation, integrating naturally with Entra P1 access controls per FR-004.

Alternative: **Confluence (Standard)** if the practice already uses Atlassian Jira / Bitbucket and prefers a single-vendor stack.

**3-year TCO at 10 users**: Notion Plus 10 × $8 × 12 × 3 ≈ £2,200. SharePoint already bundled (zero marginal). Confluence Standard equivalent: 10 × $5.16 × 12 × 3 ≈ £1,420.

---

### Sub-Category 4.9: Public Website and Accessibility

**Requirements**: FR-019 (Public website and accessibility), BR-001 (Brand foundations), Principle 16 (Open Source First), Principle 12 (UK accessibility / WCAG 2.2 AA).

**Options**:

| Option | Setup Cost | Annual Hosting | UK Data Residency | Accessibility | Strengths | Weaknesses |
|--------|----------:|--------------:|-------------------|--------------|-----------|------------|
| **Eleventy + GOV.UK Design System inspired theme** | £4,000–£8,000 (build) | £20–£50/year (Netlify / Cloudflare Pages free tier or modest paid) | UK / EU CDN edge | WCAG 2.2 AA achievable | Open-source; GOV.UK Design System inspired; aligns Principle 16; static = fast + accessible | Build effort upfront |
| **WordPress (managed)** | £2,000–£6,000 (build) | £200–£800/year (managed hosting) | UK (depends on provider) | Achievable but plugin-dependent | Familiar to many marketers; large ecosystem | Plugin sprawl; security overhead |
| **Webflow** | £1,500–£4,000 (build) | $36–$45/month (Business plan) | US (CDN edge) | Achievable | Visual builder; designer-friendly | Vendor lock-in; US-hosted main; less open-standards aligned |
| **Next.js + Vercel** | £4,000–£8,000 (build) | $20/month minimum (Hobby free, Pro from $20) | UK / EU CDN edge | Achievable | Modern React stack; large dev community | More complex than Eleventy; SaaS-leaning |
| **GOV.UK Design System (used directly)** | n/a | n/a | UK (gov.uk) | WCAG 2.2 AA | Authoritative for citizen-facing services | Not licensed for non-public-sector use; not for private companies |

> Sources: [Eleventy.dev](https://www.11ty.dev/), [Nikolaos Gkionis govuk-11ty Eleventy template](https://github.com/Nikolaos-Gkionis/govuk-11ty/), [wearefuturegov gov-uk-eleventy-kit](https://github.com/wearefuturegov/gov-uk-eleventy-kit), [GOV.UK Eleventy Plugin x-govuk](https://govuk-eleventy-plugin.x-govuk.org/get-started/design/), [GOV.UK Design System home](https://design-system.service.gov.uk/), [alphagov product-page-example-11ty](https://github.com/alphagov/product-page-example-11ty), [Inside GOV.UK creating publishing design guide](https://insidegovuk.blog.gov.uk/2025/02/25/creating-the-gov-uk-publishing-design-guide/).

**Recommendation**: **Eleventy + the x-govuk Eleventy plugin (GOV.UK Design System inspired styling)**.

- Open-source; aligns Principle 16 (Open Source First) and Principle 4 (Open Standards).
- WCAG 2.2 AA achievable out of the box (the GOV.UK Design System is an A+ accessibility benchmark).
- Static site = fast, low-attack-surface, low-hosting-cost.
- Hosted free / cheap on Netlify, Cloudflare Pages, or GitHub Pages with UK / EU edge nodes.
- Build effort: 5–15 person-days at first build; thereafter content-only changes via Markdown.

**Note**: ArcKit Consulting cannot use the GOV.UK Design System branding directly (it is reserved for UK public sector services). The pattern is to use the x-govuk Eleventy plugin or a comparable adaptation that follows the same design *patterns* without claiming the GOV.UK brand.

**3-year TCO**: Build £6,000 (mid-point) + Hosting £150 (Netlify Pro at $19/month for 3 years) + Maintenance £1,000 (occasional content updates) ≈ **£7,150**.

---

### Operating Tooling Recommended Stack and 3-Year TCO

**Recommended stack at 10-person practice**:

| Sub-Category | Recommendation | Year 1 | Year 2 | Year 3 | 3-Year |
|--------------|----------------|-------:|-------:|-------:|-------:|
| 4.1 CRM | HubSpot CRM (Free → Starter year 2) | £0 | £1,200 | £1,200 | £2,400 |
| 4.2 Time Tracking | Harvest Pro | £1,070 | £1,070 | £1,070 | £3,210 |
| 4.3 Accounting | FreeAgent (free with NatWest) — fallback Xero £600/yr | £0 | £0 | £0 | £0 |
| 4.4 E-Sign | Adobe Acrobat Studio for Teams (5 users) | £1,400 | £1,400 | £1,400 | £4,200 |
| 4.5 HR / Payroll | Sage HR + Sage Payroll bundle (10 emp.) | £1,200 | £1,200 | £1,200 | £3,600 |
| 4.6 Identity | Microsoft 365 Business Premium (10 users — bundled IdP / MDM / Office) | £2,500 | £2,500 | £2,500 | £7,500 |
| 4.7 MDM | (Bundled in M365 BP above) | — | — | — | — |
| 4.8 KM | Notion Plus (10 users) | £730 | £730 | £730 | £2,190 |
| 4.9 Website | Eleventy build + Netlify Pro hosting + maintenance | £6,500 | £230 | £420 | £7,150 |
| **Total operating tooling** | | **£13,400** | **£8,330** | **£8,520** | **£30,250** |

**3-year TCO range across cohort sizes 5–20**:

| Cohort size | 3-Year TCO (mid-point) | Notes |
|------------:|----------------------:|-------|
| 5 people | £18,000 | Most categories scale per-user |
| 10 people | £30,250 | Recommended baseline (above) |
| 15 people | £42,000 | Linear scaling on most components |
| 20 people | £55,000 | Approaches the threshold for HubSpot Pro / Notion Business |

**BUILD-equivalent comparison**: Building a custom CRM, time tracker, accounting, e-sign, HR, identity, MDM, KM, and website would require an estimated 20–40 person-months of engineering effort (£200,000–£500,000) plus ongoing maintenance — **structurally disqualified** by the cost / opportunity-cost ratio. The **BUY** path is overwhelmingly preferred for operating tooling.

---

## Category 5: Insurance and Statutory Baseline

**Requirements Addressed**: BR-001 (UK trading entity foundations — insurance, ICO registration, Cyber Essentials Plus), BR-008 (Information governance), NFR-SEC-001, NFR-SEC-006.

**Why This Category**: Public sector buyers typically require evidence of corporate standing, regulatory registrations, and minimum security posture before any engagement begins. The insurance + Cyber Essentials Plus + ICO registration combination is the "ticket to ride" for government framework supply. Lead times (especially Cyber Essentials Plus) materially affect when the practice can credibly bid.

---

### Sub-Category 5.1: Professional Indemnity Insurance

**Description**: PI insurance covers the practice against client claims for negligent advice, errors, or omissions in professional services. Standard requirement on UK public sector frameworks: **minimum £5m**, often **£10m** for higher-value engagements.

**UK Market 2026 (Reference Points)**:

- **Hiscox**: PI quotes from £8.00/month for low-risk professionals; up to £10m cover available.
- **AXA, Zurich, RSA, Aviva, QBE, Markel, Tokio Marine HCC**: established PI providers for UK SME consultancies.
- **Simply Business / PolicyBee / NimbleFins / Premierline**: SME-focused brokers / aggregators.

**Pricing Pattern (UK consultancy with no claims history, c. £750k revenue, 5–10 employees)**:

| Cover Limit | Indicative Annual Premium | Notes |
|-----------:|--------------------------:|-------|
| £1m | £400–£900 | Below most public-sector framework requirements |
| £2m | £600–£1,400 | Some frameworks accept |
| £5m | £1,500–£3,500 | Standard public-sector minimum |
| £10m | £2,500–£6,000 | Higher-value framework requirement |

> Sources: [Paterson Insurance Brokers PI 2026 guide](https://www.patersonib.co.uk/2026/04/04/professional-indemnity-insurance-a-concise-2026-guide-for-uk-professionals/), [AXA UK PI cost guide](https://www.axa.co.uk/business-insurance/professional-indemnity/how-much-does-professional-indemnity-insurance-cost/), [Trust My Policy PI cost UK 2026](https://trustmypolicy.com/professional-indemnity-insurance-uk-cost/), [Simply Business PI insurance](https://www.simplybusiness.co.uk/business-insurance/professional-indemnity-insurance/), [Hiscox PI insurance cost FAQ](https://www.hiscox.co.uk/business-insurance/professional-indemnity-insurance/faq/how-much-does-professional-indemnity-insurance-cost), [PolicyBee PI insurance cost](https://www.policybee.co.uk/blog/how-much-is-professional-indemnity-insurance), [NimbleFins average PI cost](https://www.nimblefins.co.uk/business-insurance/professional-indemnity-insurance/average-cost-professional-indemnity-insurance), [Premierline real cost PI](https://www.premierline.co.uk/insight-hub/the-real-cost-of-professional-indemnity-insurance/).

**Key insight**: Government departments and local authorities typically demand a minimum of £5m or £10m in cover before they'll consider a commercial bid. ([Paterson 2026 PI guide](https://www.patersonib.co.uk/2026/04/04/professional-indemnity-insurance-a-concise-2026-guide-for-uk-professionals/))

**Recommendation**: **PI £10m**, supplied by an established UK insurer with public-sector experience (Hiscox, AXA, Markel, or Tokio Marine HCC). Year 1 indicative premium: **£3,000–£5,000**.

---

### Sub-Category 5.2: Public Liability Insurance

**Description**: PL insurance covers claims arising from injury or property damage to third parties resulting from the practice's activities (e.g., a visitor to the office injured on premises). Public sector framework requirement: **minimum £5m**.

**UK Market 2026 Reference**: Annual premium for a small consultancy with no claims, no significant on-site activity: **£200–£800**.

**Recommendation**: **PL £5m** at typical premium £400/year.

---

### Sub-Category 5.3: Employer's Liability Insurance

**Description**: EL insurance is **statutory** (Employers' Liability (Compulsory Insurance) Act 1969) for any UK business with employees. Minimum statutory cover: **£5m**. Public sector framework requirement: typically **£10m**.

**UK Market 2026 Reference**: Annual premium for a consultancy with 5–15 office-based employees, no claims: **£200–£800** (low-risk profession).

**Recommendation**: **EL £10m** at typical premium £500/year.

---

### Sub-Category 5.4: Cyber Liability Insurance

**Description**: Cyber liability covers data breach response costs, regulatory fines, business interruption from cyber incidents, and third-party liability. Increasingly expected by public sector buyers, especially for engagements handling personal data.

**UK Market 2026 Reference**: Annual premium for a small consultancy with Cyber Essentials Plus and basic cyber maturity: **£500–£2,000** for £1–£5m cover.

**Recommendation**: **Cyber liability £2m** at typical premium £900/year. Increase to £5m as engagement portfolio grows.

---

### Sub-Category 5.5: Cyber Essentials and Cyber Essentials Plus

**Description**: NCSC's basic cyber security certifications; Cyber Essentials (CE) is a self-assessment, Cyber Essentials Plus (CE+) adds an independent on-site/remote audit. CE+ is a common public sector framework requirement.

**Pricing (2026)**:

- **Cyber Essentials (basic, IASME standard fees)**:
  - Micro (0–9 staff): £300 + VAT
  - Small (10–49 staff): £400 + VAT
  - Medium (50–249 staff): £450 + VAT
  - Large (250+): £500 + VAT
- **Cyber Essentials Plus**: pricing set by the certification body, not IASME directly. Typically £1,499–£4,000 + VAT for SMEs; £1,500–£8,000+ depending on device count and complexity.
- Including remediation support: £1,400–£2,500+ for SMEs.

**Lead Time**:

- CE basic: 1–4 weeks turnaround typical.
- CE+ requires independent audit; **must be booked within 3 months of basic CE being issued**, and the assessor needs roughly 3 weeks of lead time. Total typical CE+ lead time: 4–8 weeks.

> Sources: [NCSC Cyber Essentials overview](https://www.ncsc.gov.uk/cyberessentials/overview), [IASME Cyber Essentials](https://iasme.co.uk/cyber-essentials/), [Connection Technologies CE cost UK 2026](https://connection-technologies.co.uk/blog/cyber-security-cost-uk-2026), [Intelance CE cost UK 2026](https://www.intelance.co.uk/cyber-essentials-cost-uk/), [Paul Reynolds CE cost 2026 guide](https://paulreynolds.uk/cyber-essentials-certification-cost/), [BM Technologies CE cost UK 2026](https://bm-technologies.co.uk/cyber-essentials-cost-uk-2026-what-businesses-need-to-know/), [Compare The Cloud 5-person UK MSP CE practice](https://www.comparethecloud.net/articles/5-person-uk-msp-build-cyber-essentials-certification-practice-500-2000-per-assessment), [Connection Technologies CE+ UK 2026 managed certification](https://connection-technologies.co.uk/cyber-essentials), [Precursor Security CE assessor £1500](https://www.precursorsecurity.com/services/compliance/cyber-essentials-certification).

**Recommendation**: **Plan for CE basic + CE+ in year 1**. Budget £400 (CE) + £1,800–£3,000 (CE+ including remediation support) = **£2,200–£3,400 first year**, **£2,200–£3,400 annual recertification**.

**Critical lead time**: CE+ takes 4–8 weeks minimum. Apply within first 90 days of incorporation per BR-001 success criterion.

**Recommended assessor**: NCSC-licensed bodies — Precursor Security (advertised £1,500+ for CE+), Connection Technologies, Intelance, BM Technologies, IASME directly.

---

### Sub-Category 5.6: ICO Data Controller Registration

**Description**: Statutory requirement under the UK GDPR / Data Protection Act 2018 for any UK organisation processing personal data as a data controller. Annual fee.

**Pricing (2026)**:

- **Tier 1 (Micro)**: £52/year — turnover ≤ £632,000 OR ≤ 10 staff.
- **Tier 2 (SMEs)**: £78/year — turnover ≤ £36m OR ≤ 250 staff.
- **Tier 3 (Large)**: £3,763/year — does not meet tier 1 or tier 2 criteria.

> Sources: [ICO Data Protection Fee](https://ico.org.uk/for-organisations/data-protection-fee/), [ICO Guide to the Data Protection Fee](https://ico.org.uk/for-organisations/data-protection-fee/data-protection-fee/), [ICO Register page](https://ico.org.uk/for-organisations/data-protection-fee/register/), [LegalVision Data Protection Register](https://legalvision.co.uk/data-privacy-it/data-protection-register/), [Complyport ICO registration and fees](https://complyport.com/ico-data-protection-registration-and-fees-after-25-may-2018/).

**Recommendation**: **Register at Tier 2 (£78/year)**. ArcKit Consulting will likely cross the Tier 1 micro threshold (£632,000 turnover) within year 1.

---

### Sub-Category 5.7: Statutory Baseline Summary

**Year 1 Statutory Baseline TCO**:

| Item | Indicative Year 1 Cost | Annual Recurring | Lead Time |
|------|-----------------------:|-----------------:|-----------|
| PI £10m | £4,000 | £4,000 | 1–2 weeks |
| PL £5m | £400 | £400 | 1 week |
| EL £10m | £500 | £500 | 1 week |
| Cyber liability £2m | £900 | £900 | 1–2 weeks |
| Cyber Essentials | £400 + VAT | £400 + VAT | 1–4 weeks |
| Cyber Essentials Plus | £2,500 + VAT (incl. remediation support) | £2,500 + VAT | 4–8 weeks (after CE issued) |
| ICO registration (Tier 2) | £78 | £78 | Immediate |
| Companies House incorporation | £50 | £34 (annual confirmation statement) | Immediate |
| **Total year 1** | **£8,828** + VAT | **£8,812** + VAT | Critical path: CE+ (8 weeks) |

**Recommendation summary**:

- Apply for CE basic immediately on incorporation.
- Apply for CE+ within 30 days of CE being granted (within 90-day BR-001 deadline).
- Register with ICO immediately on incorporation (statutory requirement).
- Procure all four insurance lines by end of month 1.
- Total statutory baseline budget: **£9,000 (year 1) + £9,000 / year ongoing** (re-verify annually as cohort grows).

---

## Category 6: Comparator Practice Benchmarks

**Requirements Addressed**: BR-002 (Procurement framework standing), BR-004 (Sustainable revenue and margin), BR-009 (Pipeline and concentration), Stakeholder Analysis (positioning).

This category is presented in detail in Category 3 (SME-Tier and Cross-Subsidy Commercial Structures) above. The comparator summary is repeated here as a stand-alone summary table for reference:

| Practice | Legal Form | UK Public Sector Focus | SME-Tier Commitment | Closest Analogue | Differentiators |
|----------|-----------|------------------------|----------------------|------------------|------------------|
| Made Tech (LSE: MTEC) | Ltd / LSE plc | 90%+ | None | Yes — closest structural | Plc pressure; transparent rate cards |
| BJSS / CGI | Ltd (now multinational) | Mixed | None | No | Multinational scale post-acquisition |
| Equal Experts | Network model | Strong (top-3 G-Cloud supplier) | None | No | Global distribution |
| dxw | Ltd (EOT) | 100% public/third sector | None explicitly | Yes — closest values | Employee ownership trust |
| TPXImpact (LSE: TPX) | Ltd / LSE plc | 90%+ | None | Yes — comparable structural | Plc pressure |
| Public.io | Ltd | 100% gov | Via accelerator (capability uplift) | Yes — mission-aligned | GovStart accelerator route |
| Mastek | Multinational | Mixed | None | No | Multinational; NHS LPP DTCS framework |
| Snook | Ltd | Strong | None visible | No | Service design specialist |
| Caspian One | Ltd | Mixed (some public) | None | No | Financial services-leaning staffing |
| Big 4 (PwC, Deloitte, EY, KPMG) | LLP / Ltd | Mixed | None | No | High-fee incumbents; £700-£3,000+ day rates |

**ArcKit Consulting's white-space**: principled SME-tier, toolkit-anchored, evidence-grade, Ltd flexibility with B-Corp credibility overlay. No comparator combines these four; the closest are dxw (mission-aligned, employee-owned, but not SME-tier-anchored) and Made Tech (transparent, public-sector-only, but plc-pressured and not SME-tier-anchored).

---

## Build vs Buy: Aggregate 3-Year TCO Summary

Build-vs-Buy analysis applies *primarily to the operating tooling* (Category 4); pricing models, procurement routes, and legal vehicle decisions (Categories 1–3, 5–6) are **procurement / structural choices**, not engineering build-vs-buy choices. The table below captures the operating-tooling Build-vs-Buy analysis at the recommended 10-person practice scale.

### Build vs Buy: Operating Tooling Aggregate (10-Person Practice, 3-Year TCO)

| Approach | Categories Covered | Year 1 | Year 2 | Year 3 | 3-Year TCO | Rationale |
|----------|-------------------|-------:|-------:|-------:|-----------:|-----------|
| **BUILD ALL** (custom engineering for every category) | All 9 sub-categories | £230,000 | £80,000 | £80,000 | **£390,000** | Engineering effort ~25–35 person-months pre-go-live + 30–40% maintenance per year. Structurally disqualified. |
| **BUY ALL SaaS** (recommended baseline; no website build) | 9 sub-categories — SaaS only including SaaS-built website (Webflow / Squarespace) | £15,000 | £8,000 | £8,000 | **£31,000** | Pure SaaS subscription; ignores Principle 16 on website. |
| **HYBRID (RECOMMENDED)** — BUY commodity SaaS + BUILD on the public website only | 8 BUY + 1 BUILD | £13,400 | £8,330 | £8,520 | **£30,250** | Honors Principle 16 on the website; commodity BUY everywhere else. |
| **OPEN-SOURCE-FIRST** — adopt OSS for every category that has a credible OSS path | 5 OSS + 4 BUY | £25,000 | £18,000 | £18,000 | **£61,000** | OSS hosting cost dominates; many categories (HR, payroll, accounting) have no realistic OSS path in UK MTD context. |

**Recommendation**: **HYBRID at £30,250 over 3 years**. The combination of commodity BUY for most categories and a single BUILD on the website honours Principle 16 where it matters most (open source rendering of the practice's public face), without imposing the structural disqualification of building everything custom.

### Sensitivity Analysis (Hybrid Recommendation)

| Scenario | Year 1 | Year 2 | Year 3 | 3-Year TCO | Delta vs baseline |
|----------|-------:|-------:|-------:|-----------:|------------------:|
| **Baseline (10 people)** | £13,400 | £8,330 | £8,520 | £30,250 | — |
| **5-person practice** | £8,000 | £5,000 | £5,000 | £18,000 | -40% |
| **20-person practice** | £24,000 | £15,500 | £15,500 | £55,000 | +82% |
| **+10% annual SaaS price increases** | £13,400 | £9,200 | £10,100 | £32,700 | +8% |
| **Microsoft 365 Business Premium → E3** (more enterprise features) | £19,000 | £14,000 | £14,000 | £47,000 | +55% |
| **Switch to Webflow + WordPress (no Eleventy build)** | £8,000 | £8,000 | £8,000 | £24,000 | -21% |
| **Risk-adjusted (10% contingency on year-1 SaaS, 15% on website build)** | £15,000 | £8,500 | £8,700 | £32,200 | +6% |

**Risk-adjusted 3-year TCO range**: **£28,000 — £35,000** (mid-point £31,000 with sensitivities applied for typical 10-person practice).

---

## Vendor Evaluation Matrix (Operating Tooling)

Evaluation criteria weighted to Principle 1 affordability, Principle 16 open source, Principle 5 security, and Principle 17 FinOps transparency.

| Criterion | Weight |
|-----------|-------:|
| Per-user pricing transparency (Principle 17) | 20% |
| UK / EU data residency and UK GDPR compliance (Principle 7) | 20% |
| Security baseline — Cyber Essentials Plus compatible, MFA / phishing-resistant (Principle 5) | 15% |
| Integration with the recommended stack (M365, Harvest, Notion, etc.) | 15% |
| SME-friendly tier (no enterprise gatekeeping for governance-critical features — Principle 1) | 10% |
| Open standards / data portability (Principle 4) | 10% |
| Vendor maturity and support quality | 10% |
| **Total** | **100%** |

### Sub-Category Vendor Scoring (5 = excellent, 1 = poor)

| Sub-Category | Recommended Vendor | Pricing | Residency | Security | Integration | SME | Standards | Maturity | **Weighted Score** |
|--------------|-------------------|--------:|----------:|---------:|------------:|----:|----------:|---------:|-------------------:|
| 4.1 CRM | HubSpot Free → Starter | 5 | 4 | 4 | 5 | 5 | 4 | 5 | **4.55** |
| 4.2 Time Tracking | Harvest Pro | 5 | 3 | 4 | 5 | 5 | 4 | 5 | **4.40** |
| 4.3 Accounting | FreeAgent (with NatWest) | 5 | 5 | 4 | 4 | 5 | 4 | 5 | **4.70** |
| 4.4 E-Sign | Adobe Acrobat Sign | 4 | 5 | 5 | 4 | 4 | 4 | 5 | **4.45** |
| 4.5 HR / Payroll | Sage HR + Sage Payroll | 4 | 5 | 4 | 4 | 5 | 4 | 5 | **4.45** |
| 4.6 Identity | Microsoft Entra P1 (M365 BP bundled) | 4 | 5 | 5 | 5 | 4 | 4 | 5 | **4.60** |
| 4.7 MDM | Microsoft Intune (M365 BP bundled) | 4 | 5 | 5 | 5 | 4 | 4 | 5 | **4.60** |
| 4.8 KM | Notion Plus | 4 | 4 | 4 | 4 | 5 | 4 | 4 | **4.10** |
| 4.9 Website | Eleventy + x-govuk plugin | 5 | 5 | 5 | 4 | 5 | 5 | 4 | **4.75** |

**Top three weighted scores**: Eleventy + x-govuk plugin (4.75), FreeAgent (4.70), Microsoft Entra P1 / Intune (4.60).

---

## Procurement Pathway Notes — UK Government Digital Marketplace

### Practice's Own Listing Pathway

| Framework | Status as of 2026-05-07 | Recommended Action | Expected Listing Date |
|-----------|------------------------|--------------------|----------------------|
| G-Cloud 14 (RM1557.14) | Active, extended to October 2026 | Cannot apply mid-cycle | n/a |
| G-Cloud 15 | Applications closed January 2026 | Cannot apply | n/a |
| G-Cloud 16 | Pending CCS announcement | Apply at next open window | H2-2026 onward |
| DOS 6 (RM1043.8) | Live until 27 June 2026 | Cannot apply mid-cycle | n/a |
| DOS 7 (RM1043.9) | Live since 1 April 2026 | Cannot apply mid-cycle | n/a |
| DOS 8 / DSP successor | Pending CCS announcement | Apply at next open window | 2027 onwards |
| MCF3 (RM6187) | Superseded by MCF4 | n/a | n/a |
| MCF4 (RM6309) | Live until 28 July 2027 | Sub-contract under existing primes (cannot enter as new prime) | Sub-contract relationships in year 1 |
| MCF5 | Pending CCS announcement | Apply at next open window | Likely 2027 |
| Direct award (under threshold) | Available now | Active selling from incorporation | Immediate |
| NHS LPP / sector-specific frameworks | Various | Evaluate per opportunity | Year 2+ |

### Sub-Contractor Relationships to Pursue (MCF4 Primes)

Recommended relationships in year 1 (per BR-002 success criterion: at least 2 prime relationships):

- A boutique-friendly mid-tier prime (e.g., Methods, Capgemini, Atos, Wipro, Infosys, Cognizant) with a known history of SME sub-contracting.
- A Big 4 firm with a public-sector EA practice (PwC, Deloitte, EY, or KPMG) where the relationship is engagement-by-engagement rather than panel-based.
- A boutique digital-transformation prime (e.g., dxw, Made Tech, TPXImpact, Public.io) where sub-contracting can be reciprocal.

---

## Requirements Coverage Map

| Requirement | Pathway / Recommendation | Status |
|-------------|-------------------------|--------|
| BR-001: UK trading entity foundations | Ltd company; ICO Tier 2 registration; insurance package; CE+; HMRC registrations | ✅ Covered |
| BR-002: Procurement framework listings | G-Cloud 16 (apply); DOS 8 / DSP (apply when window opens); MCF4 sub-contracting (now) | ✅ Covered |
| BR-003: Onboard baseline cohort of consultants | Sage HR + Sage Payroll; Companies House / PAYE / IR35 process | ✅ Covered |
| BR-004: Sustainable revenue and margin | Hybrid pricing strategy (day-rate, fixed-price, retainer, SME-tier) | ✅ Covered |
| BR-005: SME-affordable engagement tier | SME-tier pro-rata pricing; Companies Act 2006 SME thresholds; FR-011 verification | ✅ Covered |
| BR-006: Evidence-grade governance artefacts | ArcKit toolkit + QA gate (FR-008); recommended pricing supports investment in QA | ✅ Covered |
| BR-007: Curate reusable IP and contribute back | Notion pattern library; open-source publishing route | ✅ Covered |
| BR-008: Provable confidentiality and information governance | Microsoft Entra P1 + Intune; Cyber Essentials Plus; engagement workspace isolation in M365 / SharePoint | ✅ Covered |
| BR-009: Build a qualified opportunity pipeline | HubSpot CRM; multi-route procurement strategy; concentration thresholds | ✅ Covered |
| BR-010: Structured product feedback | Notion / Confluence as structured feedback library; quarterly review with product team | ✅ Covered |
| FR-001: Opportunity capture | HubSpot CRM | ✅ Covered |
| FR-002: Proposal and SOW generation | ArcKit `/arckit:sow` + Adobe Acrobat Sign | ✅ Covered |
| FR-007: Time recording | Harvest Pro | ✅ Covered |
| FR-010: Sub-contractor management | Adobe Acrobat Sign; standard associate agreement template; PPN 03/23 prompt payment | ✅ Covered |
| FR-011: SME-tier intake and verification | Public website intake form (Eleventy); Companies House API lookup | ✅ Covered |
| FR-018: Identity and SSO | Microsoft Entra ID P1 (M365 BP bundled) | ✅ Covered |
| FR-019: Public website | Eleventy + x-govuk plugin | ✅ Covered |
| Principle 1: Equitable Access for SMEs | SME-tier pricing structure; Ltd + B-Corp pathway; cross-subsidy mechanism | ✅ Covered |
| Principle 16: Open Source First | Eleventy website (open-source); SaaS only where OSS is impractical | ✅ Covered |
| Principle 17: Cost Transparency / FinOps | Published rate cards; SaaS with transparent per-seat pricing | ✅ Covered |

**Coverage**: **100%** of in-scope BR / FR / Principle requirements have an identified commercial-model pathway.

---

## Risks and Mitigations Summary

| Risk | Category | Likelihood | Impact | Mitigation |
|------|----------|-----------|--------|------------|
| G-Cloud / DOS application rejected | Procurement | Low | High | Use specialist application support; budget £5,000 first time; thorough preparation |
| CE+ assessment fails on first attempt | Statutory | Medium | Medium | Use assessor with remediation support included; complete all CE basic remediations before booking CE+ |
| Day-rate compression on DOS specialist roles | Pricing | High | Medium | Differentiate on capability statement and named-consultant profile; refuse below-floor bids; rely on retainer / fixed-price for higher-margin work |
| SME-tier discount creep / abuse | Pricing | Medium | Medium | FR-011 verification (Companies House API lookup, self-declaration, evidence requirement); annual review |
| MCF4 sub-contractor margin compression | Procurement | High | Medium | Diversify across primes (BR-009 concentration thresholds); negotiate fair commercial terms; transparent rate transparency |
| Outcome-based pricing demanded by buyer | Pricing | Medium | Medium | UK Gov policy explicitly warns against; offer fixed-price with milestone hold-back instead |
| Operating tooling lock-in (HubSpot, Notion) | Tooling | Low | Low | All recommended SaaS provide data export; Notion exports to Markdown; HubSpot exports to CSV |
| Microsoft 365 price increase mid-term | Tooling | Medium | Low | M365 has historically increased ~10% / 2 years; sensitivity analysis covers this |
| Cross-subsidy mechanism challenged at audit | Cross-subsidy | Medium | Medium | Tax adviser sign-off on structure; transparent published reporting; legal review of inter-company arrangement |
| Conflict of interest on prime sub-contracting | Procurement | Medium | High | FR-016 CoI check; transparent declaration; refuse engagements with unmanageable conflicts |

---

## Recommended Decisions (For Practice Lead Approval)

1. **Pricing strategy**: Hybrid four-stack (day-rate, fixed-price, retainer, SME-tier pro-rata). Outcome-based pricing **not adopted** in v1.
2. **Primary procurement route**: G-Cloud (when window opens) + DOS (when window opens) + MCF4 sub-contracting (now) + direct award (under threshold).
3. **Legal vehicle**: Limited Company (Ltd) with B-Corp certification target in year 2 and EOT consideration in year 3-5. CIC **not adopted** (asset-lock structurally incompatible with cross-subsidy).
4. **Operating tooling stack**: Microsoft 365 Business Premium (Entra + Intune + Office) + Sage HR/Payroll + HubSpot CRM + Harvest + FreeAgent (or Xero) + Adobe Acrobat Sign + Notion Plus + Eleventy website. **3-year TCO £30,250** at 10-person scale (sensitivity range £18,000–£55,000 across cohort sizes).
5. **Statutory baseline**: PI £10m + PL £5m + EL £10m + Cyber liability £2m + Cyber Essentials Plus + ICO Tier 2 registration. **Year 1 TCO £8,800** + VAT.
6. **Cross-subsidy mechanism**: ≥10% post-tax net margin transferred annually to ArcKit-as-a-Service for SME free-tier capacity, reported in annual transparency report.
7. **SME-tier pricing**: 50% discount on standard rate card and fixed-price packages for verified UK SMEs (Companies Act 2006 thresholds), capped at quarterly capacity reservation of 5–8% of practice capacity.

---

## External References

> No external (non-ArcKit) source documents were provided for this research. All citations are to publicly accessible web URLs, listed inline above and consolidated below.

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

### Web Sources Consolidated (by category)

**Pricing models / day rates / consultancy benchmarks**:

- [ITJobsWatch Enterprise Architect contract rates](https://www.itjobswatch.co.uk/contracts/uk/enterprise%20architect.do)
- [Contractor UK market rates](https://www.contractoruk.com/market_rates)
- [Big 4 vs Accenture day rates analysis](https://www.linkedin.com/pulse/comparison-day-rates-between-big-four-accenture-tom-moore)
- [Consultancy.uk fees and rates](https://www.consultancy.uk/consulting-industry/fees-rates)
- [NMS Consulting fee benchmarks 2026](https://nmsconsulting.com/consulting-fees-and-pricing-in-2026/)
- [Consulting retainers 2026 pricing](https://consultfees.com/blog/consulting-retainers)
- [Matt Haycox UK consulting pricing 2026](https://matt-haycox.com/pricing/consulting-pricing/)
- [Mobilunity software consultant rates 2026](https://mobilunity.com/blog/cost-to-hire-it-consultants-in-2024/)
- [Sitcon Consulting SAP Enterprise Architect role](https://contracts.contractspy.co.uk/job/134735/sap-specialist-enterprise-enterprise-architect-at-sitcon-consulting-london-600-800-per-day/)
- [Glassdoor UK strategy consulting day rates](https://www.glassdoor.co.uk/Community/londoners-in-consulting/what-would-be-the-likely-range-for-a-contractors-day-rate-in-london-for-a-strategy-or-operations-role-if-exiting-bcg-as-a-principal)

**UK procurement frameworks**:

- [Crown Commercial Service framework agreements](https://www.crowncommercial.gov.uk/agreements)
- [CCS G-Cloud 14 RM1557.14](https://www.gca.gov.uk/agreements/RM1557.14)
- [Computer Weekly G-Cloud 15 explainer](https://www.computerweekly.com/feature/UK-governments-G-Cloud-15-framework-Everything-you-need-to-know)
- [G-Cloud 14 Lots 1-3 Supplier Guidance v1.0](https://www.contractsfinder.service.gov.uk/Notice/Attachment/72f479d9-9d4e-46f8-9557-be9200cab135)
- [Government Technology G-Cloud 14 review](https://www.governmenttechnology.co.uk/features/g-cloud-14)
- [GovData G-Cloud 14 framework support](https://govdata.co.uk/frameworks/it-pillar/g-cloud-14/)
- [Frameworker G-Cloud 14](https://www.frameworker.co.uk/articles/g-cloud-14/)
- [Advice Cloud G-Cloud guide](https://advice-cloud.co.uk/knowledge-hub/ultimate-guide-to-g-cloud/)
- [UK Government G-Cloud Wikipedia](https://en.wikipedia.org/wiki/UK_Government_G-Cloud)
- [CCS DOS 7 RM1043.9](https://www.crowncommercial.gov.uk/agreements/RM1043.9)
- [Find a Tender DOS 7 Notice](https://www.find-tender.service.gov.uk/Notice/004688-2026)
- [DOS 7 guide 2026 Gend.co](https://www.gend.co/blog/dos7-digital-outcomes-specialists-guide)
- [Bramble Hub DOS 6 framework guide](https://www.bramblehub.co.uk/frameworks/ccs-digital-outcomes-and-specialists-6-framework-dos6/)
- [Advice Cloud DOS guide](https://advice-cloud.co.uk/knowledge-hub/ultimate-guide-digital-outcomes-specialists/)
- [Tenders UK DOS guide](https://www.tenders-uk.com/knowledge-articles/digital-outcomes-and-specialists/)
- [techUK DSP framework](https://www.techuk.org/resource/new-digital-specialists-programmes-framework-for-the-public-sector.html)
- [Transform reappointed to DOS 7](https://www.transformuk.com/our-thinking/insights/transform-reappointed-to-digital-outcomes-and-specialists-7-dos-7/)
- [CCS MCF4 RM6309](https://www.crowncommercial.gov.uk/agreements/RM6309)
- [CCS MCF3 customer guidance](https://assets.crowncommercial.gov.uk/wp-content/uploads/RM6187-MCF3-Customer-Guidance-Document-.docx-2.pdf)
- [Thornton & Lowe MCF4 guide](https://thorntonandlowe.com/understanding-mcf4/)
- [D3 Tenders MCF4 contract](https://d3tenders.com/contract/?ocid=ocds-b5fd17-f72d46c7-ca51-470f-aae3-abbc579ef2e1)
- [UK Gov prompt payment policy](https://www.gov.uk/guidance/prompt-payment-policy)
- [PPN 021 payment spot checks](https://www.gov.uk/government/publications/ppn-021-payment-spot-checks-in-public-sub-contracts/ppn-021-payment-spot-checks-in-public-sub-contracts-html)
- [techUK new prompt payment standards 2024](https://www.techuk.org/resource/new-prompt-payment-standards-from-april-2024.html)
- [UK Gov consultancy spend controls](https://www.gov.uk/government/news/new-controls-across-government-to-curb-consultancy-spend-and-save-over-12-billion-by-2026)
- [UK Gov Risk Allocation and Pricing Approaches Guidance Note](https://www.gov.uk/government/publications/the-sourcing-and-consultancy-playbooks/risk-allocation-and-pricing-approaches-guidance-note-html)
- [UK Gov off-payroll IR35](https://www.gov.uk/guidance/understanding-off-payroll-working-ir35)
- [UK Gov SME definition](https://www.gov.uk/government/publications/procurement-act-2023-short-guides/supplementary-information-small-and-medium-sized-enterprises-definition-html)

**SME thresholds, IR35**:

- [Teamed UK company size thresholds 2026](https://www.teamed.global/blog/uk-company-size-thresholds-2026-april-2025-changes)
- [Kingsbridge IR35 small company threshold changes 2026](https://www.kingsbridge.co.uk/blog/contractors/ir35/ir35-small-company-threshold-changes-2026/)
- [RSM Companies Act 2006 size limits increase](https://www.rsmuk.com/insights/bridging-the-gaap/companies-act-2006-size-limits-increase-confirmed)
- [Companies Act 2006 Section 382](https://www.legislation.gov.uk/ukpga/2006/46/section/382)
- [Greenberg Traurig IR35 threshold changes 2026](https://www.gtlaw.com/en/insights/2026/3/threshold-changes-to-uk-off-payroll-working-rules-ir35-end-user-and-contractor-considerations)

**Legal vehicles (CIC, B-Corp)**:

- [Wikipedia Community Interest Company](https://en.wikipedia.org/wiki/Community_interest_company)
- [GOV.UK CIC guidance chapters](https://www.gov.uk/government/publications/community-interest-companies-how-to-form-a-cic/community-interest-companies-guidance-chapters)
- [GOV.UK Setting up a social enterprise](https://www.gov.uk/set-up-a-social-enterprise)
- [Plinth CIC complete guide](https://www.plinth.org.uk/complete-guide/what-is-a-community-interest-company)
- [Companies (Audit, Investigations and Community Enterprise) Act 2004 explanatory notes](https://www.legislation.gov.uk/ukpga/2004/27/notes/division/5/2)
- [LexisNexis B-Corps in the UK](https://www.lexisnexis.co.uk/blog/research-legal-analysis/b-the-best-you-can-b-the-rise-of-b-corps-in-the-uk)
- [Investing for Good B-Corp announcement](https://www.investingforgood.co.uk/news/24bmd3a9telslwzlww5c2dxl8jlpb9)
- [Community Southwark CIC overview](https://communitysouthwark.org/social-enterprise-community-interest-companies-cic/)

**Comparator practices**:

- [Made Tech LSE: MTEC company information](https://find-and-update.company-information.service.gov.uk/company/06591591)
- [Made Tech Frameworks](https://www.madetech.com/frameworks/)
- [UK Investor Magazine — Made Tech £19m GDS contract](https://ukinvestormagazine.co.uk/made-tech-lands-19m-contract-with-government-digital-service/)
- [TPXImpact EBITDA update](https://uk.advfn.com/market-news/article/12078/tpximpact-raises-ebitda-guidance-as-public-sector-contract-wins-exceed-110m)
- [TPXImpact Holdings press release](https://www.tipranks.com/news/company-announcements/tpximpact-holdings-plc-reports-strong-performance-amid-uk-public-sector-challenges)
- [TPXImpact frameworks page](https://www.tpximpact.com/about/frameworks)
- [TPXImpact homepage](https://www.tpximpact.com/)
- [TPXImpact Owler profile](https://www.owler.com/company/tpximpact)
- [BJSS CGI acquisition](https://www.cgi.com/en/CGI-completes-acquisition-UK-based-BJSS-deepening-presence-across-key-commercial-industries-public-sector)
- [BJSS — CGI strengthens UK presence](https://www.ainvest.com/news/cgi-strengthens-uk-presence-bjss-acquisition-2502/)
- [BJSS CB Insights profile](https://www.cbinsights.com/company/bjss)
- [BJSS Management Consulted profile](https://managementconsulted.com/bjss/)
- [Equal Experts top G-Cloud supplier](https://www.equalexperts.com/blog/whats-new/equal-experts-is-a-top-supplier-on-g-cloud/)
- [Equal Experts AWS Partner profile](https://partners.amazonaws.com/partners/001E000001OMOf7IAH/Equal%20Experts)
- [Equal Experts Google Cloud Partner profile](https://cloud.google.com/find-a-partner/partner/equal-experts-uk-ltd)
- [dxw — Digital solutions for public services](https://www.dxw.com/)
- [dxw employee-owned](https://www.dxw.com/employee-owned/)
- [dxw consultancy.uk profile](https://www.consultancy.uk/news/29160/digital-consultancy-dxw-becomes-employee-owned)
- [dxw Public sector digital agency goes employee-owned](https://www.thinkdigitalpartners.com/news/2021/09/29/public-sector-digital-agency-dxw-becomes-employee-owned/)
- [PUBLIC homepage](https://www.public.io/)
- [PUBLIC GovStart](https://www.public.io/case-study/govstart)
- [PUBLIC Reimagine and build](https://www.public.io/blog-post/reimagine-and-build-with-public)
- [Mastek public sector and government consulting](https://www.mastek.com/industries/public-sector-government/)
- [Mastek NHS DTCS framework](https://www.mastek.com/pressreleases/mastek-named-supplier-nhs-lpp-dtcs-framework-clinical-digital-transformation/)
- [The Stack — UK government cloud spend](https://www.thestack.technology/uk-government-cloud-spend-digital-suppliers/)
- [Top 15 IT companies in UK 2025 Gem Corp](https://gem-corp.tech/tech-blogs/top-it-companies-in-uk/)
- [techUK — UK Tech in 2025 and 2026](https://www.techuk.org/resource/uk-tech-in-2025-and-what-comes-next-for-2026.html)

**Operating tooling — CRM**:

- [Pipedrive vs HubSpot 2026 Monday](https://monday.com/blog/crm-and-sales/pipedrive-vs-hubspot/)
- [HubSpot vs Salesforce vs Pipedrive comparison](https://www.pipedrive.com/en/blog/hubspot-vs-salesforce-vs-pipedrive)
- [LaGrowthMachine 15 CRM examples 2026](https://lagrowthmachine.com/crm-software-examples-2026/)
- [Capsule CRM blog Pipedrive pricing comparison](https://capsulecrm.com/blog/pipedrive-crm-pricing/)
- [Salesflare CRM comparison](https://blog.salesflare.com/compare-salesforce-zoho-hubspot-pipedrive)
- [12 Best Pipedrive alternatives 2026](https://www.authencio.com/blog/12-best-pipedrive-alternatives-better-crms-for-scaling-sales-teams)
- [NuaCom Pipedrive vs HubSpot 2026 guide](https://nuacom.com/pipedrive-vs-hubspot-complete-crm-comparison-guide/)

**Operating tooling — Time tracking and invoicing**:

- [Harvest pricing 2026 Costbench](https://costbench.com/software/time-tracking/harvest/)
- [Clockify vs Harvest 2026 Plutio](https://www.plutio.com/compare/clockify-vs-harvest)
- [Capterra Harvest profile](https://www.capterra.com/p/75598/Harvest/)
- [Harvest official](https://www.getharvest.com/)
- [Harvest alternatives 2026 Productive.io](https://productive.io/blog/harvest-alternatives/)
- [TimeSentry Clockify vs Harvest](https://timesentry.ai/compare/clockify-vs-harvest)
- [Plutio 6 best Harvest alternatives 2026](https://www.plutio.com/alternatives/harvest)
- [Rize best time tracking for QuickBooks 2026](https://rize.io/blog/best-time-tracking-for-quickbooks)

**Operating tooling — Accounting**:

- [E-Accounts Xero vs QuickBooks vs FreeAgent 2026](https://www.e-accounts.co.uk/2025/12/16/xero-vs-quickbooks-vs-freeagent-uk-2026/)
- [HS Global MTD Software Xero vs QuickBooks vs FreeAgent 2026](https://www.hsglobalaccountancy.co.uk/mtd-software-landlords-xero-quickbooks-freeagent/)
- [FreeAgent pricing](https://www.freeagent.com/pricing/)
- [Heights Accountancy Xero vs QuickBooks vs FreeAgent service SMEs 2025/26](https://heightsaccountancy.co.uk/2025/10/29/xero-vs-quickbooks-vs-freeagent-uk-service-smes-2025-26/)
- [TaxCareAcademy FreeAgent vs Xero 2026](https://taxcareacademy.co.uk/freeagent-vs-xero-comparison/)
- [Golden Tree best accounting software UK 2026](https://www.goldentreeconsulting.co.uk/blog/best-accounting-software-for-sole-traders-uk-2026-xero-vs-quickbooks-vs-freeagent/)
- [GoForma FreeAgent vs Xero 2026](https://www.goforma.com/freeagent/freeagent-vs-xero)

**Operating tooling — E-sign**:

- [DocuSign UK pricing](https://ecom.docusign.com/plans-and-pricing/esignature)
- [eSignGlobal UK eSign provider pricing](https://www.esignglobal.com/blog/united-kingdom-docusign-subscription-plans-gbp)
- [PandaDoc Adobe Sign vs DocuSign 2026](https://www.pandadoc.com/blog/adobe-sign-vs-docusign-comparison/)
- [Adobe Sign pricing 2026 Signeasy](https://signeasy.com/blog/business/adobe-sign-pricing)
- [Eversign DocuSign pricing 2026](https://eversign.com/blog/docusign-pricing-plans-cost-alternatives)
- [Juro Adobe Sign vs DocuSign 2026](https://juro.com/learn/adobe-sign-vs-docusign-comparison)
- [eSign.co.uk best 10 providers UK 2026](https://www.esign.co.uk/resources/news-and-insights/the-top-electronic-signature-providers/)
- [Signeasy DocuSign pricing 2026](https://signeasy.com/blog/business/docusign-pricing)
- [eSign.ai GDPR-compliant e-signature](https://www.esign.ai/blog/gdpr-compliant-e-signature-eu-clients)

**Operating tooling — HR/Payroll**:

- [Stribe HR software for small UK businesses 2026](https://stribehq.com/resources/best-hr-software-small-businesses/)
- [Zelt 10 best HR software UK 2026](https://zelt.app/blog/best-hr-software-uk/)
- [BambooHR pricing 2026 Pin](https://www.pin.com/blog/bamboohr-pricing/)
- [BambooHR official pricing](https://www.bamboohr.com/pricing/)
- [Theadcompare top 11 HR software UK 2026](https://theadcompare.com/software/hr/)
- [Zelt best HR software for small business UK 2026](https://zelt.app/blog/best-hr-software-for-small-business-uk/)
- [BrightHR pricing](https://www.brighthr.com/uk/)
- [Sage HR pricing](https://www.sage.com/en-gb/sage-business-cloud/people/)
- [PeopleManagingPeople BambooHR pricing tiers 2026](https://peoplemanagingpeople.com/tools/bamboohr-pricing/)
- [TreeGarden BambooHR pricing 2026](https://treegarden.io/blog/bamboohr-pricing-2026/)
- [SoftwareFinder BambooHR](https://softwarefinder.com/hr/bamboohr)
- [LondonLovesBusiness best HR software UK 2026](https://londonlovesbusiness.com/best-hr-software-in-the-uk-top-10-platforms-ranked-for-2026/)

**Operating tooling — Identity / SSO**:

- [SoftwarePricingGuide Okta vs Entra ID 2026](https://softwarepricingguide.com/okta-vs-microsoft-entra-id-pricing-2026-the-real-cost-of-identity-sso-mfa-and-governance/)
- [Stabilise UK IAM SSO comparison](https://stabilise.io/blog-pages/blog/identity-management-platform-showdown-which-sso-and-iam-solution-works-best-for-uk-businesses)
- [JumpCloud pricing 2026 CheckThat](https://checkthat.ai/brands/jumpcloud/pricing)
- [JumpCloud Comparing Entra ID and Intune](https://jumpcloud.com/blog/comparing-jumpcloud-azure-ad-intune)
- [JumpCloud Google Cloud Identity vs Entra ID](https://jumpcloud.com/blog/google-cloud-identity-azure-active-directory)
- [JumpCloud vs Okta Infisign](https://www.infisign.ai/blog/jumpcloud-vs-okta)
- [JumpCloud Entra ID free tier guide](https://jumpcloud.com/blog/understanding-aad-pricing-free)
- [JumpCloud comparing best IAM solutions enterprises 2026](https://jumpcloud.com/blog/comparing-the-best-iam-solutions-for-enterprises-in-2025)
- [AccessOwl true cost of JumpCloud IAM 2026](https://www.accessowl.com/blog/true-cost-of-jumpcloud-identity-and-access-management)
- [TechnologyMatch Ping Identity vs Okta vs OneLogin 2026](https://technologymatch.com/blog/ping-identity-vs-okta-vs-onelogin-an-iam-comparison-guide-in-2026)

**Operating tooling — MDM**:

- [Stabilise Jamf Pro vs Intune vs Iru UK 2026](https://stabilise.io/blog/jamf-pro-vs-microsoft-intune-vs-iru-apple-mdm-comparison-2026)
- [nDuo Apple MDM comparison UK 2026](https://nduo.co.uk/mdm-comparison-uk-2026/)
- [TechnologyMatch Intune vs Jamf vs Kandji 2026](https://technologymatch.com/blog/intune-vs-jamf-pro-vs-kandji-the-it-leaders-guide-to-apple-management-in-2026)
- [Connection Technologies best MDM solutions UK 2026](https://connection-technologies.co.uk/blog/mdm-solutions-uk-compared)
- [Asset Management for Jira Microsoft Intune pricing 2026](https://assetmanagementforjira.com/blog/microsoft-intune-pricing-a-no-nonsense-breakdown)
- [Costbench Intune pricing 2026](https://costbench.com/software/mdm/microsoft-intune/)
- [SIIT 10 best remote device management 2026](https://www.siit.io/blog/remote-device-management-platform)
- [DapriPro MDM solutions compared 2026](https://dapripro.com/mobile-device-management-mdm-solutions-compared-for-2026/)
- [Asset Management for Jira Kandji Iru 2026 guide](https://assetmanagementforjira.com/blog/kandji-mdm-(now-iru)-complete-guide-for-it-teams)
- [SIIT Jamf vs Kandji 2026](https://www.siit.io/tools/comparison/jamf-vs-kandji)

**Operating tooling — Knowledge Management**:

- [eesel AI Confluence vs Notion vs SharePoint 2026](https://www.eesel.ai/blog/confluence-vs-notion-vs-sharepoint)
- [Docsie Confluence vs Notion enterprise comparison 2026](https://www.docsie.io/blog/articles/confluence-vs-notion-enterprise-comparison-2026/)
- [Atlasworkspace 8 best knowledge management tools 2026](https://www.atlasworkspace.ai/blog/best-knowledge-management-software)
- [Softgile Confluence pricing 2026](https://softgile.com/en/confluence-pricing-2026/)
- [Costbench Notion pricing 2026](https://costbench.com/software/project-management/notion/)
- [SIIT 8 best knowledge management tools 2026](https://www.siit.io/blog/tools-for-knowledge-management)
- [Toolradar Confluence vs SharePoint 2026](https://toolradar.com/blog/confluence-vs-sharepoint)
- [Sesame Disk Enterprise collaboration platforms](https://sesamedisk.com/enterprise-collaboration-platforms-comparison/)
- [Docsie Confluence vs Notion pricing 2026](https://www.docsie.io/blog/articles/confluence-vs-notion-pricing-comparison-2026/)
- [Stravito 16 best SharePoint alternatives 2026](https://www.stravito.com/resources/best-sharepoint-alternatives)

**Operating tooling — Public website**:

- [Eleventy.dev official](https://www.11ty.dev/)
- [Nikolaos Gkionis govuk-11ty Eleventy template](https://github.com/Nikolaos-Gkionis/govuk-11ty/)
- [wearefuturegov gov-uk-eleventy-kit](https://github.com/wearefuturegov/gov-uk-eleventy-kit)
- [GOV.UK Eleventy Plugin x-govuk](https://govuk-eleventy-plugin.x-govuk.org/get-started/design/)
- [GOV.UK Design System home](https://design-system.service.gov.uk/)
- [alphagov product-page-example-11ty](https://github.com/alphagov/product-page-example-11ty)
- [Inside GOV.UK creating publishing design guide](https://insidegovuk.blog.gov.uk/2025/02/25/creating-the-gov-uk-publishing-design-guide/)
- [Eleventy GovUK Vercel deployment example](https://eleventy-govuk.vercel.app/)
- [Eleventy Design System Netlify](https://eleventy-design-system.netlify.app/)
- [X-GOVUK GovUK Design History](https://x-govuk.github.io/govuk-design-history/get-started/)

**Insurance**:

- [Paterson Insurance Brokers PI 2026 guide](https://www.patersonib.co.uk/2026/04/04/professional-indemnity-insurance-a-concise-2026-guide-for-uk-professionals/)
- [AXA UK PI cost guide](https://www.axa.co.uk/business-insurance/professional-indemnity/how-much-does-professional-indemnity-insurance-cost/)
- [Trust My Policy PI cost UK 2026](https://trustmypolicy.com/professional-indemnity-insurance-uk-cost/)
- [Simply Business PI insurance](https://www.simplybusiness.co.uk/business-insurance/professional-indemnity-insurance/)
- [Hiscox PI insurance cost FAQ](https://www.hiscox.co.uk/business-insurance/professional-indemnity-insurance/faq/how-much-does-professional-indemnity-insurance-cost)
- [Coverfinder Public Liability Insurance Cost UK 2026](https://coverfinder.co.uk/public-liability/costs-2/)
- [Coverfinder Public Liability quotes 2026](https://coverfinder.co.uk/public-liability/costs/)
- [PolicyBee PI insurance cost](https://www.policybee.co.uk/blog/how-much-is-professional-indemnity-insurance)
- [Premierline real cost PI](https://www.premierline.co.uk/insight-hub/the-real-cost-of-professional-indemnity-insurance/)
- [NimbleFins average PI cost](https://www.nimblefins.co.uk/business-insurance/professional-indemnity-insurance/average-cost-professional-indemnity-insurance)

**Cyber Essentials Plus**:

- [NCSC Cyber Essentials overview](https://www.ncsc.gov.uk/cyberessentials/overview)
- [IASME Cyber Essentials](https://iasme.co.uk/cyber-essentials/)
- [Connection Technologies CE cost UK 2026](https://connection-technologies.co.uk/blog/cyber-security-cost-uk-2026)
- [Intelance CE cost UK 2026](https://www.intelance.co.uk/cyber-essentials-cost-uk/)
- [Paul Reynolds CE cost 2026 guide](https://paulreynolds.uk/cyber-essentials-certification-cost/)
- [BM Technologies CE cost UK 2026](https://bm-technologies.co.uk/cyber-essentials-cost-uk-2026-what-businesses-need-to-know/)
- [Compare The Cloud 5-person UK MSP CE practice](https://www.comparethecloud.net/articles/5-person-uk-msp-build-cyber-essentials-certification-practice-500-2000-per-assessment)
- [Connection Technologies CE+ UK 2026 managed certification](https://connection-technologies.co.uk/cyber-essentials)
- [Precursor Security CE assessor £1500](https://www.precursorsecurity.com/services/compliance/cyber-essentials-certification)

**ICO data protection registration**:

- [ICO Data Protection Fee](https://ico.org.uk/for-organisations/data-protection-fee/)
- [ICO Guide to the Data Protection Fee](https://ico.org.uk/for-organisations/data-protection-fee/data-protection-fee/)
- [ICO Register page](https://ico.org.uk/for-organisations/data-protection-fee/register/)
- [ICO Registration FAQs](https://ico.org.uk/for-organisations/data-protection-fee/faqs-data-protection-fee-payment-and-online-registration/)
- [ICO Extraterritorial organisations](https://ico.org.uk/for-organisations/data-protection-fee/paying-a-data-protection-fee-what-do-you-need-to-know/extraterritorial-organisations/)
- [DLA Piper UK registration](https://www.dlapiperdataprotection.com/index.html?t=registration&c=GB)
- [LegalVision Data Protection Register](https://legalvision.co.uk/data-privacy-it/data-protection-register/)
- [LegalVision paying ICO data protection fee](https://legalvision.co.uk/business-data-protection-fee/)
- [Complyport ICO registration and fees](https://complyport.com/ico-data-protection-registration-and-fees-after-25-may-2018/)
- [GDPR Compliance Cost 2026 reference](https://gdprcompliancecost.com/)

**Outcome-based pricing / risk allocation**:

- [Resultsense — UK consultancy cuts vs AI ambition](https://www.resultsense.com/news/2026-05-05-uk-consultancy-cuts-vs-ai-ambition-tension/)
- [Mordor Intelligence UK Management Consulting Services Market](https://www.mordorintelligence.com/industry-reports/united-kingdom-management-consulting-services-market)
- [Freshminds Evolving consultancy business models 2026](https://www.freshminds.co.uk/blog/2026/03/how-consulting-firms-are-adapting-to-evolving-business-models)
- [Consultancy.uk UK consultancy outcome-based delivery](https://www.consultancy.uk/news/43153/uk-consultancy-builds-outcome-based-delivery-infrastructure)
- [Simon-Kucher outcomes-based contracting](https://www.simon-kucher.com/en/insights/transform-your-revenue-model-outcomes-based-contracting)
- [UCCC value recognition crisis UK consultancy](https://uccc.co.uk/value-recognition-crisis-uk-consultancy-revenue-shortfall/)
- [Mordor Intelligence UK IT services market 2031](https://www.mordorintelligence.com/industry-reports/united-kingdom-itservices-market)

---

## Spawned Knowledge

The following standalone knowledge files were created or updated from this research:

### Vendor Profiles (created in `projects/003-arckit-consulting/vendors/`)

- `vendors/hubspot-profile.md` — Created (CRM, recommended for Sub-Category 4.1)
- `vendors/harvest-profile.md` — Created (Time tracking, recommended for Sub-Category 4.2)
- `vendors/freeagent-profile.md` — Created (Accounting, recommended for Sub-Category 4.3)
- `vendors/microsoft-profile.md` — Created (Identity, MDM, KM via M365 stack, recommended across Sub-Categories 4.6, 4.7)
- `vendors/sage-profile.md` — Created (HR, Payroll, recommended for Sub-Category 4.5)
- `vendors/notion-profile.md` — Created (KM, recommended for Sub-Category 4.8)
- `vendors/iasme-profile.md` — Created (Cyber Essentials Plus assessor, recommended in Sub-Category 5.5)
- `vendors/made-tech-profile.md` — Created (Comparator practice, Category 6)
- `vendors/dxw-profile.md` — Created (Comparator practice, Category 6)
- `vendors/equal-experts-profile.md` — Created (Comparator practice, Category 6)

### Tech Notes (created in `projects/003-arckit-consulting/tech-notes/`)

- `tech-notes/uk-procurement-frameworks-2026.md` — Created (G-Cloud / DOS / MCF reference for ArcKit Consulting and other projects)
- `tech-notes/uk-consulting-pricing-models.md` — Created (Day-rate / fixed-price / retainer / outcome-based reference)
- `tech-notes/uk-sme-thresholds-2026.md` — Created (Companies Act 2006 thresholds, IR35 implications, ICO fee tiers)
- `tech-notes/cyber-essentials-plus-process.md` — Created (CE / CE+ certification process, lead times, assessor market)
- `tech-notes/legal-vehicle-comparison-uk-consulting.md` — Created (Ltd / LLP / CIC / B-Corp comparison)
- `tech-notes/govuk-design-system-eleventy.md` — Created (x-govuk plugin and Eleventy patterns for non-government public websites)

---

**Generated by**: ArcKit `/arckit:research` agent
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit Consulting (Project 003)
**AI Model**: claude-opus-4-7[1m]
