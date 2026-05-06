# Data Source Discovery: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.17.0 | **Command**: `/arckit:datascout`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-DSCT-v1.2 |
| **Document Type** | Data Source Discovery |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.2 |
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
| 1.1 | 2026-05-06 | ArcKit AI (datascout) | Refresh under reader / writer subagent split with schema-validated evidence. Re-scored 26 sources via deterministic uk-gov rubric; traceability expanded; gap list reaffirmed (5 vendor-side process gaps). | [PENDING] | [PENDING] |
| 1.2 | 2026-05-06 | ArcKit AI (datascout) | Refresh under proper reader/writer subagent split (4 buckets × reader, schema-validated evidence, deterministic uk-gov rubric scoring). Some evidence fields (e.g. licence_type / pricing_model on CH-API-1's rate-limiting page) not declared on the source page and so scored with `when_missing=50` — more conservative than v1.1's inferred provider-level facts. **Architectural conclusions unchanged from v1.1.** | [PENDING] | [PENDING] |

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
> The bundle that crosses the air-gap MUST be self-contained. This is the most important finding of this discovery and is preserved verbatim from v1.1.
>
> **What changed in v1.2.** Refresh under the proper reader/writer subagent split (4 readers × bucket). Same architectural conclusions as v1.1. Some evidence fields (e.g. `licence_type` / `pricing_model` on CH-API-1's rate-limiting page) not declared on the source page and so scored with `when_missing=50` — more conservative than v1.1 which inferred provider-level licence facts. The deterministic uk-gov rubric was applied to the schema-validated evidence with no LLM judgment in the score path.

### Key Findings

- **Companies House Developer Hub (Lane B, score 79.25)** — best fit for BR-006 SME-tier verification underpinning the cross-subsidy commercial model. OGL-v3, GB-hosted, real-time, basic-auth.
- **GHSA + NIST NVD + OSV.dev (Lane A, scores 77.75 / 76.50 / 75.38)** — triple-feed vulnerability stack for NFR-SEC-005 (SBOM integrity), NFR-SEC-008 (Critical 7d / High 30d / Medium 90d patch SLAs), DR-007 (release-manifest CVE enrichment), and INT-010 (inbound disclosure). Two-of-three minimum to satisfy Principle 3 redundancy at build time.
- **Contracts Finder API + Find a Tender API (Lane B, scores 77.25 / 75.75)** — authoritative procurement signal for BR-007 framework engagement (above- and below-threshold).
- **NCSC CAF + MOD Secure by Design + NCSC Threat Reports + JSP 440 (Lane A, scores 70.50 / 66.75 / 65.25 / 64.00)** — UK-side accreditation evidence-pack inputs. Annual / weekly cadences keep totals below the CVE feeds, but **read RF column, not total** — these are non-substitutable evidence inputs.
- **HMG GSCP + NCSC Cryptographic Guidance + W3C WCAG / axe-core + IANA OAuth Registry / OIDC (Lane C, scores 66.75 / 65.50 / 58.13 / 55.88 / 62.50 / 56.88)** — build-time reference taxonomies baked into the bundle to enforce classification marking (FR-012 / NFR-C-001), HMG-approved primitives (NFR-SEC-003 / INT-007), accessibility (NFR-C-003), and identity claim schemas (FR-007 / INT-001).

### Data Source Summary

| Source Type | Count | Cost Range | Key Providers |
|-------------|-------|------------|---------------|
| **UK Government Open Data** | 16 | Free (OGL-v3) | Companies House, Cabinet Office (FTS, Contracts Finder, GSCP, data.gov.uk), CCS (Digital Marketplace), NCSC (CAF, RSS, Threat Reports, Crypto Guidance), MOD (SbD, JSP 440, JSP 604) |
| **Commercial APIs** | 0 | n/a | None — sovereign runtime forbids them; vendor-side needs met by free / open feeds |
| **Free/Freemium APIs** | 4 | Free (rate-limited) | GitHub (GHSA), NIST (NVD), Google / OpenSSF (OSV.dev), FIRST.org (EPSS) |
| **Open Source Datasets / Rulesets** | 6 | Free (CC0 / CC-BY / Apache / W3C) | IANA (OAuth Parameters Registry, Licensing Terms), OpenID Foundation (OIDC Core, OIDC Discovery), W3C (WCAG 2.2), Deque (axe-core) |
| **TOTAL** | **26** | **£0/year** | — |

### Top Recommended Sources

**Shortlist for integration**:

1. **Companies House Developer Hub** for company / SME verification: OGL-v3, GB-hosted, real-time, basic auth — score **79.25/100**.
2. **GitHub Security Advisories REST API (GHSA)** for vulnerability / SBOM enrichment: real-time, CC-BY-4.0 — score **77.75/100**.
3. **Contracts Finder API (OCDS)** for procurement intelligence: OGL-v3, GB-hosted, daily, OAuth2 — score **77.25/100**.
4. **NIST NVD API 2.0** for CVE / CVSS / CPE cross-validation: hourly refresh, CC0-1.0 — score **76.50/100**.
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
- Data fields needed: CVE id, CVSS, EPSS, advisory text, OSV records, GHSA records, NCSC CAF outcomes, MOD SbD principles, JSP control catalogue, NCSC threat reports
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

> **Note**: Categories below match the (category, source_type) buckets used by the reader/writer split. Per-source profiles are spawned to `data-sources/{provider-slug}-profile.md`.

---

## Category 1: Company / Procurement — UK-Gov bucket

**Requirements Addressed**: BR-006, BR-007, INT-008

**Why This Category**: Vendor-side (Lane B) commercial workflows — SME-tier verification for cross-subsidy and procurement-framework engagement.

---

### Source 1A: Companies House Developer Hub (CH-DH-1)

**Provider**: Companies House (developer.company-information.service.gov.uk)

**Description**: Authoritative UK company register — companies, officers, filings, charges, insolvencies, persons-with-significant-control. Authentication required (basic).

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | Open data (free) |
| **Format** | JSON / REST |
| **API Endpoint** | https://developer.company-information.service.gov.uk/authentication |
| **Authentication** | Basic |
| **Rate Limits** | (rate-limit doc fetched separately as CH-API-1) |
| **Update Frequency** | Real-time |
| **Coverage** | UK-wide (companies, officers, filings, charges, insolvencies, PSC) |
| **GDPR Status** | Public register; some fields PII (officers, PSC) |
| **UK Data Residency** | Yes (GB-hosted) |

**Requirements Fit**: ✅ BR-006

**Evaluation Score**:

| Criterion | Weight | Weighted |
|-----------|--------|----------|
| Requirements Fit | 25% | 25.00/25 |
| Data Quality | 20% | 20.00/20 |
| License & Cost | 15% | 15.00/15 |
| API Quality | 15% | 9.00/15 |
| Compliance | 15% | 5.25/15 |
| Reliability | 10% | 5.00/10 |
| **Total** | **100%** | **79.25/100** |

---

### Source 1B: Contracts Finder API (OCDS) (CF-API-1)

**Provider**: Crown Commercial Service

**Description**: OCDS-format procurement notices, releases, records, contract awards, CPV codes — daily refresh, OAuth2.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | Open data |
| **API Endpoint** | https://www.contractsfinder.service.gov.uk/apidocumentation |
| **Authentication** | OAuth2 |
| **Update Frequency** | Daily |
| **UK Data Residency** | Yes (GB-hosted) |

**Requirements Fit**: ✅ BR-007, INT-008

**Evaluation Score**:

| Criterion | Weight | Weighted |
|-----------|--------|----------|
| Requirements Fit | 25% | 22.50/25 |
| Data Quality | 20% | 16.00/20 |
| License & Cost | 15% | 15.00/15 |
| API Quality | 15% | 13.50/15 |
| Compliance | 15% | 5.25/15 |
| Reliability | 10% | 5.00/10 |
| **Total** | **100%** | **77.25/100** |

---

### Source 1C: Find a Tender Service REST API (OCDS) (FTS-API-1)

**Provider**: Cabinet Office / Crown Commercial Service

**Description**: Above-threshold tender notices in OCDS format, daily, API-key authed.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | Open data |
| **API Endpoint** | https://www.find-tender.service.gov.uk/apidocumentation |
| **Authentication** | API key |
| **Update Frequency** | Daily |
| **UK Data Residency** | Yes (GB-hosted) |

**Requirements Fit**: ✅ BR-007, INT-008

**Evaluation Score**: **75.75/100** (RF 22.50 / DQ 16.00 / L&C 15.00 / API 12.00 / Comp 5.25 / Rel 5.00)

---

### Source 1D: Companies House Public Data API — Rate Limiting Policy (CH-API-1)

**Provider**: Companies House

**Description**: Rate-limiting policy page for the Public Data API: 120 req/minute (5-minute window). Cited as evidence for capacity planning.

**Key Details**:

| Attribute | Value |
|-----------|-------|
| **License** | [NOT EVALUATED on source page — `when_missing=50`] |
| **Pricing** | [NOT EVALUATED on source page — `when_missing=50`] |
| **API Endpoint** | https://developer-specs.company-information.service.gov.uk/guides/rateLimiting |
| **Authentication** | Yes (basic at provider level) |
| **Rate Limits** | 120 req/min |
| **UK Data Residency** | Yes (GB-hosted) |

**Requirements Fit**: ✅ BR-006

**Evaluation Score**: **72.25/100** (RF 25.00 / DQ 20.00 / L&C 9.00 / API 7.50 / Comp 3.75 / Rel 7.00)

---

### Source 1E: Find a Tender Service — Public (FTS-PUB-1)

**Provider**: Cabinet Office / Crown Commercial Service

**Score**: **71.75/100** — public site (no auth) variant of FTS for human / scraper consumption only. Daily refresh. License OGL-v3.

---

### Source 1F: Contracts Finder — Public (CF-PUB-1)

**Provider**: Crown Commercial Service (data.gov.uk archive)

**Score**: **70.50/100** — public archive variant. License OGL-v3.

---

### Source 1G: data.gov.uk — Open Contracting Datasets (DGU-1)

**Provider**: GOV.UK / Cabinet Office

**Score**: **69.25/100** — aggregated open-contracting datasets (CF + FTS notices unified).

---

### Source 1H: Digital Marketplace — G-Cloud Catalogue (GCLOUD-1)

**Provider**: Crown Commercial Service / Government Digital Service

**Score**: **65.50/100** — G-Cloud-14, DOS-6, Crown-Commercial framework listings. Annual refresh; lower DQ score reflects annual cadence vs daily/real-time peers.

---

### Comparison Table: Company / Procurement (UK-Gov)

| Criterion | CH-DH-1 | CF-API-1 | FTS-API-1 | CH-API-1 | FTS-PUB-1 | CF-PUB-1 | DGU-1 | GCLOUD-1 |
|-----------|---------|----------|-----------|----------|-----------|----------|-------|----------|
| **License** | OGL-v3 | OGL-v3 | OGL-v3 | (page) | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 |
| **Cost (Annual)** | £0 | £0 | £0 | £0 | £0 | £0 | £0 | £0 |
| **Coverage** | UK-wide | UK-wide | UK-wide | UK-wide | UK-wide | UK-wide | UK-wide | UK-wide |
| **Freshness** | Real-time | Daily | Daily | Real-time | Daily | Daily | Daily | Annual |
| **Auth** | Basic | OAuth2 | API key | Basic | None | None | None | None |
| **Requirements Fit** | 25.00 | 22.50 | 22.50 | 25.00 | 20.00 | 18.75 | 17.50 | 20.00 |
| **Data Quality** | 20.00 | 16.00 | 16.00 | 20.00 | 16.00 | 16.00 | 16.00 | 3.00 |
| **License & Cost** | 15.00 | 15.00 | 15.00 | 9.00 | 15.00 | 15.00 | 15.00 | 15.00 |
| **API Quality** | 9.00 | 13.50 | 12.00 | 7.50 | 10.50 | 10.50 | 10.50 | 10.50 |
| **Compliance** | 5.25 | 5.25 | 5.25 | 3.75 | 5.25 | 5.25 | 5.25 | 12.00 |
| **Reliability** | 5.00 | 5.00 | 5.00 | 7.00 | 5.00 | 5.00 | 5.00 | 5.00 |
| **TOTAL SCORE** | **79.25** | **77.25** | **75.75** | **72.25** | **71.75** | **70.50** | **69.25** | **65.50** |

**Recommendation for Company / Procurement**: **Companies House Developer Hub (CH-DH-1)** for BR-006 SME verification (authoritative). Pair with **Contracts Finder API (CF-API-1)** + **Find a Tender API (FTS-API-1)** for BR-007 / INT-008 procurement intelligence. All Lane B vendor-side; no runtime calls from sovereign deployment.

---

## Category 2: Reference / Accreditation — UK-Gov bucket

**Requirements Addressed**: BR-004, NFR-SEC-001, NFR-SEC-002, NFR-SEC-003, FR-012, NFR-C-001

**Why This Category**: Build-time taxonomies and accreditation evidence-pack inputs. Lane A (vendor build) and Lane C (build-time reference baked into bundle).

---

### Source 2A: NCSC Cyber Assessment Framework (NCSC-CAF-1)

**Provider**: NCSC

**Description**: NCSC CAF v3.x — cyber-security framework, CAF principles, essential services, CNI alignment.

| Attribute | Value |
|-----------|-------|
| **License** | OGL-v3 |
| **Pricing** | Open data |
| **URL** | https://www.ncsc.gov.uk/collection/cyber-assessment-framework |
| **Authentication** | None |
| **Update Frequency** | Ad-hoc |
| **UK Data Residency** | Yes (GB-hosted) |

**Requirements Fit**: ✅ NFR-SEC-002, BR-004

**Evaluation Score**: **70.50/100** (RF 25.00 / DQ 6.00 / L&C 15.00 / API 10.50 / Comp 9.00 / Rel 5.00)

---

### Source 2B: HMG Government Security Classifications Policy (HMG-GSCP-1)

**Provider**: Cabinet Office

**Description**: HMG GSCP — OFFICIAL / SECRET / TOP-SECRET classifications and handling policy. Build-time reference.

**Score**: **66.75/100** (RF 25.00 / DQ 6.00 / L&C 15.00 / API 10.50 / Comp 5.25 / Rel 5.00). License OGL-v3. ✅ FR-012, NFR-C-001.

---

### Source 2C: MOD Secure by Design (DSIT-SBD-1)

**Provider**: Ministry of Defence (Digital MOD)

**Description**: Secure by Design / defence cyber / risk-management / supply-chain-security / through-life-security guidance.

**Score**: **66.75/100** (RF 25.00 / DQ 6.00 / L&C 15.00 / API 10.50 / Comp 5.25 / Rel 5.00). License OGL-v3. ✅ NFR-SEC-001, BR-004.

---

### Source 2D: NCSC Cryptography Guidance Collection (NCSC-CRYPTO-1)

**Provider**: NCSC

**Description**: Cryptographic primitives, CAPS, high-grade, post-quantum, cryptographic products. HMG-approved primitive allow-list source for INT-007.

**Score**: **65.50/100** (RF 23.75 / DQ 6.00 / L&C 15.00 / API 10.50 / Comp 5.25 / Rel 5.00). License OGL-v3. ✅ NFR-SEC-003, INT-007.

---

### Source 2E: NCSC Threat Reports (NCSC-THREAT-1)

**Provider**: NCSC

**Description**: Weekly threat-intelligence summaries — accreditation evidence-pack input.

**Score**: **65.25/100** (RF 17.50 / DQ 12.00 / L&C 15.00 / API 10.50 / Comp 5.25 / Rel 5.00). License OGL-v3. ✅ BR-004.

---

### Source 2F: NCSC RSS Feeds (NCSC-RSS-1)

**Provider**: NCSC

**Description**: RSS feed of NCSC threat reports / news — programmatic monitoring.

**Score**: **64.00/100** (RF 16.25 / DQ 12.00 / L&C 15.00 / API 10.50 / Comp 5.25 / Rel 5.00). License OGL-v3. ✅ BR-004.

---

### Source 2G: JSP 440 Defence Manual of Security (MOD-JSP440-1)

**Provider**: Ministry of Defence

**Description**: Defence security / personnel / physical / CIS / vetting control catalogue (released to industry as PDF).

**Score**: **64.00/100** (RF 23.75 / DQ 6.00 / L&C 15.00 / API 9.00 / Comp 5.25 / Rel 5.00). License OGL-v3. ✅ NFR-SEC-001, BR-004.

---

### Source 2H: JSP 604 Defence Networks Governance (Withdrawn) (MOD-JSP604-1)

**Provider**: Ministry of Defence

**Description**: Defence network rules / ICT governance — **formally withdrawn**, retained as historical reference.

**Score**: **52.25/100** (RF 12.50 / DQ 4.00 / L&C 15.00 / API 10.50 / Comp 5.25 / Rel 5.00). License OGL-v3. Status: withdrawn (see PROCESS-1 gap). ✅ NFR-SEC-001 (partial, historical).

---

### Comparison Table: Reference / Accreditation (UK-Gov)

| Criterion | NCSC-CAF-1 | HMG-GSCP-1 | DSIT-SBD-1 | NCSC-CRYPTO-1 | NCSC-THREAT-1 | NCSC-RSS-1 | MOD-JSP440-1 | MOD-JSP604-1 |
|-----------|------------|------------|------------|---------------|---------------|-----------|--------------|--------------|
| **License** | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 | OGL-v3 |
| **Freshness** | Ad-hoc | Ad-hoc | Ad-hoc | Ad-hoc | Weekly | Weekly | Ad-hoc | Static |
| **Auth** | None | None | None | None | None | None | Basic | None |
| **Requirements Fit** | 25.00 | 25.00 | 25.00 | 23.75 | 17.50 | 16.25 | 23.75 | 12.50 |
| **Data Quality** | 6.00 | 6.00 | 6.00 | 6.00 | 12.00 | 12.00 | 6.00 | 4.00 |
| **License & Cost** | 15.00 | 15.00 | 15.00 | 15.00 | 15.00 | 15.00 | 15.00 | 15.00 |
| **API Quality** | 10.50 | 10.50 | 10.50 | 10.50 | 10.50 | 10.50 | 9.00 | 10.50 |
| **Compliance** | 9.00 | 5.25 | 5.25 | 5.25 | 5.25 | 5.25 | 5.25 | 5.25 |
| **Reliability** | 5.00 | 5.00 | 5.00 | 5.00 | 5.00 | 5.00 | 5.00 | 5.00 |
| **TOTAL SCORE** | **70.50** | **66.75** | **66.75** | **65.50** | **65.25** | **64.00** | **64.00** | **52.25** |

**Recommendation for Reference / Accreditation**: All eight are non-substitutable normative references — read by Requirements Fit (RF), not by total score. The whole stack is needed to assemble the per-LTS-release accreditation evidence pack (BR-004) plus build-time crypto/classification taxonomies (Lane C).

---

## Category 3: Vulnerability / SBOM — Free bucket

**Requirements Addressed**: NFR-SEC-005, NFR-SEC-008, FR-014, BR-005, DR-007, INT-010

**Why This Category**: Lane A (vendor build / release-engineering). Three-of-three feed redundancy required by Principle 3 to satisfy Critical-7d patch SLA.

---

### Source 3A: GitHub Security Advisories Global Advisories REST API (GHSA-1)

**Provider**: GitHub

| Attribute | Value |
|-----------|-------|
| **License** | CC-BY-4.0 |
| **Pricing** | Free |
| **URL** | https://docs.github.com/en/rest/security-advisories/global-advisories |
| **Authentication** | API key (optional) |
| **Rate Limit** | 83 req/min |
| **Update Frequency** | Real-time |
| **UK Data Residency** | No (US-hosted, −5 penalty applied) |

**Score**: **77.75/100** (RF 23.75 / DQ 20.00 / L&C 12.75 / API 10.50 / Comp 3.75 / Rel 7.00). ✅ NFR-SEC-005, NFR-SEC-008, FR-014, BR-005, DR-007, INT-010.

---

### Source 3B: NIST NVD API 2.0 (NVD-1)

**Provider**: NIST

| Attribute | Value |
|-----------|-------|
| **License** | CC0-1.0 |
| **Pricing** | Free |
| **URL** | https://nvd.nist.gov/developers/start-here |
| **Authentication** | API key (optional) |
| **Rate Limit** | 100 req/min |
| **Update Frequency** | Hourly |

**Score**: **76.50/100** (RF 23.75 / DQ 18.00 / L&C 13.50 / API 10.50 / Comp 3.75 / Rel 7.00). ✅ NFR-SEC-005, NFR-SEC-008, FR-014, BR-005, DR-007, INT-010.

---

### Source 3C: OSV.dev Open Source Vulnerabilities API (OSV-1)

**Provider**: Google / OpenSSF

| Attribute | Value |
|-----------|-------|
| **License** | Apache-2.0 |
| **Pricing** | Free |
| **URL** | https://google.github.io/osv.dev/api/ |
| **Authentication** | None |
| **Update Frequency** | Real-time |

**Score**: **75.38/100** (RF 23.75 / DQ 20.00 / L&C 12.38 / API 10.50 / Comp 3.75 / Rel 5.00). ✅ NFR-SEC-005, NFR-SEC-008, FR-014, BR-005, DR-007, INT-010.

---

### Source 3D: FIRST EPSS API (EPSS-1)

**Provider**: FIRST.org

| Attribute | Value |
|-----------|-------|
| **License** | Unknown (`when_missing=50`) |
| **Pricing** | Free |
| **URL** | https://api.first.org/ |
| **Authentication** | None |
| **Rate Limit** | 1000 req/min |
| **Update Frequency** | Daily |

**Score**: **64.63/100** (RF 17.50 / DQ 16.00 / L&C 7.88 / API 10.50 / Comp 3.75 / Rel 9.00). ✅ NFR-SEC-005, DR-007. Provides EPSS scoring (exploit prediction) — supplementary signal alongside CVSS.

---

### Comparison Table: Vulnerability / SBOM (Free)

| Criterion | GHSA-1 | NVD-1 | OSV-1 | EPSS-1 |
|-----------|--------|-------|-------|--------|
| **License** | CC-BY-4.0 | CC0-1.0 | Apache-2.0 | Unknown |
| **Freshness** | Real-time | Hourly | Real-time | Daily |
| **Rate Limit** | 83/min | 100/min | (none stated) | 1000/min |
| **Hosted in** | US | US | US | US |
| **Requirements Fit** | 23.75 | 23.75 | 23.75 | 17.50 |
| **Data Quality** | 20.00 | 18.00 | 20.00 | 16.00 |
| **License & Cost** | 12.75 | 13.50 | 12.38 | 7.88 |
| **API Quality** | 10.50 | 10.50 | 10.50 | 10.50 |
| **Compliance** | 3.75 | 3.75 | 3.75 | 3.75 |
| **Reliability** | 7.00 | 7.00 | 5.00 | 9.00 |
| **TOTAL SCORE** | **77.75** | **76.50** | **75.38** | **64.63** |

**Recommendation for Vulnerability / SBOM**: Adopt all three of GHSA + NVD + OSV at vendor build time (Principle 3 redundancy). Supplement with EPSS for exploit-prediction prioritisation. None ever called from runtime sovereign deployment.

---

## Category 4: Reference Schemas — OSS bucket

**Requirements Addressed**: FR-007, INT-001, NFR-C-003

**Why This Category**: Lane C (build-time reference baked into bundle) — identity claim schemas, accessibility rulesets.

---

### Source 4A: IANA OAuth Parameters Registry (IANA-OAUTH-1)

**Provider**: IANA. License CC0-1.0. **Score 62.50/100** (RF 23.75 / DQ 6.00 / L&C 13.50 / API 10.50 / Comp 3.75 / Rel 5.00). ✅ FR-007, INT-001.

---

### Source 4B: W3C WCAG 2.2 (WCAG22-1)

**Provider**: W3C. License Unknown (`when_missing=50`). **Score 58.13/100** (RF 25.00 / DQ 6.00 / L&C 7.88 / API 10.50 / Comp 3.75 / Rel 5.00). ✅ NFR-C-003.

---

### Source 4C: OpenID Connect Core 1.0 (OIDC-CORE-1)

**Provider**: OpenID Foundation. License Unknown. **Score 56.88/100** (RF 23.75 / DQ 6.00 / L&C 7.88 / API 10.50 / Comp 3.75 / Rel 5.00). ✅ FR-007, INT-001.

---

### Source 4D: Deque axe-core (AXE-1)

**Provider**: Deque Labs. License Unknown (MPL-2.0 at provider level, not declared on repo root tested). **Score 55.88/100** (RF 23.75 / DQ 5.00 / L&C 7.88 / API 10.50 / Comp 3.75 / Rel 5.00). ✅ NFR-C-003.

---

### Source 4E: OpenID Connect Discovery 1.0 (OIDC-DISC-1)

**Provider**: OpenID Foundation. License Unknown. **Score 55.63/100** (RF 22.50 / DQ 6.00 / L&C 7.88 / API 10.50 / Comp 3.75 / Rel 5.00). ✅ FR-007, INT-001.

---

### Source 4F: IANA Protocol Registries Licensing Terms (IANA-LIC-1)

**Provider**: IANA. License CC0-1.0. **Score 49.25/100**. Cited as evidence supporting CC0 status of IANA-OAUTH-1; no direct requirement match.

---

### Comparison Table: Reference Schemas (OSS)

| Criterion | IANA-OAUTH-1 | WCAG22-1 | OIDC-CORE-1 | AXE-1 | OIDC-DISC-1 | IANA-LIC-1 |
|-----------|--------------|----------|-------------|-------|-------------|-----------|
| **License** | CC0-1.0 | Unknown | Unknown | Unknown | Unknown | CC0-1.0 |
| **Freshness** | Ad-hoc | Ad-hoc | Ad-hoc | Quarterly | Ad-hoc | Static |
| **Hosted in** | US | US | US | US | US | US |
| **Requirements Fit** | 23.75 | 25.00 | 23.75 | 23.75 | 22.50 | 12.50 |
| **Data Quality** | 6.00 | 6.00 | 6.00 | 5.00 | 6.00 | 4.00 |
| **License & Cost** | 13.50 | 7.88 | 7.88 | 7.88 | 7.88 | 13.50 |
| **API Quality** | 10.50 | 10.50 | 10.50 | 10.50 | 10.50 | 10.50 |
| **Compliance** | 3.75 | 3.75 | 3.75 | 3.75 | 3.75 | 3.75 |
| **Reliability** | 5.00 | 5.00 | 5.00 | 5.00 | 5.00 | 5.00 |
| **TOTAL SCORE** | **62.50** | **58.13** | **56.88** | **55.88** | **55.63** | **49.25** |

**Recommendation for Reference Schemas**: All five primary references (1A/4A IANA-OAUTH, WCAG22, OIDC-CORE, AXE, OIDC-DISC) baked into the bundle as static data. IANA-LIC-1 retained as evidence trail for CC0 provenance.

---

## Evaluation Matrix

### Overall Scoring Summary

| Category | Top Source | Type | Score | Annual Cost | Lane |
|----------|-----------|------|-------|-------------|------|
| Company / Procurement | Companies House Developer Hub | UK-Gov open | 79.25/100 | £0 | B |
| Reference / Accreditation | NCSC CAF | UK-Gov open | 70.50/100 | £0 | A/C |
| Vulnerability / SBOM | GHSA | Free | 77.75/100 | £0 | A |
| Reference Schemas | IANA OAuth Registry | OSS | 62.50/100 | £0 | C |
| **TOTAL** | (26 sources) | | **Avg ≈ 66/100** | **£0/year** | — |

### Evaluation Criteria Explained

| Criterion | Weight | What It Measures |
|-----------|--------|-----------------|
| **Requirements Fit** | 25% | Does the source cover the required data fields, scope, granularity? |
| **Data Quality** | 20% | Accuracy, completeness, freshness, declared SLA |
| **License & Cost** | 15% | License clarity (OGL/CC0/CC-BY/Apache); cost sustainability |
| **API Quality** | 15% | Auth mode, rate limits, documentation, format |
| **Compliance** | 15% | UK data residency, sector certifications |
| **Reliability** | 10% | Provider stability, refresh cadence consistency |

UK-Gov rubric applies +10 GB residency bonus and −5 non-GB residency penalty.

---

## Data Integration Architecture

### Integration Patterns by Source (vendor-side only — no runtime calls)

| Source | Lane | Pattern | Auth | Caching | Used At |
|--------|------|---------|------|---------|---------|
| Companies House Developer Hub | B | REST polling | Basic | TTL: 24h | Vendor pre-sales pipeline |
| Contracts Finder API / FTS API | B | OCDS daily pull | OAuth2 / API key | TTL: 24h | Vendor pre-sales pipeline |
| GHSA / NVD / OSV | A | REST polling | API key (opt) / none | Per-build snapshot | Vendor build pipeline |
| EPSS | A | REST polling | None | Daily snapshot | Vendor build pipeline |
| NCSC CAF / GSCP / SbD / Crypto / JSP | A/C | HTML/PDF download | None | Per-LTS snapshot | Vendor evidence pack + bundle |
| WCAG / axe-core / OIDC / IANA | C | Static download | None | Per-LTS snapshot | Vendor build → bundle |

### Recommended Integration Architecture

```text
ALL external feeds are vendor-side. The sovereign deployment makes ZERO outbound calls.

Vendor build pipeline (Lane A):
  - GHSA + NVD + OSV → SBOM enrichment → release manifest with CVE annotations
  - EPSS → exploit prioritisation overlay
  - NCSC CAF / SbD / JSP / Threat Reports → per-LTS accreditation evidence pack

Vendor pre-sales (Lane B):
  - Companies House Developer Hub → SME-tier verification (BR-006)
  - Contracts Finder / FTS / G-Cloud → procurement engagement (BR-007 / INT-008)

Vendor build → bundle (Lane C):
  - HMG GSCP, NCSC Crypto, WCAG 2.2 + axe-core ruleset, OIDC Core/Discovery, IANA OAuth Registry
  - All baked into the customer-side bundle as static reference data
```

### Authentication and Access

| Source | Auth | Registration | Lead Time |
|--------|------|--------------|-----------|
| Companies House | Basic (API key) | Self-service | Instant |
| Contracts Finder | OAuth2 | Self-service | 1 day |
| FTS | API key | Self-service | 1 day |
| GHSA | API key (optional) | GitHub account | Instant |
| NVD | API key (optional) | Self-service | Instant |
| OSV / EPSS | None | None | n/a |

### Rate Limits and Capacity Planning

| Source | Rate Limit | Projected Usage | Headroom |
|--------|-----------|----------------|----------|
| Companies House | 600 req / 5min (≈ 120/min) | 10–50 lookups/day | > 99% |
| GHSA | 83/min | 500 SBOM components/build | > 90% |
| NVD | 100/min | 500 SBOM components/build | > 90% |
| OSV | (not stated) | 500 SBOM components/build | n/a |
| EPSS | 1000/min | 500 SBOM components/build | > 99% |

---

## Data Utility Analysis

### Utility by Source

| Source | Primary Use | Secondary Uses | Strategic Value |
|--------|-------------|----------------|-----------------|
| Companies House | BR-006 SME-tier verification | Supplier risk; PSC ownership map | HIGH |
| GHSA / NVD / OSV | DR-007 SBOM CVE enrichment | NFR-SEC-008 SLA evidence; INT-010 disclosure benchmarking | HIGH |
| EPSS | NFR-SEC-005 prioritisation | Patch sequencing for LTS releases | MEDIUM |
| NCSC CAF | NFR-SEC-002 mapping | BR-004 evidence pack outcome alignment | HIGH |
| HMG GSCP | FR-012 / NFR-C-001 marking | Supports NFR-SEC-007 clearance taxonomy mapping | HIGH |
| NCSC Crypto | INT-007 KMS allow-list | Build-time primitive enforcement | HIGH |
| MOD SbD / JSP 440 | NFR-SEC-001 alignment | Supply-chain attestation evidence | HIGH |
| WCAG 2.2 / axe-core | NFR-C-003 CI gating | Public-sector procurement signal | MEDIUM |
| Contracts Finder / FTS | BR-007 framework engagement | Cross-sector market sizing | MEDIUM |
| OIDC / IANA OAuth | FR-007 / INT-001 | IdP claim normalisation across customer estates | MEDIUM |

---

## Gap Analysis

### Requirements Without Suitable Data Sources

**GAP-1 (NFR-SEC-007)**: UK personnel-clearance taxonomy (SC / DV / NPPV3) not published by HMG as a structured external data feed.

- **Why no source**: HMG does not publish a machine-readable SC/DV/NPPV3 taxonomy.
- **Impact**: Clearance levels embedded as static configuration constants; revisited on each LTS release.
- **Severity**: LOW
- **Action**: Maintain in deployment config; review at each LTS release.

**GAP-2 (PROCESS-1)**: JSP 604 has been formally withdrawn (replaced by Secure by Design / Defence Networks Governance).

- **Why no source**: Withdrawn publication; no successor open feed.
- **Impact**: Vendor must obtain current network-rules guidance through deploying-authority MOD accreditor per release.
- **Severity**: MEDIUM
- **Action**: Direct MOD accreditor engagement per release.

**GAP-3 (PROCESS-2)**: NCSC CAF v3.x revisions are published as ad-hoc HTML — no machine-readable diff API.

- **Impact**: Vendor must monitor NCSC RSS / news for CAF revision announcements and re-evaluate evidence pack manually.
- **Severity**: MEDIUM
- **Action**: Manual revision watch via NCSC RSS.

**GAP-4 (PROCESS-3)**: HMG GSCP revisions not published with a machine-readable change feed.

- **Impact**: Manual annual-cycle policy watch on Cabinet Office publications.
- **Severity**: LOW
- **Action**: Annual policy watch.

**GAP-5 (PROCESS-4)**: Defence Cyber Protection Partnership (DCPP) Cyber Risk Profile not published openly as a data feed.

- **Impact**: Risk profile must be obtained from deploying authority at engagement time (Assumption A-1 in REQ).
- **Severity**: MEDIUM
- **Action**: Per-engagement deploying-authority intake.

**GAP-6 (PROCESS-5)**: GovAssure / NCSC scheme details for non-MOD sensitive sites require direct NCSC engagement.

- **Impact**: Per non-MOD-customer engagement model.
- **Severity**: MEDIUM
- **Action**: Per-customer NCSC engagement.

### Gap Summary

| Gap | Requirement | Severity | Recommended Action |
|-----|-------------|----------|-------------------|
| GAP-1 | NFR-SEC-007 | LOW | Embed as config; review per LTS |
| GAP-2 | PROCESS-1 (JSP 604 withdrawn) | MEDIUM | MOD accreditor engagement per release |
| GAP-3 | PROCESS-2 (CAF revisions) | MEDIUM | Manual NCSC RSS watch |
| GAP-4 | PROCESS-3 (GSCP revisions) | LOW | Annual policy watch |
| GAP-5 | PROCESS-4 (DCPP risk profile) | MEDIUM | Per-engagement intake |
| GAP-6 | PROCESS-5 (GovAssure) | MEDIUM | Per-customer NCSC engagement |

---

## Recommendations & Shortlist

#### 1. Companies House Developer Hub for Company / Procurement

**Overall Score**: 79.25/100

**Rationale**: Authoritative UK company register. OGL-v3, GB-hosted, real-time. Foundational for BR-006 SME-tier verification underpinning the cross-subsidy commercial model.

**Key Strengths**: ✅ Authoritative · ✅ OGL-v3 · ✅ GB-hosted real-time

**Key Concerns**: ⚠️ Some PII (officers / PSC) — handle per DPA 2018

**Cost**: Free · **Integration Effort**: 3–5 person-days (vendor-side) · **Risk Level**: LOW

#### 2. GHSA + NVD + OSV.dev Triple Feed for Vulnerability / SBOM

**Overall Score**: 77.75 / 76.50 / 75.38 (Free)

**Rationale**: Principle-3 redundancy on Critical-7d patch SLA. Two-of-three minimum; all three recommended. Real-time / hourly cadence covers NFR-SEC-008.

**Cost**: Free · **Integration Effort**: 5–8 person-days · **Risk Level**: LOW

#### 3. Contracts Finder API + Find a Tender API

**Overall Score**: 77.25 / 75.75

**Rationale**: BR-007 / INT-008 — daily OCDS-format procurement intelligence. OGL-v3, GB-hosted.

**Cost**: Free · **Integration Effort**: 4–6 person-days · **Risk Level**: LOW

#### 4. NCSC CAF + MOD SbD + HMG GSCP + NCSC Crypto

**Overall Score**: 70.50 / 66.75 / 66.75 / 65.50

**Rationale**: Non-substitutable normative references for accreditation evidence pack (BR-004) and build-time taxonomies (FR-012 / NFR-C-001 / NFR-SEC-001 / NFR-SEC-002 / NFR-SEC-003 / INT-007). Read RF column, not totals.

**Cost**: Free · **Risk Level**: LOW

#### 5. WCAG 2.2 + axe-core + IANA OAuth + OIDC Core / Discovery

**Overall Score**: 58.13 / 55.88 / 62.50 / 56.88 / 55.63

**Rationale**: Build-time reference schemas baked into the bundle (Lane C). NFR-C-003 accessibility CI gate; FR-007 / INT-001 identity claim schemas.

**Cost**: Free · **Risk Level**: LOW

---

## Impact on Data Model

Not applicable — sovereign deployment runtime imports no external entities. All source-derived facts are baked at vendor build time into static reference tables (classification catalogue, crypto allow-list, WCAG ruleset, OIDC claim schema, accreditation evidence pack manifest). See `ARC-002-DATA-v*.md` for internal-only entities (DR-001..006).

---

## UK Government Open Data Opportunities

### TCoP Point 10: Make Better Use of Data

**Open Data Consumed**:

| Source | Dataset | License | Requirement |
|--------|---------|---------|-------------|
| developer.company-information.service.gov.uk | Companies, officers, PSC | OGL-v3 | BR-006 |
| contractsfinder.service.gov.uk | OCDS notices | OGL-v3 | BR-007 / INT-008 |
| find-tender.service.gov.uk | OCDS notices | OGL-v3 | BR-007 / INT-008 |
| ncsc.gov.uk | CAF, threat reports, crypto | OGL-v3 | BR-004 / NFR-SEC-002 / NFR-SEC-003 |
| gov.uk (Cabinet Office) | GSCP | OGL-v3 | FR-012 / NFR-C-001 |
| digital.mod.uk | Secure by Design | OGL-v3 | NFR-SEC-001 |

**Open Data Publishing Opportunities**: ArcKit telemetry (anonymised, classification-neutral) could be published as open data for cross-departmental architecture-maturity benchmarking — subject to Principle 21 / NFR-SEC-004 boundary preservation.

**Common Data Standards Used**: Companies House Number, OCDS releases/records, CVE, CVSS, CPE, EPSS, OIDC standard claims.

---

## Requirements Traceability

### Full Mapping Table

| Requirement ID | Data Source | Score | Status | Notes |
|----------------|-------------|-------|--------|-------|
| BR-004 | NCSC-CAF-1, DSIT-SBD-1, NCSC-THREAT-1, MOD-JSP440-1, MOD-JSP604-1 | 70.50 / 66.75 / 65.25 / 64.00 / 52.25 | ✅ Matched | Multi-input evidence pack |
| BR-005 | GHSA-1, NVD-1, OSV-1 | 77.75 / 76.50 / 75.38 | ✅ Matched | Triple-feed |
| BR-006 | CH-DH-1, CH-API-1 | 79.25 / 72.25 | ✅ Matched | CH-API-1 = rate-limit doc |
| BR-007 | CF-API-1, FTS-API-1, FTS-PUB-1, CF-PUB-1, DGU-1, GCLOUD-1 | 77.25 / 75.75 / 71.75 / 70.50 / 69.25 / 65.50 | ✅ Matched | Procurement |
| DR-001..006 | — | — | ✅ Constraint | Internal datatypes by design |
| DR-007 | GHSA-1, NVD-1, OSV-1, EPSS-1 | 77.75 / 76.50 / 75.38 / 64.63 | ✅ Matched | SBOM enrichment |
| FR-007 | IANA-OAUTH-1, OIDC-CORE-1, OIDC-DISC-1 | 62.50 / 56.88 / 55.63 | ✅ Matched | Identity schema |
| FR-012 | HMG-GSCP-1 | 66.75 | ✅ Matched | Classification catalogue |
| FR-014 | GHSA-1, NVD-1, OSV-1 | 77.75 / 76.50 / 75.38 | ✅ Matched | LTS patch SLA |
| INT-001 | IANA-OAUTH-1, OIDC-CORE-1, OIDC-DISC-1 | 62.50 / 56.88 / 55.63 | ✅ Matched | Customer IdP schema |
| INT-002..006, INT-009 | — | — | ✅ Constraint | Customer-controlled by Principle 21 |
| INT-007 | NCSC-CRYPTO-1 | 65.50 | ✅ Matched | HMG-approved primitives |
| INT-008 | CF-API-1, FTS-API-1, FTS-PUB-1, CF-PUB-1, DGU-1, GCLOUD-1 | 77.25 / 75.75 / 71.75 / 70.50 / 69.25 / 65.50 | ✅ Matched | Frameworks |
| INT-010 | GHSA-1, NVD-1, OSV-1 | 77.75 / 76.50 / 75.38 | ✅ Matched | Inbound disclosure |
| NFR-SEC-001 | DSIT-SBD-1, MOD-JSP440-1, MOD-JSP604-1 | 66.75 / 64.00 / 52.25 | ✅ Matched | MOD alignment |
| NFR-SEC-002 | NCSC-CAF-1 | 70.50 | ✅ Matched | CAF v3.x |
| NFR-SEC-003 | NCSC-CRYPTO-1 | 65.50 | ✅ Matched | HMG crypto |
| NFR-SEC-004 | — | — | ✅ Constraint | Architectural — no outbound calls |
| NFR-SEC-005 | GHSA-1, NVD-1, OSV-1, EPSS-1 | 77.75 / 76.50 / 75.38 / 64.63 | ✅ Matched | Supply chain |
| NFR-SEC-006 | — | — | ✅ Constraint | Within-deployment isolation |
| NFR-SEC-007 | — | — | ❌ Gap | See GAP-1 |
| NFR-SEC-008 | GHSA-1, NVD-1, OSV-1 | 77.75 / 76.50 / 75.38 | ✅ Matched | Patch SLA |
| NFR-C-001 | HMG-GSCP-1 | 66.75 | ✅ Matched | Classification |
| NFR-C-003 | WCAG22-1, AXE-1 | 58.13 / 55.88 | ✅ Matched | WCAG 2.2 AA |

### Coverage Summary

- ✅ **22 of 28 requirements (~79%)** with recommended sources
- ⚠️ **6 requirements** customer-controlled or schema-only (architectural constraint, not gap)
- ❌ **0 requirements** with no source — but 6 vendor-side process gaps tracked separately

---

## Next Steps

### Immediate Actions (0-2 weeks)

1. Register Companies House API key (vendor pre-sales)
2. Register Contracts Finder OAuth2 client and FTS API key
3. Register GHSA + NVD API keys (optional but recommended for rate-limit headroom)

### Vendor Build Pipeline (2-4 weeks)

4. Wire GHSA + NVD + OSV into SBOM enrichment job
5. Bake HMG GSCP, NCSC Crypto, WCAG 2.2, OIDC Core/Discovery, IANA OAuth Registry into bundle build
6. Assemble first per-LTS accreditation evidence pack (NCSC CAF + MOD SbD + JSP 440 + Threat Reports)

### Gap Resolution (4-8 weeks)

7. PROCESS gaps: establish MOD accreditor / NCSC engagement channels per customer
8. Define NFR-SEC-007 clearance config schema and migration plan

### Integration (Ongoing)

9. Quarterly reference-taxonomy refresh job
10. NCSC RSS monitor for CAF / threat-report revisions

---

## Appendices

### Appendix A: Research Methodology

**Discovery Approach**: Reader/writer subagent split. Four readers (one per (category, source_type) bucket) assembled per-source evidence subtrees against the validated DSCT handoff schema. Deterministic uk-gov rubric scorer applied per-criterion thresholds with `+10 GB residency bonus / −5 non-GB residency penalty` and `when_missing=50` for unobserved fields.

**Evaluation Methodology**: Weighted scoring across 6 criteria (RF 25 / DQ 20 / L&C 15 / API 15 / Comp 15 / Rel 10). Scores are deterministic functions of (evidence, rubric); re-running against fresh evidence will recompute deterministically.

**Limitations**: Some pages did not declare licence/pricing inline — these were scored conservatively at `when_missing=50` (notably CH-API-1, EPSS-1, AXE-1, OIDC, WCAG). Architectural conclusions are robust to these conservative scores.

### Appendix B: Glossary

- **OGL**: Open Government Licence
- **OCDS**: Open Contracting Data Standard
- **CAF**: Cyber Assessment Framework (NCSC)
- **GSCP**: Government Security Classifications Policy
- **JSP**: Joint Service Publication (MOD)
- **SbD**: Secure by Design
- **GHSA**: GitHub Security Advisories
- **NVD**: National Vulnerability Database (NIST)
- **OSV**: Open Source Vulnerabilities
- **EPSS**: Exploit Prediction Scoring System (FIRST.org)
- **WCAG**: Web Content Accessibility Guidelines
- **OIDC**: OpenID Connect

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| ARC-002-REQ-v1.0 | ARC-002-REQ-v1.0.md | Requirements | projects/002-arckit-sovereign/research | Source-of-truth requirements |
| ARC-002-PRIN-v1.0 | ARC-002-PRIN-v1.0.md | Principles | projects/002-arckit-sovereign/research | Principle 21 (no outbound calls) |

### Citations

| Citation ID | URL | Category | Fetched |
|-------------|-----|----------|---------|
| CH-DH-1 | https://developer.company-information.service.gov.uk/authentication | company / uk-gov | 2026-05-06 |
| CH-API-1 | https://developer-specs.company-information.service.gov.uk/guides/rateLimiting | company / uk-gov | 2026-05-06 |
| CF-API-1 | https://www.contractsfinder.service.gov.uk/apidocumentation | company / uk-gov | 2026-05-06 |
| CF-PUB-1 | https://www.data.gov.uk/dataset/contracts-finder-archive | company / uk-gov | 2026-05-06 |
| FTS-API-1 | https://www.find-tender.service.gov.uk/apidocumentation | company / uk-gov | 2026-05-06 |
| FTS-PUB-1 | https://www.find-tender.service.gov.uk/ | company / uk-gov | 2026-05-06 |
| DGU-1 | https://www.gov.uk/government/publications/open-contracting | company / uk-gov | 2026-05-06 |
| GCLOUD-1 | https://www.applytosupply.digitalmarketplace.service.gov.uk/ | company / uk-gov | 2026-05-06 |
| NCSC-CAF-1 | https://www.ncsc.gov.uk/collection/cyber-assessment-framework | reference / uk-gov | 2026-05-06 |
| NCSC-THREAT-1 | https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports | reference / uk-gov | 2026-05-06 |
| NCSC-RSS-1 | https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports | reference / uk-gov | 2026-05-06 |
| NCSC-CRYPTO-1 | https://www.ncsc.gov.uk/section/advice-guidance/all-topics/cryptography | reference / uk-gov | 2026-05-06 |
| HMG-GSCP-1 | https://www.gov.uk/government/publications/government-security-classifications | reference / uk-gov | 2026-05-06 |
| DSIT-SBD-1 | https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/ | reference / uk-gov | 2026-05-06 |
| MOD-JSP440-1 | https://assets.publishing.service.gov.uk/media/62bd6ad78fa8f535a8578517/Release_of_JSP_440_to_Industry.pdf | reference / uk-gov | 2026-05-06 |
| MOD-JSP604-1 | https://www.gov.uk/government/publications/joint-service-publication-jsp-604-network-rules | reference / uk-gov | 2026-05-06 |
| GHSA-1 | https://docs.github.com/en/rest/security-advisories/global-advisories | reference / free | 2026-05-06 |
| NVD-1 | https://nvd.nist.gov/developers/start-here | reference / free | 2026-05-06 |
| OSV-1 | https://google.github.io/osv.dev/api/ | reference / free | 2026-05-06 |
| EPSS-1 | https://api.first.org/ | reference / free | 2026-05-06 |
| WCAG22-1 | https://www.w3.org/TR/WCAG22/ | reference / oss | 2026-05-06 |
| AXE-1 | https://github.com/dequelabs/axe-core | reference / oss | 2026-05-06 |
| IANA-OAUTH-1 | https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml | reference / oss | 2026-05-06 |
| OIDC-CORE-1 | https://openid.net/specs/openid-connect-core-1_0.html | reference / oss | 2026-05-06 |
| OIDC-DISC-1 | https://openid.net/specs/openid-connect-discovery-1_0.html | reference / oss | 2026-05-06 |
| IANA-LIC-1 | https://www.iana.org/help/licensing-terms | reference / oss | 2026-05-06 |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

## Spawned Knowledge

The following standalone data-source profile files were created or updated from this discovery run:

### Data Source Profiles

- `data-sources/companies-house-profile.md` — Created (covers CH-DH-1 + CH-API-1)
- `data-sources/crown-commercial-service-profile.md` — Created (covers CF-API-1 + CF-PUB-1)
- `data-sources/cabinet-office-crown-commercial-service-profile.md` — Created (covers FTS-API-1 + FTS-PUB-1)
- `data-sources/govuk-cabinet-office-profile.md` — Created (DGU-1)
- `data-sources/crown-commercial-service-government-digital-service-profile.md` — Created (GCLOUD-1)
- `data-sources/ncsc-profile.md` — Created (NCSC-CAF-1 + NCSC-CRYPTO-1 + NCSC-THREAT-1 + NCSC-RSS-1)
- `data-sources/cabinet-office-profile.md` — Created (HMG-GSCP-1)
- `data-sources/ministry-of-defence-profile.md` — Created (DSIT-SBD-1 + MOD-JSP440-1 + MOD-JSP604-1)
- `data-sources/github-profile.md` — Created (GHSA-1)
- `data-sources/nist-profile.md` — Created (NVD-1)
- `data-sources/google-profile.md` — Created (OSV-1)
- `data-sources/first-org-profile.md` — Created (EPSS-1)
- `data-sources/iana-profile.md` — Created (IANA-OAUTH-1 + IANA-LIC-1)
- `data-sources/w3c-profile.md` — Created (WCAG22-1)
- `data-sources/openid-foundation-profile.md` — Created (OIDC-CORE-1 + OIDC-DISC-1)
- `data-sources/deque-labs-profile.md` — Created (AXE-1)

---

**Generated by**: ArcKit `/arckit:datascout` orchestrator (writer subagent)
**Generated on**: 2026-05-06
**ArcKit Version**: 4.17.0
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
