# Data Source Profile: Google — OSV.dev Open Source Vulnerabilities API

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

OSV.dev is Google / OpenSSF's distributed-database vulnerability API for open-source ecosystems under Apache-2.0. Lane A vendor-build feed; provides SBOM-keyed redundancy alongside GHSA + NVD.

**Provider**: Google
**Source name**: OSV.dev Open Source Vulnerabilities API
**Category**: reference
**Source type**: free
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | US | [OSV-1](https://google.github.io/osv.dev/api/) |
| Licence type | Apache-2.0 | [OSV-1](https://google.github.io/osv.dev/api/) |
| Pricing model | free | [OSV-1](https://google.github.io/osv.dev/api/) |
| Refresh cadence | real-time | [OSV-1](https://google.github.io/osv.dev/api/) |
| Auth required | false (none) | [OSV-1](https://google.github.io/osv.dev/api/) |
| Data categories supported | vulnerabilities, osv, packages, ecosystems, sbom, commits | [OSV-1](https://google.github.io/osv.dev/api/) |

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 95/100 | 23.75 |
| Data quality | 20% | 100/100 | 20.00 |
| Licence and cost | 15% | 82.5/100 | 12.38 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 25/100 | 3.75 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **75.38/100** |

## Requirements Matched

- NFR-SEC-005, NFR-SEC-008, FR-014, BR-005, DR-007, INT-010

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
