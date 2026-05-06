# Data Source Profile: OpenID Foundation — OpenID Connect Core 1.0 (and Discovery 1.0)

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

The OpenID Foundation publishes OpenID Connect Core 1.0 and OpenID Connect Discovery 1.0 (errata set 2). Lane C build-time references baked into the bundle for FR-007 / INT-001 customer-IdP integration. Licence not declared inline on the spec pages (`when_missing=50`).

**Provider**: OpenID Foundation
**Source name**: OpenID Connect Core 1.0 [primary]
**Category**: reference
**Source type**: oss
**Confidence**: high
**Last researched**: 2026-05-06

## Evidence

| Field | Value | Source |
|---|---|---|
| Hosted in | US | [OIDC-CORE-1](https://openid.net/specs/openid-connect-core-1_0.html) |
| Licence type | Unknown (when_missing=50) | [OIDC-CORE-1](https://openid.net/specs/openid-connect-core-1_0.html), [OIDC-DISC-1](https://openid.net/specs/openid-connect-discovery-1_0.html) |
| Pricing model | free | [OIDC-CORE-1](https://openid.net/specs/openid-connect-core-1_0.html) |
| Refresh cadence | ad-hoc | [OIDC-CORE-1](https://openid.net/specs/openid-connect-core-1_0.html) |
| Auth required | false (none) | [OIDC-CORE-1](https://openid.net/specs/openid-connect-core-1_0.html) |
| Data categories supported | openid-connect, oauth2, identity, authentication, discovery, metadata | [OIDC-CORE-1](https://openid.net/specs/openid-connect-core-1_0.html), [OIDC-DISC-1](https://openid.net/specs/openid-connect-discovery-1_0.html) |

## Weighted Score (uk-gov rubric)

OIDC-CORE-1 (primary):

| Criterion | Weight | Per-criterion score | Weighted contribution |
|---|---|---|---|
| Requirements fit | 25% | 95/100 | 23.75 |
| Data quality | 20% | 30/100 | 6.00 |
| Licence and cost | 15% | 52.5/100 | 7.88 |
| API quality | 15% | 70/100 | 10.50 |
| Compliance | 15% | 25/100 | 3.75 |
| Reliability | 10% | 50/100 | 5.00 |
| **Total** |  |  | **56.88/100** |

OIDC-DISC-1 — **55.63/100** (FR-007, INT-001) with the same provider context.

## Requirements Matched

- FR-007 — Identity claim mapping
- INT-001 — Customer IdP integration schemas

## Projects Referenced In

- 002-arckit-sovereign

## Last Updated

2026-05-06
