# Data Source Discovery: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.16.0 | **Command**: `/arckit:datascout`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-DSCT-v1.0 |
| **Document Type** | Data Source Discovery |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-06 |
| **Last Modified** | 2026-05-06 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-08-06 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, MOD Defence Digital liaison, NCSC liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-06 | ArcKit AI (datascout) | Initial creation from `/arckit:datascout` agent. Rubric: `uk-gov` (auto-detected from MOD/NCSC/JSP patterns in REQ + PRIN). Mode: legacy single-agent (`ajv` not installed at repo root). | [PENDING] | [PENDING] |

---

## Executive Summary

### Data Needs Overview

This document presents data source discovery findings for the **ArcKit as a Service (Sovereign Deployment)** project, identifying external APIs, datasets, and data portals that can fulfil the data and integration requirements documented in `ARC-002-REQ-v1.0.md`.

**Requirements Analyzed**: 7 data requirements (DR-001..007), 14 functional requirements (FR-007, FR-012, FR-014, etc.), 10 integration requirements (INT-001..010), 8 security non-functional requirements (NFR-SEC-001..008) plus compliance NFR-C-001/003.

**Data Source Categories Identified**: 3 categories based on requirement analysis.

**Discovery Approach**: UK Government open data first (api.gov.uk, data.gov.uk, NCSC publications, MOD gov.uk publications), then commercial / free supply-chain feeds for build-pipeline use, then build-time reference taxonomies. Deterministic UK-Gov rubric scoring (RF 25 / DQ 20 / L&C 15 / API 15 / Comp 15 / Rel 10).

> **Critical architectural framing — read first.** This project is a **sovereign / air-gapped deployment**. Per **Principle 21 / BR-002 / NFR-SEC-004 / TC-1**, the running system **MUST NOT** make any outbound network call to any endpoint outside the customer's accredited boundary. None of the sources discovered below are runtime data sources for the deployed system. All are vendor-side feeds across three lanes:
>
> - **Lane A — Vendor build / release-engineering** (outside customer boundary): SBOM augmentation, CVE alerting, LTS patch SLA tracking, accreditation evidence pack assembly.
> - **Lane B — Vendor pre-sales / commercial** (outside customer boundary): SME-tier eligibility verification (cross-subsidy basis), G-Cloud / DOS / FTS framework engagement.
> - **Lane C — Reference taxonomies** (consumed at vendor build time, baked into the bundle as static data): classification catalogue, WCAG ruleset, NCSC crypto guidance, JSP control catalogues.
>
> The bundle that crosses the air-gap MUST be self-contained. This is the most important finding of this discovery.

### Key Findings

- **Companies House Public Data API (Lane B, score 85.5)**: best fit for BR-006 SME-tier verification underpinning the cross-subsidy commercial model (links to project-001 BR-005). OGL-v3, GB-hosted.
- **GHSA + OSV.dev + NVD (Lane A, scores 84.0 / 79.75 / 73.0)**: triple-feed vulnerability stack for NFR-SEC-005 (SBOM integrity) and NFR-SEC-008 (Critical 7d / High 30d / Medium 90d patch SLAs). Two-of-three minimum to satisfy Principle 3 redundancy for the build pipeline.
- **NCSC CAF + MOD SbD + JSP guidance (Lane A, scores 67.5 / 65.75)**: lower deterministic score (annual/quarterly cadence) but **mandatory** in every per-release evidence pack regardless of total — read RF column, not total, for these.
- **Find a Tender + CCS Digital Marketplace (Lane B, scores 73.5 / 70.0)**: authoritative procurement signal for BR-007 framework engagement (above- and below-threshold).
- **HMG GSCP + NCSC Cryptographic Guidance + W3C WCAG / axe-core (Lane C, scores 63.75 / 67.5 / 61.45)**: build-time reference taxonomies baked into the bundle to enforce classification marking (FR-012), HMG-approved primitives (NFR-SEC-003), and accessibility (NFR-C-003).

### Data Source Summary

| Source Type | Count | Cost Range | Key Providers |
|-------------|-------|------------|---------------|
| **UK Government Open Data** | 10 | Free (OGL-v3) | Companies House, Cabinet Office (FTS, Contracts Finder, GSCP), CCS, NCSC (CAF, advisories, crypto guidance), MOD (SbD/JSP) |
| **Commercial APIs** | 0 | n/a | None required for this project (sovereign runtime forbids them; vendor-side needs met by free feeds) |
| **Free/Freemium APIs** | 5 | Free (rate-limited) | GitHub (GHSA), Google/OpenSSF (OSV.dev), NIST (NVD, CSRC), FIRST.org (EPSS) |
| **Open Source Datasets / Rulesets** | 1 | Free (Apache-2.0 / W3C licence) | W3C / Deque (WCAG + axe-core), IANA registries |
| **TOTAL** | 16 | £0/year | — |

### Top Recommended Sources

**Shortlist for integration**:

1. **Companies House Public Data API** for company/SME verification: OGL-v3, GB-hosted, daily refresh, 600/min — score **85.5/100**.
2. **GitHub Security Advisories (GHSA)** for vulnerability/SBOM: real-time, OAuth2, ISO27001+SOC2, CC-BY-4.0 — score **84.0/100**.
3. **OSV.dev** for vulnerability/SBOM (redundancy): hourly, free, > 6000 req/min, CC-BY-4.0 — score **79.75/100**.
4. **Find a Tender Service** for procurement framework engagement: OGL-v3, daily, GB-hosted — score **73.5/100**.
5. **NIST NVD CVE feed** for vulnerability cross-validation: hourly, broader CVSS coverage as backstop — score **73.0/100**.

### Requirements Coverage

- ✅ **22 requirements (78.6%)** fully matched to external data sources
- ⚠️ **5 requirements (17.9%)** partially matched (schema-only or partial coverage)
- ❌ **0 requirements (0%)** with no suitable external source — but **5 vendor-side process gaps** identified (none CRITICAL; all Lane A/B process matters)

---

## Data Needs Analysis

> **Note**: Data needs are extracted from `ARC-002-REQ-v1.0.md` and categorised by the lane they serve. Runtime needs INT-002..006 are **customer-controlled** by design and therefore have no external source.

### Extracted Data Needs

