# Data Source Profile: FIRST.org — FIRST EPSS (Exploit Prediction Scoring System) API

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

FIRST.org publishes the Exploit Prediction Scoring System (EPSS) — a daily-refreshed CVE exploit-prediction score complementing CVSS. Lane A supplementary feed for prioritisation. Licence not declared on landing page (`when_missing=50`).

**Provider**: FIRST.org
**Source name**: FIRST EPSS API
**Category**: reference
**Source type**: free
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | US | [EPSS-1](https://api.first.org/) |
| Licence type | Unknown (when_missing=50) | [EPSS-1](https://api.first.org/) |
| Pricing model | free | [EPSS-1](https://api.first.org/) |
| Rate limit | 1000/min | [EPSS-1](https://api.first.org/) |
| Refresh cadence | daily | [EPSS-1](https://api.first.org/) |
| Auth required | false (none) | [EPSS-1](https://api.first.org/) |
| Data categories supported | epss, cve, exploit-prediction, vulnerability-scoring | [EPSS-1](https://api.first.org/) |

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 70/100 | 17.50 |
| Data quality | 20% | 80/100 | 16.00 |
| Licence and cost | 15% | 52.5/100 | 7.88 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 25/100 | 3.75 |
| Reliability | 10% | 90/100 | 9.00 |
| **Total** |  |  | **64.63/100** |

## Requirements Matched

- NFR-SEC-005
- DR-007

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
