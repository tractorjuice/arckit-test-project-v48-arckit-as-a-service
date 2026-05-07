# UK Grants Research: arckit-saas

> **Template Origin**: Official | **ArcKit Version**: 4.18.0 | **Command**: `/arckit.grants`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GRNT-001-v1.0 |
| **Document Type** | Grants Research (GRNT) |
| **Project** | 001-arckit-saas |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Date Issued** | 2026-05-07 |
| **Next Review** | 2026-08-07 |
| **Owner** | Mark Craddock |
| **Distribution** | ArcKit team, Service Owner, CCS liaison, GDS, CDDO |
| **Rubric Used** | grants-uk-gov |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-07 | ArcKit AI | Initial creation from `/arckit:grants` command — UK-Gov rubric | PENDING | PENDING |

---

## Document Purpose

This document identifies and evaluates UK funding opportunities relevant to the **ArcKit as a Service** project, including government R&D grants, charitable foundations, social-impact investors, and accelerator programmes. Each opportunity is scored against the project profile using the `grants-uk-gov` rubric (six weighted criteria: eligibility fit, funding-size fit, timing fit, complexity burden, historic traction, match-funding burden).

## Executive Summary

ArcKit as a Service is a multi-tenant UK-resident SaaS for SME architecture governance, with a free tier for verified UK SMEs supplying government (Procurement Act 2023 SME-spend support), AI-assisted artefact generation via a pluggable provider abstraction, and a G-Cloud / TCoP / GDS Service Standard / NCSC CAF / UK GDPR / WCAG 2.2 AA compliance posture. The project is currently TRL 5 (multi-tenant SaaS in build through Alpha/Beta with GA target 2027-04-30 per ARC-001-SOBC) and seeks single-grant capital in the £100,000 — £600,000 window, with grant stacking envisaged across multiple bodies.

**Top 3 Actionable Programmes (next 60 days):**

1. **Wayra UK Open Innovation Programme** (rank 2, score 73, High) — rolling intake; sector-perfect; SME/startup eligible. Equity-based investment, not grant — but immediately actionable. (`WAYRA-UK-1`)
2. **UKRI Future Leaders Fellowships Round 11** (rank 3, score 70, High) — opening-soon, deadline 2026-06-16 (40 days). Academic partnership required; FLF awards typically £1M+ over 7 years. (`UKRI-FLF-11`)
3. **Innovate UK Frontier AI Discovery** (rank 16, score 61, Medium) — open, deadline 2026-06-10 (34 days). Award £25,000 — £50,000 (discovery-tier) with 30% match; sole-applicant route OK. Best fit for funding the FR-004 / G-8 pluggable-AI feasibility sprint. (`IUK-FAID-1`)

**Total Potential Funding (High-band programmes):** £350,100 — £8,550,000.

> **Note on totals.** Sum of `award_min`/`award_max` across the 4 High-band programmes: NESTA-1 historical aggregate (£100 — £8,000,000), WAYRA-UK-1 (£50,000 — £250,000), UKRI-FLF-11 (amount unspecified), IUK-CYBR-1 (£300,000 flat). Excluding the historical Nesta aggregate, the actionable High-band range is **£350,000 — £550,000**.

**Score-band distribution:**

| Band | Count |
|------|-------|
| High | 4 |
| Medium | 46 |
| Low | 3 |
| **Total programmes assessed** | **53** |

**Rubric used:** `grants-uk-gov` — six weighted criteria with funder-type bonuses (Innovate UK / UKRI council / GDS / NCSC / DSIT) and adjustments for tight deadlines (&lt; 21 days), international geography, EU-programme post-Brexit access, TRL band mismatch, and missing-data defaults.

## Project Funding Profile

| Attribute | Value |
|-----------|-------|
| **Sector (primary)** | digital |
| **Sectors (full)** | digital, ai, cross-sector |
| **Organisation Type** | sme |
| **TRL Level** | 5 |
| **TRL Estimation Note** | TRL 5 estimated from project maturity signals — multi-tenant SaaS in build through Alpha/Beta with GA target 2027-04-30 per ARC-001-SOBC. Technology validated in relevant environment (private alpha + planned pilot with 3 buying authorities pre-GA). |
| **Funding Sought** | £100,000 — £600,000 |
| **Budget Basis** | Capital build £1.65M (per SOBC Option 2). Single-grant ask sized for typical Innovate UK Smart-class window £100k — £600k. Stacking multiple grants envisaged. |
| **Project Start** | 2026-09-30 |
| **Key Objectives** | Multi-tenant UK-resident SaaS for SME architecture governance (BR-001, BR-007); Free tier for verified UK SMEs supplying government — Procurement Act 2023 SME-spend support (Principle 1, BR-001); AI-assisted artefact generation with pluggable provider abstraction (FR-004, ADR pluggable AI); G-Cloud listing and TCoP/GDS Service Standard / NCSC CAF / UK GDPR / WCAG 2.2 AA evidence pack (BR-004, BR-006); Cross-subsidy unit economics — large-enterprise tier funds SME tier (BR-005); Sovereign-ready single codebase shared with Project 002 (Principle 21). |

## Scored Programmes — Summary Comparison