| # | Requirement ID | Data Need | Type | Criticality | Volume | Freshness | Source Category | Lane |
|---|----------------|-----------|------|-------------|--------|-----------|-----------------|------|
| 1 | BR-006 | SME-tier eligibility (cross-subsidy basis) | Business | MUST | ~10–50 lookups/day | Daily | Company / procurement | B |
| 2 | BR-007 | Procurement framework engagement intelligence | Business | SHOULD | Daily monitoring | Daily | Company / procurement | B |
| 3 | BR-004 | Per-release accreditation evidence pack | Business | MUST | Per LTS release (~2/year) | Annual / on-revision | Cybersecurity reference | A |
| 4 | BR-005 | LTS patch tracking | Business | MUST | Per release + ongoing | Real-time | Vulnerability feeds | A |
| 5 | FR-012 | Classification marking | Functional | MUST | Build-time embedded | Annual | Classification reference | C |
| 6 | FR-014 | LTS patch delivery | Functional | MUST | 7d / 30d / 90d SLA | Real-time | Vulnerability feeds | A |
| 7 | INT-001 | Customer IdP integration schemas | Integration | MUST | Schema only | Ad-hoc | Identity reference | C |
| 8 | INT-007 | Customer KMS — HMG-approved primitive allow-list | Integration | MUST | Build-time embedded | Annual | Crypto reference | C |
| 9 | INT-008 | G-Cloud / DOS / Defence framework listings | Integration | SHOULD | Daily | Daily | Procurement | B |
| 10 | INT-010 | Inbound vulnerability disclosure channel | Integration | MUST | Real-time monitoring | Real-time | Vulnerability feeds | A |
| 11 | NFR-SEC-001 | MOD SbD / JSP 440 / JSP 604 alignment | Security NFR | MUST | Per release | Quarterly | Accreditation reference | A |
| 12 | NFR-SEC-002 | NCSC CAF v3.x mapping | Security NFR | MUST | Per release | Annual | Accreditation reference | A |
| 13 | NFR-SEC-003 | HMG-approved cryptography | Security NFR | MUST | Build-time enforced | Annual | Crypto reference | C |
| 14 | NFR-SEC-005 | Supply-chain integrity / SBOM | Security NFR | MUST | Per build | Real-time | Vulnerability feeds | A |
| 15 | NFR-SEC-008 | Patch SLA evidence | Security NFR | MUST | Per release | Real-time | Vulnerability feeds | A |
| 16 | NFR-C-001 | Classification policy enforcement | Compliance NFR | MUST | Build-time embedded | Annual | Classification reference | C |
| 17 | NFR-C-003 | WCAG 2.2 AA | Compliance NFR | MUST | Per CI build | Quarterly | A11y reference | C |
| 18 | DR-001..006 | Internal datatypes (project content, deployment, audit) | Data | MUST | — | — | Internal — no external feed | — |
| 19 | DR-007 | SBOM / release manifest CVE enrichment | Data | MUST | Per build | Real-time | Vulnerability feeds | A |

### Data Needs by Category

**Category 1: Company / Procurement (Lane B — vendor pre-sales)**

- Requirements: BR-006, BR-007, INT-008
- Data fields needed: company number, SME status, director PII (limited), accounts, framework listings, contract notices, supplier metadata
- Volume: 10–50 SME lookups/day; daily monitoring of FTS/CCS feeds
- Freshness: Daily
- Quality threshold: authoritative source required (Companies House for SME flag); 100% completeness for SME field

**Category 2: Cybersecurity / Vulnerability / Accreditation (Lane A — vendor build)**

- Requirements: BR-004, BR-005, FR-014, INT-010, NFR-SEC-001, NFR-SEC-002, NFR-SEC-005, NFR-SEC-008, DR-007
- Data fields needed: CVE id, CVSS v3.1/v4, EPSS, advisory text, OSV records, NCSC CAF outcomes, MOD SbD principles, JSP 440/604 control catalogue
- Volume: real-time CVE alerting on ~500 SBOM components; quarterly accreditation pack assembly
- Freshness: real-time (CVE feeds), quarterly (MOD), annual (NCSC CAF / JSP revisions)
- Quality threshold: ≥ 99% recall on Critical CVEs (justifies dual-feed: GHSA + OSV minimum)

**Category 3: Classification / A11y / Cryptography / Identity (Lane C — build-time reference)**

- Requirements: FR-007, FR-012, INT-001, INT-007, NFR-SEC-003, NFR-C-001, NFR-C-003
- Data fields needed: HMG GSCP categories + handling caveats; WCAG 2.2 success criteria + axe-core ruleset; HMG-approved cryptographic primitive list; OIDC/SAML claim registries
- Volume: static reference, embedded once per release
- Freshness: annual (NCSC, GSCP, JSPs); quarterly (axe-core)
- Quality threshold: 100% — these are normative references baked into the bundle

---

## Data Source Discovery

> **Note**: Categories are dynamically identified from project requirements, not a fixed list. Three categories were generated; categories with no relevant requirements (geospatial, financial markets, demographics, weather, health, transport, energy, education, property, crime, KYC/identity-verification) are deliberately excluded — they are **not gaps**.

---

## Category 1: Company / Procurement (Lane B — vendor pre-sales / commercial)

**Requirements Addressed**: BR-006, BR-007, INT-008

**Why This Category**: BR-006 establishes a tiered cross-subsidy commercial model that requires authoritative SME-status verification of customers. BR-007 and INT-008 require vendor-side awareness of UK government procurement signals to engage frameworks (G-Cloud, DOS, Find a Tender, Defence-specific frameworks).

**Data Fields Needed**: company number; SME flag (inferred from accounts thresholds); registered office; SIC code; active filings; director list (PII); CCS framework listings; FTS contract notices.

---

### Source 1A: Companies House Public Data API (UK Gov Open Data)

**Provider**: UK Government / Companies House. URL: `https://api.company-information.service.gov.uk/`

**Description**: Authoritative UK source for company registration, filings, accounts, and directors. Real-time API + bulk product. Used to derive SME status from accounts size thresholds.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free |
| **Format** | JSON (REST) + CSV/XML bulk |
| **API Endpoint** | `https://api.company-information.service.gov.uk/` |
| **Authentication** | API Key |
| **Rate Limits** | ~600 requests / 5 minutes (public quota) |
| **Update Frequency** | Daily |
| **Coverage** | UK-wide (England, Wales, Scotland, NI) |
| **Temporal Coverage** | Live + historical filings |
| **Data Quality** | Authoritative source; high completeness on SME flag |
| **Documentation** | Excellent — `developer-specs.company-information.service.gov.uk` |
| **SLA** | Best-effort; not contractual |
| **GDPR Status** | Contains director PII — Article 6(1)(c)/(e) lawful basis available; minimisation required |
| **UK Data Residency** | Yes (GB-hosted) |

**Requirements Fit**:

- ✅ Covers: company registration, SME-determining account fields, director identity for diligence
- ❌ Missing: customer's internal classification (out of scope)
- ⚠️ Partial: PSC (people with significant control) data has known under-reporting — flag in DPIA

**Integration Approach**:

- **Pattern**: REST API call on demand, cached 24h
- **Estimated Effort**: 2 person-days (Lane B vendor tooling, not deployed system)
- **Dependencies**: free API key registration; documented sub-processor agreement if customer asks

**Evaluation Score** (uk-gov rubric):

| Criterion | Weight | Score | Weighted |
|-----------|--------|-------|----------|
| Requirements Fit | 25% | 100 | 25.0 |
| Data Quality | 20% | 80 | 16.0 |
| License & Cost | 15% | 100 | 15.0 |
| API Quality | 15% | 80 | 12.0 |
| Compliance | 15% | 70 | 10.5 |
| Reliability | 10% | 70 | 7.0 |
| **Total** | **100%** | | **85.5/100** |

---

### Source 1B: CCS Digital Marketplace — G-Cloud catalogue (UK Gov Open Data)

**Provider**: Crown Commercial Service. URL: `https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search` (browse) and bulk via `data.gov.uk`

