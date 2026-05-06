# Data Source Discovery: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.16.3 | **Command**: `/arckit:datascout`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-DSCT-v1.1 |
| **Document Type** | Data Source Discovery |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.1 |
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
| 1.0 | 2026-05-06 | ArcKit AI (datascout) | Initial creation from `/arckit:datascout` agent. Rubric: `uk-gov` (auto-detected). Mode: legacy single-agent (`ajv` not installed at repo root). | [PENDING] | [PENDING] |
| 1.1 | 2026-05-06 | ArcKit AI (datascout) | Refresh under the proper reader / writer subagent split with schema-validated evidence. Re-scored 26 sources via deterministic uk-gov rubric; traceability expanded to 28 rows; gap list reaffirmed (5 vendor-side process gaps). v1.0 was generated in legacy single-agent mode; v1.1 supersedes it. | [PENDING] | [PENDING] |

---

## Executive Summary

### Data Needs Overview

This document presents data source discovery findings for the **ArcKit as a Service (Sovereign Deployment)** project, identifying external APIs, datasets, and reference taxonomies that can fulfil the data and integration requirements documented in `ARC-002-REQ-v1.0.md`.

**Requirements Analyzed**: 7 data requirements (DR-001..007), functional requirements (FR-007, FR-012, FR-014), 10 integration requirements (INT-001..010), 8 security non-functional requirements (NFR-SEC-001..008), and compliance non-functional requirements (NFR-C-001, NFR-C-003).

**Data Source Categories Identified**: 5 (category, source_type) buckets covering 3 architectural lanes.

**Discovery Approach**: UK Government open data first (api.gov.uk, data.gov.uk, NCSC publications, MOD gov.uk publications), then free supply-chain feeds for build-pipeline use, then build-time reference taxonomies and OSS schema registries. Deterministic UK-Gov rubric scoring (RF 25 / DQ 20 / L&C 15 / API 15 / Comp 15 / Rel 10) with +10 GB residency bonus and −5 non-GB residency penalty.

> **Critical architectural framing — read first.** This project is a **sovereign / air-gapped deployment**. Per **Principle 21 / BR-002 / NFR-SEC-004 / TC-1**, the running system **MUST NOT** make any outbound network call to any endpoint outside the customer's accredited boundary. **None of the 26 sources discovered below are runtime data sources for the deployed system.** All are vendor-side feeds across three lanes:
>
> - **Lane A — Vendor build / release-engineering** (outside customer boundary): SBOM augmentation, CVE alerting, LTS patch SLA tracking, accreditation evidence pack assembly.
> - **Lane B — Vendor pre-sales / commercial** (outside customer boundary): SME-tier eligibility verification (cross-subsidy basis), G-Cloud / DOS / FTS framework engagement.
> - **Lane C — Reference taxonomies** (consumed at vendor build time, baked into the bundle as static data): classification catalogue, WCAG ruleset, NCSC crypto guidance, JSP control catalogues, OIDC/OAuth schema registries.
>
> The bundle that crosses the air-gap MUST be self-contained. This is the most important finding of this discovery and is preserved verbatim from v1.0.
>
> **What changed in v1.1.** This refresh runs under the proper reader / writer subagent split: the reader stage assembled per-source evidence subtrees against the validated DSCT handoff schema, and a deterministic scorer applied the uk-gov rubric. v1.0 was produced in legacy single-agent mode without schema validation. The architectural conclusions are unchanged; the per-source evidence is now schema-validated and the scoring is deterministic and reproducible.

### Key Findings

- **Companies House Public Data API (Lane B, score 82.75)** — best fit for BR-006 SME-tier verification underpinning the cross-subsidy commercial model. OGL-v3, GB-hosted, real-time, API-key authed.
- **GHSA + NIST NVD + OSV.dev (Lane A, scores 77.75 / 76.0 / 75.38)** — triple-feed vulnerability stack for NFR-SEC-005 (SBOM integrity), NFR-SEC-008 (Critical 7d / High 30d / Medium 90d patch SLAs), DR-007 (release-manifest CVE enrichment), and INT-010 (inbound disclosure). Two-of-three minimum to satisfy Principle 3 redundancy at build time.
- **NCSC RSS / NCSC Threat Reports / Secure by Design (Lane A, scores 67.75 / 66.25 / 65.5)** — UK-side accreditation evidence-pack inputs. Annual / weekly cadences keep the deterministic total below the CVE feeds, but **read RF column, not total**, for these — they are non-substitutable evidence inputs.
- **Find a Tender (FTS) OCDS API + Contracts Finder API (Lane B, scores 72.75 / 73.25)** — authoritative procurement signal for BR-007 framework engagement (above- and below-threshold).
- **HMG GSCP + NCSC Cryptographic Guidance + W3C WCAG / axe-core + IANA OAuth Registry (Lane C, scores 63.75 / 65.25 / 56.88 / 56.63 / 59.13)** — build-time reference taxonomies baked into the bundle to enforce classification marking (FR-012 / NFR-C-001), HMG-approved primitives (NFR-SEC-003 / INT-007), accessibility (NFR-C-003), and identity claim schemas (FR-007 / INT-001).

### Data Source Summary

| Source Type | Count | Cost Range | Key Providers |
|-------------|-------|------------|---------------|
| **UK Government Open Data** | 16 | Free (OGL-v3) | Companies House, Cabinet Office (FTS, Contracts Finder, GSCP, data.gov.uk), CCS (Digital Marketplace), NCSC (CAF, RSS, Threat Reports, Crypto Guidance), DSIT (Secure by Design), MOD (JSP 441, JSP 604) |
| **Commercial APIs** | 0 | n/a | None — sovereign runtime forbids them; vendor-side needs met by free / open feeds |
| **Free/Freemium APIs** | 4 | Free (rate-limited) | GitHub (GHSA), NIST (NVD), Google / OpenSSF (OSV.dev), FIRST.org (EPSS) |
| **Open Source Datasets / Rulesets** | 6 | Free (CC0 / CC-BY / Apache / W3C) | IANA (OAuth Parameters Registry, Licensing Terms), OpenID Foundation (OIDC Core, OIDC Discovery), W3C (WCAG 2.2), Deque (axe-core) |
| **TOTAL** | **26** | **£0/year** | — |

### Top Recommended Sources

**Shortlist for integration**:

1. **Companies House Public Data API** for company / SME verification: OGL-v3, GB-hosted, real-time, API-key — score **82.75/100**.
2. **Companies House Developer Hub (REST API)** for company search / profile / officers / PSC: OGL-v3, GB-hosted, real-time — score **78.25/100**.
3. **GitHub Security Advisories REST API (GHSA)** for vulnerability / SBOM enrichment: real-time, OAuth2-capable, CC-BY-4.0 — score **77.75/100**.
4. **NIST NVD API 2.0** for CVE / CVSS / CPE / KEV cross-validation: real-time, CC0-1.0 — score **76.00/100**.
5. **OSV.dev Open Source Vulnerabilities API** for SBOM-keyed redundancy: real-time, Apache-2.0 — score **75.38/100**.

### Requirements Coverage

- ✅ **~22 of 28 requirements (78.6%)** addressable from external sources
- ⚠️ **6 requirements (21.4%)** partial / schema-only / customer-controlled
- ❌ **0 requirements (0%)** with no source — but **5 vendor-side process gaps** identified (none CRITICAL; all Lane A / B process matters)

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
| 5 | FR-007 | Identity claim mapping | Functional | MUST | Schema only | Ad-hoc | Identity reference | C |
| 6 | FR-012 | Classification marking | Functional | MUST | Build-time embedded | Annual | Classification reference | C |
| 7 | FR-014 | LTS patch delivery (SLAs) | Functional | MUST | 7d / 30d / 90d SLA | Real-time | Vulnerability feeds | A |
| 8 | INT-001 | Customer IdP integration schemas | Integration | MUST | Schema only | Ad-hoc | Identity reference | C |
| 9 | INT-007 | Customer KMS — HMG-approved primitive allow-list | Integration | MUST | Build-time embedded | Annual | Crypto reference | C |
| 10 | INT-008 | G-Cloud / DOS / Defence framework listings | Integration | SHOULD | Daily | Daily | Procurement | B |
| 11 | INT-010 | Inbound vulnerability disclosure channel | Integration | MUST | Real-time monitoring | Real-time | Vulnerability feeds | A |
| 12 | NFR-SEC-001 | MOD SbD / JSP 440 / JSP 604 alignment | Security NFR | MUST | Per release | Quarterly | Accreditation reference | A |
| 13 | NFR-SEC-002 | NCSC CAF v3.x mapping | Security NFR | MUST | Per release | Annual | Accreditation reference | A |
| 14 | NFR-SEC-003 | HMG-approved cryptography | Security NFR | MUST | Build-time enforced | Annual | Crypto reference | C |
| 15 | NFR-SEC-005 | Supply-chain integrity / SBOM | Security NFR | MUST | Per build | Real-time | Vulnerability feeds | A |
| 16 | NFR-SEC-007 | UK personnel-clearance taxonomy | Security NFR | MUST | Schema only | Static | Identity / clearance | — |
| 17 | NFR-SEC-008 | Patch SLA evidence | Security NFR | MUST | Per release | Real-time | Vulnerability feeds | A |
| 18 | NFR-C-001 | Classification policy enforcement | Compliance NFR | MUST | Build-time embedded | Annual | Classification reference | C |
| 19 | NFR-C-003 | WCAG 2.2 AA | Compliance NFR | MUST | Per CI build | Quarterly | A11y reference | C |
| 20 | DR-001..006 | Internal datatypes (project content, deployment, audit) | Data | MUST | — | — | Internal — no external feed | — |
| 21 | DR-007 | SBOM / release manifest CVE enrichment | Data | MUST | Per build | Real-time | Vulnerability feeds | A |

