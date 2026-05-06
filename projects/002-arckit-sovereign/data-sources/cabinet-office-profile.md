# Data Source Profile: Cabinet Office — HMG Government Security Classifications Policy

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

HMG Government Security Classifications Policy (GSCP) defines the OFFICIAL / SECRET / TOP SECRET classification scheme and handling caveats. Baked into the Project 002 bundle at vendor build time (Lane C) to enforce FR-012 marking and NFR-C-001 classification policy.

**Provider**: Cabinet Office
**Source name**: HMG Government Security Classifications Policy
**Category**: reference
**Source type**: uk-gov
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | GB | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |
| Licence type | OGL-v3 | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |
| Pricing model | open-data | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |
| Refresh cadence | ad-hoc | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |
| Auth required | false (none) | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |
| Certifications | OGL-v3 | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |
| Data categories supported | security-classifications, official, secret, top-secret, handling-policy | [HMG-GSCP-1](https://www.gov.uk/government/publications/government-security-classifications) |

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 100/100 | 25.00 |
| Data quality | 20% | 30/100 | 6.00 |
| Licence and cost | 15% | 100/100 | 15.00 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 35/100 | 5.25 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **66.75/100** |

## Requirements Matched

- FR-012 — Classification marking
- NFR-C-001 — Classification policy enforcement

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
