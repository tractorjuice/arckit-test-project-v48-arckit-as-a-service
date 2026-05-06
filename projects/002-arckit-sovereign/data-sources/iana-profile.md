# Data Source Profile: IANA — OAuth Parameters Registry (and Licensing Terms)

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

IANA publishes the OAuth Parameters Registry (CC0-1.0) and supporting licensing terms. Lane C build-time reference baked into the bundle to validate identity-claim and OAuth-protocol parameters (FR-007 / INT-001).

**Provider**: IANA
**Source name**: OAuth Parameters Registry [primary]
**Category**: reference
**Source type**: oss
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | US | [IANA-OAUTH-1](https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml) |
| Licence type | CC0-1.0 | [IANA-OAUTH-1](https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml), [IANA-LIC-1](https://www.iana.org/help/licensing-terms) |
| Pricing model | free | [IANA-OAUTH-1](https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml) |
| Refresh cadence | ad-hoc (registry) / static (licensing terms) | [IANA-OAUTH-1](https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml), [IANA-LIC-1](https://www.iana.org/help/licensing-terms) |
| Auth required | false (none) | [IANA-OAUTH-1](https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml) |
| Data categories supported | oauth, protocol-registry, iana-assignments, licensing, public-domain, iana-policy | [IANA-OAUTH-1](https://www.iana.org/assignments/oauth-parameters/oauth-parameters.xhtml), [IANA-LIC-1](https://www.iana.org/help/licensing-terms) |

## Weighted Score (uk-gov rubric)

IANA-OAUTH-1 (primary):

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 95/100 | 23.75 |
| Data quality | 20% | 30/100 | 6.00 |
| Licence and cost | 15% | 90/100 | 13.50 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 25/100 | 3.75 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **62.50/100** |

IANA-LIC-1 — **49.25/100** (no direct requirement match; cited as evidence for CC0 provenance).

## Requirements Matched

- FR-007 — Identity claim mapping
- INT-001 — Customer IdP integration schemas

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