**Description**: Catalogue of services published by suppliers on G-Cloud and DOS frameworks; bulk dataset on data.gov.uk.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free |
| **Format** | CSV / JSON (bulk) |
| **API Endpoint** | bulk via data.gov.uk; search via web UI |
| **Authentication** | None (public) |
| **Rate Limits** | n/a (bulk) |
| **Update Frequency** | Monthly (catalogue refresh) |
| **Coverage** | UK Government suppliers |
| **GDPR Status** | No personal data |
| **UK Data Residency** | Yes |

**Requirements Fit**: ✅ Covers competitor and own listings on G-Cloud (BR-007, INT-008). ❌ Does not cover Defence-specific frameworks.

**Evaluation Score**: RF 90, DQ 40, L&C 100, API 70, Comp 60, Rel 50 → **70.0/100**

---

### Source 1C: Find a Tender Service (UK Gov Open Data)

**Provider**: Cabinet Office. URL: `https://www.find-tender.service.gov.uk/`

**Description**: UK successor to OJEU; daily stream of above-threshold public-sector contract notices.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | Open Government Licence v3.0 |
| **Pricing** | Free |
| **Format** | JSON / XML notices |
| **Authentication** | None (read) / API key (downloads) |
| **Update Frequency** | Daily |
| **Coverage** | UK-wide above-threshold notices |
| **UK Data Residency** | Yes |

**Evaluation Score**: RF 75, DQ 80, L&C 100, API 80, Comp 45, Rel 50 → **73.5/100**

---

### Source 1D: Contracts Finder (UK Gov Open Data)

**Provider**: Cabinet Office. URL: `https://www.contractsfinder.service.gov.uk/`

**Description**: Below-threshold contract notices (£10k–threshold range).

**Evaluation Score**: RF 60, DQ 80, L&C 100, API 70, Comp 35, Rel 50 → **66.75/100**

---

### Comparison Table: Company / Procurement

| Criterion | Companies House | CCS Marketplace | Find a Tender | Contracts Finder |
|-----------|-----------------|-----------------|---------------|------------------|
| **Provider** | Companies House | CCS | Cabinet Office | Cabinet Office |
| **License** | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 |
| **Cost (Annual)** | £0 | £0 | £0 | £0 |
| **Coverage** | UK-wide | UK Gov suppliers | UK above-threshold | UK below-threshold |
| **Freshness** | Daily | Monthly | Daily | Daily |
| **API Quality** | Good | Fair | Good | Fair |
| **Requirements Fit** | 25 | 22.5 | 18.75 | 15 |
| **Data Quality** | 16 | 8 | 16 | 16 |
| **License & Cost** | 15 | 15 | 15 | 15 |
| **API Quality** | 12 | 10.5 | 12 | 10.5 |
| **Compliance** | 10.5 | 9 | 6.75 | 5.25 |
| **Reliability** | 7 | 5 | 5 | 5 |
| **TOTAL SCORE** | **85.5** | **70.0** | **73.5** | **66.75** |

**Recommendation for Category 1**: **Companies House** for BR-006 (authoritative SME verification). **Find a Tender + CCS Marketplace** as a pair for BR-007/INT-008 (above- and below-threshold + framework supplier listings). Contracts Finder is a useful tertiary signal but not load-bearing.

---

## Category 2: Cybersecurity / Vulnerability / Accreditation (Lane A — vendor build)

**Requirements Addressed**: BR-004, BR-005, FR-014, INT-010, NFR-SEC-001, NFR-SEC-002, NFR-SEC-005, NFR-SEC-008, DR-007

**Why This Category**: Per-release evidence packs (BR-004) require currency on NCSC CAF outcomes and MOD SbD/JSP control catalogues. Patch SLAs (NFR-SEC-008) and SBOM integrity (NFR-SEC-005) require near real-time CVE intelligence on ~500 dependencies. INT-010 inbound vulnerability disclosure is fed primarily by NCSC + GHSA.

---

### Source 2A: NCSC Cyber Assessment Framework v3.x (UK Gov Open Data)

**Provider**: NCSC. URL: `https://www.ncsc.gov.uk/collection/cyber-assessment-framework`

**Description**: Authoritative outcome-based control framework adopted across HMG for cyber assurance.

**Evaluation Score**: RF 100, DQ 15, L&C 100, API 70, Comp 60, Rel 50 → **67.5/100**

> **Read RF, not total.** Annual cadence drags total down, but RF is 100 and this is a mandatory input to the per-release evidence pack.

---

### Source 2B: MOD Secure by Design + JSP guidance (UK Gov Open Data)

**Provider**: MOD Defence Digital. URL: `https://www.gov.uk/government/publications/secure-by-design` (and DCPP / JSP 440 / JSP 604 references via gov.uk).

**Description**: MOD's outcome-based security assessment approach plus the JSP control catalogues used for accreditation evidence.

**Evaluation Score**: RF 100, DQ 25, L&C 100, API 70, Comp 35, Rel 50 → **65.75/100**

---

### Source 2C: NIST NVD CVE feed (Free API, US-hosted)

**Provider**: NIST CSRC. URL: `https://services.nvd.nist.gov/rest/json/cves/2.0`

**Description**: Authoritative US-side CVE database with CVSS v3.1/v4 base scores. Backstop / cross-validation for GHSA + OSV.

**Evaluation Score**: RF 90, DQ 90, L&C 55 (US residency −5), API 80, Comp 35, Rel 70 → **73.0/100**

---

### Source 2D: OSV.dev (Free API, US-hosted)

**Provider**: Google / Open Source Security Foundation. URL: `https://api.osv.dev/v1/query`

**Description**: High-throughput open-source vulnerability database optimised for SBOM lookups.

**Evaluation Score**: RF 90, DQ 90, L&C 85, API 70, Comp 40, Rel 100 → **79.75/100**

---

### Source 2E: GitHub Security Advisories (Free API, US-hosted)

**Provider**: GitHub Inc. URL: `https://api.github.com/graphql` (securityAdvisories) + `https://github.com/advisories`

**Description**: GitHub-curated advisory database with strong ecosystem coverage and real-time updates.

**Evaluation Score**: RF 90, DQ 100, L&C 85, API 90, Comp 55, Rel 70 → **84.0/100**

---

### Source 2F: FIRST.org EPSS (Free API, US-hosted)

**Provider**: FIRST. URL: `https://api.first.org/data/v1/epss`

**Description**: Exploit Prediction Scoring System — daily probability that a CVE will be exploited in the next 30 days. Right-sizes patch prioritisation under NFR-SEC-008.

**Evaluation Score**: RF 70, DQ 80, L&C 85, API 70, Comp 35, Rel 50 → **67.0/100**

---

### Source 2G: NCSC Vulnerability Advisories (UK Gov Open Data)

**Provider**: NCSC. URL: `https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports`

**Description**: NCSC-published threat reports and vendor advisories — primary inbound disclosure channel for INT-010.

**Evaluation Score**: RF 70, DQ 60, L&C 100, API 70, Comp 60, Rel 50 → **69.0/100**

---

### Comparison Table: Cybersecurity / Vulnerability / Accreditation

