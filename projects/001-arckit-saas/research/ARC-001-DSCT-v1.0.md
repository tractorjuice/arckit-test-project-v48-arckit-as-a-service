# Data Source Discovery: ArcKit as a Service

> **Template Origin**: Official | **ArcKit Version**: 4.16.6 | **Command**: `/arckit.datascout`

## Document Control

<!-- DOC-CONTROL-HEADER -->
<!-- Resolved at command-execution time to _partials/document-control-uk.md or _partials/document-control-uae.md based on plugin userConfig classification_scheme + governance_framework. See _partials/RENDERING.md (when present). -->

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DSCT-v1.0 |
| **Project** | ArcKit as a Service (001) |
| **Classification** | OFFICIAL |
| **Version** | 1.0 |
| **Date** | 2026-05-06 |
| **Owner** | Mark Craddock, ArcKit as a Service Owner |
| **Rubric Used** | uk-gov |
| **AI Model** | Claude Opus 4.7 (1M context) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-06 | ArcKit AI | Initial creation from `/arckit.datascout` agent | PENDING | PENDING |

---

## Executive Summary

### Data Needs Overview

This document presents data source discovery findings for the **ArcKit as a Service** project, identifying external APIs, datasets, and data portals that can fulfil the data and integration requirements documented in `ARC-001-REQ-v*.md`.

**Requirements Analyzed**: 7 data requirements (DR-xxx), 4 functional requirements (FR-xxx), 4 integration requirements (INT-xxx), 2 non-functional requirements (NFR-xxx)

**Data Source Categories Identified**: 4 categories based on requirement analysis (company, identity, financial, reference)

**Discovery Approach**: UK Government open data, commercial API research via G-Cloud Digital Marketplace, free/freemium API discovery, structured WebSearch and WebFetch by reader subagent.

### Key Findings

- **company**: Companies House Public Data API (score 73.0/100) — only canonical, OGL-v3, GB-hosted source for FR-001 / BR-003 / INT-003.
- **identity**: Microsoft Entra ID (score 70.5/100) — G-Cloud-14 listed, ISO 27001 + SOC 2 Type 2; broad SSO footprint suits both SME tenants and large-enterprise cross-subsidy customers; Auth0 by Okta (67.1) and Okta Workforce (66.8) are credible alternatives.
- **financial**: HMRC VAT (MTD) API (score 67.0/100) — authoritative GB-hosted VAT integration for FR-011; companion gap (GAP-2) exists for VAT-number validation.
- **reference**: OS Data Hub (52.8/100) and postcodes.io (52.6/100) — free/freemium UK gazetteer + MIT-licensed postcode lookup, complemented by ONSPD bulk download (51.5/100) for sovereign / offline mode (Principle 21).
- **Sovereign mode (GAP-4, HIGH)**: every shortlisted live API needs an offline-capable equivalent (e.g., ONSPD for postcodes.io, Companies House bulk product for the Public Data API).

### Data Source Summary

| Source Type | Count | Cost Range | Key Providers |
|-------------|-------|------------|---------------|
| **UK Government Open Data** | 12 | Free (OGL-v3) | Companies House, FCA, GDS (One Login), DVLA, DBS, HMRC, Bank of England, ONS |
| **Commercial APIs** | 9 | £0–£enterprise/year | Microsoft (Entra), Okta (Auth0/Workforce), Yoti, Onfido, GLEIF, OpenCorporates, Creditsafe, Dun & Bradstreet, Experian |
| **Free/Freemium APIs** | 5 | Free / freemium | Ordnance Survey OS Data Hub, postcodes.io, ONSPD, ONS Open Geography, SIC codes |
| **Open Source Datasets** | 0 | Free | — |
| **TOTAL** | 26 | £0 (open/free preferred) – enterprise quote (rejected) | |

### Top Recommended Sources

**Shortlist for integration**:

1. **Companies House Public Data API** for company: authoritative UK register, OGL-v3, real-time, GB-hosted, score 73.0/100
2. **Microsoft Entra ID** for identity: ISO 27001 + SOC 2 Type 2, G-Cloud-14 listed, score 70.5/100
3. **HMRC VAT (MTD) API** for financial: authoritative GB-hosted VAT integration, OGL-v3, score 67.0/100
4. **GLEIF LEI API** for company (cross-border): CC0-1.0 open beneficial-ownership data, score 54.4/100
5. **OS Data Hub APIs** for reference: authoritative UK gazetteer, OGL-v3 base, score 52.8/100
6. **postcodes.io** for reference: MIT-licensed open postcode lookup, score 52.6/100
7. **GOV.UK One Login** for identity: free relying-party model, GB-hosted, score 61.25/100
8. **SIC code reference data** for reference: small static OGL-v3 dataset, score 51.25/100

### Requirements Coverage

- ✅ **9 requirements (~41%)** fully matched to external data sources (BR-003, FR-001, FR-007, FR-011, INT-001, INT-003, NFR-SEC-001, DR-001, DR-007)
- ⚠️ **0 requirements (0%)** partially matched
- ❌ **13 requirements (~59%)** out of scope, internal, or constraint (no external data source applicable; see traceability)

---

## Data Needs Analysis

> **Note**: Data needs are extracted from requirements, categorised by type, with criticality and volume/freshness expectations.

### Extracted Data Needs

| # | Requirement ID | Data Need | Type | Criticality | Volume | Freshness | Source Category |
|---|----------------|-----------|------|-------------|--------|-----------|-----------------|
| 1 | DR-001 | Tenant entity (Companies House number, residency_region) | Data | MUST | ≤ 5,000 verifications | Real-time onboarding; daily refresh | company |
| 2 | DR-007 | SME Verification Record (snapshot retained 7 years) | Data | MUST | ≤ 5,000 records | Real-time on event | company |
| 3 | FR-001 | Tenant Provisioning + SME Verification | Functional | MUST | ≤ 5,000 onboardings | Real-time | company / reference |
| 4 | FR-007 | SSO Integration (OIDC/SAML 2.0) | Functional | MUST | ~5,000 users; peak ~100 sign-ins/sec | Real-time (sub-2-second) | identity |
| 5 | FR-011 | Billing & Subscription Management (VAT-compliant invoicing) | Functional | MUST | A few VAT/FX lookups per tenant per month | Daily (FX); ad-hoc (VAT); monthly (CPI) | financial |
| 6 | FR-013 | Form-input validation (postcode, address) | Functional | SHOULD | ~10,000 requests/month at GA | ad-hoc | reference |
| 7 | INT-001 | Tenant Identity Provider (SSO) | Integration | MUST | Federation events for ~5,000 users | Real-time | identity |
| 8 | INT-003 | Companies House (UK SME Verification) | Integration | MUST | ≤ 5,000 verifications | Real-time | company |
| 9 | NFR-SEC-001 | Authentication (incl. MFA) | Non-Functional | MUST | — | — | identity (constraint) |
| 10 | NFR-SEC-007 | Service-to-Service Authentication | Non-Functional | MUST | — | — | constraint |

### Data Needs by Category

**Category 1: company**

- Requirements: BR-003, FR-001, INT-003, DR-001, DR-007
- Data fields needed: Company number, legal name, status, SIC codes, registered office, officers, persons-with-significant-control, filing history, SME-size indicators
- Volume: ≤ 5,000 verifications at GA + 24 months (DR-001 cap), with annual re-verification
- Freshness: Real-time at onboarding; daily refresh acceptable for renewals
- Quality threshold: Authoritative (official register); completeness ≥ 99% on incorporated UK entities

**Category 2: identity**

- Requirements: FR-007, INT-001, NFR-SEC-001, NFR-SEC-007
- Data fields needed: OIDC/SAML federation primitives, MFA, group/role claims, optional identity-proofing assertions for high-assurance flows
- Volume: Federation events for ~5,000 tenant-users (DR-002), peak ~100 sign-ins/sec
- Freshness: Real-time (sub-2-second federation per INT-001 SLA)
- Quality threshold: FIDO2/WebAuthn-class MFA preferred; provider must align with NCSC CAF and GDPR/Article 46 transfer mechanism