### Data Needs by Category

**Category 1: Company / Procurement (Lane B — vendor pre-sales)**

- Requirements: BR-006, BR-007, INT-008
- Data fields needed: company number, SME status (derived from accounts thresholds), registered office, SIC code, active filings, officers, PSC, framework listings, contract notices, supplier metadata
- Volume: 10–50 SME lookups/day; daily monitoring of FTS / CCS / Contracts Finder feeds
- Freshness: Daily (procurement) / real-time (Companies House)
- Quality threshold: authoritative source required (Companies House for SME flag); 100% completeness on SME-determining fields

**Category 2: Cybersecurity / Vulnerability / Accreditation (Lane A — vendor build)**

- Requirements: BR-004, BR-005, FR-014, INT-010, NFR-SEC-001, NFR-SEC-002, NFR-SEC-005, NFR-SEC-008, DR-007
- Data fields needed: CVE id, CVSS v3.1/v4, EPSS, advisory text, OSV records, GHSA records, KEV flag, NCSC CAF outcomes, MOD SbD principles, JSP 440/604 control catalogue, NCSC threat reports
- Volume: real-time CVE alerting on ~500 SBOM components; quarterly accreditation pack assembly
- Freshness: real-time (CVE feeds), weekly (NCSC threat reports), quarterly (MOD), annual (NCSC CAF / JSP revisions)
- Quality threshold: ≥ 99% recall on Critical CVEs (justifies dual-feed: GHSA + OSV minimum)

**Category 3: Classification / A11y / Cryptography / Identity Schemas (Lane C — build-time reference)**

- Requirements: FR-007, FR-012, INT-001, INT-007, NFR-SEC-003, NFR-C-001, NFR-C-003
- Data fields needed: HMG GSCP categories + handling caveats; WCAG 2.2 success criteria + axe-core ruleset; HMG-approved cryptographic primitive list; OAuth parameter registry; OIDC standard / profile claims; OIDC discovery metadata
- Volume: static reference, embedded once per release
- Freshness: annual (NCSC, GSCP); quarterly (axe-core); ad-hoc (IANA, OIDF)
- Quality threshold: 100% — these are normative references baked into the bundle

---

## Data Source Discovery

> **Note**: Categories are dynamically identified from project requirements. Five (category, source_type) buckets were generated; categories with no relevant requirements (geospatial, financial markets, demographics, weather, health, transport, energy, education, property, crime, KYC/identity-verification) are deliberately excluded — they are **not gaps**.

---

## Category 1: Company / Procurement (Lane B — vendor pre-sales / commercial)

**Requirements Addressed**: BR-006, BR-007, INT-008

**Why This Category**: BR-006 establishes a tiered cross-subsidy commercial model that requires authoritative SME-status verification of customers. BR-007 and INT-008 require vendor-side awareness of UK government procurement signals to engage frameworks (G-Cloud, DOS, Find a Tender, Defence-specific frameworks).

**Data Fields Needed**: company number; SME flag (inferred from accounts thresholds); registered office; SIC code; active filings; officers / PSC; CCS framework listings; FTS contract notices; OCDS releases / records.

---

### Source 1A: Companies House Public Data API (UK Gov Open Data)

**Provider**: Companies House
**Source Name**: Companies House Public Data API
**Citation**: `[CH-API-1]`
**Fetched From**: <https://developer-specs.company-information.service.gov.uk/guides/rateLimiting>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Rate Limit** | 120 req / minute |
| **Refresh Cadence** | real-time |
| **Authentication Required** | true |
| **Authentication Method** | api-key |
| **Data Categories Supported** | company-profile, filing-history, officers, persons-with-significant-control, charges, insolvency |

**Evaluation Score** (uk-gov rubric):

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 100 | 25.00 |
| Data Quality | 20% | 100 | 20.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 80 | 12.00 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 70 | 7.00 |
| **Total** | **100%** | | **82.75/100** |

---

### Source 1B: Companies House Developer Hub (REST API) (UK Gov Open Data)

**Provider**: Companies House
**Source Name**: Companies House Developer Hub (REST API)
**Citation**: `[CH-API-2]`
**Fetched From**: <https://developer-specs.company-information.service.gov.uk/guides/authorisation>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | real-time |
| **Authentication Required** | true |
| **Authentication Method** | api-key |
| **Data Categories Supported** | company-search, company-profile, filing-history, officers, psc, registered-office |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 90 | 22.50 |
| Data Quality | 20% | 100 | 20.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 80 | 12.00 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **78.25/100** |

---

### Source 1C: Contracts Finder API (UK Gov Open Data)

**Provider**: Crown Commercial Service
**Source Name**: Contracts Finder API
**Citation**: `[CF-API-1]`
**Fetched From**: <https://www.contractsfinder.service.gov.uk/apidocumentation>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | daily |
| **Authentication Required** | true |
| **Authentication Method** | oauth2 |
| **Data Categories Supported** | future-opportunities, live-opportunities, contract-awards, early-engagement, below-threshold, cpv-codes |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 80 | 20.00 |
| Data Quality | 20% | 80 | 16.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 90 | 13.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **73.25/100** |

---

### Source 1D: Find a Tender Service (FTS) OCDS API (UK Gov Open Data)

**Provider**: Cabinet Office
**Source Name**: Find a Tender Service (FTS) OCDS API
**Citation**: `[FTS-API-1]`
**Fetched From**: <https://www.find-tender.service.gov.uk/Developer/Documentation>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | daily |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | procurement-notices, ocds-release, ocds-record, above-threshold, below-threshold, contract-awards |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 90 | 22.50 |
| Data Quality | 20% | 80 | 16.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **72.75/100** |

---

### Source 1E: Find a Tender Service (Public UI / OGL content) (UK Gov Open Data)

**Provider**: Cabinet Office
**Source Name**: Find a Tender Service (Public UI / OGL content)
**Citation**: `[FTS-UI-1]`
**Fetched From**: <https://www.find-tender.service.gov.uk/>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | daily |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | procurement-notices, contract-lifecycle, public-sector-tenders |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 70 | 17.50 |
| Data Quality | 20% | 80 | 16.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **67.75/100** |

---

### Source 1F: Contracts Finder (Public Service) (UK Gov Open Data)

**Provider**: Crown Commercial Service
**Source Name**: Contracts Finder (Public Service)
**Citation**: `[CF-UI-1]`
**Fetched From**: <https://www.contractsfinder.service.gov.uk/>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | daily |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | contract-notices, awarded-contracts, procurement-stage, below-threshold |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 65 | 16.25 |
| Data Quality | 20% | 80 | 16.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **66.50/100** |

---

### Source 1G: Digital Marketplace — G-Cloud Catalogue (UK Gov Open Data)

**Provider**: Crown Commercial Service
**Source Name**: Digital Marketplace - G-Cloud Catalogue
**Citation**: `[DM-GC-1]`
**Fetched From**: <https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search>
**Confidence**: medium

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Contract Vehicles** | G-Cloud-14, G-Cloud-13, DOS-6, Crown-Commercial |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | g-cloud-suppliers, g-cloud-services, cloud-hosting, cloud-software, cloud-support, dos-suppliers |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 85 | 21.25 |
| Data Quality | 20% | 0 | 0.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **55.50/100** |

---

### Source 1H: Government CloudStore Catalogue (data.gov.uk) (UK Gov Open Data)

**Provider**: Cabinet Office
**Source Name**: Government CloudStore Catalogue (data.gov.uk)
**Citation**: `[DGU-CS-1]`
**Fetched From**: <https://www.data.gov.uk/dataset/5462ae53-ebec-4464-ac8d-5325213fb4f9/cloudstore_catalogue_version>
**Confidence**: medium

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | static |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | cloud-ict-services, public-sector-procurement, supplier-catalogue |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 50 | 12.50 |
| Data Quality | 20% | 20 | 4.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **50.75/100** |

---

### Comparison Table: Company / Procurement (uk-gov)