| Source | RF | DQ | L&C | API | Comp | Rel | Total | Role |
|--------|----|----|-----|-----|------|-----|-------|------|
| GHSA | 22.5 | 20 | 12.75 | 13.5 | 8.25 | 7 | **84.0** | Primary CVE feed |
| OSV.dev | 22.5 | 18 | 12.75 | 10.5 | 6 | 10 | **79.75** | Redundancy CVE feed |
| NIST NVD | 22.5 | 18 | 8.25 | 12 | 5.25 | 7 | **73.0** | Cross-validation backstop |
| NCSC Advisories | 17.5 | 12 | 15 | 10.5 | 9 | 5 | **69.0** | UK-side INT-010 inbound |
| NCSC CAF | 25 | 3 | 15 | 10.5 | 9 | 5 | **67.5** | Mandatory evidence input |
| FIRST EPSS | 17.5 | 16 | 12.75 | 10.5 | 5.25 | 5 | **67.0** | Patch prioritisation |
| MOD SbD / JSP | 25 | 5 | 15 | 10.5 | 5.25 | 5 | **65.75** | Mandatory evidence input |

**Recommendation for Category 2**: **Pair GHSA + OSV.dev** as primary CVE feeds (Principle 3 redundancy); **NIST NVD** as cross-validation; **EPSS** to weight prioritisation. **NCSC CAF + MOD SbD + JSP** are non-substitutable accreditation inputs regardless of score. **NCSC Advisories** is the canonical UK channel for INT-010.

---

## Category 3: Classification / Accessibility / Cryptography / Identity (Lane C — build-time reference)

**Requirements Addressed**: FR-007, FR-012, INT-001, INT-007, NFR-SEC-003, NFR-C-001, NFR-C-003

**Why This Category**: These taxonomies are normative references that get embedded in the bundle as static data so they apply inside the customer's accredited boundary without any outbound call.

---

### Source 3A: HMG Government Security Classifications Policy (UK Gov Open Data)

**Provider**: Cabinet Office. URL: `https://www.gov.uk/government/publications/government-security-classifications`

**Evaluation Score**: RF 100, DQ 15, L&C 100, API 70, Comp 35, Rel 50 → **63.75/100**

---

### Source 3B: W3C WCAG 2.2 + axe-core ruleset (Open Source)

**Provider**: W3C / Deque. URL: `https://www.w3.org/TR/WCAG22/` and `https://github.com/dequelabs/axe-core`

**Evaluation Score**: RF 90, DQ 25, L&C 83, API 70, Comp 40, Rel 50 → **61.45/100**

---

### Source 3C: NIST CSRC Cryptographic Catalogues (Free API, US-hosted)

**Provider**: NIST. URL: `https://csrc.nist.gov/publications`

**Evaluation Score**: RF 80, DQ 15, L&C 55, API 70, Comp 25, Rel 50 → **50.5/100**

> Superseded by NCSC guidance for HMG mandates — kept for cross-reference only.

---

### Source 3D: NCSC Cryptographic Guidance (UK Gov Open Data)

**Provider**: NCSC. URL: `https://www.ncsc.gov.uk/collection/topics/cryptography`

**Evaluation Score**: RF 100, DQ 15, L&C 100, API 70, Comp 60, Rel 50 → **67.5/100**

> **Authoritative for NFR-SEC-003** — UK-Gov override of NIST for HMG.

---

### Source 3E: IANA OIDC/SAML Registries (Open Source)

**Provider**: IANA / OpenID Foundation. URL: `https://www.iana.org/assignments/oauth-parameters`

**Evaluation Score**: RF 60, DQ 30, L&C 55, API 70, Comp 25, Rel 50 → **48.5/100**

---

### Comparison Table: Classification / A11y / Cryptography / Identity

| Source | Total | Role |
|--------|-------|------|
| NCSC Cryptographic Guidance | **67.5** | NFR-SEC-003 — authoritative |
| HMG GSCP | **63.75** | FR-012 / NFR-C-001 — authoritative |
| W3C WCAG / axe-core | **61.45** | NFR-C-003 — CI ruleset |
| NIST CSRC | **50.5** | Cross-reference only |
| IANA OIDC/SAML | **48.5** | Schema reference for INT-001 |

**Recommendation for Category 3**: All five embedded into the bundle as build-time reference. NCSC overrides NIST for HMG-approved primitives. IANA provides schema only; runtime IdP integration is customer-controlled.

---

## Evaluation Matrix

### Overall Scoring Summary

| Category | Recommended Source(s) | Type | Score | Annual Cost | Integration Effort |
|----------|----------------------|------|-------|-------------|-------------------|
| 1. Company / Procurement | Companies House (primary) + FTS + CCS Marketplace | UK-Gov Open | 85.5 / 73.5 / 70.0 | £0 | 4 days (Lane B tooling) |
| 2. Vulnerability / Accreditation | GHSA + OSV.dev + NVD + EPSS + NCSC CAF + MOD SbD + NCSC Advisories | Free API + UK-Gov Open | 84.0 / 79.75 / 73.0 / 67.0 / 67.5 / 65.75 / 69.0 | £0 | 8 days (Lane A pipeline) |
| 3. Classification / A11y / Crypto | HMG GSCP + WCAG/axe-core + NCSC Crypto + IANA | UK-Gov Open + OSS | 63.75 / 61.45 / 67.5 / 48.5 | £0 | 3 days (build-time embed) |
| **TOTAL** | | | **Avg: 70.4** | **£0/year** | **15 days** |

### Evaluation Criteria Explained

| Criterion | Weight | What It Measures |
|-----------|--------|-----------------|
| **Requirements Fit** | 25% | Coverage of needed fields against the requirement |
| **Data Quality** | 20% | Refresh cadence, completeness, accuracy |
| **License & Cost** | 15% | OGL/CC/proprietary terms, cost; UK-Gov rubric applies +10 GB residency / −5 non-GB |
| **API Quality** | 15% | Authentication method, documentation, versioning |
| **Compliance** | 15% | OGL-v3, GDPR, ISO27001, SOC2, NCSC-CAF, G-Cloud listing bonuses |
| **Reliability** | 10% | Rate limit headroom, vendor stability |

---

## Data Integration Architecture

### Integration Patterns by Source

| Source | Lane | Pattern | Auth | Caching | Error Handling | Monitoring |
|--------|------|---------|------|---------|----------------|------------|
| Companies House | B | REST on-demand | API Key | TTL 24h | Retry 3x + circuit breaker | Health check + DPA log |
| GHSA | A | GraphQL polling (build pipeline) | OAuth2 | TTL 1h | Retry 5x; degrade to OSV+NVD | Health check |
| OSV.dev | A | REST polling | None | TTL 1h | Degrade to GHSA+NVD | Health check |
| NIST NVD | A | REST polling | API Key | TTL 6h | Tertiary backstop | Health check |
| FIRST EPSS | A | Daily CSV pull | None | TTL 24h | Skip if down (non-critical) | Daily success metric |
| NCSC sites | A | RSS/web watcher | None | TTL 24h | Manual review on miss | Weekly digest |
| FTS / CCS / Contracts Finder | B | Bulk pull | None / API Key | TTL 24h | Skip if down (non-critical) | Daily success metric |
| HMG GSCP / NCSC Crypto / WCAG / IANA | C | One-shot at release time | None | Embedded in bundle | Build-time validator | Per-release diff log |