**Category 3: financial**

- Requirements: FR-011, BR-002, BR-005
- Data fields needed: VAT registration validation, daily reference exchange rates (GBP/EUR/USD), CPI for indexation
- Volume: Light: a few VAT/FX lookups per tenant per month
- Freshness: Daily (exchange rates); ad-hoc (VAT validation); monthly (inflation)
- Quality threshold: Authoritative (HMRC, Bank of England, ONS)

**Category 4: reference**

- Requirements: DR-001, FR-001, FR-013
- Data fields needed: UK postcode validation, address geocoding, SIC code lookups, ISO country/currency codes
- Volume: One lookup per onboarding + form-input validation; ~10,000 requests/month at GA scale
- Freshness: ad-hoc / quarterly refresh acceptable
- Quality threshold: Authoritative geographies (ONS / OS); fully open licence preferred

---

## Data Source Discovery

> **Note**: Categories are dynamically identified from project requirements, not a fixed list.

---

## Category 1: company

**Requirements Addressed**: BR-003, FR-001, INT-003, DR-001, DR-007

**Why This Category**: SME eligibility verification is a load-bearing requirement (BR-003) for ArcKit as a Service. The platform must verify that a tenant signing up is a UK-incorporated SME, capture an authoritative snapshot of their registered status (DR-007), and refresh that record annually.

**Data Fields Needed**: Company number, legal name, status, SIC codes, registered office, officers, persons-with-significant-control, filing history, SME-size indicators.

---

### Source 1A: Companies House Public Data API (UK Government Open Data)

**Provider**: Companies House — https://developer-specs.company-information.service.gov.uk/

**Description**: Authoritative UK company register; profile, officers, filing history, persons-with-significant-control, registered office, insolvency, charges; the canonical source for SME verification.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | open-data (free) |
| **Format** | JSON (REST) |
| **API Endpoint** | https://developer-specs.company-information.service.gov.uk/ |
| **Authentication** | API Key |
| **Rate Limits** | 120 requests/minute |
| **Update Frequency** | real-time |
| **Coverage** | UK-wide (all incorporated entities) |
| **Temporal Coverage** | Live register |
| **Data Quality** | Authoritative; completeness ≥ 99% on incorporated UK entities |
| **Documentation** | Excellent (developer-specs portal) |
| **SLA** | Best-effort (no contractual SLA on free tier) |
| **GDPR Status** | Public register; officer PII is publicly published per statute |
| **UK Data Residency** | Yes (GB) |

**Requirements Fit**:

- ✅ Covers: company-profile, officers, filing-history, persons-with-significant-control, company-search, registered-office, insolvency, charges
- ❌ Missing: PEP/sanctions screening (see GAP-1); SME-size derivation requires accounts (see CH-DOC-1)
- ⚠️ Partial: rate limit may need backoff under high concurrency

**Integration Approach**:

- **Pattern**: REST API call on demand + Streaming API (CH-STREAM-1) for delta refresh
- **Estimated Effort**: 5–8 person-days
- **Dependencies**: API key registration (self-service), retry/backoff strategy

**Evaluation Score**:

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 5.5/10 | 13.75/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 (residency adj. +10 GB applied, capped at 100) |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 7/10 | 7/10 |
| **Total** | **100%** | | **73.0/100** |

**Recommendation**: shortlist

---

### Source 1B: Companies House Streaming API (UK Government Open Data)

**Provider**: Companies House — https://developer-specs.company-information.service.gov.uk/

**Description**: Companion event-stream API for changes to company-profile, filing-history, officers, PSC, charges, insolvency.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | open-data (free) |
| **Format** | JSON event stream |
| **API Endpoint** | https://developer-specs.company-information.service.gov.uk/ |
| **Authentication** | API Key |
| **Rate Limits** | n/a (streaming) |
| **Update Frequency** | real-time |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **57.25/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0/10 | 0/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 (residency adj. +10 GB) |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Use to keep tenant SME records fresh between annual re-verifications.

---

### Source 1C: Companies House Document API (UK Government Open Data)

**Provider**: Companies House — https://developer-specs.company-information.service.gov.uk/

**Description**: Filed accounts and statutory documents (accounts, confirmation statements, annual returns).

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | open-data |
| **Authentication** | API Key |
| **Rate Limits** | 120/min |
| **Update Frequency** | daily |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **55.25/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0/10 | 0/25 |
| Data Quality | 20% | 8/10 | 16/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 7/10 | 7/10 |

**Rationale**: Useful for SME size verification (employee/turnover bands) when SME thresholds need evidencing beyond company status.

---

### Source 1D: FCA Financial Services Register API (UK Government Open Data)

**Provider**: Financial Conduct Authority — https://www.fca.org.uk/firms/financial-services-register

**Description**: Authorised firms, approved individuals, permissions, appointed representatives, regulatory status.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | free |
| **Authentication** | API Key |
| **Update Frequency** | daily |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **51.75/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0/10 | 0/25 |
| Data Quality | 20% | 8/10 | 16/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Relevant if a future tenant cohort includes FS firms requiring regulatory-status validation; not required for the GA scope.

---

### Source 1E: GLEIF LEI API (Commercial / Open Beneficial-Ownership)

**Provider**: GLEIF — https://www.gleif.org/en/about/open-data

**Description**: Cross-jurisdiction Legal Entity Identifier lookup; CC0-1.0 open beneficial-ownership register.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | CC0-1.0 |
| **Pricing** | open-data |
| **Authentication** | None |
| **Update Frequency** | daily |
| **UK Data Residency** | Not stated |

**Evaluation Score**: **54.4/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1.8/10 | 4.5/25 |
| Data Quality | 20% | 8/10 | 16/20 |
| License & Cost | 15% | 9.75/10 | 14.625/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Pairs naturally with Companies House for non-UK SME edge-cases and global supply-chain due diligence.

---

### Source 1F: OpenCorporates Public API (Commercial Aggregator)

**Provider**: OpenCorporates — https://api.opencorporates.com/documentation/API-Reference

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Freemium |
| **Pricing** | freemium |
| **Authentication** | API Key |

**Evaluation Score**: **48.0/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 3/10 | 7.5/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 6.5/10 | 9.75/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Aggregator across ~140 jurisdictions; freemium tier supports proof-of-concept; useful supplement when tenants are non-UK incorporated.

---

### Source 1G: Creditsafe Business Information API (Commercial)

**Provider**: Creditsafe — G-Cloud-14 listing

**Evaluation Score**: **44.6/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 3/10 | 7.5/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 4.25/10 | 6.375/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: G-Cloud-14 listed UK SME credit data provider; useful for BR-005 cross-subsidy creditworthiness signal; subscription cost competes with the SME-affordable principle and would need an ADR.

---

### Source 1H: Dun & Bradstreet Data Cloud (Commercial — REJECTED)

**Provider**: Dun & Bradstreet — G-Cloud-14 listing

**Evaluation Score**: **34.9/100** — Recommendation: reject

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1.5/10 | 3.75/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 3.25/10 | 4.875/15 |
| API Quality | 15% | 5/10 | 7.5/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Enterprise-quote pricing and limited evidence of UK residency commitments; cost-of-serve unsuitable for SME-tier funding model.

---

### Source 1I: Experian Business Information (Commercial — REJECTED)

**Provider**: Experian — G-Cloud-14 listing

**Evaluation Score**: **33.1/100** — Recommendation: reject

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0.8/10 | 2/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 3.25/10 | 4.875/15 |
| API Quality | 15% | 5/10 | 7.5/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Enterprise-quote pricing; identity-verification scope overlaps with dedicated identity providers; not preferred over Companies House + postcodes.io + identity vendor combination.

---

### Comparison Table: company

