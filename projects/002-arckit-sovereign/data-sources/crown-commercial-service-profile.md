# Data Source Profile: Crown Commercial Service — Contracts Finder API (OCDS)

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

Crown Commercial Service operates Contracts Finder, the UK government's below- and above-threshold procurement-notice service. The OCDS API exposes notices, releases, records and contract awards. In Project 002 it is a Lane B (vendor pre-sales) source for BR-007 / INT-008 procurement-framework engagement intelligence — not a runtime feed.

**Provider**: Crown Commercial Service
**Source name**: Contracts Finder API (OCDS)
**Category**: company
**Source type**: uk-gov
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | GB | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |
| Licence type | OGL-v3 | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |
| Pricing model | open-data | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |
| Refresh cadence | daily | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |
| Auth required | true (oauth2) | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |
| Certifications | OGL-v3 | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |
| Data categories supported | procurement-notices, ocds-releases, ocds-records, contract-awards, cpv-codes | [CF-API-1](https://www.contractsfinder.service.gov.uk/apidocumentation) |

A second source CF-PUB-1 (https://www.data.gov.uk/dataset/contracts-finder-archive — score 70.50) is the public archive variant, no auth, daily.

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 90/100 | 22.50 |
| Data quality | 20% | 80/100 | 16.00 |
| Licence and cost | 15% | 100/100 | 15.00 |
| API quality | 15% | 90/100 | 13.50 |
| Compliance | 15% | 35/100 | 5.25 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **77.25/100** |

## Requirements Matched

- BR-007 — Procurement framework engagement intelligence
- INT-008 — G-Cloud / DOS / Defence framework listings

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