### Recommended Integration Architecture

```text
LANE A (vendor build / release engineering — outside customer boundary)
  CVE feeds (GHSA primary, OSV redundancy, NVD backstop)
       │
       ▼
  SBOM × CVE matcher  +  EPSS prioritisation
       │
       ▼
  Per-release evidence pack assembler
       ├── NCSC CAF mapping
       ├── MOD SbD / JSP control mapping
       └── Patch SLA evidence
       │
       ▼
  Signed release bundle (no outbound deps at runtime) ─► customer air-gap

LANE B (vendor pre-sales — outside customer boundary)
  Companies House (SME flag) ─► tier-eligibility decision
  FTS + CCS Marketplace + Contracts Finder ─► procurement signal pipeline

LANE C (build-time embed — bundled, no runtime fetch)
  HMG GSCP ─┐
  NCSC Crypto ─┤
  WCAG + axe-core ─┼──► snapshot frozen into release bundle ──► runs inside customer boundary
  IANA registries ─┘
```

### Authentication and Access

| Source | Auth Method | Credentials | Registration | Lead Time |
|--------|-------------|-------------|--------------|-----------|
| Companies House | API Key | Free key | Self-service portal | Instant |
| GHSA | OAuth2 / PAT | GitHub PAT | GitHub account | Instant |
| OSV.dev | None | n/a | n/a | n/a |
| NIST NVD | API Key (recommended) | NIST key | Self-service | 1 day |
| FIRST EPSS | None | n/a | n/a | n/a |
| FTS | API Key (downloads) | Free key | gov.uk login | Instant |
| All NCSC / MOD / Cabinet Office sites | None (fetch + RSS) | n/a | n/a | n/a |

### Rate Limits and Capacity Planning

| Source | Rate Limit | Projected Usage | Headroom | Upgrade |
|--------|------------|-----------------|----------|---------|
| Companies House | ~600 / 5min | ~50 / day | > 99% | n/a |
| GHSA | 5000/h authed | ~1000/build × 4 builds/day = 4000/day | > 99% | Enterprise quota |
| OSV.dev | > 6000/min | ~500/build | > 99% | n/a |
| NIST NVD | 50/30s with key | ~100/build | ~ 50% | n/a |

---

## Data Utility Analysis

> **Note**: Most sources have valuable secondary uses. Identifying them increases the strategic value of vendor-side data ingestion.

### Utility by Source

| Source | Primary Use | Secondary Uses | Strategic Value | Combination Opportunities |
|--------|-------------|----------------|-----------------|--------------------------|
| Companies House | BR-006 SME tier verification | (1) director conflict-of-interest scan for staff onboarding to MOD engagements; (2) supplier/sub-processor diligence | HIGH | + CCS Marketplace ─► automated SME-tier eligibility + competitor mapping |
| GHSA + OSV.dev | NFR-SEC-005/008 CVE alerting | (1) weekly LTS-line risk dashboards for accreditators; (2) trend reports for R-3 (offline-incompatible deps) | HIGH | + EPSS ─► exploit-prediction-weighted prioritisation that right-sizes the 7/30/90d SLAs |
| NIST NVD | Cross-validation | CVSS v3.1 / v4 normalisation across feeds | MEDIUM | + CISA KEV (informational) for US-side validation trail |
| FTS + Contracts Finder | BR-007 framework engagement | (1) competitor sovereign-EA bid intelligence; (2) pricing evidence for SOBC iteration | MEDIUM | + CCS Marketplace ─► end-to-end procurement signal pipeline |
| NCSC CAF + MOD SbD | Per-release evidence pack | (1) vendor staff training material; (2) gap analysis on R-2 (accreditation effort variance) | HIGH | + GSCP + NCSC Crypto ─► unified "UK sensitive-site control catalogue" baked into bundle |
| HMG GSCP | FR-012 marking | (1) edit-time marking enforcement; (2) export-time classification banner | HIGH | + customer maximum-classification config ─► automatic per-deployment validation rules |
| WCAG / axe-core | NFR-C-003 a11y CI | A11y Statement auto-generation per release | MEDIUM | Standalone |
| NCSC Cryptographic Guidance | NFR-SEC-003 enforcement | (1) bundle-time crypto-config validator; (2) KMS allow-list at INT-007 | HIGH | + customer KMS metadata at install ─► in-boundary primitive enforcement |

### Common Secondary Use Patterns Identified

| Pattern | Source | Primary Use | Secondary Use | Value |
|---------|--------|-------------|---------------|-------|
| **Proxy Indicator** | EPSS | exploit probability | proxy for "should accreditator escalate?" — Critical-SLA quality metric | Accreditator confidence |
| **Cross-Domain Enrichment** | Companies House | SME flag | enriches due-diligence on sub-processors used by vendor | Supply-chain trust |
| **Trend Detection** | GHSA + OSV | Per-build CVE delta | reveals whether dependency-base health is improving or drifting | Predicts R-3 materialisation |
| **Predictive Feature** | EPSS | Patch prioritisation | feature for forecasting backlog burn-down | Release-planning input |

### Data Combination Opportunities

1. **SME-tier + Procurement Signal**: Companies House + FTS + CCS Marketplace ─► automated SME-tier eligibility decision *and* opportunity matching for tier-targeted outreach.
2. **CVE × EPSS × SBOM**: GHSA + OSV + EPSS + internal SBOM ─► 30-day exploit-prediction-weighted patch backlog driving NFR-SEC-008 7/30/90 SLAs.
3. **UK Sensitive-Site Control Catalogue**: NCSC CAF + MOD SbD + JSP + GSCP + NCSC Crypto ─► single bundled reference set that drives both build-time validators and per-release accreditation evidence packs — same source-of-truth, two consumers.

---

## Gap Analysis

### Requirements Without Suitable Data Sources

**GAP-1**: BR-007 / A-1 — DCPP Cyber Risk Profile per engagement

- **Data Need**: Per-engagement risk profile issued by MOD DCPP
- **Why No Source**: Issued per-engagement to the supplier; not openly published
- **Impact**: Vendor cannot pre-compute response; must wait for engagement-time issue
- **Severity**: HIGH (process gap; not runtime gap)
- **Recommended Action**: Templated intake form, escalate via MOD framework owner relationship; track per-engagement
- **Estimated Effort**: 2 person-days for intake form + workflow
- **Cost Estimate**: £0

**GAP-2**: NFR-SEC-003 — HMG-approved cryptographic primitive registry (machine-readable)

- **Data Need**: Authoritative list of HMG-approved primitives in machine-readable form
- **Why No Source**: NCSC publishes guidance as PDF/HTML, not as a registry feed
- **Impact**: Cannot fully automate crypto-config validator from a live source
- **Severity**: MEDIUM
- **Recommended Action**: Maintain internal versioned `crypto-allow-list.yaml`, refresh annually against NCSC publications as part of LTS evidence pack
- **Estimated Effort**: 3 person-days initial + 1 day/year refresh
- **Cost Estimate**: £0

**GAP-3**: BR-004 / NFR-SEC-001 — JSP 440 / JSP 604 control catalogue (machine-readable)

