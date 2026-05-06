# Data Source Profile: GitHub — GitHub Security Advisories (GHSA) Global Advisories REST API

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

GitHub Security Advisories (GHSA) is GitHub's vulnerability dataset published via REST under CC-BY-4.0. Used in Project 002 at vendor build time (Lane A) for SBOM enrichment, NFR-SEC-008 patch SLAs, INT-010 inbound disclosure benchmarking. US-hosted — −5 GB-residency penalty applied.

**Provider**: GitHub
**Source name**: GitHub Security Advisories (GHSA) Global Advisories REST API
**Category**: reference
**Source type**: free
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | US | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |
| Licence type | CC-BY-4.0 | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |
| Pricing model | free | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |
| Rate limit | 83/min | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |
| Refresh cadence | real-time | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |
| Auth required | false (api-key optional) | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |
| Data categories supported | vulnerabilities, cve, cvss, epss, cwe, advisories, packages | [GHSA-1](https://docs.github.com/en/rest/security-advisories/global-advisories) |

## Weighted Score (uk-gov rubric)

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 95/100 | 23.75 |
| Data quality | 20% | 100/100 | 20.00 |
| Licence and cost | 15% | 85/100 | 12.75 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 25/100 | 3.75 |
| Reliability | 10% | 70/100 | 7.00 |
| **Total** |  |  | **77.75/100** |

## Requirements Matched

- NFR-SEC-005 — Supply-chain integrity / SBOM
- NFR-SEC-008 — Patch SLA evidence
- FR-014 — LTS patch delivery (SLAs)
- BR-005 — LTS patch tracking
- DR-007 — SBOM / release manifest CVE enrichment
- INT-010 — Inbound vulnerability disclosure channel

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