| Criterion | CH Public Data | CH Streaming | CH Document | FCA FSR | GLEIF | OpenCorporates | Creditsafe | D&B | Experian |
|-----------|----|----|----|----|----|----|----|----|----|
| **Provider** | Companies House | Companies House | Companies House | FCA | GLEIF | OpenCorporates | Creditsafe | D&B | Experian |
| **License** | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | CC0-1.0 | Freemium | Commercial | Commercial | Commercial |
| **Cost (Annual)** | £0 | £0 | £0 | £0 | £0 | £0–subscription | Subscription | Enterprise quote | Enterprise quote |
| **Coverage** | UK | UK | UK | UK | Global | Global (~140 jx) | UK SME | Global | Global |
| **Freshness** | Real-time | Real-time | Daily | Daily | Daily | Varies | Varies | Varies | Varies |
| **Requirements Fit** | 13.75/25 | 0/25 | 0/25 | 0/25 | 4.5/25 | 7.5/25 | 7.5/25 | 3.75/25 | 2/25 |
| **Data Quality** | 20/20 | 20/20 | 16/20 | 16/20 | 16/20 | 10/20 | 10/20 | 10/20 | 10/20 |
| **License & Cost** | 15/15 | 15/15 | 15/15 | 15/15 | 14.6/15 | 9.75/15 | 6.4/15 | 4.9/15 | 4.9/15 |
| **API Quality** | 12/15 | 12/15 | 12/15 | 12/15 | 10.5/15 | 12/15 | 12/15 | 7.5/15 | 7.5/15 |
| **Compliance** | 5.25/15 | 5.25/15 | 5.25/15 | 3.75/15 | 3.75/15 | 3.75/15 | 3.75/15 | 3.75/15 | 3.75/15 |
| **Reliability** | 7/10 | 5/10 | 7/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 |
| **TOTAL SCORE** | **73.0** | **57.25** | **55.25** | **51.75** | **54.4** | **48.0** | **44.6** | **34.9** | **33.1** |

**Recommendation for company**: **Companies House Public Data API** as primary; supplement with **Companies House Streaming API** for delta refresh, **Companies House Document API** for SME-size derivation, and **GLEIF LEI API** for cross-border edge cases. Reject D&B and Experian on cost-of-serve grounds (Principle 1: SME-affordable).

---

## Category 2: identity

**Requirements Addressed**: FR-007, INT-001, NFR-SEC-001, NFR-SEC-007

**Why This Category**: Tenants federate via OIDC/SAML; ArcKit must integrate against any commercial IdP and optionally GOV.UK One Login for buying-authority sign-in.

**Data Fields Needed**: OIDC/SAML federation primitives, MFA, group/role claims, optional identity-proofing assertions for high-assurance flows.

---

### Source 2A: GOV.UK One Login Technical Documentation (UK Government)

**Provider**: Government Digital Service — https://docs.sign-in.service.gov.uk/

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | free (relying-party) |
| **Authentication** | OAuth2 / OIDC |
| **Update Frequency** | real-time |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **61.25/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1/10 | 2.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Relevant if buying-authority-staff sign-in is added (Persona 3); GB-hosted; complements (does not replace) tenant-side commercial IdP.

---

### Source 2B: DVLA Access to Driver Data API (UK Government)

**Provider**: DVLA — https://developer-portal.driver-vehicle-licensing.api.gov.uk/availableapis.html

**Evaluation Score**: **56.5/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0/10 | 0/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 8.5/10 | 12.75/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Could harden identity proofing for high-assurance tenant-admin actions; not in MVP scope.

---

### Source 2C: GOV.UK One Login (Service Overview) (UK Government)

**Provider**: GDS — https://www.sign-in.service.gov.uk/about

**Evaluation Score**: **53.0/100** — Recommendation: shortlist (citation companion to ONELOGIN-DOCS-1)

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1.7/10 | 4.25/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

---

### Source 2D: DVLA Developer Portal (Landing) (UK Government — REJECTED)

**Evaluation Score**: **49.25/100** — Recommendation: reject (superseded by DVLA-API-1).

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1.1/10 | 2.75/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 8.5/10 | 12.75/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

---

### Source 2E: DBS Checks (UK Government — REJECTED for v1)

**Provider**: Disclosure and Barring Service — https://www.gov.uk/government/organisations/disclosure-and-barring-service

**Evaluation Score**: **40.5/100** — Recommendation: reject (out-of-scope for v1; revisit if MOD/sovereign-cleared customers require operator vetting).

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0/10 | 0/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 8.5/10 | 12.75/15 |
| API Quality | 15% | 5/10 | 7.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

---

### Source 2F: Microsoft Entra ID (Commercial)

**Provider**: Microsoft — https://learn.microsoft.com/en-us/entra/identity/

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Commercial (per-seat) |
| **Certifications** | ISO 27001, SOC 2 Type 2, GDPR-compliant-asserted, G-Cloud-listed |
| **Authentication** | OAuth2 / OIDC / SAML |
| **Update Frequency** | real-time |
| **UK Data Residency** | UK Azure regions available (hosted_in not formally stated) |

**Evaluation Score**: **70.5/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 5/10 | 12.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 4/10 | 6/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 9/10 | 13.5/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: G-Cloud-14 listed; broad SSO footprint among likely SME tenants and large-enterprise cross-subsidy customers; UK Azure regions deliverable.

---

### Source 2G: Auth0 by Okta (Commercial)

**Provider**: Okta — https://security.okta.com/

**Evaluation Score**: **67.1/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 5/10 | 12.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 4.25/10 | 6.375/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 6.5/10 | 9.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Strong B2B/B2C OIDC + SAML stack; mature developer experience.

---

### Source 2H: Okta Workforce Identity Cloud (Commercial)

**Provider**: Okta — https://security.okta.com/

**Evaluation Score**: **66.8/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 5/10 | 12.5/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 4/10 | 6/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 6.5/10 | 9.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: SCIM lifecycle hooks attractive for tenant admin lifecycle automation. Choice between Auth0 and Workforce hinges on tenant model — record an ADR.

---

### Source 2I: Yoti Identity Verification (Commercial)

**Provider**: Yoti — https://www.yoti.com/business/identity-verification/

**Evaluation Score**: **57.0/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0.8/10 | 2/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 5.5/10 | 8.25/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 6.5/10 | 9.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: GB-hosted UK identity-proofing; useful as add-on for high-assurance flows.

---

### Source 2J: Onfido Document and Biometric Identity Verification (Commercial)

**Provider**: Onfido — G-Cloud-14 listing

**Evaluation Score**: **55.0/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0.9/10 | 2.25/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 4.5/10 | 6.75/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 6/10 | 9/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: G-Cloud-14 alternative to Yoti; pick one identity-proofing partner via ADR if scope expands.

---

### Comparison Table: identity

| Criterion | One Login (Docs) | DVLA API | One Login (About) | DVLA Portal | DBS | Entra ID | Auth0 | Okta WIC | Yoti | Onfido |
|-----------|----|----|----|----|----|----|----|----|----|----|
| **License** | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | Commercial | Commercial | Commercial | Commercial | Commercial |
| **Cost** | Free | Usage-based | Free | Usage-based | Usage-based | Per-seat | Subscription | Per-seat | Usage-based | Usage-based |
| **Requirements Fit** | 2.5/25 | 0/25 | 4.25/25 | 2.75/25 | 0/25 | 12.5/25 | 12.5/25 | 12.5/25 | 2/25 | 2.25/25 |
| **Data Quality** | 20/20 | 20/20 | 10/20 | 10/20 | 10/20 | 20/20 | 20/20 | 20/20 | 20/20 | 20/20 |
| **License & Cost** | 15/15 | 12.75/15 | 15/15 | 12.75/15 | 12.75/15 | 6/15 | 6.4/15 | 6/15 | 8.25/15 | 6.75/15 |
| **API Quality** | 13.5/15 | 13.5/15 | 13.5/15 | 13.5/15 | 7.5/15 | 13.5/15 | 13.5/15 | 13.5/15 | 12/15 | 12/15 |
| **Compliance** | 5.25/15 | 5.25/15 | 5.25/15 | 5.25/15 | 5.25/15 | 13.5/15 | 9.75/15 | 9.75/15 | 9.75/15 | 9/15 |
| **Reliability** | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 |
| **TOTAL SCORE** | **61.25** | **56.5** | **53.0** | **49.25** | **40.5** | **70.5** | **67.1** | **66.8** | **57.0** | **55.0** |