| Source | Provider | Refresh | Auth | RF | DQ | L&C | API | Comp | Rel | TOTAL |
|--------|----------|---------|------|----|----|-----|-----|------|-----|-------|
| Companies House Public Data API | Companies House | real-time | api-key | 25.00 | 20.00 | 15.00 | 12.00 | 3.75 | 7.00 | **82.75** |
| Companies House Developer Hub | Companies House | real-time | api-key | 22.50 | 20.00 | 15.00 | 12.00 | 3.75 | 5.00 | **78.25** |
| Contracts Finder API | CCS | daily | oauth2 | 20.00 | 16.00 | 15.00 | 13.50 | 3.75 | 5.00 | **73.25** |
| FTS OCDS API | Cabinet Office | daily | none | 22.50 | 16.00 | 15.00 | 10.50 | 3.75 | 5.00 | **72.75** |
| FTS Public UI | Cabinet Office | daily | none | 17.50 | 16.00 | 15.00 | 10.50 | 3.75 | 5.00 | **67.75** |
| Contracts Finder UI | CCS | daily | none | 16.25 | 16.00 | 15.00 | 10.50 | 3.75 | 5.00 | **66.50** |
| Digital Marketplace G-Cloud | CCS | n/a | none | 21.25 | 0.00 | 15.00 | 10.50 | 3.75 | 5.00 | **55.50** |
| CloudStore Catalogue (data.gov.uk) | Cabinet Office | static | none | 12.50 | 4.00 | 15.00 | 10.50 | 3.75 | 5.00 | **50.75** |

**Recommendation for Category 1**: **Companies House Public Data API** (primary) for BR-006 SME verification — authoritative and uniquely fit for purpose. **FTS OCDS API + Contracts Finder API** as the procurement signal pair for BR-007 / INT-008. **Digital Marketplace G-Cloud** as a secondary supplier-catalogue signal for INT-008. Public-UI variants (FTS-UI, CF-UI) are used for human review only.

---

## Category 2: Cybersecurity / Vulnerability / Accreditation (Lane A — vendor build)

**Requirements Addressed**: BR-004, BR-005, FR-014, INT-010, NFR-SEC-001, NFR-SEC-002, NFR-SEC-005, NFR-SEC-008, DR-007

**Why This Category**: Per-release evidence packs (BR-004) require currency on NCSC CAF outcomes and MOD SbD / JSP control catalogues. Patch SLAs (NFR-SEC-008) and SBOM integrity (NFR-SEC-005) require near real-time CVE intelligence on ~500 dependencies. INT-010 inbound vulnerability disclosure is fed primarily by NCSC channels supplemented by GHSA. Two sub-buckets here: free APIs (CVE feeds) and UK-Gov references (accreditation evidence).

---

### Sub-bucket 2A: Free APIs — Vulnerability Feeds

#### Source 2A-1: GitHub Security Advisories REST API (GHSA) (Free API, US-hosted)

**Provider**: GitHub
**Source Name**: GitHub Security Advisories REST API (GHSA)
**Citation**: `[GH-GHSA-1]`
**Fetched From**: <https://docs.github.com/en/rest/security-advisories>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Licence Type** | CC-BY-4.0 |
| **Pricing Model** | free |
| **Rate Limit** | 83 req / minute |
| **Refresh Cadence** | real-time |
| **Authentication Required** | false |
| **Authentication Method** | oauth2 |
| **Data Categories Supported** | cve, ghsa, security-advisories, vulnerabilities, cvss |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 95 | 23.75 |
| Data Quality | 20% | 100 | 20.00 |
| Licence & Cost (residency_bonus −5) | 15% | 85 | 12.75 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 70 | 7.00 |
| **Total** | **100%** | | **77.75/100** |

---

#### Source 2A-2: NIST National Vulnerability Database (NVD) API 2.0 (Free API, US-hosted)

**Provider**: NIST
**Source Name**: National Vulnerability Database (NVD) API 2.0
**Citation**: `[NIST-NVD-1]`
**Fetched From**: <https://nvd.nist.gov/developers/start-here>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Licence Type** | CC0-1.0 |
| **Pricing Model** | free |
| **Rate Limit** | 100 req / minute |
| **Refresh Cadence** | real-time |
| **Authentication Required** | false |
| **Authentication Method** | api-key |
| **Data Categories Supported** | cve, cvss, cpe, cwe, kev, vulnerabilities |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 85 | 21.25 |
| Data Quality | 20% | 100 | 20.00 |
| Licence & Cost (residency_bonus −5) | 15% | 90 | 13.50 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 70 | 7.00 |
| **Total** | **100%** | | **76.00/100** |

---

#### Source 2A-3: OSV.dev Open Source Vulnerabilities API (Free API, US-hosted)

**Provider**: Google
**Source Name**: OSV.dev Open Source Vulnerabilities API
**Citation**: `[OSV-DEV-1]`
**Fetched From**: <https://google.github.io/osv.dev/api/>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Licence Type** | Apache-2.0 |
| **Pricing Model** | free |
| **Refresh Cadence** | real-time |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | cve, osv, vulnerabilities, package-advisories, ghsa |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 95 | 23.75 |
| Data Quality | 20% | 100 | 20.00 |
| Licence & Cost (residency_bonus −5) | 15% | 82.5 | 12.38 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **75.38/100** |

---

#### Source 2A-4: FIRST EPSS Exploit Prediction Scoring System API (Free API, US-hosted)

**Provider**: FIRST.org
**Source Name**: EPSS Exploit Prediction Scoring System API
**Citation**: `[FIRST-EPSS-1]`
**Fetched From**: <https://api.first.org/>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Licence Type** | Unknown |
| **Pricing Model** | free |
| **Rate Limit** | 1000 req / minute |
| **Refresh Cadence** | daily |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | epss, exploit-prediction, cve, vulnerability-scoring |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 75 | 18.75 |
| Data Quality | 20% | 80 | 16.00 |
| Licence & Cost (residency_bonus −5) | 15% | 52.5 | 7.88 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 90 | 9.00 |
| **Total** | **100%** | | **65.88/100** |

---

#### Comparison Table: Sub-bucket 2A — Vulnerability Feeds

| Source | Refresh | Rate Limit | Licence | RF | DQ | L&C | API | Comp | Rel | TOTAL |
|--------|---------|-----------|---------|----|----|-----|-----|------|-----|-------|
| GHSA | real-time | 83/min | CC-BY-4.0 | 23.75 | 20.00 | 12.75 | 10.50 | 3.75 | 7.00 | **77.75** |
| NIST NVD 2.0 | real-time | 100/min | CC0-1.0 | 21.25 | 20.00 | 13.50 | 10.50 | 3.75 | 7.00 | **76.00** |
| OSV.dev | real-time | n/a | Apache-2.0 | 23.75 | 20.00 | 12.38 | 10.50 | 3.75 | 5.00 | **75.38** |
| FIRST EPSS | daily | 1000/min | Unknown | 18.75 | 16.00 | 7.88 | 10.50 | 3.75 | 9.00 | **65.88** |

---

### Sub-bucket 2B: UK Gov — Accreditation / Threat Intelligence References

#### Source 2B-1: NCSC RSS Feeds (all-content) (UK Gov Open Data)

**Provider**: NCSC
**Source Name**: NCSC RSS Feeds (all-content)
**Citation**: `[NCSC-RSS-1]`
**Fetched From**: <https://www.ncsc.gov.uk/information/rss-feeds>
**Confidence**: medium

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | daily |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | rss-feed, threat-reports, guidance, blog-posts |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 70 | 17.50 |
| Data Quality | 20% | 80 | 16.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **67.75/100** |

---

#### Source 2B-2: NCSC Threat Reports (UK Gov Open Data)

**Provider**: NCSC
**Source Name**: NCSC Threat Reports
**Citation**: `[NCSC-THREAT-1]`
**Fetched From**: <https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | weekly |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | threat-intelligence, vulnerability-advisories, rss-feed |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 80 | 20.00 |
| Data Quality | 20% | 60 | 12.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **66.25/100** |

---

#### Source 2B-3: Secure by Design (UK Gov Open Data)

**Provider**: Department for Science, Innovation and Technology
**Source Name**: Secure by Design
**Citation**: `[DSIT-SBD-1]`
**Fetched From**: <https://www.gov.uk/government/publications/secure-by-design>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Certifications** | OGL-v3 |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | ad-hoc |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | secure-by-design, security-policy, assurance |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 95 | 23.75 |
| Data Quality | 20% | 30 | 6.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 35 | 5.25 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **65.50/100** |

---

#### Source 2B-4: NCSC Cyber Assessment Framework (CAF) (UK Gov Open Data)

**Provider**: NCSC
**Source Name**: Cyber Assessment Framework (CAF)
**Citation**: `[NCSC-CAF-1]`
**Fetched From**: <https://www.ncsc.gov.uk/collection/cyber-assessment-framework>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Certifications** | OGL-v3 |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | annual |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | cyber-assessment, ncsc-caf, outcomes, critical-infrastructure |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 100 | 25.00 |
| Data Quality | 20% | 15 | 3.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 35 | 5.25 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **63.75/100** |

> **Read RF (100), not total** — annual cadence drags total down, but the CAF is non-substitutable for NFR-SEC-002 evidence.

---

#### Source 2B-5: JSP 441 Managing Information in Defence (UK Gov Open Data)

**Provider**: Ministry of Defence
**Source Name**: JSP 441 Managing Information in Defence
**Citation**: `[MOD-JSP441-1]`
**Fetched From**: <https://assets.publishing.service.gov.uk/media/5a82b0d240f0b62305b93d65/2017-02121.pdf>
**Confidence**: low

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | ad-hoc |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | mod-jsp, information-management, defence |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 50 | 12.50 |
| Data Quality | 20% | 30 | 6.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **52.75/100** |