| Rank | Funder | Programme | Funder Type | Status | Deadline | Award Range | Score | Band |
|------|--------|-----------|-------------|--------|----------|-------------|-------|------|
| 1 | Nesta | Nesta Grants (historical portfolio) | charitable-foundation | unknown | — | £100 — £8,000,000 | 76 | High |
| 2 | Wayra UK (Telefonica) | Wayra UK Open Innovation Programme | corporate-vc | rolling | rolling | £50,000 — £250,000 | 73 | High |
| 3 | UK Research and Innovation | Future Leaders Fellowships Round 11 | ukri-council | opening-soon | 2026-06-16 | — | 70 | High |
| 4 | Innovate UK | Contracts for Innovation: Cyber Scale in Critical Sectors | innovate-uk | opening-soon | 2026-06-10 | £300,000 | 70 | High |
| 5 | Innovate UK | Innovate UK Innovation Loans Round 25 | innovate-uk | closed | 2026-03-04 | £100,000 — £5,000,000 | 69 | Medium |
| 6 | Joseph Rowntree Reform Trust | JRRT Democracy Priorities Funding | charitable-foundation | rolling | rolling | £1,000 — £300,000 | 67 | Medium |
| 7 | Nesta Challenge Works | Metascience Novelty Indicators Challenge | charitable-foundation | open | 2026-03-31 | up to £300,000 | 67 | Medium |
| 8 | Innovate UK | Knowledge Transfer Partnership: 2026-2027 Round 1 | innovate-uk | opening-soon | 2026-04-01 | — | 66 | Medium |
| 9 | Fair By Design | Fair By Design Venture Fund | social-impact-investor | open | rolling | — | 66 | Medium |
| 10 | PUBLIC | GovStart Accelerator | accelerator | unknown | — | — | 65 | Medium |
| 11 | Plexal & NCSC | NCSC for Startups | accelerator | unknown | — | — | 65 | Medium |
| 12 | Resonance | Resonance Enterprise Investment Fund | social-impact-investor | open | rolling | £25,001 — £250,000 | 65 | Medium |
| 13 | Innovate UK | Frontier AI Benchmarking Datasets | innovate-uk | open | 2026-05-27 | £500,000 — £750,000 | 64 | Medium |
| 14 | Plexal & DSIT | Cyber Runway | accelerator | closed | — | — | 63 | Medium |
| 15 | Tech Nation | Upscale | accelerator | unknown | — | — | 62 | Medium |
| 16 | Innovate UK | Frontier AI Discovery | innovate-uk | open | 2026-06-10 | £25,000 — £50,000 | 61 | Medium |
| 17 | Sustainable Ventures | National Climate Tech Accelerator (NCTA) | accelerator | open | — | — | 61 | Medium |
| 18 | Bethnal Green Ventures | BGV Tech for Good Accelerator - Autumn 2026 | accelerator | opening-soon | — | £60,000 | 61 | Medium |
| 19 | Social Investment Business | Community Builders Fund | social-impact-investor | rolling | rolling | £100,000 — £1,500,000 | 61 | Medium |
| 20 | Nesta Challenge Works | Water Efficiency Lab 1 | charitable-foundation | open | 2026-03-10 | up to £5,000,000 | 60 | Medium |
| 21 | Innovate UK | Innovate UK Growth Catalyst - Investor Partnerships Round 2 | innovate-uk | closed | 2026-02-03 | £50,000 — £2,000,000 | 60 | Medium |
| 22 | Digital Catapult | QTAP in Partnership with NQCC SparQ | accelerator | open | 2026-05-12 | — | 59 | Medium |
| 23 | Innovate UK | Secure Software for Resilient Growth | innovate-uk | closed | 2026-04-29 | £250,000 — £750,000 | 59 | Medium |
| 24 | European Innovation Council | EIC Accelerator 2026 (Grant-only for UK applicants) | eu-programme | open | 2026-10-28 | up to £2,100,000 | 59 | Medium |
| 25 | Ordnance Survey & HM Land Registry | Geovation Accelerator Programme - Autumn 2026 | accelerator | opening-soon | — | £20,000 | 57 | Medium |
| 26 | National Lottery Community Fund | Reaching Communities England | charitable-foundation | open | — | £20,001 — £20,000,000 | 55 | Medium |
| 27 | Ufi VocTech Trust | VocTech Challenge | charitable-foundation | closed | — | £200,000 — £250,000 | 55 | Medium |
| 28 | PUBLIC & AWS | AWS Defence Accelerator | accelerator | unknown | — | — | 55 | Medium |
| 29 | Tech Nation | Future Fifty 2026 | accelerator | closed | — | — | 55 | Medium |
| 30 | Digital Catapult | Future Networks Lab Accelerator | accelerator | unknown | — | £17,000 | 52 | Medium |
| 31 | Innovate UK | AI Champions: Frontier AI Phase 1 | innovate-uk | closed | 2026-04-29 | £150,000 — £250,000 | 51 | Medium |
| 32 | Carbon13 | Venture Launchpad (Cohort 5) | accelerator | rolling | rolling | £200,000 | 50 | Medium |
| 33 | Connected Places Catapult | Rail Stations Innovation Accelerator | accelerator | unknown | — | £49,000 | 49 | Medium |
| 34 | Social Investment Business | Flexible Finance | social-impact-investor | rolling | rolling | — | 49 | Medium |
| 35 | National Lottery Community Fund | Fairer Life Chances Scotland | charitable-foundation | open | — | £20,001 — £500,000 | 49 | Medium |
| 36 | Ufi VocTech Trust | VocTech Activate | charitable-foundation | closed | — | £30,000 — £60,000 | 48 | Medium |
| 37 | Better Society Capital | Better Society Capital - Fund of Funds | social-impact-investor | unknown | — | — | 47 | Medium |
| 38 | National Lottery Community Fund | National Lottery Awards for All England | charitable-foundation | open | — | £300 — £20,000 | 47 | Medium |
| 39 | Social Investment Business | Energy Resilience Fund | social-impact-investor | rolling | rolling | £25,000 — £250,000 | 46 | Medium |
| 40 | Esmee Fairbairn Foundation | Main Grants and Funding Plus | charitable-foundation | open | — | — | 46 | Medium |
| 41 | WCIT Charity | IT4Good Grant Programme | charitable-foundation | open | 2026-05-20 | £15,000 | 46 | Medium |
| 42 | Ufi VocTech Trust | VocTech Ignite | charitable-foundation | closed | — | — | 46 | Medium |
| 43 | Ordnance Survey & HM Land Registry | Geovation Accelerator Programme - Spring 2026 | accelerator | closed | 2026-02-28 | £20,000 | 45 | Medium |
| 44 | Indigo Trust | Indigo Trust Grants | charitable-foundation | closed | — | £222 — £1,000,000 | 45 | Medium |
| 45 | Esmee Fairbairn Foundation | Esmee Fairbairn Main Fund | charitable-foundation | rolling | rolling | from £30,000 | 45 | Medium |
| 46 | Social Investment Business | Reach Fund | social-impact-investor | rolling | rolling | £5,000 — £15,000 | 43 | Medium |
| 47 | Paul Hamlyn Foundation | Paul Hamlyn Foundation Open Funds | charitable-foundation | unknown | — | — | 43 | Medium |
| 48 | National Lottery Community Fund | Awards for All England - Environment | charitable-foundation | open | — | £300 — £20,000 | 43 | Medium |
| 49 | Nesta Challenge Works | Longitude Prize on ALS | charitable-foundation | closed | 2025-06-25 | up to £7,500,000 | 40 | Medium |
| 50 | Nesta | Collective Intelligence Grants | charitable-foundation | closed | — | £30,000 | 39 | Low |
| 51 | Lloyds Bank Foundation for England and Wales | Specialist and Equity Programmes | charitable-foundation | opening-soon | — | £75,000 | 38 | Low |
| 52 | Nesta | Mission Studio | charitable-foundation | unknown | — | — | 36 | Low |
| 53 | Lankelly Chase Foundation | Lankelly Chase Endowment Redistribution | charitable-foundation | closed | — | — | 35 | Low |

## Per-Programme Detail

<!-- One block per programme, sorted by rank ascending. Each block carries: full score breakdown, score rationale, evidence, citation_id, fetched_from_url, confidence. -->

### #1 — Nesta Grants (historical portfolio) — Score 76 (High)

| Attribute | Value |
|-----------|-------|
| Funder | Nesta |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | NESTA-1 |
| Source URL | https://grantnav.threesixtygiving.org/org/GB-CHC-1144091 |
| Programme URL | https://www.nesta.org.uk/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | unknown |
| Eligible Org Types | charity, academic, sme |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £100 — £8,000,000 |
| Historical Grants Count | 1637 |

**Score breakdown:** eligibility_fit 33 · funding_size_fit 20 · timing_fit 7 · complexity_burden 3 · historic_traction 7 · match_funding_burden 5 → **76 (High)**

**Rationale:** Strong eligibility (SME accepted, sectors match digital/AI/cross-sector, large historic volume 1637 grants); award range fully contains project budget. Caveat: this is a historical Nesta-portfolio aggregate from GrantNav — NOT a single open call. Use to identify Nesta thematic priorities, not as a direct application target.

### #2 — Wayra UK Open Innovation Programme — Score 73 (High)

| Attribute | Value |
|-----------|-------|
| Funder | Wayra UK (Telefonica) |
| Funder Type | corporate-vc |
| Funder Category | accelerator |
| Citation | WAYRA-UK-1 |
| Source URL | https://wayra.co.uk/ |
| Programme URL | https://wayra.co.uk/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | low |
| Application Status | rolling |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award Range | £50,000 — £250,000 |
| Partnership Required | false |

**Score breakdown:** eligibility_fit 30 · funding_size_fit 14 · timing_fit 13 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **73 (High)**

**Rationale:** Rolling intake, SME/startup eligible, sector-perfect (digital/AI/cross-sector), award range partial-overlaps project budget. Funder-type bonus negative (corporate-vc) but eligibility composite still strong. Equity-based investment, not grant.

### #3 — UKRI Future Leaders Fellowships Round 11 — Score 70 (High)

| Attribute | Value |
|-----------|-------|
| Funder | UK Research and Innovation |
| Funder Type | ukri-council |
| Funder Category | government-rd |
| Citation | UKRI-FLF-11 |
| Source URL | https://www.ukri.org/opportunity/future-leaders-fellowship-round-11/ |
| Programme URL | https://www.ukri.org/opportunity/future-leaders-fellowship-round-11/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | opening-soon |
| Deadline | 2026-06-16 |
| Eligible Org Types | sme, large-enterprise, academic, research-organisation, charity, public-sector |
| Eligible Sectors | cross-sector, digital, ai |
| Geography | uk-wide |
| Application Complexity | high |
| Partnership Required | true (academic) |

**Score breakdown:** eligibility_fit 35 · funding_size_fit 10 · timing_fit 12 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **70 (High)**

**Rationale:** Open round at UKRI deadline 2026-06-16 (40 days). Eligibility composite at ceiling — sector overlap perfect (cross-sector/digital/AI), SME accepted, ukri-council bonus +10. Funding size missing but FLF awards typically £1M+ over 7 years. Academic partnership required.

### #4 — Innovate UK Contracts for Innovation: Cyber Scale in Critical Sectors — Score 70 (High)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-CYBR-1 |
| Source URL | https://apply-for-innovation-funding.service.gov.uk/competition/2452/overview/df0addbf-9146-4b7f-b8b5-e78470917675 |
| Programme URL | (same) |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | opening-soon |
| Deadline | 2026-06-10 |
| Eligible Org Types | sme, startup, large-enterprise, any |
| Eligible Sectors | digital, health, energy, transport, spacetech, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £300,000 (flat) |
| Match Funding Required | false |
| TRL Band | 7 — 8 |

**Score breakdown:** eligibility_fit 23 · funding_size_fit 14 · timing_fit 12 · complexity_burden 6 · historic_traction 5 · match_funding_burden 10 → **70 (High)**

**Rationale:** Opening soon, deadline 2026-06-10 (34 days). 'Any' organisation type accepted; £300k flat award partially overlaps project budget; no match funding required. TRL band 7-8 mismatches project TRL 5 — ZERO score on TRL component pulls eligibility down despite Innovate UK bonus.

### #5 — Innovate UK Innovation Loans Round 25 — Score 69 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-LOAN-25 |
| Source URL | https://apply-for-innovation-funding.service.gov.uk/competition/2373/overview/609dc5dd-d3e8-4f51-af3a-3eb1b3314710 |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Deadline | 2026-03-04 |
| Eligible Org Types | sme |
| Eligible Sectors | digital, ai, health, energy, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £100,000 — £5,000,000 |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 31 · funding_size_fit 20 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 10 → **69 (Medium)**