**Recommendation for identity**: **Microsoft Entra ID** as primary, with **Auth0 by Okta** as a credible alternative; **GOV.UK One Login** for buying-authority sign-in. Defer DVLA / DBS / identity-proofing add-ons to a future scope expansion (capture in ADR).

---

## Category 3: financial

**Requirements Addressed**: FR-011, BR-002, BR-005

**Why This Category**: VAT-compliant invoicing (FR-011), optional FX for non-GBP billing, and indexation for cross-subsidy review (BR-005).

**Data Fields Needed**: VAT registration validation, daily reference exchange rates, CPI for indexation.

---

### Source 3A: HMRC VAT (MTD) API (UK Government)

**Provider**: HMRC — https://developer.service.hmrc.gov.uk/api-documentation/docs/authorisation

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | open-data |
| **Authentication** | OAuth2 |
| **Rate Limits** | 180/min |
| **Update Frequency** | real-time |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **67.0/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 2.5/10 | 6.25/25 |
| Data Quality | 20% | 10/10 | 20/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 7/10 | 7/10 |

**Rationale**: Authoritative VAT integration for FR-011; OAuth2 onboarding is non-trivial but plausible.

---

### Source 3B: HMRC Developer Hub (UK Government)

**Provider**: HMRC — https://developer.service.hmrc.gov.uk/api-documentation

**Evaluation Score**: **53.5/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1.1/10 | 2.75/25 |
| Data Quality | 20% | 5/10 | 10/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 9/10 | 13.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 7/10 | 7/10 |

**Rationale**: Foundational gateway for any future HMRC API needs (corporation tax, customs).

---

### Source 3C: Bank of England IADB — Daily Spot Exchange Rates (UK Government)

**Provider**: Bank of England — https://www.bankofengland.co.uk/boeapps/database/

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Unknown (re-distribution comfort to confirm) |
| **Pricing** | open-data |
| **Authentication** | None |
| **Update Frequency** | daily |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **49.0/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 1.3/10 | 3.25/25 |
| Data Quality | 20% | 8/10 | 16/20 |
| License & Cost | 15% | 7/10 | 10.5/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Daily reference exchange rates for non-GBP customer billing; licence type unverified — confirm before re-distribution.

---

### Source 3D: ONS Inflation and Price Indices (UK Government)

**Provider**: ONS — https://www.ons.gov.uk/economy/inflationandpriceindices

**Evaluation Score**: **43.75/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 0/10 | 0/25 |
| Data Quality | 20% | 4/10 | 8/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: CPI/CPIH for any contract-indexation clauses (BR-005 cross-subsidy review); not a direct billing input but useful for pricing review cadence.

---

### Comparison Table: financial

| Criterion | HMRC VAT (MTD) | HMRC Dev Hub | BoE IADB | ONS CPI |
|-----------|----|----|----|----|
| **License** | OGL-v3 | OGL-v3 | Unknown | OGL-v3 |
| **Cost** | Free | Free | Free | Free |
| **Requirements Fit** | 6.25/25 | 2.75/25 | 3.25/25 | 0/25 |
| **Data Quality** | 20/20 | 10/20 | 16/20 | 8/20 |
| **License & Cost** | 15/15 | 15/15 | 10.5/15 | 15/15 |
| **API Quality** | 13.5/15 | 13.5/15 | 10.5/15 | 10.5/15 |
| **Compliance** | 5.25/15 | 5.25/15 | 3.75/15 | 5.25/15 |
| **Reliability** | 7/10 | 7/10 | 5/10 | 5/10 |
| **TOTAL SCORE** | **67.0** | **53.5** | **49.0** | **43.75** |

**Recommendation for financial**: **HMRC VAT (MTD) API** as the GA financial integration; companion gap GAP-2 (VAT-number validation) is LOW severity and can be closed in v1.1. BoE / ONS as optional secondary feeds.

---

## Category 4: reference

**Requirements Addressed**: DR-001, FR-001, FR-013

**Why This Category**: Form-input validation (postcodes, addresses), industry classification, and (optionally) regional analytics.

**Data Fields Needed**: UK postcode validation, address geocoding, SIC code lookups, ISO country/currency codes.

---

### Source 4A: OS Data Hub APIs (Free / Freemium)

**Provider**: Ordnance Survey — https://api.os.uk/

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 (base tier) |
| **Pricing** | freemium |
| **Authentication** | API Key |
| **Update Frequency** | monthly |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **52.8/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 3.3/10 | 8.25/25 |
| Data Quality | 20% | 4/10 | 8/20 |
| License & Cost | 15% | 9.5/10 | 14.25/15 |
| API Quality | 15% | 8/10 | 12/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Authoritative UK gazetteer; free tier supports MVP onboarding; clear upgrade path for scale.

---

### Source 4B: postcodes.io (Free)

**Provider**: Ideal Postcodes — https://postcodes.io/

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | MIT |
| **Pricing** | free |
| **Authentication** | None |
| **Update Frequency** | ad-hoc |

**Evaluation Score**: **52.6/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 5.7/10 | 14.25/25 |
| Data Quality | 20% | 3/10 | 6/20 |
| License & Cost | 15% | 8.75/10 | 13.125/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 2.5/10 | 3.75/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: MIT-licensed open postcode lookup — perfect for SME signup form (FR-001) postcode validation; expect to self-host or have a fallback for resilience.

---

### Source 4C: ONS Postcode Directory (ONSPD) (Free / Bulk Download)

**Provider**: ONS — https://www.ons.gov.uk/methodology/geography/licences

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | open-data |
| **Authentication** | None |
| **Update Frequency** | quarterly |
| **UK Data Residency** | Yes (GB) |

**Evaluation Score**: **51.5/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 4.3/10 | 10.75/25 |
| Data Quality | 20% | 2.5/10 | 5/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Authoritative bulk download for self-hosted reference; complements postcodes.io or replaces it for offline / sovereign mode (Principle 21).

---

### Source 4D: UK SIC Codes (Free)

**Provider**: Companies House — https://www.gov.uk/government/publications/standard-industrial-classification-of-economic-activities-sic

**Evaluation Score**: **51.25/100** — Recommendation: shortlist

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 3.8/10 | 9.5/25 |
| Data Quality | 20% | 3/10 | 6/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Small static dataset — ship as bundled reference data.

---

### Source 4E: ONS Open Geography Portal (Free)

**Provider**: ONS — https://geoportal.statistics.gov.uk/

**Evaluation Score**: **50.25/100** — Recommendation: consider

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 3.8/10 | 9.5/25 |
| Data Quality | 20% | 2.5/10 | 5/20 |
| License & Cost | 15% | 10/10 | 15/15 |
| API Quality | 15% | 7/10 | 10.5/15 |
| Compliance | 15% | 3.5/10 | 5.25/15 |
| Reliability | 10% | 5/10 | 5/10 |

**Rationale**: Geography boundaries for any future regional tenant analytics; not in MVP scope.

---

### Comparison Table: reference

| Criterion | OS Data Hub | postcodes.io | ONSPD | SIC Codes | ONS Geo |
|-----------|----|----|----|----|----|
| **License** | OGL-v3 | MIT | OGL-v3 | OGL-v3 | OGL-v3 |
| **Cost** | Freemium | Free | Free | Free | Free |
| **Coverage** | UK | UK | UK | UK | UK |
| **Freshness** | Monthly | ad-hoc | Quarterly | ad-hoc | Quarterly |
| **Requirements Fit** | 8.25/25 | 14.25/25 | 10.75/25 | 9.5/25 | 9.5/25 |
| **Data Quality** | 8/20 | 6/20 | 5/20 | 6/20 | 5/20 |
| **License & Cost** | 14.25/15 | 13.125/15 | 15/15 | 15/15 | 15/15 |
| **API Quality** | 12/15 | 10.5/15 | 10.5/15 | 10.5/15 | 10.5/15 |
| **Compliance** | 5.25/15 | 3.75/15 | 5.25/15 | 5.25/15 | 5.25/15 |
| **Reliability** | 5/10 | 5/10 | 5/10 | 5/10 | 5/10 |
| **TOTAL SCORE** | **52.8** | **52.6** | **51.5** | **51.25** | **50.25** |