---

#### Source 2B-6: JSP 604 Defence Networks Governance (Withdrawn) (UK Gov Open Data)

**Provider**: Ministry of Defence
**Source Name**: JSP 604 Defence Networks Governance (Withdrawn)
**Citation**: `[MOD-JSP604-1]`
**Fetched From**: <https://www.gov.uk/government/publications/joint-service-publication-jsp-604-network-rules>
**Confidence**: medium

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | static |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | mod-jsp, ict-accreditation, defence-networks, withdrawn |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 40 | 10.00 |
| Data Quality | 20% | 20 | 4.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **48.25/100** |

---

#### Comparison Table: Sub-bucket 2B — UK-Gov Accreditation References

| Source | Refresh | RF | DQ | L&C | API | Comp | Rel | TOTAL | Role |
|--------|---------|----|----|-----|-----|------|-----|-------|------|
| NCSC RSS Feeds | daily | 17.50 | 16.00 | 15.00 | 10.50 | 3.75 | 5.00 | **67.75** | INT-010 inbound channel |
| NCSC Threat Reports | weekly | 20.00 | 12.00 | 15.00 | 10.50 | 3.75 | 5.00 | **66.25** | INT-010 / threat intel |
| Secure by Design (DSIT) | ad-hoc | 23.75 | 6.00 | 15.00 | 10.50 | 5.25 | 5.00 | **65.50** | NFR-SEC-001 evidence |
| NCSC CAF | annual | 25.00 | 3.00 | 15.00 | 10.50 | 5.25 | 5.00 | **63.75** | NFR-SEC-002 evidence |
| JSP 441 | ad-hoc | 12.50 | 6.00 | 15.00 | 10.50 | 3.75 | 5.00 | **52.75** | Reference; partial JSP coverage |
| JSP 604 (Withdrawn) | static | 10.00 | 4.00 | 15.00 | 10.50 | 3.75 | 5.00 | **48.25** | Historical reference only |

**Recommendation for Category 2**: **Pair GHSA + OSV.dev** as primary CVE feeds with **NIST NVD** as cross-validation backstop (Principle 3 redundancy at build time); **EPSS** for prioritisation weighting. **NCSC CAF + Secure by Design + NCSC Threat Reports + NCSC RSS** are non-substitutable evidence and inbound-disclosure inputs regardless of total score. **JSP 441** retained as partial reference — JSP 440 / 604 process gap captured in **GAP-3**.

---

## Category 3: Identity Schemas (Lane C — build-time reference, OSS)

**Requirements Addressed**: FR-007, INT-001

**Why This Category**: Identity claim and authorisation-server schemas are required for build-time wiring of the OIDC / OAuth2 customer-IdP integration surface. Runtime identity flows are customer-controlled (INT-001 is customer-controlled in the deployed system); only the schema is bundled.

---

### Source 3A: IANA OAuth Parameters Registry (OSS)

**Provider**: IANA
**Source Name**: OAuth Parameters Registry
**Citation**: `[IANA-OAUTH-1]`
**Fetched From**: <https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Licence Type** | CC0-1.0 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | ad-hoc |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | oauth-parameters, access-token-types, authentication-methods, metadata, error-codes |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 80 | 20.00 |
| Data Quality | 20% | 30 | 6.00 |
| Licence & Cost (residency_bonus −5) | 15% | 92.5 | 13.88 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **59.13/100** |

---

### Source 3B: OpenID Connect Core 1.0 (errata set 2) (OSS)

**Provider**: OpenID Foundation
**Source Name**: OpenID Connect Core 1.0 (errata set 2)
**Citation**: `[OIDF-CORE-1]`
**Fetched From**: <https://openid.net/specs/openid-connect-core-1_0.html>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Pricing Model** | free |
| **Refresh Cadence** | ad-hoc |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Licence Type** | Unknown |
| **Data Categories Supported** | standard-claims, profile-claims, address-claims, authentication-methods, id-token |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 85 | 21.25 |
| Data Quality | 20% | 30 | 6.00 |
| Licence & Cost (residency_bonus −5) | 15% | 52.5 | 7.88 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **54.38/100** |

---

### Source 3C: OpenID Connect Discovery 1.0 (errata set 2) (OSS)

**Provider**: OpenID Foundation
**Source Name**: OpenID Connect Discovery 1.0 (errata set 2)
**Citation**: `[OIDF-DISC-1]`
**Fetched From**: <https://openid.net/specs/openid-connect-discovery-1_0.html>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Pricing Model** | free |
| **Refresh Cadence** | ad-hoc |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Licence Type** | Unknown |
| **Data Categories Supported** | discovery, well-known-uri, authorization-server-metadata, claims-supported, userinfo-endpoint |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 80 | 20.00 |
| Data Quality | 20% | 30 | 6.00 |
| Licence & Cost (residency_bonus −5) | 15% | 52.5 | 7.88 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **53.13/100** |

---

### Source 3D: IANA Protocol Registries Licensing Terms (OSS)

**Provider**: IANA
**Source Name**: IANA Protocol Registries Licensing Terms
**Citation**: `[IANA-LIC-1]`
**Fetched From**: <https://www.iana.org/help/licensing-terms>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | US |
| **Licence Type** | CC0-1.0 |
| **Pricing Model** | open-data |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | licence-terms, protocol-registries |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 30 | 7.50 |
| Data Quality | 20% | 0 | 0.00 |
| Licence & Cost (residency_bonus −5) | 15% | 92.5 | 13.88 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **40.63/100** |

---

### Comparison Table: Identity Schemas (OSS)

| Source | Provider | Licence | RF | DQ | L&C | API | Comp | Rel | TOTAL |
|--------|----------|---------|----|----|-----|-----|------|-----|-------|
| IANA OAuth Parameters | IANA | CC0-1.0 | 20.00 | 6.00 | 13.88 | 10.50 | 3.75 | 5.00 | **59.13** |
| OIDC Core 1.0 | OpenID Foundation | Unknown | 21.25 | 6.00 | 7.88 | 10.50 | 3.75 | 5.00 | **54.38** |
| OIDC Discovery 1.0 | OpenID Foundation | Unknown | 20.00 | 6.00 | 7.88 | 10.50 | 3.75 | 5.00 | **53.13** |
| IANA Licensing Terms | IANA | CC0-1.0 | 7.50 | 0.00 | 13.88 | 10.50 | 3.75 | 5.00 | **40.63** |

**Recommendation for Category 3 (Identity)**: Bundle **IANA OAuth Parameters Registry + OIDC Core + OIDC Discovery** schemas at build time. These satisfy FR-007 / INT-001 *at the schema level only*; the runtime IdP itself is customer-controlled.

---

## Category 4: Reference / Free APIs

This bucket is rendered as Sub-bucket 2A above (Vulnerability Feeds: GHSA, NIST NVD, OSV.dev, FIRST EPSS) — included here as a cross-reference. See Sub-bucket 2A for full per-source cards and comparison table.

---

## Category 5: Reference / OSS — Accessibility

**Requirements Addressed**: NFR-C-003

**Why This Category**: WCAG 2.2 AA must be enforced both as a normative ruleset (success criteria) and as a CI-runnable validator (axe-core).

---

### Source 5A: W3C Web Content Accessibility Guidelines (WCAG) 2.2 (OSS)

**Provider**: W3C
**Source Name**: Web Content Accessibility Guidelines (WCAG) 2.2
**Citation**: `[WCAG-22-1]`
**Fetched From**: <https://www.w3.org/TR/WCAG22/>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Licence Type** | Unknown |
| **Pricing Model** | free |
| **Refresh Cadence** | static |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | accessibility-success-criteria, wcag-22-aa, wcag-22-aaa, perceivable, operable, understandable, robust |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 100 | 25.00 |
| Data Quality | 20% | 20 | 4.00 |
| Licence & Cost (residency_bonus 0) | 15% | 57.5 | 8.63 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **56.88/100** |

---

### Source 5B: axe-core accessibility testing engine (OSS)

**Provider**: Deque Systems
**Source Name**: axe-core accessibility testing engine
**Citation**: `[AXE-CORE-1]`
**Fetched From**: <https://github.com/dequelabs/axe-core>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Licence Type** | Unknown |
| **Pricing Model** | free |
| **Refresh Cadence** | quarterly |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | wcag-rules, accessibility-rules, html-checks, aria-checks, axe-rules-engine |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 95 | 23.75 |
| Data Quality | 20% | 25 | 5.00 |
| Licence & Cost (residency_bonus 0) | 15% | 57.5 | 8.63 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **56.63/100** |

---

### Comparison Table: Accessibility (OSS)

| Source | Refresh | RF | DQ | L&C | API | Comp | Rel | TOTAL |
|--------|---------|----|----|-----|-----|------|-----|-------|
| W3C WCAG 2.2 | static | 25.00 | 4.00 | 8.63 | 10.50 | 3.75 | 5.00 | **56.88** |
| axe-core | quarterly | 23.75 | 5.00 | 8.63 | 10.50 | 3.75 | 5.00 | **56.63** |