**Rationale:** SME-only, sector-strong (digital/AI/cross-sector), award range fully contains project budget, no match funding. Round 25 closed 2026-03-04 — track Round 26 announcement. High complexity is loan-style application.

### #6 — JRRT Democracy Priorities Funding — Score 67 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Joseph Rowntree Reform Trust |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | JRRT-1 |
| Source URL | https://www.jrrt.org.uk/apply-for-a-grant/what-we-fund/ |
| Programme URL | https://www.jrrt.org.uk/apply-for-a-grant/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | rolling |
| Eligible Org Types | charity, any |
| Eligible Sectors | cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award Range | £1,000 — £300,000 |

**Score breakdown:** eligibility_fit 24 · funding_size_fit 14 · timing_fit 13 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **67 (Medium)**

**Rationale:** Rolling open intake; 'any' organisation type accepted; £1k — £300k award range partially overlaps. Cross-sector match modest. JRRT focus on democracy/governance is loosely aligned to public-sector tooling theme.

### #7 — Metascience Novelty Indicators Challenge — Score 67 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Nesta Challenge Works |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | CW-MNI-1 |
| Source URL | https://challengeworks.org/about-challenge-prizes/our-challenge-prizes/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Deadline | 2026-03-31 |
| Eligible Org Types | sme, academic, research-organisation, consortium |
| Eligible Sectors | data, ai, digital |
| Geography | uk-wide |
| Application Complexity | medium |
| Award (max) | £300,000 |

**Score breakdown:** eligibility_fit 26 · funding_size_fit 10 · timing_fit 15 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **67 (Medium)**

**Rationale:** Status open per reader, but listed deadline 2026-03-31 has passed — refresh required before action. SME accepted, sectors digital/AI/data overlap project profile. Challenge-prize structure suits demonstrable AI-assisted innovation.

### #8 — Innovate UK KTP 2026-2027 Round 1 — Score 66 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-KTP-2627-1 |
| Source URL | https://iuk-business-connect.org.uk/opportunities/knowledge-transfer-partnership-ktp-2026-2027-round-1/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | opening-soon |
| Deadline | 2026-04-01 |
| Eligible Org Types | sme, large-enterprise, academic, research-organisation, consortium |
| Eligible Sectors | digital, ai, advanced-manufacturing, health, creative, energy, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Match Funding | required, 33% |
| Partnership Required | true (academic) |

**Score breakdown:** eligibility_fit 29 · funding_size_fit 10 · timing_fit 12 · complexity_burden 6 · historic_traction 5 · match_funding_burden 4 → **66 (Medium)**

**Rationale:** KTP partners SME with academic for innovation embed — strong fit for AI/digital architecture R&D. Innovate UK +10 bonus and uk-wide +5. Status opening-soon but Round 1 deadline 2026-04-01 has passed; track Round 2 announcement. Match funding 33% from SME.

### #9 — Fair By Design Venture Fund — Score 66 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Fair By Design |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | FBD-VF-1 |
| Source URL | https://fairbydesign.com/ |
| Programme URL | https://fairbydesign.com/about-us/the-venture-fund/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | open |
| Eligible Org Types | startup, sme |
| Eligible Sectors | fintech, digital, cross-sector |
| Geography | uk-wide |

**Score breakdown:** eligibility_fit 26 · funding_size_fit 10 · timing_fit 15 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **66 (Medium)**

**Rationale:** Open status; SME/startup eligible; sectors fintech/digital/cross-sector overlap. Fair By Design's mission (poverty premium reduction) loosely aligns with SME equitable-access mission. Investment vehicle, not grant.

### #10 — PUBLIC GovStart Accelerator — Score 65 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | PUBLIC |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | PUBLIC-GOVSTART-1 |
| Source URL | https://www.computerweekly.com/news/252486640/Venture-firm-Public-launches-fourth-GovTech-accelerator |
| Programme URL | https://www.public.io/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | unknown |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Delivery Partners | public-sector |

**Score breakdown:** eligibility_fit 31 · funding_size_fit 10 · timing_fit 7 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **65 (Medium)**

**Rationale:** PUBLIC GovStart is the canonical UK GovTech accelerator. Sector-perfect, SME/startup eligible, public-sector delivery network is high-leverage for buyer-trust building. Status unknown for current cohort — verify cohort calendar.

### #11 — NCSC for Startups — Score 65 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Plexal & NCSC |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | PLEXAL-NCSC-1 |
| Source URL | https://www.plexal.com/our-work/ncsc-for-startups/ |
| Programme URL | https://www.ncsc.gov.uk/section/ncsc-for-startups/overview |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | unknown |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, ai |
| Geography | uk-wide |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 27 · funding_size_fit 10 · timing_fit 7 · complexity_burden 6 · historic_traction 5 · match_funding_burden 10 → **65 (Medium)**

**Rationale:** Plexal-delivered NCSC for Startups: deep alignment with Principle 5 (Security by Design) and CAF posture goals. SME/startup eligible, sectors digital/AI overlap, no match funding. Cohort timing requires verification.

### #12 — Resonance Enterprise Investment Fund — Score 65 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Resonance |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | RES-REI-1 |
| Source URL | https://resonance.ltd.uk/get-investment/enterprise-growth-funds/resonance-enterprise-investment-fund |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | charity, sme |
| Eligible Sectors | health, energy, cross-sector |
| Geography | multi-region |
| Application Complexity | medium |
| Award Range | £25,001 — £250,000 |

**Score breakdown:** eligibility_fit 20 · funding_size_fit 14 · timing_fit 15 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **65 (Medium)**

**Rationale:** Open, SME/charity eligible, partial-overlap on award range. Resonance is investment (not grant) — equity/loan instruments. Cross-sector match modest.

### #13 — Innovate UK Frontier AI Benchmarking Datasets — Score 64 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-FAIB-1 |
| Source URL | https://apply-for-innovation-funding.service.gov.uk/competition/2424/overview/e618b7a8-ab7f-45f3-a098-57c01b334fcd |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Deadline | 2026-05-27 |
| Eligible Org Types | sme, large-enterprise, academic, research-organisation, charity, public-sector, consortium |
| Eligible Sectors | ai, data, health, advanced-manufacturing |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £500,000 — £750,000 |
| Match Funding | required (pct unspecified) |
| Partnership Required | true |

**Score breakdown:** eligibility_fit 25 · funding_size_fit 14 · timing_fit 12 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **64 (Medium)**

**Rationale:** Large grant (£500k — £750k) overlaps high-end of project budget. Open with deadline 2026-05-27 (20 days — TIGHT) triggers -20 timing adjustment. Sector overlap weak (only AI matches). Partnership required (consortium with academic). Match funding required, pct unspecified.

### #14 — Cyber Runway — Score 63 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Plexal & DSIT |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | PLEXAL-CR-1 |
| Source URL | https://www.plexal.com/our-work/cyber-runway/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | closed |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 31 · funding_size_fit 10 · timing_fit 0 · complexity_burden 6 · historic_traction 5 · match_funding_burden 10 → **63 (Medium)**

**Rationale:** Cyber Runway: DSIT/Plexal-delivered cyber accelerator. Sector-perfect, SME/startup eligible, no match funding. Closed status pulls timing to 0 — track next cohort. Strong fit with Principle 5 / CAF goals.

### #15 — Tech Nation Upscale — Score 62 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Tech Nation |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | TN-UPSCALE-1 |
| Source URL | https://technation.io/programmes/upscale/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | low |
| Application Status | unknown |
| Eligible Org Types | sme |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |

**Score breakdown:** eligibility_fit 31 · funding_size_fit 10 · timing_fit 7 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **62 (Medium)**

**Rationale:** Tech Nation Upscale: scale-up programme for SMEs. Sector-perfect. Status unknown — Tech Nation re-organisation 2024 affects current operating model; verify before applying.

### #16 — Innovate UK Frontier AI Discovery — Score 61 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-FAID-1 |
| Source URL | https://apply-for-innovation-funding.service.gov.uk/competition/2422/overview/a5c16dd4-c60d-4cc1-8035-33fe76a52489 |
| Guidance URL | https://iuk-business-connect.org.uk/opportunities/frontier-ai-discovery/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Deadline | 2026-06-10 |
| Eligible Org Types | sme, large-enterprise, research-organisation, charity, public-sector |
| Eligible Sectors | ai, health, advanced-manufacturing, defence, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award Range | £25,000 — £50,000 |
| Match Funding | required, 30% |

**Score breakdown:** eligibility_fit 27 · funding_size_fit 4 · timing_fit 15 · complexity_burden 6 · historic_traction 5 · match_funding_burden 4 → **61 (Medium)**

**Rationale:** Open round, deadline 2026-06-10 (34 days). Award size (£25-50k) too small for project's £100-£600k window — discovery-tier funding only. Match funding 30% required. Useful for AI feasibility sprint (e.g., pluggable AI provider validation per ADR / G-8).

### #17 — National Climate Tech Accelerator (NCTA) — Score 61 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Sustainable Ventures |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | SUSVEN-NCTA-1 |
| Source URL | https://www.sustainableventures.co.uk/opportunities |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | sme, startup |
| Eligible Sectors | environment, energy, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |

