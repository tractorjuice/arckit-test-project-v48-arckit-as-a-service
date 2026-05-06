# Data Source Profile: Cabinet Office / Crown Commercial Service — Find a Tender Service REST API (OCDS)

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

Find a Tender Service (FTS) is the UK above-threshold tender notification service operated by Cabinet Office / CCS. The REST API exposes OCDS-format procurement notices, releases, records and contract awards. In Project 002 it is a Lane B (vendor pre-sales) source for BR-007 / INT-008.

**Provider**: Cabinet Office / Crown Commercial Service
**Source name**: Find a Tender Service REST API (OCDS)
**Category**: company
**Source type**: uk-gov
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | GB | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |
| Licence type | OGL-v3 | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |
| Pricing model | open-data | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |
| Refresh cadence | daily | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |
| Auth required | true (api-key) | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |
| Certifications | OGL-v3 | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |
| Data categories supported | procurement-notices, ocds-releases, ocds-records, contract-awards | [FTS-API-1](https://www.find-tender.service.gov.uk/apidocumentation) |

A second source FTS-PUB-1 (https://www.find-tender.service.gov.uk/ — score 71.75) is the public service variant, no auth, daily.

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 90/100 | 22.50 |
| Data quality | 20% | 80/100 | 16.00 |
| Licence and cost | 15% | 100/100 | 15.00 |
| API quality | 15% | 80/100 | 12.00 |
| Compliance | 15% | 35/100 | 5.25 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **75.75/100** |

## Requirements Matched

- BR-007 — Procurement framework engagement intelligence
- INT-008 — G-Cloud / DOS / Defence framework listings

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