- **Data Need**: Structured JSP control catalogue
- **Why No Source**: Issued as PDF annexes; no public structured feed
- **Impact**: Manual mapping required per LTS issue; revisions risk drift
- **Severity**: MEDIUM
- **Recommended Action**: Maintain release-pinned internal mapping file with change-log diff per LTS issue
- **Estimated Effort**: 5 person-days initial + 2 days per LTS
- **Cost Estimate**: £0

**GAP-4**: DR-002 / NFR-SEC-007 — UK personnel-clearance taxonomy

- **Data Need**: SC / DV / NPPV3 / etc. taxonomy
- **Why No Source**: Policy-defined, not published as a registry
- **Impact**: Schema must be hard-coded
- **Severity**: LOW (taxonomy stable; rarely changes)
- **Recommended Action**: Hard-code documented taxonomy; surface via customer IdP claim mapping
- **Estimated Effort**: 1 person-day
- **Cost Estimate**: £0

**GAP-5**: INT-008 — Defence-specific framework listings

- **Data Need**: Listings on DSP / Defence Crown frameworks beyond G-Cloud / DOS
- **Why No Source**: Often gated behind defence-customer access
- **Impact**: Vendor relies on relationship-based visibility
- **Severity**: MEDIUM (commercial gap, not technical)
- **Recommended Action**: Vendor-side relationship engagement with MOD framework owners; private deal-pipeline log
- **Estimated Effort**: Ongoing commercial activity
- **Cost Estimate**: BAU sales effort

### Gap Summary

| Gap | Requirement | Severity | Recommended Action | Effort | Cost |
|-----|-------------|----------|-------------------|--------|------|
| GAP-1 | BR-007 | HIGH | Engagement intake form | 2 d | £0 |
| GAP-2 | NFR-SEC-003 | MEDIUM | Internal crypto allow-list | 3 d + 1 d/yr | £0 |
| GAP-3 | BR-004 / NFR-SEC-001 | MEDIUM | Internal JSP mapping file | 5 d + 2 d/LTS | £0 |
| GAP-4 | NFR-SEC-007 | LOW | Hard-code taxonomy | 1 d | £0 |
| GAP-5 | INT-008 | MEDIUM | Relationship engagement | Ongoing | BAU |

**Severity rule applied**: CRITICAL is reserved for runtime-blocking gaps. Per Principle 21 the runtime data-source surface is empty by design; therefore no gap here is CRITICAL — they are all vendor-side process matters.

---

## Recommendations & Shortlist

### Top 5 Recommended Sources

#### 1. Companies House Public Data API for SME Verification (Lane B)

**Overall Score**: **85.5/100**

**Rationale**: Authoritative UK source for company status; the only source that can definitively determine SME flag for the BR-006 cross-subsidy tiering. OGL-v3, GB-hosted, daily-refreshed.

**Key Strengths**:

- ✅ Authoritative — no substitute exists
- ✅ OGL-v3 + free + GB-hosted (best possible posture)
- ✅ Daily refresh sufficient for monthly tier reviews

**Key Concerns**:

- ⚠️ Director PII triggers DPIA review — confirm Article 6(1)(c)/(e) lawful basis
- ⚠️ PSC under-reporting — flag in DPIA

**Cost**: Free | **Integration Effort**: 2 person-days | **Risk Level**: LOW

**Next Steps**:

- [ ] Register API key
- [ ] Run DPIA increment for director-PII processing (vendor-side)
- [ ] POC SME-flag determination logic against threshold rules (1 day)

---

#### 2. GitHub Security Advisories (GHSA) for Vulnerability Feed (Lane A)

**Overall Score**: **84.0/100**

**Rationale**: Real-time, ecosystem-aware, OAuth2-authed, ISO27001+SOC2 — the strongest single feed for NFR-SEC-008 patch SLAs and DR-007 SBOM enrichment.

**Key Strengths**:

- ✅ Real-time updates
- ✅ OAuth2 + strong rate limits (5000/h authed)
- ✅ Excellent ecosystem coverage (npm, PyPI, Maven, etc.)

**Key Concerns**:

- ⚠️ US-hosted (−5 in residency under uk-gov rubric, but Lane A so not runtime)
- ⚠️ Single-vendor concentration risk — mitigated by pairing with OSV.dev

**Cost**: Free | **Integration Effort**: 3 person-days | **Risk Level**: LOW

**Next Steps**:

- [ ] Provision GitHub PAT in build pipeline
- [ ] Wire into SBOM × CVE matcher
- [ ] Feed into per-release evidence pack assembler

---

#### 3. OSV.dev for SBOM Vulnerability Coverage (Lane A — redundancy)

**Overall Score**: **79.75/100**

**Rationale**: Provides Principle 3 redundancy for GHSA. Highest throughput of any free feed (> 6000/min). CC-BY-4.0 + free.

**Key Strengths**: ✅ No auth, no rate cost; ✅ Different curation lineage from GHSA so genuine redundancy.

**Cost**: Free | **Integration Effort**: 2 person-days | **Risk Level**: LOW

**Next Steps**:

- [ ] Implement parallel query against OSV alongside GHSA
- [ ] Difference-report job for divergent verdicts

---

#### 4. Find a Tender Service for Procurement Signals (Lane B)

**Overall Score**: **73.5/100**

**Rationale**: Authoritative, daily, OGL-v3 source for above-threshold MOD/HMG opportunities — the canonical input to BR-007 framework engagement.

**Cost**: Free | **Integration Effort**: 2 person-days | **Risk Level**: LOW

**Next Steps**:

- [ ] Register FTS download key
- [ ] Daily ingest into vendor opportunity log

---

#### 5. NIST NVD CVE Feed for Cross-Validation (Lane A)

**Overall Score**: **73.0/100**

**Rationale**: Independent backstop for GHSA + OSV with broader CVSS v3.1/v4 coverage. Used to detect drift between the two primary feeds.

**Cost**: Free | **Integration Effort**: 1 person-day | **Risk Level**: LOW

**Next Steps**:

- [ ] Provision NVD API key
- [ ] Wire into difference-report job

---

## Impact on Data Model

> **Note**: An `ARC-002-DATA-*.md` artefact does not yet exist for this project. Findings below indicate the additions a future data model should include for **vendor-side tooling only** — no entities are added to the deployed sovereign system.

### New Entities from External Sources (Vendor-Side Only)

| Entity | Source | Description | Key Attributes | Sync Strategy | Lane |
|--------|--------|-------------|----------------|---------------|------|
| `ProspectCompany` | Companies House | Vendor CRM extension for tier-eligibility | company_number, sme_flag, accounts_size, registered_office | API on-demand, TTL 24h | B |
| `CveAdvisory` | GHSA + OSV + NVD | Build-pipeline vulnerability record | cve_id, cvss_v31, epss_30d, affected_components, severity | Polling, TTL 1h | A |
| `ProcurementOpportunity` | FTS + CCS + Contracts Finder | Vendor opportunity log | notice_id, framework, value_band, deadline | Daily pull | B |
| `AccreditationControl` | NCSC CAF + MOD SbD + JSP | Per-release evidence-pack control mapping | control_id, framework, version, evidence_link | Per-LTS refresh | A |
| `BundledReference` | GSCP + NCSC Crypto + WCAG + IANA | Build-time embedded reference data | reference_set, version, sha256 | Per-release embed | C |

