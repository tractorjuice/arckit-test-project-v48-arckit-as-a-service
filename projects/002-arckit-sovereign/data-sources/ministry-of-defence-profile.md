# Data Source Profile: Ministry of Defence — Secure by Design (and JSP control catalogues)

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

The Ministry of Defence publishes Secure by Design (SbD) policy via Digital MOD, plus the historical JSP 440 (Defence Manual of Security) and JSP 604 (Defence Networks Governance — formally withdrawn). All Lane A inputs to the per-LTS-release accreditation evidence pack for NFR-SEC-001 and BR-004.

**Provider**: Ministry of Defence
**Source name**: MOD Secure by Design [primary]
**Category**: reference
**Source type**: uk-gov
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | GB | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/) |
| Licence type | OGL-v3 | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/) |
| Pricing model | open-data | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/) |
| Refresh cadence | ad-hoc (SbD) / static (JSP 604 withdrawn) | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/), [MOD-JSP604-1](https://www.gov.uk/government/publications/joint-service-publication-jsp-604-network-rules) |
| Auth required | false (SbD), true basic (JSP 440 PDF) | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/), [MOD-JSP440-1](https://assets.publishing.service.gov.uk/media/62bd6ad78fa8f535a8578517/Release_of_JSP_440_to_Industry.pdf) |
| Certifications | OGL-v3 | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/) |
| Data categories supported | secure-by-design, defence-cyber, risk-management, supply-chain-security, through-life-security, defence-security, personnel-security, physical-security, cis-security, vetting, defence-networks, ict-governance, network-rules | [DSIT-SBD-1](https://www.digital.mod.uk/policy-rules-standards-and-guidance/secure-by-design/), [MOD-JSP440-1](https://assets.publishing.service.gov.uk/media/62bd6ad78fa8f535a8578517/Release_of_JSP_440_to_Industry.pdf), [MOD-JSP604-1](https://www.gov.uk/government/publications/joint-service-publication-jsp-604-network-rules) |

## Weighted Score (uk-gov rubric)

DSIT-SBD-1 (primary):

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 100/100 | 25.00 |
| Data quality | 20% | 30/100 | 6.00 |
| Licence and cost | 15% | 100/100 | 15.00 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 35/100 | 5.25 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **66.75/100** |

Sibling MOD sources rendered with the same provider context:

- MOD-JSP440-1 — **64.00/100** (NFR-SEC-001, BR-004)
- MOD-JSP604-1 — **52.25/100** (NFR-SEC-001 — historical/withdrawn; see PROCESS-1 gap)

## Requirements Matched

- NFR-SEC-001 — MOD SbD / JSP 440 / JSP 604 alignment
- BR-004 — Per-release accreditation evidence pack

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