**Recommendation for Category 5 (Accessibility)**: Bundle both — WCAG 2.2 as the normative ruleset and axe-core as the CI executable validator.

---

## Category 6: Reference / UK-Gov — Classification & Cryptography

**Requirements Addressed**: FR-012, INT-007, NFR-SEC-003, NFR-C-001

The two UK-Gov sources in this bucket — **NCSC Cryptography Guidance** and **HMG Government Security Classifications Policy** — are rendered as Sub-bucket 2B sources by topical adjacency. Re-emitted here for traceability:

---

### Source 6A: NCSC Cryptography Guidance (UK Gov Open Data)

**Provider**: NCSC
**Source Name**: NCSC Cryptography Guidance
**Citation**: `[NCSC-CRYPTO-1]`
**Fetched From**: <https://www.ncsc.gov.uk/collection/topics/cryptography>
**Confidence**: medium

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | ad-hoc |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | cryptography, hmg-approved-primitives, key-management |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 100 | 25.00 |
| Data Quality | 20% | 30 | 6.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 25 | 3.75 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **65.25/100** |

> **Authoritative for NFR-SEC-003 / INT-007** — UK-Gov override of NIST for HMG-approved primitives.

---

### Source 6B: HMG Government Security Classifications Policy (UK Gov Open Data)

**Provider**: Cabinet Office
**Source Name**: HMG Government Security Classifications Policy
**Citation**: `[CO-GSCP-1]`
**Fetched From**: <https://www.gov.uk/government/publications/government-security-classifications>
**Confidence**: high

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **Hosted In** | GB |
| **Certifications** | OGL-v3 |
| **Licence Type** | OGL-v3 |
| **Pricing Model** | open-data |
| **Refresh Cadence** | annual |
| **Authentication Required** | false |
| **Authentication Method** | none |
| **Data Categories Supported** | security-classification, official, secret, top-secret, handling-rules |

**Evaluation Score**:

| Criterion | Weight | Raw | Weighted |
|-----------|--------|-----|----------|
| Requirements Fit | 25% | 100 | 25.00 |
| Data Quality | 20% | 15 | 3.00 |
| Licence & Cost (residency_bonus +10) | 15% | 100 | 15.00 |
| API Quality | 15% | 70 | 10.50 |
| Compliance | 15% | 35 | 5.25 |
| Reliability | 10% | 50 | 5.00 |
| **Total** | **100%** | | **63.75/100** |

---

### Comparison Table: Classification & Cryptography (UK-Gov reference)

| Source | Provider | Refresh | RF | DQ | L&C | API | Comp | Rel | TOTAL |
|--------|----------|---------|----|----|-----|-----|------|-----|-------|
| NCSC Cryptography Guidance | NCSC | ad-hoc | 25.00 | 6.00 | 15.00 | 10.50 | 3.75 | 5.00 | **65.25** |
| HMG GSCP | Cabinet Office | annual | 25.00 | 3.00 | 15.00 | 10.50 | 5.25 | 5.00 | **63.75** |

**Recommendation for Category 6**: Bundle both at build time. NCSC Cryptography Guidance is authoritative for HMG-approved primitives (NFR-SEC-003 / INT-007); HMG GSCP for classification marking (FR-012 / NFR-C-001).

---

## Evaluation Matrix

### Overall Scoring Summary (top sources per category)

| Category / Bucket | Recommended Source(s) | Type | Top Score | Annual Cost | Lane |
|---|---|---|---|---|---|
| 1. Company / Procurement | Companies House Public Data API + FTS OCDS API + Contracts Finder API + Digital Marketplace G-Cloud | uk-gov | 82.75 / 78.25 / 73.25 / 72.75 / 55.50 | £0 | B |
| 2A. Vulnerability Feeds | GHSA + NIST NVD + OSV.dev + EPSS | free | 77.75 / 76.00 / 75.38 / 65.88 | £0 | A |
| 2B. UK-Gov Accreditation | NCSC RSS + NCSC Threat Reports + Secure by Design + NCSC CAF | uk-gov | 67.75 / 66.25 / 65.50 / 63.75 | £0 | A |
| 3. Identity Schemas | IANA OAuth + OIDC Core + OIDC Discovery | oss | 59.13 / 54.38 / 53.13 | £0 | C |
| 5. Accessibility | W3C WCAG 2.2 + axe-core | oss | 56.88 / 56.63 | £0 | C |
| 6. Classification & Crypto | NCSC Cryptography Guidance + HMG GSCP | uk-gov | 65.25 / 63.75 | £0 | C |
| **TOTAL** | | | **Avg: ~65** | **£0/year** | — |

### Evaluation Criteria Explained

| Criterion | Weight | What It Measures |
|-----------|--------|-----------------|
| **Requirements Fit** | 25% | Coverage of required fields against the requirement |
| **Data Quality** | 20% | Refresh cadence, completeness, accuracy |
| **Licence & Cost** | 15% | Licence terms, pricing; uk-gov rubric applies +10 GB residency / −5 non-GB |
| **API Quality** | 15% | Authentication method, documentation, versioning |
| **Compliance** | 15% | OGL-v3 / GDPR / ISO27001 / SOC2 / NCSC-CAF / G-Cloud listing bonuses |
| **Reliability** | 10% | Rate-limit headroom, vendor stability |

---

## Data Integration Architecture

### Integration Patterns by Source

| Source | Lane | Pattern | Auth | Caching | Error Handling | Monitoring |
|--------|------|---------|------|---------|----------------|------------|
| Companies House Public Data API | B | REST on-demand | api-key | TTL 24h | Retry 3x + circuit breaker | Health check + DPA log |
| Companies House Developer Hub | B | REST on-demand | api-key | TTL 24h | Retry 3x | Health check |
| Contracts Finder API | B | OAuth2 polling | oauth2 | TTL 24h | Skip if down | Daily success metric |
| FTS OCDS API | B | Polling | none | TTL 24h | Skip if down | Daily success metric |
| Digital Marketplace G-Cloud | B | Bulk pull | none | TTL 24h | Skip if down | Daily success metric |
| GHSA | A | REST polling (build pipeline) | oauth2 | TTL 1h | Retry 5x; degrade to OSV+NVD | Health check |
| NIST NVD | A | REST polling | api-key | TTL 6h | Tertiary backstop | Health check |
| OSV.dev | A | REST polling | none | TTL 1h | Degrade to GHSA+NVD | Health check |
| FIRST EPSS | A | Daily pull | none | TTL 24h | Skip if down (non-critical) | Daily success metric |
| NCSC RSS / Threat Reports | A | RSS polling | none | TTL 24h | Manual review on miss | Weekly digest |
| Secure by Design | A | Document fetch | none | Embedded per release | Manual review | Per-release diff |
| NCSC CAF | A | Document fetch | none | Embedded per release | Manual review | Per-release diff |
| HMG GSCP | C | Document fetch | none | Embedded in bundle | Build-time validator | Per-release diff |
| NCSC Cryptography Guidance | C | Document fetch | none | Embedded in bundle | Build-time validator | Per-release diff |
| W3C WCAG 2.2 | C | Document fetch | none | Embedded in bundle | Build-time validator | Per-release diff |
| axe-core | C | npm dependency | none | Pinned version | Build-time validator | Per-release diff |
| IANA / OIDF schemas | C | Document fetch | none | Embedded in bundle | Build-time validator | Per-release diff |

### Recommended Integration Architecture

```text
LANE A (vendor build / release engineering — outside customer boundary)
  CVE feeds (GHSA primary, OSV redundancy, NVD backstop, EPSS prioritisation)
       │
       ▼
  SBOM × CVE matcher  +  EPSS prioritisation
       │
       ▼
  Per-release evidence pack assembler
       ├── NCSC CAF mapping
       ├── Secure by Design mapping
       ├── JSP control mapping (release-pinned internal — see GAP-3)
       ├── NCSC Threat Reports / RSS (INT-010 inbound)
       └── Patch SLA evidence
       │
       ▼
  Signed release bundle (no outbound deps at runtime) ─► customer air-gap

LANE B (vendor pre-sales — outside customer boundary)
  Companies House Public Data API + Developer Hub ─► tier-eligibility decision
  FTS OCDS API + Contracts Finder API + Digital Marketplace G-Cloud ─► procurement signal pipeline

LANE C (build-time embed — bundled, no runtime fetch)
  HMG GSCP ─┐
  NCSC Cryptography Guidance ─┤
  W3C WCAG 2.2 + axe-core ─┼──► snapshot frozen into release bundle ──► runs inside customer boundary
  IANA OAuth + OIDC Core + OIDC Discovery ─┘
```

### Authentication and Access

| Source | Auth Method | Credentials | Registration | Lead Time |
|--------|-------------|-------------|--------------|-----------|
| Companies House (both APIs) | api-key | Free key | Self-service portal | Instant |
| GHSA | oauth2 / PAT | GitHub PAT | GitHub account | Instant |
| OSV.dev | none | n/a | n/a | n/a |
| NIST NVD | api-key | NIST key | Self-service | 1 day |
| FIRST EPSS | none | n/a | n/a | n/a |
| Contracts Finder API | oauth2 | OAuth client | gov.uk / CCS | 1–5 days |
| FTS OCDS API | none | n/a | n/a | n/a |
| NCSC / DSIT / MOD / GSCP | none | n/a | n/a | n/a |
| WCAG / axe-core / IANA / OIDF | none | n/a | n/a | n/a |