**Recommendation for reference**: **postcodes.io** for live MVP postcode validation; **ONSPD** as the offline fallback / sovereign-mode equivalent; **OS Data Hub** for richer geocoding when needed; **SIC Codes** bundled as static reference data.

---

## Evaluation Matrix

### Overall Scoring Summary

| Category | Recommended Source | Type | Score | Annual Cost | Integration Effort |
|----------|-------------------|------|-------|-------------|-------------------|
| company | Companies House Public Data API | UK-Gov Open | 73.0/100 | £0 | 5–8 days |
| identity | Microsoft Entra ID | Commercial | 70.5/100 | Per-seat (tenant-funded; ArcKit pays for own admin tier) | 5–10 days |
| financial | HMRC VAT (MTD) API | UK-Gov Open | 67.0/100 | £0 | 5–8 days |
| reference | OS Data Hub / postcodes.io | Free / Freemium | 52.8 / 52.6 | £0 (MVP) | 2–4 days |
| **TOTAL** | | | **Avg: ~65.6/100** (top picks) | **£0–per-seat IdP** | **~17–30 days** |

### Evaluation Criteria Explained

| Criterion | Weight | What It Measures |
|-----------|--------|-----------------|
| **Requirements Fit** | 25% | Does the source cover the required data fields, scope, granularity, and volume? |
| **Data Quality** | 20% | Accuracy, completeness, consistency, timeliness, and known quality issues |
| **License & Cost** | 15% | License terms (OGL, CC, proprietary), pricing sustainability, total cost (residency adjustment +10 GB applied where applicable, capped at 100) |
| **API Quality** | 15% | REST/GraphQL, documentation quality, SDKs, versioning, error handling, pagination |
| **Compliance** | 15% | GDPR, UK data residency, data classification, terms of use, DPA 2018 |
| **Reliability** | 10% | SLA, uptime history, vendor stability, community/support, track record |

---

## Data Integration Architecture

### Integration Patterns by Source

| Source | Pattern | Auth | Caching | Error Handling | Monitoring |
|--------|---------|------|---------|----------------|------------|
| Companies House Public Data | REST API on demand | API Key | TTL: 24h | Retry 3x + circuit breaker; cached fallback for outage | Health check + alert |
| Companies House Streaming | Event stream | API Key | n/a | Resume from cursor; backoff on disconnect | Lag/freshness alert |
| Microsoft Entra ID | OIDC federation | OAuth2 | Token cache (TTL claim) | IdP discovery fallback; degrade to read-only | Sign-in success-rate SLO |
| HMRC VAT (MTD) | REST API | OAuth2 | None (transactional) | Retry; alert on auth failure | Submission success-rate |
| postcodes.io | REST API | None | TTL: 7 days | Fallback to ONSPD self-hosted | Freshness check |
| OS Data Hub | REST API | API Key | TTL: 24h | Fallback to postcodes.io | Quota monitor |
| SIC Codes | Bundled static | None | Bake into image | n/a | Refresh on release |

### Recommended Integration Architecture

```text
ArcKit core (control plane)
  ├─ Onboarding service ──► Companies House Public Data API (via API gateway)
  │                          ├─ cache layer (TTL 24h)
  │                          └─ Streaming consumer for delta refresh
  ├─ Identity broker     ──► Tenant IdP (Entra ID / Auth0 / Okta) via OIDC
  │                          + GOV.UK One Login (relying party, optional)
  ├─ Billing service     ──► HMRC VAT MTD (OAuth2) + BoE IADB (read-only)
  └─ Reference service   ──► postcodes.io (live) / ONSPD (offline fallback)
                              + bundled SIC codes
Sovereign (Principle 21) deployment substitutes every live API with a signed
offline bundle (Companies House bulk product, ONSPD, HMRC VAT static list).
```

### Authentication and Access

| Source | Auth Method | Credentials Required | Registration Process | Lead Time |
|--------|-----------|---------------------|---------------------|-----------|
| Companies House Public Data | API Key | Free account | Self-service portal | Instant |
| Companies House Streaming | API Key | Free account | Self-service portal | Instant |
| HMRC VAT MTD | OAuth2 | Production credentials | HMRC developer onboarding | 2–4 weeks |
| GOV.UK One Login | OAuth2 | Relying-party registration | GDS service portal | 1–2 weeks |
| Microsoft Entra ID | OAuth2 / OIDC | Tenant-side app registration | Tenant-driven | per-tenant |
| OS Data Hub | API Key | Free account | Self-service | Instant |
| postcodes.io | None | n/a | n/a | Instant |

### Rate Limits and Capacity Planning

| Source | Rate Limit | Projected Usage | Headroom | Upgrade Option |
|--------|-----------|----------------|----------|---------------|
| Companies House Public Data | 120/min | ~1/min average, burst 10/min on onboarding cohorts | ~92% | Apply for higher quota |
| HMRC VAT MTD | 180/min | A few per tenant per month | >99% | n/a |
| postcodes.io | None published (fair-use) | ~10,000/month | ample | Self-host fallback |
| OS Data Hub | Free tier (variable) | ~10,000/month | ample | Paid tier on growth |

---

## Data Utility Analysis

> **Note**: Most data sources have alternative and secondary uses beyond their primary requirement.

### Utility by Source

| Source | Primary Use (Requirement) | Secondary Uses | Strategic Value | Combination Opportunities |
|--------|--------------------------|----------------|-----------------|--------------------------|
| Companies House Public Data | DR-001 / DR-007: SME verification | 1. Officer change monitoring (governance signal) 2. Industry analytics (SIC distribution across tenants) | HIGH | Combines with GLEIF for international beneficial-ownership and with SIC codes for sector reporting |
| Microsoft Entra ID | FR-007 / INT-001: SSO | 1. Conditional-access posture signals 2. Group-based feature flagging | HIGH | Combines with audit trail (DR-005) for unified sign-in + action telemetry |
| HMRC VAT MTD | FR-011: VAT-compliant invoicing | 1. Quarterly tax reconciliation 2. Tenant tax-status signal | MEDIUM | Combines with BoE IADB for non-GBP invoice presentation |
| postcodes.io / ONSPD | FR-001 / FR-013: postcode validation | 1. Regional tenant analytics 2. Sovereign deployment mode (Principle 21) | MEDIUM | Combines with ONS Open Geography for regional cross-subsidy reporting (BR-005) |
| GLEIF LEI | BR-003: cross-border verification | 1. Supply-chain due diligence 2. Group-structure mapping | MEDIUM | Combines with Companies House for hybrid UK + global verification |

### Common Secondary Use Patterns Identified

| Pattern | Source | Primary Use | Secondary Use | Value |
|---------|--------|-------------|---------------|-------|
| **Proxy Indicator** | Companies House Streaming | Delta refresh | PSC change as governance-risk proxy | Early warning for high-risk tenants |
| **Cross-Domain Enrichment** | SIC Codes + Companies House | Industry classification | Enriches billing analytics by sector | Sector-level cross-subsidy reporting (BR-005) |
| **Trend Detection** | ONS CPI | Indexation | Reveals affordability drift in SME tier | Triggers pricing-review cadence |
| **Predictive Feature** | postcodes.io / ONSPD | Form validation | Region as feature for tenant-success modelling | Future ML for retention |

### Data Combination Opportunities