**Score breakdown:** eligibility_fit 20 · funding_size_fit 10 · timing_fit 15 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **61 (Medium)**

**Rationale:** Open status, SME/startup eligible. Sectors weak — climate-tech focus only matches via 'cross-sector'. Suitable only if ArcKit positions sustainability angle (e.g., low-carbon SaaS + green-software practices).

### #18 — BGV Tech for Good Accelerator - Autumn 2026 — Score 61 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Bethnal Green Ventures |
| Funder Type | accelerator |
| Funder Category | social-impact |
| Citation | BGV-TFG-1 |
| Source URL | https://www.bethnalgreenventures.com/apply |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | opening-soon |
| Eligible Org Types | startup, sme |
| Eligible Sectors | digital, ai, health, environment, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £60,000 (flat) |
| Success Rate | 4% |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 26 · funding_size_fit 4 · timing_fit 12 · complexity_burden 6 · historic_traction 3 · match_funding_burden 10 → **61 (Medium)**

**Rationale:** Tech for Good accelerator — strong mission alignment with Principle 1 SME affordability, but £60k flat award is below project's £100 — £600k window. Success rate 4% reflects high competition. No match funding. Equity element common in BGV portfolio.

### #19 — SIB Community Builders Fund — Score 61 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Social Investment Business |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | SIB-CBF-1 |
| Source URL | https://www.sibgroup.org.uk/ |
| Programme URL | https://www.sibgroup.org.uk/fund/community-builders-fund/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | rolling |
| Eligible Org Types | charity |
| Geography | uk-wide |
| Award Range | £100,000 — £1,500,000 |

**Score breakdown:** eligibility_fit 12 · funding_size_fit 20 · timing_fit 13 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **61 (Medium)**

**Rationale:** Rolling, full-overlap funding range (£100k — £1.5M). Charity-only eligibility blocks direct application as commercial SME. Could be relevant if a charitable spinout / partner intermediary route is engineered.

### #20 — Water Efficiency Lab 1 — Score 60 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Nesta Challenge Works |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | CW-WEL-1 |
| Source URL | https://challengeworks.org/about-challenge-prizes/our-challenge-prizes/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Deadline | 2026-03-10 |
| Eligible Org Types | sme, large-enterprise, startup, consortium |
| Eligible Sectors | data, environment, digital |
| Geography | uk-wide |
| Application Complexity | high |
| Award (max) | £5,000,000 |

**Score breakdown:** eligibility_fit 22 · funding_size_fit 10 · timing_fit 15 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **60 (Medium)**

**Rationale:** Status open per reader, deadline 2026-03-10 has passed — refresh required. SME-eligible, sector partial overlap (digital). Challenge-prize structure.

### #21 — IUK Growth Catalyst Investor Partnerships R2 — Score 60 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-IP-R2 |
| Source URL | https://apply-for-innovation-funding.service.gov.uk/competition/2360/overview/37d8f6e1-5600-4e9e-bbfc-11bc320f8808 |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Deadline | 2026-02-03 |
| Eligible Org Types | sme |
| Eligible Sectors | digital, ai, advanced-manufacturing, energy, defence, creative, biotech, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £50,000 — £2,000,000 |
| Match Funding | required, 50% |

**Score breakdown:** eligibility_fit 28 · funding_size_fit 20 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 4 → **60 (Medium)**

**Rationale:** SME-only, full-overlap funding range £50k — £2M. Investor-partnership match funding 50% (heavy burden). Round 2 closed 2026-02-03 — track Round 3 announcement.

### #22 — Digital Catapult QTAP — Score 59 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Digital Catapult |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | DC-QTAP-1 |
| Source URL | https://www.digicatapult.org.uk/apply/opportunities/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Deadline | 2026-05-12 |
| Eligible Org Types | sme, startup |
| Eligible Sectors | quantum, digital |
| Geography | uk-wide |
| Application Complexity | medium |

**Score breakdown:** eligibility_fit 21 · funding_size_fit 10 · timing_fit 12 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **59 (Medium)**

**Rationale:** Open with deadline 2026-05-12 (5 days — VERY TIGHT) triggers -20 adjustment. Sectors quantum/digital — only digital matches project profile. Likely too late to apply this round; track next cohort.

### #23 — Innovate UK Secure Software for Resilient Growth — Score 59 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-SSRG-1 |
| Source URL | https://apply-for-innovation-funding.service.gov.uk/competition/2421/overview/3d6991fa-73b2-48c0-93eb-cc5393b5cf3d |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Deadline | 2026-04-29 |
| Eligible Org Types | sme, large-enterprise, academic, research-organisation, charity, public-sector, consortium |
| Eligible Sectors | digital, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £250,000 — £750,000 |
| Match Funding Required | true |
| Partnership Required | true |

**Score breakdown:** eligibility_fit 32 · funding_size_fit 14 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **59 (Medium)**

**Rationale:** SME/large/academic eligible, sector strong (digital/cross-sector), award range £250 — 750k partial-overlaps. Innovate UK +10 + uk-wide +5 boost eligibility to 92. Closed 2026-04-29 — track next round; this competition theme is recurrent.

### #24 — EIC Accelerator 2026 (Grant-only for UK applicants) — Score 59 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | European Innovation Council |
| Funder Type | eu-programme |
| Funder Category | government-rd |
| Citation | EIC-ACC-2026 |
| Source URL | https://iuk-business-connect.org.uk/opportunities/european-innovation-council-pathfinder-transition-accelerator-2026/ |
| Programme URL | https://eic.ec.europa.eu/eic-funding-opportunities/eic-accelerator_en |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | open |
| Deadline | 2026-10-28 |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, ai, energy, environment, biotech, cross-sector |
| Geography | international |
| Application Complexity | high |
| Award (max) | £2,100,000 |
| Match Funding Required | false |
| TRL Band | 6 — 8 |

**Score breakdown:** eligibility_fit 16 · funding_size_fit 10 · timing_fit 15 · complexity_burden 3 · historic_traction 5 · match_funding_burden 10 → **59 (Medium)**

**Rationale:** Open, deadline 2026-10-28 (174 days, +10 timing adj). Sectors digital/AI/cross-sector overlap. TRL 6-8 mismatch with project TRL 5 — zero score on TRL component. EU-programme bonus -5; international geography -10 — heavy adjustments. Strategic option if project advances to TRL 6+.

### #25 — Geovation Accelerator Programme - Autumn 2026 — Score 57 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Ordnance Survey & HM Land Registry |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | GEOVATION-AUT-2026 |
| Source URL | https://geovation.uk/apply/accelerator/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | opening-soon |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, data, housing, transport |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £20,000 (flat) |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 20 · funding_size_fit 4 · timing_fit 12 · complexity_burden 6 · historic_traction 5 · match_funding_burden 10 → **57 (Medium)**

**Rationale:** Geospatial-data accelerator — partial sector match (digital). £20k flat too small for project budget. Only relevant if geospatial-features extension is on the roadmap.

### #26 — Reaching Communities England — Score 55 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | National Lottery Community Fund |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | TNL-RCE-1 |
| Source URL | https://www.tnlcommunityfund.org.uk/funding |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | charity, public-sector |
| Eligible Sectors | cross-sector, social-care |
| Geography | england |
| Application Complexity | high |
| Award Range | £20,001 — £20,000,000 |

**Score breakdown:** eligibility_fit 7 · funding_size_fit 20 · timing_fit 15 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **55 (Medium)**

**Rationale:** Open, full-overlap funding range £20k — £20M. Charity/public-sector only eligibility blocks direct SME application. High complexity. Strong fit on quantum but org-type fail dominates.

### #27 — VocTech Challenge — Score 55 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Ufi VocTech Trust |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | UFI-CHA-1 |
| Source URL | https://ufi.co.uk/grant-funding/voctech-challenge/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Eligible Org Types | charity, sme, consortium |
| Eligible Sectors | education, digital |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £200,000 — £250,000 |
| Match Funding Required | false |
| Partnership Required | true |

**Score breakdown:** eligibility_fit 23 · funding_size_fit 14 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 10 → **55 (Medium)**

**Rationale:** Charity/SME/consortium eligible, partial-overlap funding (£200 — 250k). Education/digital sector — partial match. No match funding required. Closed status pulls timing to 0 — track next round.

### #28 — AWS Defence Accelerator — Score 55 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | PUBLIC & AWS |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | PUBLIC-AWS-DEF-1 |
| Source URL | https://www.public.io/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | low |
| Application Status | unknown |
| Eligible Org Types | sme, startup |
| Eligible Sectors | defence, digital |
| Geography | uk-wide |
| Application Complexity | medium |
| Delivery Partners | public-sector, large-enterprise |

**Score breakdown:** eligibility_fit 21 · funding_size_fit 10 · timing_fit 7 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **55 (Medium)**