### Rate Limits and Capacity Planning

| Source | Rate Limit | Projected Usage | Headroom |
|--------|------------|-----------------|----------|
| Companies House Public Data | 120 / minute | ~50 / day | > 99% |
| GHSA | 83 / minute | ~1000 / build × 4 builds/day | adequate with caching |
| NIST NVD 2.0 | 100 / minute | ~100 / build | > 95% |
| OSV.dev | n/a | ~500 / build | > 99% |
| FIRST EPSS | 1000 / minute | daily pull | > 99% |

---

## Data Utility Analysis

### Utility by Source

| Source | Primary Use | Secondary Uses | Strategic Value | Combination Opportunities |
|--------|-------------|----------------|-----------------|--------------------------|
| Companies House Public Data API | BR-006 SME tier verification | (1) director conflict-of-interest scan; (2) sub-processor diligence | HIGH | + Digital Marketplace G-Cloud → SME-tier eligibility + competitor mapping |
| GHSA + OSV.dev + NVD | NFR-SEC-005 / 008 / DR-007 | (1) weekly LTS-line risk dashboards; (2) trend reports | HIGH | + EPSS → exploit-prediction-weighted prioritisation |
| FTS OCDS + Contracts Finder | BR-007 framework engagement | (1) competitor sovereign-EA bid intel; (2) pricing evidence for SOBC iteration | MEDIUM | + Digital Marketplace G-Cloud → end-to-end procurement signal |
| NCSC CAF + Secure by Design | Per-release evidence pack | (1) staff training material; (2) gap analysis on accreditation effort | HIGH | + GSCP + NCSC Crypto → unified UK sensitive-site control catalogue |
| HMG GSCP | FR-012 marking | (1) edit-time marking enforcement; (2) export-time classification banner | HIGH | + customer max-classification config → automatic per-deployment validation rules |
| W3C WCAG / axe-core | NFR-C-003 a11y CI | A11y Statement auto-generation per release | MEDIUM | Standalone |
| NCSC Cryptography Guidance | NFR-SEC-003 / INT-007 enforcement | (1) bundle-time crypto-config validator; (2) KMS allow-list | HIGH | + customer KMS metadata at install → in-boundary primitive enforcement |
| IANA OAuth + OIDC Core + OIDC Discovery | INT-001 / FR-007 schemas | Schema-only contract for customer IdP integrators | MEDIUM | Standalone |

### Common Secondary Use Patterns Identified

| Pattern | Source | Primary Use | Secondary Use | Value |
|---------|--------|-------------|---------------|-------|
| **Proxy Indicator** | EPSS | exploit probability | proxy for "should accreditator escalate?" | Accreditator confidence |
| **Cross-Domain Enrichment** | Companies House | SME flag | enriches due-diligence on sub-processors | Supply-chain trust |
| **Trend Detection** | GHSA + OSV | per-build CVE delta | reveals dependency-base health drift | Predicts R-3 materialisation |
| **Predictive Feature** | EPSS | patch prioritisation | feature for forecasting backlog burn-down | Release-planning input |

### Data Combination Opportunities

1. **SME-tier + Procurement Signal**: Companies House + FTS OCDS + Digital Marketplace → automated SME-tier eligibility decision *and* opportunity matching for tier-targeted outreach.
2. **CVE × EPSS × SBOM**: GHSA + OSV + NVD + EPSS + internal SBOM → 30-day exploit-prediction-weighted patch backlog driving NFR-SEC-008 7 / 30 / 90 SLAs.
3. **UK Sensitive-Site Control Catalogue**: NCSC CAF + Secure by Design + JSP refs + GSCP + NCSC Cryptography Guidance → single bundled reference set that drives both build-time validators and per-release accreditation evidence packs.

---

## Gap Analysis

### Requirements Without Suitable Data Sources

**GAP-1**: BR-007 / A-1 — DCPP Cyber Risk Profile per engagement

- **Reason**: DCPP Cyber Risk Profile is issued per-engagement to the supplier; no public registry. Vendor must wait for engagement-time issue and run a templated intake form.
- **Severity**: HIGH (process gap; not runtime gap)
- **Recommended Action**: Templated intake form + escalation via MOD framework owner relationship; track per-engagement.
- **Cost**: £0

**GAP-2**: NFR-SEC-003 — HMG-approved cryptographic primitive registry (machine-readable)

- **Reason**: HMG-approved cryptographic primitive registry — NCSC publishes guidance as PDF/HTML, not as a machine-readable feed. Mitigation: maintain internal versioned `crypto-allow-list.yaml` refreshed annually against NCSC publications.
- **Severity**: MEDIUM
- **Recommended Action**: Maintain internal versioned `crypto-allow-list.yaml`; refresh annually against NCSC publications as part of LTS evidence pack.
- **Cost**: £0

**GAP-3**: BR-004 / NFR-SEC-001 — JSP 440 / JSP 604 control catalogue (machine-readable)

- **Reason**: JSP 440 Defence Manual of Security is not publicly published in full (404 on gov.uk). JSP 604 has been withdrawn. Mitigation: maintain release-pinned internal control mapping with change-log per LTS issue.
- **Severity**: MEDIUM
- **Recommended Action**: Maintain release-pinned internal mapping file with change-log diff per LTS issue.
- **Cost**: £0

**GAP-4**: DR-002 / NFR-SEC-007 — UK personnel-clearance taxonomy

- **Reason**: UK personnel-clearance taxonomy (SC / DV / NPPV3) is policy-defined, not published as a registry. Mitigation: hard-code documented taxonomy and surface via customer IdP claim mapping.
- **Severity**: LOW
- **Recommended Action**: Hard-code documented taxonomy; surface via customer IdP claim mapping.
- **Cost**: £0

**GAP-5**: INT-008 — Defence-specific framework listings

- **Reason**: Defence-specific framework listings (DSP / Defence Crown frameworks beyond G-Cloud / DOS) are gated behind defence-customer access. Mitigation: vendor relationship-based engagement; private deal-pipeline log.
- **Severity**: MEDIUM (commercial gap, not technical)
- **Recommended Action**: Vendor-side relationship engagement with MOD framework owners; private deal-pipeline log.
- **Cost**: BAU sales effort

### Gap Summary

| Gap | Requirement | Severity | Recommended Action | Cost |
|-----|-------------|----------|-------------------|------|
| GAP-1 | BR-007 / A-1 | HIGH | Engagement intake form | £0 |
| GAP-2 | NFR-SEC-003 | MEDIUM | Internal `crypto-allow-list.yaml` | £0 |
| GAP-3 | BR-004 / NFR-SEC-001 | MEDIUM | Internal JSP mapping file | £0 |
| GAP-4 | DR-002 / NFR-SEC-007 | LOW | Hard-code taxonomy | £0 |
| GAP-5 | INT-008 | MEDIUM | Relationship engagement | BAU |

**Severity rule applied**: CRITICAL is reserved for runtime-blocking gaps. Per Principle 21 the runtime data-source surface is empty by design; therefore no gap here is CRITICAL — they are all vendor-side process matters.

---

## Recommendations & Shortlist

### Top 5 Recommended Sources

#### 1. Companies House Public Data API for SME Verification (Lane B)

**Overall Score**: **82.75 / 100**

**Rationale**: Authoritative UK source for company status; the only source that can definitively determine SME flag for the BR-006 cross-subsidy tiering. OGL-v3, GB-hosted, real-time, api-key authed.

**Key Strengths**:

- ✅ Authoritative — no substitute exists
- ✅ OGL-v3 + free + GB-hosted (best possible posture; +10 residency bonus)
- ✅ Real-time refresh

**Key Concerns**:

- ⚠️ Director PII triggers DPIA review — confirm Article 6(1)(c)/(e) lawful basis
- ⚠️ Compliance score 25 (no certs claimed) drags total down

**Cost**: Free | **Risk Level**: LOW

**Next Steps**:

- [ ] Register API key
- [ ] Run DPIA increment for director-PII processing (vendor-side)
- [ ] POC SME-flag determination logic against threshold rules

---

#### 2. Companies House Developer Hub (REST API) (Lane B)

**Overall Score**: **78.25 / 100**

**Rationale**: Companion endpoint to 1A — the search / officers / PSC surface. Same licence and posture; useful for company-search workflows.

**Cost**: Free | **Risk Level**: LOW

---

#### 3. GitHub Security Advisories REST API (GHSA) (Lane A)

**Overall Score**: **77.75 / 100**

**Rationale**: Real-time, ecosystem-aware, OAuth2-capable — the strongest single feed for NFR-SEC-008 patch SLAs and DR-007 SBOM enrichment.

**Key Strengths**:

- ✅ Real-time updates
- ✅ Strong ecosystem coverage (npm, PyPI, Maven, etc.)
- ✅ CC-BY-4.0 licence

**Key Concerns**:

