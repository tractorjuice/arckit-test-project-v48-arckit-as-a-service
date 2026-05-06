# Data Source Profile: NCSC — Cyber Assessment Framework (CAF) (and related collections)

> **Template Origin**: Official | **ArcKit Version**: 4.17.0 | **Command**: `/arckit:datascout`

## Document Control

| Field | Value |
|-------|-------|
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-06 | ArcKit AI | Initial creation from `/arckit:datascout` orchestrator | PENDING | PENDING |

---

## Overview

The National Cyber Security Centre publishes the Cyber Assessment Framework (CAF) and supporting collections (cryptography, threat reports, RSS feeds). All consumed at vendor build time (Lane A / Lane C) for accreditation evidence and build-time reference baked into the bundle. Project 002's runtime sovereign deployment never calls these.

**Provider**: NCSC
**Source name**: Cyber Assessment Framework (CAF) [primary]
**Category**: reference
**Source type**: uk-gov
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | GB | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework) |
| Licence type | OGL-v3 | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework) |
| Pricing model | open-data | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework) |
| Refresh cadence | ad-hoc (CAF) / weekly (Threat Reports, RSS) | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework), [NCSC-THREAT-1](https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports) |
| Auth required | false (none) | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework) |
| Certifications | OGL-v3, NCSC-CAF-aligned-asserted | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework) |
| Data categories supported | cyber-security-framework, caf-principles, essential-services, cni, cryptography, threat-intelligence, rss-feed | [NCSC-CAF-1](https://www.ncsc.gov.uk/collection/cyber-assessment-framework), [NCSC-CRYPTO-1](https://www.ncsc.gov.uk/section/advice-guidance/all-topics/cryptography), [NCSC-THREAT-1](https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports), [NCSC-RSS-1](https://www.ncsc.gov.uk/section/keep-up-to-date/threat-reports) |

## Weighted Score (uk-gov rubric)

NCSC-CAF-1 (primary):

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 100/100 | 25.00 |
| Data quality | 20% | 30/100 | 6.00 |
| Licence and cost | 15% | 100/100 | 15.00 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 60/100 | 9.00 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **70.50/100** |

Sibling NCSC sources rendered with the same provider context:

- NCSC-CRYPTO-1 — **65.50/100** (NFR-SEC-003, INT-007)
- NCSC-THREAT-1 — **65.25/100** (BR-004)
- NCSC-RSS-1 — **64.00/100** (BR-004)

## Requirements Matched

- NFR-SEC-002 — NCSC CAF v3.x mapping
- BR-004 — Per-release accreditation evidence pack
- NFR-SEC-003 — HMG-approved cryptography (via NCSC-CRYPTO-1)
- INT-007 — Customer KMS HMG-approved primitive allow-list (via NCSC-CRYPTO-1)

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