**Rationale:** PUBLIC + AWS defence-themed. Sector defence/digital — only digital matches project profile. Project 001 (SaaS) is not defence-scoped (defence is sovereign Project 002). Useful intel for sovereign-route consideration.

### #29 — Tech Nation Future Fifty 2026 — Score 55 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Tech Nation |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | TN-FF-2026 |
| Source URL | https://technation.io/programmes/future-fifty/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | closed |
| Eligible Org Types | sme |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |

**Score breakdown:** eligibility_fit 31 · funding_size_fit 10 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **55 (Medium)**

**Rationale:** Tech Nation Future Fifty: scale-up cohort. Sector-perfect, SME eligible. Closed status pulls timing to 0 and Tech Nation post-2024 reorganisation creates uncertainty. Verify operating model.

### #30 — Digital Catapult Future Networks Lab — Score 52 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Digital Catapult |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | DC-FNL-1 |
| Source URL | https://www.digicatapult.org.uk/apply/labs/future-networks-lab/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | unknown |
| Eligible Org Types | sme |
| Eligible Sectors | digital, ai, advanced-manufacturing |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £17,000 (flat) |

**Score breakdown:** eligibility_fit 25 · funding_size_fit 4 · timing_fit 7 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **52 (Medium)**

**Rationale:** Digital Catapult lab. SME-eligible, sectors digital/AI partial match, £17k too small. Useful for technology validation experiments rather than core build funding.

### #31 — IUK AI Champions: Frontier AI Phase 1 — Score 51 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Innovate UK |
| Funder Type | innovate-uk |
| Funder Category | government-rd |
| Citation | IUK-AICH-1 |
| Source URL | https://iuk-business-connect.org.uk/opportunities/ai-champions-frontier-ai-phase-1/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Deadline | 2026-04-29 |
| Eligible Org Types | sme |
| Eligible Sectors | ai, health, advanced-manufacturing, defence |
| Geography | uk-wide |
| Application Complexity | high |
| Award Range | £150,000 — £250,000 |
| Match Funding | required, 30% |
| TRL Max | 3 |

**Score breakdown:** eligibility_fit 25 · funding_size_fit 14 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 4 → **51 (Medium)**

**Rationale:** SME-only, partial-overlap funding £150 — 250k. AI/health/defence sector — only AI matches. trl_max=3 mismatch with project TRL 5 (zero on TRL component). Match funding 30%. Closed 2026-04-29 — track Phase 2.

### #32 — Carbon13 Venture Launchpad (Cohort 5) — Score 50 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Carbon13 |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | C13-VLP-5 |
| Source URL | https://carbonthirteen.smapply.io/prog/venture_launchpad_cohort_5/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | rolling |
| Eligible Org Types | startup |
| Eligible Sectors | environment, energy, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £200,000 (flat) |
| Partnership Required | true |

**Score breakdown:** eligibility_fit 6 · funding_size_fit 14 · timing_fit 13 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **50 (Medium)**

**Rationale:** Climate-tech only — startup-only eligibility (excludes SME), sector mismatch. Listed for completeness; not actionable for ArcKit's profile.

### #33 — CPC Rail Stations Innovation Accelerator — Score 49 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Connected Places Catapult |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | CPC-RAIL-1 |
| Source URL | https://cp.catapult.org.uk/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | low |
| Application Status | unknown |
| Eligible Org Types | sme, startup |
| Eligible Sectors | transport, digital |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £49,000 (flat) |

**Score breakdown:** eligibility_fit 21 · funding_size_fit 4 · timing_fit 7 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **49 (Medium)**

**Rationale:** Rail-stations themed. Sector mismatch dominates. Only relevant if rail-sector vertical added to roadmap.

### #34 — SIB Flexible Finance — Score 49 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Social Investment Business |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | SIB-FF-1 |
| Source URL | https://www.sibgroup.org.uk/ |
| Programme URL | https://www.sibgroup.org.uk/fund/flexible-finance/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | rolling |
| Eligible Org Types | charity |

**Score breakdown:** eligibility_fit 11 · funding_size_fit 10 · timing_fit 13 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **49 (Medium)**

**Rationale:** Charity-only eligibility blocks SME application. Listed for completeness; route only via charitable spinout/partner.

### #35 — Fairer Life Chances Scotland — Score 49 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | National Lottery Community Fund |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | TNL-FLC-1 |
| Source URL | https://www.tnlcommunityfund.org.uk/funding |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | charity |
| Eligible Sectors | social-care, cross-sector |
| Geography | scotland |
| Application Complexity | high |
| Award Range | £20,001 — £500,000 |

**Score breakdown:** eligibility_fit 7 · funding_size_fit 14 · timing_fit 15 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **49 (Medium)**

**Rationale:** Charity-only, Scotland-only geography. Open with partial-overlap funding. Only via charitable partner.

### #36 — VocTech Activate — Score 48 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Ufi VocTech Trust |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | UFI-ACT-1 |
| Source URL | https://ufi.co.uk/grant-funding/voctech-activate/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Eligible Org Types | charity, sme, sole-trader |
| Eligible Sectors | education, digital |
| Geography | uk-wide |
| Application Complexity | medium |
| Award Range | £30,000 — £60,000 |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 23 · funding_size_fit 4 · timing_fit 0 · complexity_burden 6 · historic_traction 5 · match_funding_burden 10 → **48 (Medium)**

**Rationale:** SME-eligible, education/digital sectors. Award £30 — 60k below project budget window. Closed — track next round.

### #37 — Better Society Capital Fund-of-Funds — Score 47 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Better Society Capital |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | BSC-FOF-1 |
| Source URL | https://bettersocietycapital.com/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | unknown |
| Eligible Sectors | housing, health, energy, cross-sector |
| Geography | uk-wide |

**Score breakdown:** eligibility_fit 15 · funding_size_fit 10 · timing_fit 7 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **47 (Medium)**

**Rationale:** BSC operates as fund-of-funds — does not fund SMEs directly but routes via portfolio funds. Use as discovery for portfolio of UK social-investment funds rather than direct apply.

### #38 — National Lottery Awards for All England — Score 47 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | National Lottery Community Fund |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | TNL-AFA-1 |
| Source URL | https://www.tnlcommunityfund.org.uk/funding |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | charity, public-sector |
| Eligible Sectors | cross-sector |
| Geography | england |
| Application Complexity | low |
| Award Range | £300 — £20,000 |

**Score breakdown:** eligibility_fit 8 · funding_size_fit 4 · timing_fit 15 · complexity_burden 10 · historic_traction 5 · match_funding_burden 5 → **47 (Medium)**

**Rationale:** Charity/public-sector only. Award £300 — £20k below project budget. Low-complexity simple form. Listed for completeness.

### #39 — SIB Energy Resilience Fund — Score 46 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Social Investment Business |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | SIB-ERF-1 |
| Source URL | https://www.sibgroup.org.uk/ |
| Programme URL | https://www.sibgroup.org.uk/fund/energy-resilience-fund/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | rolling |
| Eligible Org Types | charity |
| Eligible Sectors | energy |
| Award Range | £25,000 — £250,000 |

**Score breakdown:** eligibility_fit 4 · funding_size_fit 14 · timing_fit 13 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **46 (Medium)**

**Rationale:** Charity-only, energy-only sector. Sector and org-type mismatches. Listed for completeness.

### #40 — Esmee Fairbairn Main Grants and Funding Plus — Score 46 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Esmee Fairbairn Foundation |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | EFF-MAIN-1 |
| Source URL | https://esmeefairbairn.org.uk/our-support/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | charity |
| Eligible Sectors | environment, social-care, creative, cross-sector |
| Geography | uk-wide |
| Application Complexity | high |

**Score breakdown:** eligibility_fit 8 · funding_size_fit 10 · timing_fit 15 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **46 (Medium)**

**Rationale:** Charity-only — blocks SME direct application. Open status. Loose cross-sector match.

### #41 — WCIT IT4Good Grant Programme — Score 46 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | WCIT Charity (Worshipful Company of Information Technologists) |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | WCIT-IT4G-1 |
| Source URL | https://forumcio.org.uk/funding/wcit-it4good-grant-programme/ |
| Programme URL | https://wcitcharity.org.uk/apply-for-a-grant/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | open |
| Deadline | 2026-05-20 |
| Eligible Org Types | charity, academic |
| Eligible Sectors | digital, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £15,000 (flat) |
| Historical Grants Count | 0 |

**Score breakdown:** eligibility_fit 15 · funding_size_fit 4 · timing_fit 12 · complexity_burden 6 · historic_traction 4 · match_funding_burden 5 → **46 (Medium)**

**Rationale:** WCIT IT4Good open with deadline 2026-05-20 (13 days, -20 timing adj). Charity/academic only — blocks SME. £15k below budget window. Niche but mission-adjacent (IT for charitable causes).

### #42 — VocTech Ignite — Score 46 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Ufi VocTech Trust |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | UFI-IGN-1 |
| Source URL | https://ufi.co.uk/grant-funding/voctech-ignite/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | closed |
| Eligible Sectors | education, digital |
| Geography | uk-wide |
| Application Complexity | low |