1. **Hybrid SME verification**: Companies House Public Data + GLEIF LEI → unified UK + global beneficial-ownership view for tenants with non-UK holding structures.
2. **Sovereign-mode data plane**: ONSPD + Companies House bulk product + HMRC VAT static list → fully air-gapped equivalent of the GA data plane (Principle 21).
3. **Cross-subsidy analytics**: HMRC VAT MTD + ONS CPI + Companies House SIC distribution → evidence base for BR-005 quarterly cross-subsidy review.

---

## Gap Analysis

### Requirements Without Suitable Data Sources

**GAP-1**: BR-003 / FR-001 (enhanced) — Sanctions / Politically Exposed Persons (PEP) screening for SME verification, beyond Companies House status checks

- **Data Need**: Sanctions / PEP screening for SME verification, beyond Companies House status checks
- **Why No Source**: Not researched in this DSCT cycle; commercial KYC providers (ComplyAdvantage, Refinitiv World-Check, Yoti AML add-on) exist but introduce per-check cost.
- **Impact**: If onboarded an SME later flagged as sanctioned, reputational and regulatory exposure for ArcKit as a Service operator (BR-005, NFR-C-001).
- **Severity**: MEDIUM
- **Recommended Action**: Run a follow-up DSCT pass for category=identity, source_type=commercial focused on AML/PEP, or rely on Yoti AML add-on (already shortlisted).
- **Estimated Effort**: 5 person-days research + 5–10 days integration
- **Cost Estimate**: £0.10–£0.50 per check (volume-dependent)

**GAP-2**: FR-011 — VAT registration number validation (separate from MTD VAT submissions)

- **Data Need**: VAT registration number validation
- **Why No Source**: HMRC publishes a 'Check a UK VAT number' API but it was not the primary URL fetched — HMRC-VAT-MTD-1 covers submission, not validation.
- **Impact**: Invoice issued with invalid VAT number could fail VAT recoverability for tenant; minor tenant-side friction.
- **Severity**: LOW
- **Recommended Action**: Add HMRC 'Check a UK VAT number' API to a future DSCT refresh; integrate as part of FR-011 implementation.
- **Estimated Effort**: 1–2 person-days
- **Cost Estimate**: Free (HMRC OGL-v3)

**GAP-3**: FR-011 / BR-002 — Real-time foreign-exchange API for billing non-GBP customers

- **Data Need**: Real-time FX feed for billing non-GBP customers (e.g., G-Cloud cross-border commerce)
- **Why No Source**: BoE IADB (BOE-IADB-1) gives daily reference rates — not a real-time FX feed; licence_type Unknown reduces re-distribution comfort.
- **Impact**: GA scope is GBP-only per BR-002, so impact is LOW; would become MEDIUM if international SaaS expansion is planned.
- **Severity**: LOW
- **Recommended Action**: Defer until international expansion in scope; if needed, evaluate commercial FX APIs (Open Exchange Rates, currencyapi.com).
- **Estimated Effort**: 2–3 person-days research
- **Cost Estimate**: £20–£200/month subscription

**GAP-4**: Principle 21 / sovereign-deployment — Offline / air-gapped equivalents for every external data source

- **Data Need**: Offline / air-gapped equivalents for every external data source the platform consumes (Companies House, postcodes.io, HMRC, OS, etc.) — verifiable signed bundles consumable inside a sovereign deployment with no internet egress
- **Why No Source**: Most sources researched are network-only APIs; sovereign deployments need static or signed-bundle equivalents (e.g., ONSPD bulk download instead of postcodes.io).
- **Impact**: Sovereign-deployment customers cannot use platform features that depend on live external data unless an offline fallback is provided.
- **Severity**: HIGH (for Principle 21 conformance)
- **Recommended Action**: Pair every shortlisted live API with an offline-capable fallback (ONSPD for postcodes.io; Companies House bulk product for Public Data API; HMRC publishes a static VAT number list for validation). Capture in an ADR under `/arckit:adr`.
- **Estimated Effort**: 10–15 person-days (data engineering) + ongoing refresh pipeline
- **Cost Estimate**: Negligible licence cost; engineering only

### Gap Summary

| Gap | Requirement | Severity | Recommended Action | Effort | Cost |
|-----|-------------|----------|-------------------|--------|------|
| GAP-1 | BR-003 / FR-001 (enhanced) | MEDIUM | Follow-up DSCT for AML/PEP or use Yoti AML add-on | 5 days research + 5–10 days integration | £0.10–£0.50/check |
| GAP-2 | FR-011 | LOW | Add HMRC 'Check a UK VAT number' API | 1–2 days | Free |
| GAP-3 | FR-011 / BR-002 | LOW | Defer until international expansion | 2–3 days research | £20–£200/month |
| GAP-4 | Principle 21 | HIGH | Offline fallback for every live API + ADR | 10–15 days | Engineering only |

---

## Recommendations & Shortlist

### Top 5 Recommended Sources

#### 1. Companies House Public Data API for company

**Overall Score**: 73.0/100

**Rationale**: The only canonical, OGL-v3, GB-hosted source for FR-001 / BR-003 / INT-003 SME verification. Real-time profile + streaming events; rate-limited but adequate for onboarding flows.

**Key Strengths**:

- ✅ Authoritative UK register (data quality 10/10)
- ✅ OGL-v3 open licence, free, GB-hosted
- ✅ Real-time profile + streaming companion API for delta refresh

**Key Concerns**:

- ⚠️ 120/min rate limit — needs backoff under cohort onboarding bursts
- ⚠️ No PEP/sanctions screening (see GAP-1)

**Cost**: Free
**Integration Effort**: 5–8 person-days
**Risk Level**: LOW

**Next Steps**:

- [ ] Register for API access
- [ ] Conduct integration POC (3 days)
- [ ] Validate data quality against requirements
- [ ] Review terms of use / data sharing agreement

#### 2. Microsoft Entra ID for identity

**Overall Score**: 70.5/100

**Rationale**: G-Cloud-14 listed; ISO 27001 + SOC 2 Type 2 + GDPR-asserted; broad enterprise SSO footprint among likely SME tenants and large-enterprise cross-subsidy customers; UK Azure regions deliverable.

**Key Strengths**:

- ✅ Strong compliance posture (compliance 9/10)
- ✅ G-Cloud-14 contract vehicle
- ✅ Broad market coverage among tenant IdPs

**Key Concerns**:

- ⚠️ Per-seat licence cost (Licence & Cost 4/10)
- ⚠️ `hosted_in` not formally stated (UK Azure regions available; confirm during contracting)

**Cost**: Per-seat (tenant-funded for federation; ArcKit pays for own admin tier only)
**Integration Effort**: 5–10 person-days
**Risk Level**: LOW

**Next Steps**:

- [ ] Confirm UK region commitment
- [ ] OIDC integration POC against multi-tenant test app
- [ ] Validate conditional-access flow

#### 3. HMRC VAT (MTD) API for financial

**Overall Score**: 67.0/100

**Rationale**: Authoritative VAT integration for FR-011 invoice flow; OGL-v3, GB-hosted; OAuth2 onboarding is non-trivial but plausible inside delivery scope.

**Key Strengths**:

- ✅ Authoritative HMRC source (data quality 10/10)
- ✅ Free / OGL-v3
- ✅ GB-hosted, 180/min rate limit ample

**Key Concerns**:

- ⚠️ OAuth2 production onboarding 2–4 week lead time
- ⚠️ Companion gap: VAT-number validation API (GAP-2)

**Cost**: Free
**Integration Effort**: 5–8 person-days + lead time
**Risk Level**: LOW

#### 4. GLEIF LEI API for company (cross-border)

**Overall Score**: 54.4/100

**Rationale**: CC0-1.0 open beneficial-ownership register; cross-jurisdiction LEI lookup useful for non-UK SME edge-cases and global supply-chain due diligence.

**Cost**: Free
**Integration Effort**: 2–3 person-days
**Risk Level**: LOW

#### 5. OS Data Hub + postcodes.io for reference

**Overall Score**: 52.8 / 52.6 (paired)

**Rationale**: OS Data Hub is the authoritative UK gazetteer with an OGL-v3 base; postcodes.io is MIT-licensed and zero-auth — pair them with ONSPD as a sovereign fallback.