### New Relationships

| From Entity | To Entity | Relationship | Source |
|-------------|-----------|--------------|--------|
| `Customer` (existing) | `ProspectCompany` | 1:1 (when known) | Companies House |
| `ReleaseManifest` (existing DR-007) | `CveAdvisory` | N:M | GHSA + OSV + NVD |
| `ReleaseManifest` | `AccreditationControl` | N:M | NCSC CAF / MOD SbD / JSP |
| `ReleaseManifest` | `BundledReference` | N:M | GSCP / NCSC Crypto / WCAG / IANA |

### Sync Strategy

| Source | Pattern | Frequency | Staleness Tolerance | Fallback |
|--------|---------|-----------|---------------------|----------|
| Companies House | API on-demand | Daily TTL | 24 h | Serve last-known + flag |
| GHSA | Polling | 1 h | 4 h | Degrade to OSV+NVD |
| OSV.dev | Polling | 1 h | 4 h | Degrade to GHSA+NVD |
| NIST NVD | Polling | 6 h | 24 h | Tertiary; non-blocking |
| FTS / CCS / Contracts Finder | Bulk pull | Daily | 48 h | Skip if down |
| NCSC / MOD / GSCP | RSS + manual | Weekly | n/a | Manual review |
| WCAG / axe-core / IANA | Per-release | Per LTS | n/a | Pinned version |

---

## UK Government Open Data Opportunities

### TCoP Point 10: Make Better Use of Data

**Open Data Consumed**:

| Source | Dataset | License | Requirement | Status |
|--------|---------|---------|-------------|--------|
| Companies House | Public Data API | OGL-v3 | BR-006 | ✅ Recommended |
| FTS | Notices feed | OGL-v3 | BR-007, INT-008 | ✅ Recommended |
| CCS Digital Marketplace | G-Cloud catalogue | OGL-v3 | INT-008 | ✅ Recommended |
| Contracts Finder | Below-threshold notices | OGL-v3 | BR-007 | ✅ Recommended |
| NCSC | CAF v3.x outcomes | OGL-v3 | NFR-SEC-002 | ✅ Recommended |
| NCSC | Cryptographic guidance | OGL-v3 | NFR-SEC-003 | ✅ Recommended |
| NCSC | Vulnerability advisories | OGL-v3 | INT-010 | ✅ Recommended |
| MOD Defence Digital | Secure by Design / JSP guidance | OGL-v3 | NFR-SEC-001 | ✅ Recommended |
| Cabinet Office | HMG GSCP | OGL-v3 | FR-012, NFR-C-001 | ✅ Recommended |

**Open Data Publishing Opportunities**:

- The vendor's **CAF/SbD/JSP control mapping per release** could be published as supplier reference for other suppliers facing similar accreditation paths (subject to MOD release approval).
- The **`crypto-allow-list.yaml`** maintained against NCSC guidance (GAP-2 mitigation) could be shared with other suppliers if NCSC permits.

**Common Data Standards Used**:

- Companies House Company Number (CRN)
- CVE-ID (NIST/MITRE)
- CVSS v3.1 / v4
- OSV schema (Google/OpenSSF)
- WCAG 2.2 success-criterion identifiers

**Data Ethics Framework Compliance** (Companies House director-PII processing only):

- [ ] Clear user need for data (BR-006 cross-subsidy tiering)
- [ ] Proportionate (only SME flag and director identity for diligence)
- [ ] Lawful basis (Article 6(1)(c)/(f) — to be confirmed in DPIA)
- [ ] Data minimisation (SME flag derived; raw accounts not stored)
- [ ] Transparency (privacy notice to apply)
- [ ] Data quality (authoritative source)

---

## Requirements Traceability

### Full Mapping Table

| Requirement | Need | Best-fit source | Score | Status | Lane | Notes |
|---|---|---|---|---|---|---|
| BR-004 | Per-release accreditation evidence | NCSC CAF + MOD SbD + JSP refs | 67.5 / 65.75 | ✅ Matched | A | See GAP-3 partial |
| BR-005 | LTS patch tracking | GHSA + OSV.dev + NVD | 84 / 79.75 / 73 | ✅ Matched | A | |
| BR-006 | SME-tier eligibility | Companies House | 85.5 | ✅ Matched | B | |
| BR-007 | Procurement framework engagement | FTS + CCS + Contracts Finder | 73.5 / 70 / 66.75 | ✅ Matched | B | |
| BR-008 | Reference customer engagement | — | — | ⚠️ Process-only | — | No data feed needed |
| FR-007 | Identity claim mapping | IANA OIDC/SAML registries | 48.5 | ⚠️ Partial | C | Schema only |
| FR-012 | Classification marking | HMG GSCP | 63.75 | ✅ Matched | C | |
| FR-014 | LTS patch delivery | GHSA + OSV + NVD + EPSS | 84 / 79.75 / 73 / 67 | ✅ Matched | A | |
| INT-001 | Customer IdP | IANA registries | 48.5 | ⚠️ Schema | C | Customer-controlled at runtime |
| INT-002 | Customer storage / DB | — | — | ✅ Customer-controlled | — | Inside boundary |
| INT-003 | Customer time / CA / mirror | — | — | ✅ Customer-controlled | — | Inside boundary |
| INT-004 | Customer observability | — | — | ✅ Customer-controlled | — | Inside boundary |
| INT-005 | Customer AI endpoint | — | — | ✅ Customer-controlled | — | Inside boundary |
| INT-006 | Customer email/notify | — | — | ✅ Customer-controlled | — | Inside boundary |
| INT-007 | Customer KMS | NCSC Cryptographic Guidance (allow-list) | 67.5 | ✅ Matched | C | Embedded primitive list |
| INT-008 | G-Cloud / DOS / Defence frameworks | FTS + CCS Marketplace | 73.5 / 70 | ✅ Matched | B | See GAP-5 |
| INT-009 | Vendor remote support | — | — | ✅ Process | — | Customer-toggled |
| INT-010 | Vulnerability disclosure inbound | NCSC Advisories + GHSA | 69 / 84 | ✅ Matched | A | |
| NFR-SEC-001 | MOD SbD / JSP alignment | MOD SbD + GAP-3 | 65.75 | ⚠️ Partial | A | See GAP-3 |
| NFR-SEC-002 | NCSC CAF mapping | NCSC CAF | 67.5 | ✅ Matched | A | |
| NFR-SEC-003 | HMG-approved cryptography | NCSC Crypto + GAP-2 | 67.5 | ⚠️ Partial | C | See GAP-2 |
| NFR-SEC-005 | Supply-chain integrity / SBOM | OSV + GHSA + NVD | 79.75 / 84 / 73 | ✅ Matched | A | |
| NFR-SEC-007 | Cleared-personnel claims | DR-002 + GAP-4 | — | ⚠️ Schema | — | See GAP-4 |
| NFR-SEC-008 | Patch SLAs | GHSA + OSV + NVD + EPSS | 84 / 79.75 / 73 / 67 | ✅ Matched | A | |
| NFR-C-001 | Classification policy | HMG GSCP | 63.75 | ✅ Matched | C | |
| NFR-C-003 | WCAG 2.2 AA | W3C WCAG + axe-core | 61.45 | ✅ Matched | C | |
| DR-001..006 | Internal datatypes | — | — | ✅ Internal | — | Not external feeds |
| DR-007 | SBOM / release manifest | OSV + GHSA + NVD | 79.75 / 84 / 73 | ✅ Matched | A | |