- ⚠️ US-hosted (−5 in residency under uk-gov rubric, but Lane A so not runtime)
- ⚠️ Single-vendor concentration risk — mitigated by pairing with OSV.dev and NVD

**Cost**: Free | **Risk Level**: LOW

**Next Steps**:

- [ ] Provision GitHub PAT in build pipeline
- [ ] Wire into SBOM × CVE matcher
- [ ] Feed into per-release evidence pack assembler

---

#### 4. NIST National Vulnerability Database (NVD) API 2.0 (Lane A)

**Overall Score**: **76.00 / 100**

**Rationale**: Authoritative US-side CVE / CVSS / CPE / KEV surface. Cross-validation backstop for GHSA + OSV. CC0-1.0 licence.

**Cost**: Free | **Risk Level**: LOW

---

#### 5. OSV.dev Open Source Vulnerabilities API (Lane A — redundancy)

**Overall Score**: **75.38 / 100**

**Rationale**: Provides Principle 3 redundancy for GHSA. Apache-2.0, no auth required, real-time. Different curation lineage from GHSA so genuine redundancy.

**Cost**: Free | **Risk Level**: LOW

**Next Steps**:

- [ ] Implement parallel query against OSV alongside GHSA
- [ ] Difference-report job for divergent verdicts

---

## Impact on Data Model

> **Note**: An `ARC-002-DATA-*.md` artefact does not yet exist for this project. Findings below indicate the additions a future data model should include for **vendor-side tooling only** — no entities are added to the deployed sovereign system.

### New Entities from External Sources (Vendor-Side Only)

| Entity | Source | Description | Key Attributes | Sync Strategy | Lane |
|--------|--------|-------------|----------------|---------------|------|
| `ProspectCompany` | Companies House (Public Data + Developer Hub) | Vendor CRM extension for tier-eligibility | company_number, sme_flag, accounts_size, registered_office, officers, psc | API on-demand, TTL 24h | B |
| `CveAdvisory` | GHSA + NVD + OSV | Build-pipeline vulnerability record | cve_id, cvss_v31, epss_30d, affected_components, severity | Polling, TTL 1h | A |
| `ProcurementOpportunity` | FTS OCDS + Contracts Finder + Digital Marketplace | Vendor opportunity log | notice_id, framework, value_band, deadline | Daily pull | B |
| `AccreditationControl` | NCSC CAF + Secure by Design + JSP refs | Per-release evidence-pack control mapping | control_id, framework, version, evidence_link | Per-LTS refresh | A |
| `BundledReference` | GSCP + NCSC Cryptography + WCAG + axe-core + IANA + OIDF | Build-time embedded reference data | reference_set, version, sha256 | Per-release embed | C |

### New Relationships

| From Entity | To Entity | Relationship | Source |
|-------------|-----------|--------------|--------|
| `Customer` (existing) | `ProspectCompany` | 1:1 (when known) | Companies House |
| `ReleaseManifest` (existing DR-007) | `CveAdvisory` | N:M | GHSA + OSV + NVD |
| `ReleaseManifest` | `AccreditationControl` | N:M | NCSC CAF / SbD / JSP |
| `ReleaseManifest` | `BundledReference` | N:M | GSCP / NCSC Crypto / WCAG / axe-core / IANA / OIDF |

### Sync Strategy

| Source | Pattern | Frequency | Staleness Tolerance | Fallback |
|--------|---------|-----------|---------------------|----------|
| Companies House | API on-demand | Daily TTL | 24 h | Serve last-known + flag |
| GHSA | Polling | 1 h | 4 h | Degrade to OSV+NVD |
| OSV.dev | Polling | 1 h | 4 h | Degrade to GHSA+NVD |
| NIST NVD | Polling | 6 h | 24 h | Tertiary; non-blocking |
| EPSS | Daily pull | 24 h | 48 h | Skip if down |
| FTS / Contracts Finder / Digital Marketplace | Bulk pull | Daily | 48 h | Skip if down |
| NCSC RSS / Threat Reports | RSS polling | Daily | 7 d | Manual review |
| NCSC CAF / SbD / GSCP / NCSC Crypto | Per-release | Per LTS | n/a | Pinned snapshot |
| WCAG / axe-core / IANA / OIDF | Per-release | Per LTS | n/a | Pinned version |

---

## UK Government Open Data Opportunities

### TCoP Point 10: Make Better Use of Data

**Open Data Consumed**:

| Source | Dataset | Licence | Requirement | Status |
|--------|---------|---------|-------------|--------|
| Companies House | Public Data API | OGL-v3 | BR-006 | ✅ Recommended |
| Companies House | Developer Hub | OGL-v3 | BR-006 | ✅ Recommended |
| Cabinet Office (FTS) | OCDS API | OGL-v3 | BR-007, INT-008 | ✅ Recommended |
| Cabinet Office (FTS) | Public UI / OGL content | OGL-v3 | BR-007 | ⚙️ Secondary |
| CCS | Contracts Finder API | OGL-v3 | BR-007 | ✅ Recommended |
| CCS | Contracts Finder Public Service | OGL-v3 | BR-007 | ⚙️ Secondary |
| CCS | Digital Marketplace G-Cloud | OGL-v3 | INT-008 | ✅ Recommended |
| Cabinet Office | data.gov.uk CloudStore Catalogue | OGL-v3 | INT-008 | ⚙️ Tertiary |
| NCSC | CAF v3.x outcomes | OGL-v3 | NFR-SEC-002 | ✅ Recommended |
| NCSC | Cryptography Guidance | OGL-v3 | NFR-SEC-003, INT-007 | ✅ Recommended |
| NCSC | RSS Feeds (all-content) | OGL-v3 | INT-010 | ✅ Recommended |
| NCSC | Threat Reports | OGL-v3 | INT-010 | ✅ Recommended |
| DSIT | Secure by Design | OGL-v3 | NFR-SEC-001 | ✅ Recommended |
| Cabinet Office | HMG GSCP | OGL-v3 | FR-012, NFR-C-001 | ✅ Recommended |
| MOD | JSP 441 | OGL-v3 | NFR-SEC-001 | ⚙️ Partial |
| MOD | JSP 604 (Withdrawn) | OGL-v3 | NFR-SEC-001 | ⚙️ Historical |

**Open Data Publishing Opportunities**:

- The vendor's **CAF / SbD / JSP control mapping per release** could be published as supplier reference for other suppliers facing similar accreditation paths (subject to MOD release approval).
- The **`crypto-allow-list.yaml`** maintained against NCSC guidance (GAP-2 mitigation) could be shared with other suppliers if NCSC permits.

**Common Data Standards Used**:

- Companies House Company Number (CRN)
- CVE-ID (NIST/MITRE)
- CVSS v3.1 / v4
- OSV schema (Google/OpenSSF)
- WCAG 2.2 success-criterion identifiers
- OAuth Parameters (IANA)
- OIDC standard / profile claims (OpenID Foundation)

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

| Requirement | Source(s) | Score | Status | Notes |
|---|---|---|---|---|
| BR-006 | Companies House Public Data API | 82.75 | ✅ Matched | |
| BR-007 | Find a Tender Service (FTS) OCDS API + Contracts Finder API + Digital Marketplace G-Cloud | 72.75 | ✅ Matched | |
| BR-008 | — | — | ⚠️ Process-only | Reference customer engagement |
| INT-008 | Digital Marketplace G-Cloud + FTS OCDS API | 55.50 | ✅ Matched | See gap on Defence-specific frameworks |
| BR-004 | NCSC CAF + Secure by Design + (JSP gap) | 65.50 | ⚠️ Partial | JSP control catalogue gap (GAP-3) |
| BR-005 | GHSA + OSV.dev + NIST NVD | 77.75 | ✅ Matched | |
| FR-014 | GHSA + OSV.dev + NIST NVD + EPSS | 77.75 | ✅ Matched | |
| INT-010 | NCSC Threat Reports + GHSA | 77.75 | ✅ Matched | |
| NFR-SEC-001 | Secure by Design + (JSP gap) | 65.50 | ⚠️ Partial | See GAP-3 |
| NFR-SEC-002 | NCSC Cyber Assessment Framework (CAF) | 63.75 | ✅ Matched | Read RF (100), not total — annual cadence drags total down |
| NFR-SEC-005 | GHSA + OSV.dev + NIST NVD | 77.75 | ✅ Matched | |
| NFR-SEC-008 | GHSA + OSV.dev + EPSS | 77.75 | ✅ Matched | |
| DR-007 | GHSA + OSV.dev + NIST NVD | 77.75 | ✅ Matched | |
| FR-007 | IANA OAuth Parameters Registry + OpenID Connect Core 1.0 | 59.13 | ⚠️ Partial | Schema only; runtime IdP customer-controlled |
| FR-012 | HMG Government Security Classifications Policy | 63.75 | ✅ Matched | |
| INT-001 | IANA OAuth Parameters Registry + OpenID Connect Core / Discovery | 59.13 | ⚠️ Partial | Schema only; runtime IdP customer-controlled |
| INT-007 | NCSC Cryptography Guidance (allow-list) | 65.25 | ✅ Matched | |
| NFR-SEC-003 | NCSC Cryptography Guidance + (machine-readable gap) | 65.25 | ⚠️ Partial | See GAP-2 |
| NFR-SEC-007 | — | — | ❌ Gap | See GAP-4 |
| NFR-C-001 | HMG Government Security Classifications Policy | 63.75 | ✅ Matched | |
| NFR-C-003 | W3C WCAG 2.2 + axe-core | 56.88 | ✅ Matched | |
| INT-002 | — | — | ✅ Customer-controlled | Inside boundary |
| INT-003 | — | — | ✅ Customer-controlled | Inside boundary |
| INT-004 | — | — | ✅ Customer-controlled | Inside boundary |
| INT-005 | — | — | ✅ Customer-controlled | Inside boundary |
| INT-006 | — | — | ✅ Customer-controlled | Inside boundary |
| INT-009 | — | — | ✅ Customer-controlled | Inside boundary |
| DR-001..006 | — | — | ✅ Internal | Not external feeds |