**Score breakdown:** eligibility_fit 16 · funding_size_fit 10 · timing_fit 0 · complexity_burden 10 · historic_traction 5 · match_funding_burden 5 → **46 (Medium)**

**Rationale:** Eligibility data missing — when_missing 50 substituted. Education/digital sectors. Closed — track next round. Listed for completeness.

### #43 — Geovation Accelerator Programme - Spring 2026 — Score 45 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Ordnance Survey & HM Land Registry |
| Funder Type | accelerator |
| Funder Category | accelerator |
| Citation | GEOVATION-SPR-2026 |
| Source URL | https://geovation.uk/insights/what-could-you-build-with-os-hmlr-data-applications-open/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Deadline | 2026-02-28 |
| Eligible Org Types | sme, startup |
| Eligible Sectors | digital, data, housing, transport |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £20,000 (flat) |
| Match Funding Required | false |

**Score breakdown:** eligibility_fit 20 · funding_size_fit 4 · timing_fit 0 · complexity_burden 6 · historic_traction 5 · match_funding_burden 10 → **45 (Medium)**

**Rationale:** Closed Spring 2026 round. £20k flat below project budget. Geospatial focus weakly matches digital. See Autumn 2026 sibling for next opportunity.

### #44 — Indigo Trust Grants — Score 45 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Indigo Trust |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | INDIGO-1 |
| Source URL | https://indigotrust.org.uk/what-we-fund/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Eligible Org Types | charity |
| Eligible Sectors | digital, cross-sector |
| Geography | international |
| Application Complexity | high |
| Award Range | £222 — £1,000,000 |
| Historical Grants Count | 634 |

**Score breakdown:** eligibility_fit 9 · funding_size_fit 20 · timing_fit 0 · complexity_burden 3 · historic_traction 7 · match_funding_burden 5 → **45 (Medium)**

**Rationale:** Charity-only and 'closed to new applications' since 2023 per Indigo Trust statement. Listed historic-traction high (634 grants) but actively no longer funding. Reference only.

### #45 — Esmee Fairbairn Main Fund — Score 45 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Esmee Fairbairn Foundation |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | EFF-1 |
| Source URL | https://esmeefairbairn.org.uk/our-support/grants/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | rolling |
| Eligible Org Types | charity |
| Eligible Sectors | cross-sector, environment, creative |
| Geography | uk-wide |
| Application Complexity | high |
| Award Floor | £30,000 |

**Score breakdown:** eligibility_fit 8 · funding_size_fit 10 · timing_fit 13 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **45 (Medium)**

**Rationale:** Same funder as EFF-MAIN-1 (rank 40); slightly different programme_name in evidence — possibly the same programme. Charity-only — blocks SME. Rolling intake.

### #46 — SIB Reach Fund — Score 43 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Social Investment Business |
| Funder Type | social-impact-investor |
| Funder Category | social-impact |
| Citation | SIB-REACH-1 |
| Source URL | https://www.sibgroup.org.uk/ |
| Programme URL | https://www.sibgroup.org.uk/fund/reach-fund/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | rolling |
| Eligible Org Types | charity |
| Geography | england |
| Award Range | £5,000 — £15,000 |

**Score breakdown:** eligibility_fit 11 · funding_size_fit 4 · timing_fit 13 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **43 (Medium)**

**Rationale:** Charity-only, England-only, £5 — 15k below budget window. Listed for completeness.

### #47 — Paul Hamlyn Foundation Open Funds — Score 43 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Paul Hamlyn Foundation |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | PHF-1 |
| Source URL | https://www.phf.org.uk/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | low |
| Application Status | unknown |
| Eligible Org Types | charity |
| Eligible Sectors | cross-sector, digital, creative |
| Geography | uk-wide |
| Application Complexity | high |

**Score breakdown:** eligibility_fit 12 · funding_size_fit 10 · timing_fit 7 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **43 (Medium)**

**Rationale:** Charity-only. Cross-sector/digital/creative match modest. Status unknown — Paul Hamlyn Foundation operates rolling Open Funds for charity beneficiaries.

### #48 — National Lottery Awards for All England - Environment — Score 43 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | National Lottery Community Fund |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | TNL-AFE-1 |
| Source URL | https://www.tnlcommunityfund.org.uk/funding |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | open |
| Eligible Org Types | charity |
| Eligible Sectors | environment |
| Geography | england |
| Application Complexity | low |
| Award Range | £300 — £20,000 |

**Score breakdown:** eligibility_fit 4 · funding_size_fit 4 · timing_fit 15 · complexity_burden 10 · historic_traction 5 · match_funding_burden 5 → **43 (Medium)**

**Rationale:** Charity-only, environment-only sector — sector mismatch dominates. Open. Listed for completeness.

### #49 — Longitude Prize on ALS — Score 40 (Medium)

| Attribute | Value |
|-----------|-------|
| Funder | Nesta Challenge Works |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | CW-LP-1 |
| Source URL | https://challengeworks.org/about-challenge-prizes/our-challenge-prizes/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Deadline | 2025-06-25 |
| Eligible Org Types | sme, academic, research-organisation, consortium |
| Eligible Sectors | health, ai, data |
| Geography | international |
| Application Complexity | high |
| Award (max) | £7,500,000 |

**Score breakdown:** eligibility_fit 17 · funding_size_fit 10 · timing_fit 0 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **40 (Medium)**

**Rationale:** Health/AI/data sectors — only AI matches. International geography (-10). Closed. Listed for completeness.

### #50 — Nesta Collective Intelligence Grants — Score 39 (Low)

| Attribute | Value |
|-----------|-------|
| Funder | Nesta |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | NESTA-CI-1 |
| Source URL | https://www.nesta.org.uk/project/collective-intelligence-grants/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | closed |
| Eligible Org Types | academic, charity, public-sector |
| Eligible Sectors | digital, ai, cross-sector |
| Geography | uk-wide |
| Application Complexity | medium |
| Award | £30,000 (flat) |

**Score breakdown:** eligibility_fit 19 · funding_size_fit 4 · timing_fit 0 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **39 (Low)**

**Rationale:** Academic/charity/public-sector only — blocks SME. Sector match strong. £30k below budget window. Closed.

### #51 — LBF Specialist and Equity Programmes — Score 38 (Low)

| Attribute | Value |
|-----------|-------|
| Funder | Lloyds Bank Foundation for England and Wales |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | LBF-SPEC-1 |
| Source URL | https://www.lloydsbankfoundation.org.uk/funding |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | high |
| Application Status | opening-soon |
| Eligible Org Types | charity |
| Eligible Sectors | social-care, housing, cross-sector |
| Geography | england |
| Application Complexity | medium |
| Award | £75,000 (flat) |

**Score breakdown:** eligibility_fit 6 · funding_size_fit 4 · timing_fit 12 · complexity_burden 6 · historic_traction 5 · match_funding_burden 5 → **38 (Low)**

**Rationale:** Charity-only (England), sectors social-care/housing — sector and org mismatches. Listed for completeness.

### #52 — Nesta Mission Studio — Score 36 (Low)

| Attribute | Value |
|-----------|-------|
| Funder | Nesta |
| Funder Type | charitable-foundation |
| Funder Category | charitable |
| Citation | NESTA-MS-1 |
| Source URL | https://www.nesta.org.uk/project/mission-studio/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | unknown |
| Eligible Org Types | startup |
| Eligible Sectors | health, education, environment |
| Geography | uk-wide |
| Application Complexity | high |

**Score breakdown:** eligibility_fit 5 · funding_size_fit 10 · timing_fit 7 · complexity_burden 3 · historic_traction 5 · match_funding_burden 5 → **36 (Low)**

**Rationale:** Startup-only (no SME), sectors health/education/environment — sector and org mismatch dominate.

### #53 — Lankelly Chase Endowment Redistribution — Score 35 (Low)

| Attribute | Value |
|-----------|-------|
| Funder | Lankelly Chase Foundation |
| Funder Type | charitable-foundation |
| Funder Category | open-data |
| Citation | LANKELLY-1 |
| Source URL | https://lankellychase.org.uk/ |
| Fetched At | 2026-05-07T12:00:00Z |
| Confidence | medium |
| Application Status | closed |
| Eligible Org Types | charity |
| Eligible Sectors | cross-sector |
| Geography | uk-wide |

**Score breakdown:** eligibility_fit 10 · funding_size_fit 10 · timing_fit 0 · complexity_burden 5 · historic_traction 5 · match_funding_burden 5 → **35 (Low)**

**Rationale:** Charity-only. Endowment-spend-down strategy means no new applications. Reference only.

## Gap Analysis

The following project requirements / profile aspects do not map cleanly onto any open programme in this assessment:

