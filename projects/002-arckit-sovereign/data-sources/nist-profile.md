# Data Source Profile: NIST — NVD National Vulnerability Database API 2.0

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

NIST's National Vulnerability Database (NVD) API 2.0 is the canonical CVE / CVSS / CPE / CWE source under CC0-1.0. Lane A vendor-build feed for Project 002 — never called from runtime sovereign deployment.

**Provider**: NIST
**Source name**: NVD National Vulnerability Database API 2.0
**Category**: reference
**Source type**: free
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | US | [NVD-1](https://nvd.nist.gov/developers/start-here) |
| Licence type | CC0-1.0 | [NVD-1](https://nvd.nist.gov/developers/start-here) |
| Pricing model | free | [NVD-1](https://nvd.nist.gov/developers/start-here) |
| Rate limit | 100/min | [NVD-1](https://nvd.nist.gov/developers/start-here) |
| Refresh cadence | hourly | [NVD-1](https://nvd.nist.gov/developers/start-here) |
| Auth required | false (api-key optional) | [NVD-1](https://nvd.nist.gov/developers/start-here) |
| Data categories supported | vulnerabilities, cve, cvss, cpe, cwe | [NVD-1](https://nvd.nist.gov/developers/start-here) |

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 95/100 | 23.75 |
| Data quality | 20% | 90/100 | 18.00 |
| Licence and cost | 15% | 90/100 | 13.50 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 25/100 | 3.75 |
| Reliability | 10% | 70/100 | 7.00 |
| **Total** |  |  | **76.50/100** |

## Requirements Matched

- NFR-SEC-005, NFR-SEC-008, FR-014, BR-005, DR-007, INT-010

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