### Coverage Summary

- ✅ **16 requirements (57%)** fully matched to external data sources
- ⚠️ **6 requirements (21%)** partial / process-only / schema-only
- ❌ **6 requirements (21%)** customer-controlled (by design — inside the air-gapped boundary)
- ⚙️ **1 requirement (DR-001..006)** internal data, no external feed expected

Treating customer-controlled and internal as "addressable by design" yields **~22 of 28 requirements (78.6%) addressable; 6 partial / schema-only (21.4%); 0 with no source — but 5 vendor-side process gaps**.

---

## Next Steps

### Immediate Actions (0–2 weeks)

1. Register API keys: Companies House (Public Data + Developer Hub), GitHub PAT (GHSA), NIST NVD, Contracts Finder OAuth client.
2. Stand up Lane A pipeline scaffolding for GHSA + OSV + NVD + EPSS pulls.
3. Confirm DPIA increment scope for Companies House director-PII processing (Lane B).
4. Snapshot WCAG 2.2 + axe-core, HMG GSCP, NCSC Cryptography Guidance, IANA OAuth + OIDC Core + OIDC Discovery as bundle-time reference set v1.

### Data Model Updates (2–4 weeks)

5. Run `/arckit:data-model` for project 002 — add the five vendor-side entities listed in "Impact on Data Model".
6. Run `/arckit:adr` — record ADR: "Sovereign system has zero external runtime data sources by design (anchored to Principle 21)".
7. Run `/arckit:adr` — record ADR: "Pair GHSA + OSV.dev + NVD as primary CVE feeds for build-pipeline redundancy".
8. Run `/arckit:dpia` — DPIA increment for vendor-side Companies House processing.

### Gap Resolution (4–8 weeks)

9. Build internal `crypto-allow-list.yaml` per GAP-2 mitigation (refreshed annually against NCSC guidance).
10. Build internal release-pinned JSP 440 / 604 control mapping per GAP-3 mitigation.
11. Build engagement intake form per GAP-1 mitigation.
12. Hard-code SC / DV / NPPV3 clearance taxonomy per GAP-4 mitigation; surface via IdP claim mapping.

### Integration (Ongoing)

13. Wire CVE × EPSS × SBOM matcher into per-release evidence pack assembler.
14. Difference-report job between GHSA, OSV, NVD verdicts.
15. Daily FTS OCDS + Contracts Finder + Digital Marketplace pull into vendor opportunity log.
16. Per-release diff log for bundled reference set (GSCP / NCSC Crypto / WCAG / axe-core / IANA / OIDF).

---

## Appendices

### Appendix A: Research Methodology

**Data Sources Searched**:

- UK Government open data portals: data.gov.uk, api.gov.uk, gov.uk publications
- NCSC publications and threat-report channel
- MOD Defence Digital publications via gov.uk
- Cabinet Office publications (FTS, GSCP)
- Crown Commercial Service (Contracts Finder, Digital Marketplace)
- DSIT (Secure by Design)
- Free vulnerability feeds: GHSA, NIST NVD, OSV.dev, FIRST EPSS
- W3C and Deque axe-core repositories
- IANA registries; OpenID Foundation specifications

**Evaluation Methodology**:

- Deterministic UK-Gov rubric (RF 25 / DQ 20 / L&C 15 / API 15 / Comp 15 / Rel 10)
- Licence & cost includes +10 GB residency / −5 non-GB modifier (visible per-source as `residency_bonus`)
- API quality scored deterministically by auth method
- Reliability scored deterministically by rate-limit band

**Limitations**:

- v1.1 is rendered under the proper reader / writer subagent split with schema-validated evidence — supersedes v1.0 (legacy single-agent, no schema validation).
- Pricing all £0 (free / OGL / OSS) — no commercial sources discovered or required.
- API quality assessed from documentation, not hands-on testing.
- Discovery valid for ~ 6 months given the pace of vulnerability-feed and gov.uk catalogue evolution.

### Appendix B: Glossary

- **API**: Application Programming Interface
- **CAF**: Cyber Assessment Framework (NCSC)
- **CC-BY-4.0** / **CC0-1.0**: Creative Commons licences
- **CRN**: Company Registration Number (Companies House)
- **CVE**: Common Vulnerabilities and Exposures
- **CVSS**: Common Vulnerability Scoring System
- **DCPP**: Defence Cyber Protection Partnership
- **DPA 2018**: Data Protection Act 2018
- **DSP**: Defence Sourcing Portal
- **EPSS**: Exploit Prediction Scoring System (FIRST.org)
- **FTS**: Find a Tender Service
- **GDPR**: General Data Protection Regulation (UK GDPR)
- **GHSA**: GitHub Security Advisories
- **GSCP**: Government Security Classifications Policy
- **JSP**: Joint Service Publication (MOD)
- **NCSC**: National Cyber Security Centre
- **NVD**: National Vulnerability Database (NIST)
- **OCDS**: Open Contracting Data Standard
- **OGL**: Open Government Licence
- **OIDC**: OpenID Connect
- **OSV**: Open Source Vulnerabilities
- **PII**: Personally Identifiable Information
- **PSC**: People with Significant Control (Companies House)
- **SBOM**: Software Bill of Materials
- **SbD**: Secure by Design (DSIT / MOD)
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
| ARC-002-DSCT-v1.0 | ARC-002-DSCT-v1.0.md | Data Source Discovery (prior version) | projects/002-arckit-sovereign/research/ | Superseded by this version (v1.1) |

### Citations

| Citation ID | URL |
|-------------|-----|
| CH-API-1 | <https://developer-specs.company-information.service.gov.uk/guides/rateLimiting> |
| CH-API-2 | <https://developer-specs.company-information.service.gov.uk/guides/authorisation> |
| CF-API-1 | <https://www.contractsfinder.service.gov.uk/apidocumentation> |
| FTS-API-1 | <https://www.find-tender.service.gov.uk/Developer/Documentation> |
| FTS-UI-1 | <https://www.find-tender.service.gov.uk/> |
| CF-UI-1 | <https://www.contractsfinder.service.gov.uk/> |
| DM-GC-1 | <https://www.applytosupply.digitalmarketplace.service.gov.uk/g-cloud/search> |
| DGU-CS-1 | <https://www.data.gov.uk/dataset/5462ae53-ebec-4464-ac8d-5325213fb4f9/cloudstore_catalogue_version> |
| IANA-OAUTH-1 | <https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml> |
| OIDF-CORE-1 | <https://openid.net/specs/openid-connect-core-1_0.html> |
| OIDF-DISC-1 | <https://openid.net/specs/openid-connect-discovery-1_0.html> |
| IANA-LIC-1 | <https://www.iana.org/help/licensing-terms> |
| GH-GHSA-1 | <https://docs.github.com/en/rest/security-advisories> |
| NIST-NVD-1 | <https://nvd.nist.gov/developers/start-here> |
| OSV-DEV-1 | <https://google.github.io/osv.dev/api/> |
| FIRST-EPSS-1 | <https://api.first.org/> |
| WCAG-22-1 | <https://www.w3.org/TR/WCAG22/> |
| AXE-CORE-1 | <https://github.com/dequelabs/axe-core> |
| NCSC-RSS-1 | <https://www.ncsc.gov.uk/information/rss-feeds> |
| NCSC-THREAT-1 | <https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports> |
| DSIT-SBD-1 | <https://www.gov.uk/government/publications/secure-by-design> |
| NCSC-CRYPTO-1 | <https://www.ncsc.gov.uk/collection/topics/cryptography> |
| NCSC-CAF-1 | <https://www.ncsc.gov.uk/collection/cyber-assessment-framework> |
| CO-GSCP-1 | <https://www.gov.uk/government/publications/government-security-classifications> |
| MOD-JSP441-1 | <https://assets.publishing.service.gov.uk/media/5a82b0d240f0b62305b93d65/2017-02121.pdf> |
| MOD-JSP604-1 | <https://www.gov.uk/government/publications/joint-service-publication-jsp-604-network-rules> |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:datascout` agent (orchestrator) + reader / writer subagent split with schema-validated evidence
**Generated on**: 2026-05-06
**ArcKit Version**: 4.16.3
**Project**: ArcKit as a Service (Sovereign Deployment)
**Model**: Claude Opus 4.7 (1M context)