**Cost**: Free (MVP)
**Integration Effort**: 2–4 person-days
**Risk Level**: LOW

---

## Impact on Data Model

> **Note**: Only applicable if data model (`ARC-*-DATA-*.md`) exists.

### New Entities from External Sources

| Entity | Source | Description | Key Attributes | Sync Strategy |
|--------|--------|-------------|---------------|---------------|
| SMEVerificationRecord (DR-007) | Companies House Public Data | Snapshot of CH response at verification time | company_number, status, registered_office, officers, psc, verified_at | Real-time on event; retained 7 years |
| TenantCompanyProfile | Companies House Public Data + Streaming | Live linked view of tenant's CH record | company_number, sic_codes, status, last_filing | Stream-driven |
| LEIRecord (optional) | GLEIF | Legal entity identifier for cross-border tenants | lei, legal_name, jurisdiction | Daily refresh |

### New Attributes on Existing Entities

| Existing Entity | New Attribute | Source | Type | Update Frequency |
|----------------|---------------|--------|------|-----------------|
| Tenant (DR-001) | companies_house_number | Companies House | string | At onboarding + annual re-verify |
| Tenant (DR-001) | residency_region | postcodes.io / ONSPD | string | At onboarding |
| Tenant (DR-001) | sic_codes | Companies House + SIC reference | string[] | At onboarding |
| Subscription (DR-006) | vat_number_validated | HMRC VAT MTD (+ GAP-2 API) | bool + timestamp | At billing setup |

### New Relationships

| From Entity | To Entity | Relationship | Source | Description |
|-------------|-----------|-------------|--------|-------------|
| Tenant | SMEVerificationRecord | 1:N | Companies House | Each tenant has one+ verification snapshots over time |
| Tenant | LEIRecord | 0..1:1 | GLEIF | Optional for tenants with non-UK holding structures |

### Sync Strategy

| Source | Pattern | Frequency | Staleness Tolerance | Fallback |
|--------|---------|-----------|--------------------|---------|
| Companies House Public Data | API call on demand | Real-time (onboarding); annual re-verify | 24h | Serve cached snapshot; degrade to read-only |
| Companies House Streaming | Event-driven | Real-time | 1h lag | Resume from cursor |
| postcodes.io | API call on demand | ad-hoc | 7 days | ONSPD self-hosted bundle |
| HMRC VAT MTD | API call on demand | Real-time | n/a | Block submission; alert |
| Microsoft Entra ID | OIDC redirect | Real-time | n/a (token-based) | IdP-side concern |

---

## UK Government Open Data Opportunities

> **Note**: Only applicable if this is a UK Government project.

### TCoP Point 10: Make Better Use of Data

**Open Data Consumed**:

| Source | Dataset | License | Requirement | Status |
|--------|---------|---------|-------------|--------|
| Companies House | Public Data API | OGL-v3 | BR-003, FR-001, INT-003, DR-001, DR-007 | ✅ Recommended |
| Companies House | Streaming API | OGL-v3 | DR-007 (refresh) | ✅ Recommended |
| HMRC | VAT (MTD) API | OGL-v3 | FR-011 | ✅ Recommended |
| GDS | GOV.UK One Login | OGL-v3 | FR-007 (Persona 3) | ✅ Recommended |
| Ordnance Survey | OS Data Hub | OGL-v3 | FR-001, FR-013 | ✅ Recommended |
| ONS | ONSPD | OGL-v3 | FR-001, FR-013 (sovereign) | ✅ Recommended |
| Companies House | UK SIC Codes | OGL-v3 | FR-001 | ✅ Recommended |
| Bank of England | IADB Spot Rates | Unknown | BR-002 (optional) | ⚠️ Consider (verify licence) |
| ONS | CPI / CPIH | OGL-v3 | BR-005 (review cadence) | ⚠️ Consider |
| FCA | Financial Services Register | OGL-v3 | BR-006 (future) | ⚠️ Consider |

**Open Data Publishing Opportunities**:

- Anonymised tenant-onboarding success metrics (no PII) could be published as part of GDS Service Standard transparency.
- Aggregate SIC distribution of UK SMEs adopting governance tooling — a public-good signal for the wider public sector.

**Common Data Standards Used**:

- Companies House Number for business entities (DR-001)
- UPRN / Postcode for property addresses (FR-001 / FR-013 via OS Data Hub / ONSPD)
- SIC codes for industry classification
- LEI for cross-border legal entities
- ISO country / currency codes for billing

**Data Ethics Framework Compliance**:

- [ ] Clear user need for data collection (BR-003 / FR-001 documented)
- [ ] Proportionate to the need (only fields required for SME verification retained)
- [ ] Lawful basis established (legitimate interests + contractual necessity)
- [ ] Data minimisation applied (officer PII pulled live where possible; not bulk-replicated)
- [ ] Transparency about data use (privacy notice referencing Companies House)
- [ ] Data quality maintained (annual re-verification + streaming delta)

---

## Requirements Traceability

### Full Mapping Table

| Requirement ID | Requirement Description | Data Source | Score | Status | Notes |
|----------------|------------------------|-------------|-------|--------|-------|
| BR-003 | SME Eligibility Verification | Companies House Public Data API (+ Streaming for delta refresh) | 73.0/100 | ✅ Matched | Authoritative for UK incorporated SMEs; pair with annual re-verification. |
| FR-001 | Tenant Provisioning + SME Verification | Companies House Public Data API; postcodes.io / OS Data Hub for address; SIC-1 for industry classification | 73.0/100 | ✅ Matched | Companies House outage path handled per FR-001 acceptance criteria. |
| FR-007 | SSO Integration (OIDC/SAML 2.0) | Microsoft Entra ID; Auth0 by Okta; Okta Workforce; GOV.UK One Login (for buying-authority sign-in) | 70.5/100 | ✅ Matched | Tenants bring their own IdP; ArcKit must federate against any of the shortlisted commercial IdPs. |
| FR-011 | Billing & Subscription Management (VAT-compliant invoicing) | HMRC VAT MTD API; BoE IADB (currency); ONS CPI (indexation review) | 67.0/100 | ✅ Matched | VAT validation gap (GAP-2) — add HMRC 'Check a UK VAT number' API in v1.1. |
| INT-001 | Tenant Identity Provider (SSO) | Microsoft Entra ID; Auth0; Okta | 70.5/100 | ✅ Matched | Federation only; ArcKit does not store IdP credentials. |
| INT-002 | Payment Processing (PCI-DSS-minimised) | — | — | ❌ Out of scope | Not a data source per se; researched separately under `/arckit:research`. |
| INT-003 | Companies House (UK SME Verification) | Companies House Public Data API | 73.0/100 | ✅ Matched | Direct match to INT-003 specification. |
| INT-004 | Email Delivery | — | — | ❌ Out of scope | Operational integration, not an external data source. |
| INT-005 | AI / LLM Endpoint | — | — | ❌ Out of scope | Technology dependency tracked via `/arckit:research` and ADRs. |
| INT-006 | Object Storage / Database | — | — | ❌ Out of scope | Infrastructure; tracked via `/arckit:aws-research` and `/arckit:azure-research`. |
| INT-007 | Observability Backend | — | — | ❌ Out of scope | Infrastructure. |
| INT-008 | G-Cloud / Digital Marketplace Listing | — | — | ❌ Out of scope | Procurement vehicle, not a data source. |
| INT-009 | Vulnerability Disclosure | — | — | ❌ Out of scope | Inbound channel. |
| NFR-SEC-001 | Authentication (incl. MFA) | Microsoft Entra ID; Auth0; Okta; GOV.UK One Login | 70.5/100 | ✅ Matched | MFA enforced by IdP; ArcKit consumes claims. |
| NFR-SEC-007 | Service-to-Service Authentication | — | — | ✅ Constraint | Architectural constraint; not satisfied by an external data source. |
| DR-001 | Tenant entity (Companies House number, residency_region) | Companies House Public Data API; postcodes.io; SIC-1 | 73.0/100 | ✅ Matched | |
| DR-002 | User entity (PII) | — | — | ✅ Internal | Internally generated; no external source. |
| DR-003 | Project entity | — | — | ✅ Internal | |
| DR-004 | Artefact entity | — | — | ✅ Internal | |
| DR-005 | Audit Event entity | — | — | ✅ Internal | |
| DR-006 | Subscription entity | — | — | ✅ Internal | Generated by FR-011 billing flow. |
| DR-007 | SME Verification Record | Companies House Public Data API (snapshot of response stored) | 73.0/100 | ✅ Matched | Snapshot retained for 7 years per audit requirement. |