| # | Requirement | Reason |
|---|-------------|--------|
| 1 | BR-005 | Cross-Subsidy Funding Model — no UK grant programme directly funds operating cross-subsidies. Grants fund R&D capital; cross-subsidy ops must come from large-enterprise tier (per BR-005 design). |
| 2 | BR-001 | Free Tier for Verified UK SMEs — no grant programme directly funds running the free tier. Mission alignment is strong with charitable funders (Nesta, JRRT, Esmee Fairbairn) but those funders typically restrict to charities. Charitable spinout / partner intermediary route could unlock these (governance review needed). |
| 3 | NFR-SEC-002 | Tenant isolation testing in CI — Innovate UK Cyber Scale (IUK-CYBR-1, rank 4) is opening-soon and on-mission, but its TRL band 7-8 mismatches project's current TRL 5. Plan TRL ramp to TRL 7 before that round, or apply to TRL-flexible rounds first (Frontier AI Discovery, KTP). |
| 4 | FR-004 | AI-assisted artefact generation R&D — IUK-FAID-1 (rank 16, open, 34 days) and IUK-FAIB-1 (rank 13, open, 20 days) directly addressable, but Frontier AI Discovery max £50k and Frontier AI Benchmarking requires partnership consortium. |
| 5 | BR-003 | SME eligibility verification (Companies House integration) — no grant programme specifically funds this; absorb into capital build. |
| 6 | BR-006 | UK public-sector compliance evidence pack — no grant programme funds compliance ops; absorb into capital build, recover via paid-tier pricing. |
| 7 | BR-008 | Adoption ≥200 SMEs in 12 months — no grant directly funds market-development. Accelerators (Wayra, BGV, GovStart, NCSC for Startups, Tech Nation Upscale) provide market-access mentoring instead of grant capital. |
| 8 | PROFILE-TRL | Project TRL 5 sits in the awkward gap between early-stage Innovate UK competitions (TRL 1-4) and growth/scale competitions (TRL 7-8). Several otherwise-strong programmes (IUK-AICH-1 trl_max=3, IUK-CYBR-1 trl_min=7, EIC-ACC-2026 trl_min=6) miss because of TRL band. Ramp to TRL 7 before applying to scale-stage rounds. |
| 9 | PROFILE-MATCH | 6 of the 10 government-rd programmes require match funding (30-50%). For an SME pre-revenue, match-funding burden is high. Innovation Loans (IUK-LOAN-25) avoids match but is debt-finance not grant. |
| 10 | PROJECT-001-SCOPE | Defence-security funder bucket (DASA, DSTL) intentionally excluded from project 001 scope — sovereign deployment is project 002. DASA Themed Competitions could become relevant for project 002; not assessed here. |

## Traceability Matrix

| Requirement / Need | Matched Programmes (citation, score, band) |
|--------------------|--------------------------------------------|
| AI-assisted generation R&D (FR-004, ADR pluggable AI / G-8) | IUK-FAID-1 (61, Medium); IUK-FAIB-1 (64, Medium); EIC-ACC-2026 (59, Medium, TRL gap) |
| Cyber-secure platform development (Principle 5, NFR-SEC-002) | IUK-CYBR-1 (70, High, TRL gap); PLEXAL-CR-1 (63, Medium); PLEXAL-NCSC-1 (65, Medium); IUK-SSRG-1 (59, Medium) |
| Open standards / portable platform (Principle 4, BR-007) | NESTA-1 (76, High, historical aggregate caveat); JRRT-1 (67, Medium) |
| SME affordability cross-subsidy (Principle 1, BR-001/005) | [GAP — no direct grant; route via charitable spinout or accelerator non-dilutive support: BGV-TFG-1, FBD-VF-1] |
| Pluggable AI provider (G-8, ADR) | IUK-FAID-1 (61, Medium); IUK-FAIB-1 (64, Medium) |
| Academic R&D embedment (KTP-style) | IUK-KTP-2627-1 (66, Medium, deadline past); UKRI-FLF-11 (70, High, opening-soon) |
| Acceleration / scale-up (BR-008 adoption) | WAYRA-UK-1 (73, High); BGV-TFG-1 (61, Medium); RES-REI-1 (65, Medium); FBD-VF-1 (66, Medium); TN-UPSCALE-1 (62, Medium) |
| GovTech market-fit validation (DDaT-recognisable artefacts G-1) | PUBLIC-GOVSTART-1 (65, Medium); PLEXAL-CR-1 (63, Medium); PLEXAL-NCSC-1 (65, Medium) |
| Innovation loans / non-dilutive growth capital | IUK-LOAN-25 (69, Medium, track Round 26); IUK-IP-R2 (60, Medium, track Round 3) |

## Application Calendar

Sorted by `date_iso` ascending. Rolling and track entries grouped at the end.

| Date | Action | Programme | Status |
|------|--------|-----------|--------|
| 2026-05-12 | Apply (5 days from today — likely too tight) | Digital Catapult QTAP (DC-QTAP-1) | open |
| 2026-05-20 | Apply (charity/academic only — not direct route) | WCIT IT4Good (WCIT-IT4G-1) | open |
| 2026-05-27 | Apply (consortium required — partner urgently) | Innovate UK Frontier AI Benchmarking Datasets (IUK-FAIB-1) | open |
| 2026-06-10 | Apply (sole-applicant route OK) | Innovate UK Frontier AI Discovery (IUK-FAID-1) | open |
| 2026-06-10 | Apply when round opens (TRL 7-8 — plan TRL ramp first) | Innovate UK Cyber Scale in Critical Sectors (IUK-CYBR-1) | opening-soon |
| 2026-06-16 | Apply (academic partnership required) | UKRI Future Leaders Fellowships Round 11 (UKRI-FLF-11) | opening-soon |
| 2026-10-28 | Apply once project hits TRL 6+ | EIC Accelerator 2026 (EIC-ACC-2026) | open |
| rolling | Pitch any time | Wayra UK Open Innovation (WAYRA-UK-1) | rolling |
| rolling | Apply any time | Resonance Enterprise Investment Fund (RES-REI-1) | open |
| rolling | Apply any time | Fair By Design Venture Fund (FBD-VF-1) | open |
| rolling | Apply any time (cross-sector mission angle) | Joseph Rowntree Reform Trust (JRRT-1) | rolling |
| rolling | Watch for next cohort announcement | BGV Tech for Good Autumn 2026 (BGV-TFG-1) | opening-soon |
| rolling | Watch for next cohort announcement | Geovation Autumn 2026 (GEOVATION-AUT-2026) | opening-soon |
| rolling | Track LBF Specialist & Equity strategy launch | Lloyds Bank Foundation Specialist & Equity (LBF-SPEC-1) | opening-soon |
| track | Track Round 26 announcement | Innovate UK Innovation Loans (IUK-LOAN-25) | closed |
| track | Track next cohort announcement | Innovate UK Secure Software for Resilient Growth (IUK-SSRG-1) | closed |
| track | Track Round 3 announcement | Innovate UK Growth Catalyst Investor Partnerships (IUK-IP-R2) | closed |
| track | Track KTP Round 2 2026-2027 | Innovate UK KTP Round 1 (IUK-KTP-2627-1) | closed |
| track | Track Phase 2 announcement | Innovate UK AI Champions Phase 1 (IUK-AICH-1) | closed |

## Citations