### Coverage Summary

- ✅ **22 requirements (78.6%)** fully matched
- ⚠️ **5 requirements (17.9%)** partial / schema-only
- ❌ **0 requirements (0%)** with no source — but **5 vendor-side process gaps** noted

---

## Next Steps

### Immediate Actions (0-2 weeks)

1. Register API keys: Companies House, GitHub PAT, NIST NVD, FTS download
2. Stand up Lane A pipeline scaffolding for GHSA + OSV + NVD pulls
3. Confirm DPIA increment scope for Companies House director-PII (Lane B)
4. Snapshot WCAG 2.2 + axe-core, HMG GSCP, NCSC Crypto guidance as bundle-time reference set v1

### Data Model Updates (2-4 weeks)

5. Run `/arckit:data-model` for project 002 — add the five vendor-side entities listed in "Impact on Data Model"
6. Run `/arckit:adr` — record ADR: "Sovereign system has zero external runtime data sources by design (anchored to Principle 21)"
7. Run `/arckit:adr` — record ADR: "Pair GHSA + OSV.dev as primary CVE feeds for build-pipeline redundancy"
8. Run `/arckit:dpia` — DPIA increment for vendor-side Companies House processing

### Gap Resolution (4-8 weeks)

9. Build internal `crypto-allow-list.yaml` per GAP-2 mitigation (refreshed annually against NCSC guidance)
10. Build internal release-pinned JSP 440/604 control mapping per GAP-3 mitigation
11. Build engagement intake form per GAP-1 mitigation

### Integration (Ongoing)

12. Wire CVE × EPSS × SBOM matcher into per-release evidence pack assembler
13. Difference-report job between GHSA, OSV, NVD verdicts
14. Daily FTS + CCS + Contracts Finder pull into vendor opportunity log
15. Per-release diff log for bundled reference set (GSCP / NCSC Crypto / WCAG / IANA)

---

## Appendices

### Appendix A: Research Methodology

**Data Sources Searched**:

- UK Government open data portals: data.gov.uk, api.gov.uk, gov.uk publications
- NCSC publications and threat-report channel
- MOD Defence Digital publications via gov.uk
- Cabinet Office publications (FTS, GSCP)
- Free vulnerability feeds: GHSA, OSV.dev, NIST NVD, FIRST EPSS
- W3C and Deque axe-core repositories

**Evaluation Methodology**:

- Deterministic UK-Gov rubric (RF 25 / DQ 20 / L&C 15 / API 15 / Comp 15 / Rel 10)
- License/cost includes +10 GB residency / −5 non-GB modifier
- Compliance includes bonuses: OGL-v3 +10, GDPR +10, ISO27001 +15, SOC2 +15, NCSC-CAF +25, G-Cloud-listed +25 (capped at 100)
- API quality scored deterministically by auth method (oauth2 90 / mtls 95 / api-key 80 / basic 60 / no-auth-required 70)
- Reliability scored deterministically by rate-limit band

**Limitations**:

- `ajv` not installed at repo root; reader/writer subagent split disabled — discovery used training-time knowledge of these well-known UK public sector and OSS sources rather than per-call live evidence. Recommend `npm install ajv` at repo root and re-run for evidence-validated output.
- Pricing all £0 (free / OGL / OSS) — no commercial sources discovered or required.
- API quality assessed from documentation, not hands-on testing.
- Discovery valid for ~ 6 months given the pace of vulnerability-feed and gov.uk catalogue evolution.

### Appendix B: Glossary

- **API**: Application Programming Interface
- **CAF**: Cyber Assessment Framework (NCSC)
- **CC-BY-4.0**: Creative Commons Attribution 4.0
- **CRN**: Company Registration Number (Companies House)
- **CVE**: Common Vulnerabilities and Exposures
- **CVSS**: Common Vulnerability Scoring System
- **DCPP**: Defence Cyber Protection Partnership
- **DPA 2018**: Data Protection Act 2018
- **DSP**: Defence Sourcing Portal
- **EPSS**: Exploit Prediction Scoring System (FIRST.org)
- **ETL**: Extract, Transform, Load
- **FTS**: Find a Tender Service
- **GDPR**: General Data Protection Regulation (UK GDPR)
- **GHSA**: GitHub Security Advisories
- **GSCP**: Government Security Classifications Policy
- **JSP**: Joint Service Publication (MOD)
- **NCSC**: National Cyber Security Centre
- **NVD**: National Vulnerability Database (NIST)
- **OGL**: Open Government Licence
- **OSV**: Open Source Vulnerabilities
- **PII**: Personally Identifiable Information
- **PSC**: People with Significant Control (Companies House)
- **SBOM**: Software Bill of Materials
- **SbD**: Secure by Design (MOD)
- **SLA**: Service Level Agreement
- **SME**: Small and Medium-sized Enterprise
- **TCoP**: Technology Code of Practice (UK Government)
- **TTL**: Time To Live (cache expiry)

## External References

> This section provides traceability from generated content back to source documents.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| ARC-002-REQ-v1.0 | ARC-002-REQ-v1.0.md | Requirements | projects/002-arckit-sovereign/ | Source of requirement IDs cited throughout |
| ARC-000-PRIN-v2.0 | ARC-000-PRIN-v2.0.md | Architecture Principles | projects/000-global/ | Source of Principle 21 (Sovereign and Air-Gapped) |
| ARC-001-DSCT-v1.0 | (not yet created) | Data Source Discovery | projects/001-arckit-saas/research/ | Sister DSCT for managed-SaaS route — to be cross-referenced once created |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| C1 | ARC-000-PRIN-v2.0 | Principle 21 | Architectural anchor | "MUST be installable, operable, updatable, and uninstallable without any reliance on vendor-controlled services or outbound network connectivity" |
| C2 | ARC-002-REQ-v1.0 | NFR-SEC-004 | Runtime constraint | Sovereign deployment shall make no outbound network call outside the customer's accredited boundary |
| C3 | ARC-002-REQ-v1.0 | BR-006 | SME-tier basis | Cross-subsidy commercial model dependent on SME-tier eligibility verification |
| C4 | ARC-002-REQ-v1.0 | NFR-SEC-008 | Patch SLAs | Critical 7d / High 30d / Medium 90d patch delivery SLAs |
| C5 | ARC-002-REQ-v1.0 | NFR-SEC-005 | SBOM | Supply-chain integrity via SBOM verification per build |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:datascout` agent (orchestrator) + main-conversation file render (writer subagent disabled — `ajv` missing at repo root)
**Generated on**: 2026-05-06
**ArcKit Version**: 4.16.0
**Project**: ArcKit as a Service (Sovereign Deployment)
**Model**: Claude Opus 4.7 (1M context)