### Coverage Summary

- ✅ **9 requirements (~41%)** have recommended data sources (matched)
- ✅ **6 requirements (~27%)** are internally generated (no external source needed)
- ✅ **1 requirement (~5%)** is an architectural constraint (NFR-SEC-007)
- ❌ **6 requirements (~27%)** are out of scope for DSCT (operational, infrastructure, procurement)
- ⚠️ **0 requirements (0%)** partially covered

---

## Next Steps

### Immediate Actions (0–2 weeks)

1. **Register for API access** for Companies House (Public Data + Streaming + Document) and OS Data Hub
2. **Begin HMRC MTD VAT OAuth2 production onboarding** (2–4 week lead time)
3. **Conduct integration POCs** for Companies House Public Data and Microsoft Entra ID (multi-tenant)
4. **Validate data quality** against FR-001 / DR-007 thresholds

### Data Model Updates (2–4 weeks)

5. **Update data model** (`/arckit.data-model`) with `SMEVerificationRecord`, `TenantCompanyProfile`, optional `LEIRecord`
6. **Create ADRs** (`/arckit.adr`) for: (a) Auth0 vs Okta Workforce choice; (b) sovereign-mode offline data plane (GAP-4); (c) FX provider deferral (GAP-3)
7. **DPIA review** (`/arckit.dpia`) for Companies House officer / PSC PII handling

### Gap Resolution (4–8 weeks)

8. **Address GAP-2** (VAT-number validation): add HMRC 'Check a UK VAT number' API in v1.1
9. **Address GAP-4** (sovereign mode, HIGH): pair every live API with an offline fallback bundle
10. **Decide on GAP-1** (PEP/sanctions): commission follow-up DSCT or commit to Yoti AML add-on

### Integration (Ongoing)

11. **Build data ingestion pipelines** per integration patterns above
12. **Implement caching** (TTL 24h on Companies House profile; TTL 7d on postcodes.io)
13. **Set up data quality monitoring** for freshness, completeness, rate-limit headroom
14. **Document data lineage** for audit (DR-005 Audit Event entity captures upstream source IDs)

---

## Appendices

### Appendix A: Research Methodology

**Data Sources Searched**:

- UK Government open data portals (data.gov.uk, ONS, NHS Digital, Companies House developer portal, HMRC developer hub, GDS)
- Commercial data provider websites (Microsoft Learn, Okta, Yoti, Onfido, GLEIF, OpenCorporates, Creditsafe, Dun & Bradstreet, Experian)
- G-Cloud Digital Marketplace (G-Cloud-14)
- API directories and documentation

**Evaluation Methodology**:

- Weighted scoring across 6 criteria (Requirements Fit 25%, Data Quality 20%, Licence & Cost 15%, API Quality 15%, Compliance 15%, Reliability 10%)
- Residency adjustment of +10 to the Licence & Cost component for sources with `hosted_in_iso_country = GB` (capped at component max 100)
- All scores based on verified information from official sources
- Pricing verified from vendor websites or G-Cloud listings

**Limitations**:

- Pricing based on published rates (volume discounts may be available)
- API quality assessed from documentation, not hands-on testing
- Data quality indicators from provider claims (validate during POC)
- Market evolves — discovery valid for approximately 6 months

### Appendix B: Glossary

- **API**: Application Programming Interface
- **ETL**: Extract, Transform, Load
- **OGL**: Open Government Licence
- **GDPR**: General Data Protection Regulation (UK GDPR / EU GDPR)
- **DPA 2018**: Data Protection Act 2018
- **TCoP**: Technology Code of Practice (UK Government)
- **SLA**: Service Level Agreement
- **TTL**: Time To Live (cache expiry)
- **UPRN**: Unique Property Reference Number
- **PII**: Personally Identifiable Information
- **LEI**: Legal Entity Identifier (GLEIF)
- **PSC**: Persons with Significant Control (Companies House)
- **MTD**: Making Tax Digital (HMRC)
- **ONSPD**: ONS Postcode Directory

## External References

> This section provides traceability from generated content back to source documents.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| CH-API-1 | — | — | company / uk-gov | https://developer-specs.company-information.service.gov.uk/ |
| CH-DOC-1 | — | — | company / uk-gov | https://developer-specs.company-information.service.gov.uk/ |
| CH-STREAM-1 | — | — | company / uk-gov | https://developer-specs.company-information.service.gov.uk/ |
| FCA-FSR-1 | — | — | company / uk-gov | https://www.fca.org.uk/firms/financial-services-register |
| DNB-GC14-1 | — | — | company / commercial | https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search?q=dun+bradstreet |
| CS-GC14-1 | — | — | company / commercial | https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search?q=creditsafe |
| EXP-GC14-1 | — | — | company / commercial | https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search?q=experian |
| GLEIF-API-1 | — | — | company / commercial | https://www.gleif.org/en/about/open-data |
| OC-API-1 | — | — | company / commercial | https://api.opencorporates.com/documentation/API-Reference |
| ONELOGIN-1 | — | — | identity / uk-gov | https://www.sign-in.service.gov.uk/about |
| ONELOGIN-DOCS-1 | — | — | identity / uk-gov | https://docs.sign-in.service.gov.uk/ |
| DVLA-API-1 | — | — | identity / uk-gov | https://developer-portal.driver-vehicle-licensing.api.gov.uk/availableapis.html |
| DVLA-PORTAL-1 | — | — | identity / uk-gov | https://developer-portal.driver-vehicle-licensing.api.gov.uk/ |
| DBS-1 | — | — | identity / uk-gov | https://www.gov.uk/government/organisations/disclosure-and-barring-service |
| ENTRA-1 | — | — | identity / commercial | https://learn.microsoft.com/en-us/entra/identity/ |
| AUTH0-1 | — | — | identity / commercial | https://security.okta.com/ |
| OKTA-1 | — | — | identity / commercial | https://security.okta.com/ |
| YOTI-1 | — | — | identity / commercial | https://www.yoti.com/business/identity-verification/ |
| ONFIDO-1 | — | — | identity / commercial | https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search?q=Onfido |
| HMRC-VAT-MTD-1 | — | — | financial / uk-gov | https://developer.service.hmrc.gov.uk/api-documentation/docs/authorisation |
| HMRC-DEV-HUB-1 | — | — | financial / uk-gov | https://developer.service.hmrc.gov.uk/api-documentation |
| BOE-IADB-1 | — | — | financial / uk-gov | https://www.bankofengland.co.uk/boeapps/database/ |
| ONS-CPI-1 | — | — | financial / uk-gov | https://www.ons.gov.uk/economy/inflationandpriceindices |
| POSTCODES-IO-1 | — | — | reference / free | https://postcodes.io/ |
| ONS-GEO-1 | — | — | reference / free | https://geoportal.statistics.gov.uk/ |
| ONSPD-1 | — | — | reference / free | https://www.ons.gov.uk/methodology/geography/licences |
| OS-API-1 | — | — | reference / free | https://api.os.uk/ |
| SIC-1 | — | — | reference / free | https://www.gov.uk/government/publications/standard-industrial-classification-of-economic-activities-sic |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit.datascout` agent
**Generated on**: 2026-05-06
**ArcKit Version**: 4.16.6
**Project**: ArcKit as a Service
**Model**: Claude Opus 4.7 (1M context)