| Citation ID | Source URL |
|-------------|------------|
| NESTA-1 | https://grantnav.threesixtygiving.org/org/GB-CHC-1144091 |
| WAYRA-UK-1 | https://wayra.co.uk/ |
| UKRI-FLF-11 | https://www.ukri.org/opportunity/future-leaders-fellowship-round-11/ |
| IUK-CYBR-1 | https://apply-for-innovation-funding.service.gov.uk/competition/2452/overview/df0addbf-9146-4b7f-b8b5-e78470917675 |
| IUK-LOAN-25 | https://apply-for-innovation-funding.service.gov.uk/competition/2373/overview/609dc5dd-d3e8-4f51-af3a-3eb1b3314710 |
| JRRT-1 | https://www.jrrt.org.uk/apply-for-a-grant/what-we-fund/ |
| CW-MNI-1 | https://challengeworks.org/about-challenge-prizes/our-challenge-prizes/ |
| IUK-KTP-2627-1 | https://iuk-business-connect.org.uk/opportunities/knowledge-transfer-partnership-ktp-2026-2027-round-1/ |
| FBD-VF-1 | https://fairbydesign.com/ |
| PUBLIC-GOVSTART-1 | https://www.computerweekly.com/news/252486640/Venture-firm-Public-launches-fourth-GovTech-accelerator |
| PLEXAL-NCSC-1 | https://www.plexal.com/our-work/ncsc-for-startups/ |
| RES-REI-1 | https://resonance.ltd.uk/get-investment/enterprise-growth-funds/resonance-enterprise-investment-fund |
| IUK-FAIB-1 | https://apply-for-innovation-funding.service.gov.uk/competition/2424/overview/e618b7a8-ab7f-45f3-a098-57c01b334fcd |
| PLEXAL-CR-1 | https://www.plexal.com/our-work/cyber-runway/ |
| TN-UPSCALE-1 | https://technation.io/programmes/upscale/ |
| IUK-FAID-1 | https://apply-for-innovation-funding.service.gov.uk/competition/2422/overview/a5c16dd4-c60d-4cc1-8035-33fe76a52489 |
| SUSVEN-NCTA-1 | https://www.sustainableventures.co.uk/opportunities |
| BGV-TFG-1 | https://www.bethnalgreenventures.com/apply |
| SIB-CBF-1 | https://www.sibgroup.org.uk/ |
| CW-WEL-1 | https://challengeworks.org/about-challenge-prizes/our-challenge-prizes/ |
| IUK-IP-R2 | https://apply-for-innovation-funding.service.gov.uk/competition/2360/overview/37d8f6e1-5600-4e9e-bbfc-11bc320f8808 |
| DC-QTAP-1 | https://www.digicatapult.org.uk/apply/opportunities/ |
| IUK-SSRG-1 | https://apply-for-innovation-funding.service.gov.uk/competition/2421/overview/3d6991fa-73b2-48c0-93eb-cc5393b5cf3d |
| EIC-ACC-2026 | https://iuk-business-connect.org.uk/opportunities/european-innovation-council-pathfinder-transition-accelerator-2026/ |
| GEOVATION-AUT-2026 | https://geovation.uk/apply/accelerator/ |
| TNL-RCE-1 | https://www.tnlcommunityfund.org.uk/funding |
| UFI-CHA-1 | https://ufi.co.uk/grant-funding/voctech-challenge/ |
| PUBLIC-AWS-DEF-1 | https://www.public.io/ |
| TN-FF-2026 | https://technation.io/programmes/future-fifty/ |
| DC-FNL-1 | https://www.digicatapult.org.uk/apply/labs/future-networks-lab/ |
| IUK-AICH-1 | https://iuk-business-connect.org.uk/opportunities/ai-champions-frontier-ai-phase-1/ |
| C13-VLP-5 | https://carbonthirteen.smapply.io/prog/venture_launchpad_cohort_5/ |
| CPC-RAIL-1 | https://cp.catapult.org.uk/ |
| SIB-FF-1 | https://www.sibgroup.org.uk/ |
| TNL-FLC-1 | https://www.tnlcommunityfund.org.uk/funding |
| UFI-ACT-1 | https://ufi.co.uk/grant-funding/voctech-activate/ |
| BSC-FOF-1 | https://bettersocietycapital.com/ |
| TNL-AFA-1 | https://www.tnlcommunityfund.org.uk/funding |
| SIB-ERF-1 | https://www.sibgroup.org.uk/ |
| EFF-MAIN-1 | https://esmeefairbairn.org.uk/our-support/ |
| WCIT-IT4G-1 | https://forumcio.org.uk/funding/wcit-it4good-grant-programme/ |
| UFI-IGN-1 | https://ufi.co.uk/grant-funding/voctech-ignite/ |
| GEOVATION-SPR-2026 | https://geovation.uk/insights/what-could-you-build-with-os-hmlr-data-applications-open/ |
| INDIGO-1 | https://indigotrust.org.uk/what-we-fund/ |
| EFF-1 | https://esmeefairbairn.org.uk/our-support/grants/ |
| SIB-REACH-1 | https://www.sibgroup.org.uk/ |
| PHF-1 | https://www.phf.org.uk/ |
| TNL-AFE-1 | https://www.tnlcommunityfund.org.uk/funding |
| CW-LP-1 | https://challengeworks.org/about-challenge-prizes/our-challenge-prizes/ |
| NESTA-CI-1 | https://www.nesta.org.uk/project/collective-intelligence-grants/ |
| LBF-SPEC-1 | https://www.lloydsbankfoundation.org.uk/funding |
| NESTA-MS-1 | https://www.nesta.org.uk/project/mission-studio/ |
| LANKELLY-1 | https://lankellychase.org.uk/ |

## Next Steps

- Run `/arckit:sobc` to refresh the Strategic Outline Business Case on a funded scenario incorporating the Top-3 actionable programmes.
- Run `/arckit:plan` to time grant calendar against build phases (Alpha / Beta / GA target 2027-04-30).
- Run `/arckit:risk` to add R-001 cross-subsidy mitigation entries based on grant-stack outcome (e.g., debt-finance fallback via IUK-LOAN-25 Round 26).
- Run `/arckit:adr` to record explicit decisions where a grant is pursued vs declined (esp. consortium-required programmes IUK-FAIB-1, UKRI-FLF-11).

## Spawned Knowledge

The following standalone tech-note files were created from this discovery run (one per scored programme):

### Tech Notes

- `tech-notes/nesta-grants-historical-portfolio.md` — Created
- `tech-notes/wayra-uk-telefonica-open-innovation-programme.md` — Created
- `tech-notes/uk-research-and-innovation-future-leaders-fellowships-round-11.md` — Created
- `tech-notes/innovate-uk-contracts-for-innovation-cyber-scale-in-critical-sectors.md` — Created
- `tech-notes/innovate-uk-innovation-loans-round-25.md` — Created
- `tech-notes/joseph-rowntree-reform-trust-democracy-priorities-funding.md` — Created
- `tech-notes/nesta-challenge-works-metascience-novelty-indicators-challenge.md` — Created
- `tech-notes/innovate-uk-knowledge-transfer-partnership-2026-2027-round-1.md` — Created
- `tech-notes/fair-by-design-venture-fund.md` — Created
- `tech-notes/public-govstart-accelerator.md` — Created
- `tech-notes/plexal-ncsc-for-startups.md` — Created
- `tech-notes/resonance-enterprise-investment-fund.md` — Created
- `tech-notes/innovate-uk-frontier-ai-benchmarking-datasets.md` — Created
- `tech-notes/plexal-dsit-cyber-runway.md` — Created
- `tech-notes/tech-nation-upscale.md` — Created
- `tech-notes/innovate-uk-frontier-ai-discovery.md` — Created
- `tech-notes/sustainable-ventures-national-climate-tech-accelerator.md` — Created
- `tech-notes/bethnal-green-ventures-tech-for-good-accelerator-autumn-2026.md` — Created
- `tech-notes/social-investment-business-community-builders-fund.md` — Created
- `tech-notes/nesta-challenge-works-water-efficiency-lab-1.md` — Created
- `tech-notes/innovate-uk-growth-catalyst-investor-partnerships-round-2.md` — Created
- `tech-notes/digital-catapult-qtap-nqcc-sparq.md` — Created
- `tech-notes/innovate-uk-secure-software-for-resilient-growth.md` — Created
- `tech-notes/european-innovation-council-eic-accelerator-2026.md` — Created
- `tech-notes/ordnance-survey-geovation-accelerator-autumn-2026.md` — Created
- `tech-notes/national-lottery-community-fund-reaching-communities-england.md` — Created
- `tech-notes/ufi-voctech-trust-voctech-challenge.md` — Created
- `tech-notes/public-aws-defence-accelerator.md` — Created
- `tech-notes/tech-nation-future-fifty-2026.md` — Created
- `tech-notes/digital-catapult-future-networks-lab-accelerator.md` — Created
- `tech-notes/innovate-uk-ai-champions-frontier-ai-phase-1.md` — Created
- `tech-notes/carbon13-venture-launchpad-cohort-5.md` — Created
- `tech-notes/connected-places-catapult-rail-stations-innovation-accelerator.md` — Created
- `tech-notes/social-investment-business-flexible-finance.md` — Created
- `tech-notes/national-lottery-community-fund-fairer-life-chances-scotland.md` — Created
- `tech-notes/ufi-voctech-trust-voctech-activate.md` — Created
- `tech-notes/better-society-capital-fund-of-funds.md` — Created
- `tech-notes/national-lottery-community-fund-awards-for-all-england.md` — Created
- `tech-notes/social-investment-business-energy-resilience-fund.md` — Created
- `tech-notes/esmee-fairbairn-foundation-main-grants-and-funding-plus.md` — Created
- `tech-notes/wcit-charity-it4good-grant-programme.md` — Created
- `tech-notes/ufi-voctech-trust-voctech-ignite.md` — Created
- `tech-notes/ordnance-survey-geovation-accelerator-spring-2026.md` — Created
- `tech-notes/indigo-trust-grants.md` — Created
- `tech-notes/esmee-fairbairn-foundation-main-fund.md` — Created
- `tech-notes/social-investment-business-reach-fund.md` — Created
- `tech-notes/paul-hamlyn-foundation-open-funds.md` — Created
- `tech-notes/national-lottery-community-fund-awards-for-all-england-environment.md` — Created
- `tech-notes/nesta-challenge-works-longitude-prize-on-als.md` — Created
- `tech-notes/nesta-collective-intelligence-grants.md` — Created
- `tech-notes/lloyds-bank-foundation-specialist-and-equity-programmes.md` — Created
- `tech-notes/nesta-mission-studio.md` — Created
- `tech-notes/lankelly-chase-endowment-redistribution.md` — Created

---

**Generated by**: ArcKit `/arckit:grants` command
**Generated on**: 2026-05-07
**ArcKit Version**: 4.18.0
**Project**: 001-arckit-saas
**Model**: Claude Opus 4.7
