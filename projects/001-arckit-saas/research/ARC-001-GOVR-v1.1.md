# Government Reuse Assessment: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.19.0 | **Command**: `/arckit:gov-reuse`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GOVR-v1.1 |
| **Document Type** | Government Code Reuse Assessment |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.1 |
| **Created Date** | 2026-05-07 |
| **Last Modified** | 2026-05-07 |
| **Review Cycle** | 6-monthly (gov repo landscape changes quickly) |
| **Next Review Date** | 2026-11-07 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project 001 team, Lead Architect, Service Owner, downstream `/arckit:research` and `/arckit:adr` consumers, CCS liaison |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:gov-reuse` agent (govreposcrape MCP + WebFetch). | PENDING | PENDING |
| 1.1 | 2026-05-07 | ArcKit AI | Re-run under three-tier architecture (researcher / scorer / writer). 10 capabilities, 49 deduped scored candidates, deterministic rubric (`gov-reuse-uk-gov`). | PENDING | PENDING |

---

## Executive Summary

### Search Scope

This v1.1 reassessment was generated under the three-tier subagent split (researcher / scorer / writer). The researcher tier surveyed UK government open-source repositories across 10 capability areas drawn from `ARC-001-REQ-v1.0.md` (BR, FR, NFR-SEC, INT requirements). The scorer tier applied the deterministic `gov-reuse-uk-gov` rubric (licence_compatibility 25 / code_quality 20 / documentation 20 / tech_stack_alignment 20 / activity_maintenance 15) with trusted-org bonuses for `alphagov`, `ministryofjustice`, `nhsuk`, `co-cddo`, `dfe-digital`, `hmrc`, `companieshouse`, `govuk-one-login`. This writer tier renders the validated, scored payload verbatim — no re-scoring or synthesis.

**Capabilities Assessed**: 10 capability areas across 9 trusted UK-government organisations (alphagov, GDS DI / govuk-one-login, NHS, MoJ, i.AI / Cabinet Office, Companies House, HMRC, DfE Digital, plus community contributors).

**Repositories Evaluated**: 49 distinct repositories scored after dedup; bands assigned: **Fork** (≥80) — 18 entries; **Library** (60–79) — 27 entries; **Reference** (40–59) — 3 entries; **None** (<40) — 1 entry.

**Project Profile**: preferred languages — TypeScript, JavaScript, Python; framework hints — Next.js, govuk-frontend, OpenAPI, Terraform, Kubernetes/Helm; sectors — cross-government, DDaT, SaaS; licence constraints — MIT, Apache-2.0, OGL-v3.

### Key Findings

| Capability | Best Candidate | Organisation | Reuse Strategy | Score |
|------------|---------------|--------------|----------------|-------|
| GOV.UK Design System frontend components and accessible web UI | x-govuk/govuk-eleventy-plugin | x-govuk | Fork | 92/100 |
| GOV.UK One Login OIDC and SAML SSO authentication middleware | govuk-one-login/simulator | GOV.UK One Login | Fork | 82/100 |
| Multi-tenant SaaS isolation and per-tenant RBAC framework | alphagov/digitalmarketplace-api | alphagov | Fork | 82/100 |
| Tamper-evident audit logging and structured telemetry library | alphagov/govuk_app_config | alphagov | Library | 72/100 |
| Companies House SME verification client and onboarding workflow | companieshouse/overseas-entities-web | Companies House | Fork | 83/100 |
| GOV.UK Notify transactional email and notification client | alphagov/notifications-api | alphagov | Fork | 82/100 |
| AI and LLM provider abstraction layer for government services | i-dot-ai/consult | i.AI / Cabinet Office | Fork | 92/100 |
| AWS multi-cloud landing-zone IaC for UK-resident SaaS workloads | ministryofjustice/cloud-platform-terraform-rds-instance | Ministry of Justice | Fork | 80/100 |
| G-Cloud Digital Marketplace listing and call-off tooling | alphagov/digitalmarketplace-api | alphagov | Library | 72/100 |
| Subscription billing and payment processing for government SaaS | alphagov/pay-frontend | alphagov | Fork | 83/100 |

### Reuse Summary

**Reuse Coverage**: All 10 assessed capabilities have at least one band ≥ Library candidate; **8 of 10** have a top candidate at the Fork band.

**Recommended Approach**: Adopt `alphagov/govuk-frontend` (and `x-govuk/govuk-eleventy-plugin` for documentation chrome) as the foundational frontend stack; depend on `companieshouse/api-sdk-node` directly for SME verification (BR-003, FR-001, INT-003); take the GOV.UK One Login `simulator` as the local CI test harness for INT-001/NFR-SEC-001; use `i-dot-ai/i-dot-ai-utilities` (LiteLLM-based) as the spine of the AI provider abstraction (FR-004, INT-005); cherry-pick the MoJ Cloud Platform Terraform modules (RDS, S3, infrastructure) for INT-006/NFR-A-001/A-002/S-001; learn isolation patterns from `alphagov/digitalmarketplace-api` and `alphagov/notifications-api` rather than forking wholesale; reference `alphagov/pay-frontend` and `pay-selfservice` for FR-011/INT-002 design alignment with GOV.UK Design System. Build new where gaps remain (tamper-evident hash-chain log; tenant-isolation middleware kernel; tenant export; admin console; status page; vulnerability disclosure tooling) and publish under MIT to seed cross-government reuse.

---

## Capability Analysis

### Capability 1: GOV.UK Design System frontend components and accessible web UI

**Verdict: Fork — `x-govuk/govuk-eleventy-plugin` ranks first numerically and is MIT, x-govuk JS plugin actively maintained (Mar 2026), full tests/CI/docs; aligns with project's JS+govuk-frontend stack.**

**Strategic note**: Although `alphagov/govuk-frontend` ranks 3rd numerically (83/100), it remains the canonical primary frontend dependency; the higher-scored repos are complementary tools.

---

#### Candidate 1: x-govuk/govuk-eleventy-plugin — Fork (92/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | x-govuk |
| **Repository URL** | https://github.com/x-govuk/govuk-eleventy-plugin |
| **Language** | javascript |
| **Framework** | govuk-frontend |
| **License** | MIT |
| **Last Commit** | 2026-03-06 |
| **Stars / Forks** | 65 / 17 |
| **Tests / CI / Docs** | yes / yes / yes |
| **Archived** | no |
| **Install** | `npm install @x-govuk/govuk-eleventy-plugin` |

**Description**: Build documentation websites using Markdown and GOV.UK styles.

**Score breakdown**: licence 24, code quality 20, documentation 20, tech-stack alignment 14, activity 15 — **total 92** (band: Fork).

**Rationale**: MIT, x-govuk JS plugin actively maintained (Mar 2026), full tests/CI/docs; aligns with project's JS+govuk-frontend stack. Niche use case (Markdown docs sites) bumps score above main GDS repos due to recent commit signal.

**Citation**: XGOVUK-11TY-1.

---

#### Candidate 2: penx/govuk-react — Fork (85/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | penx |
| **Repository URL** | https://github.com/penx/govuk-react |
| **Language** | typescript |
| **Framework** | react, govuk-frontend |
| **License** | MIT |
| **Last Commit** | 2024-05-13 |
| **Stars / Forks** | 455 / 87 |
| **Install** | `npm install govuk-react styled-components @types/styled-components --save` |

**Description**: Implementation of the GOV.UK Design System in React using CSS-in-JS Object notation (styled-components).

**Score breakdown**: licence 24, code quality 20, documentation 20, tech-stack alignment 13, activity 8 — **total 85** (band: Fork).

**Rationale**: MIT, TypeScript+React port of GOV.UK Design System matching ArcKit's preferred stack; community-maintained (last commit 2024-05) — freshness check before adoption recommended.

**Citation**: PENX-GOVUK-REACT-1.

---

#### Candidate 3: alphagov/govuk-frontend — Fork (83/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk-frontend |
| **Language** | javascript |
| **Framework** | govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 1400 / 364 |
| **Install** | `npm install govuk-frontend` |

**Description**: GOV.UK Frontend contains the code you need to start building a user interface for government platforms and services.

**Score breakdown**: licence 24, code quality 20, documentation 20, tech-stack alignment 14, activity 6 — **total 83** (band: Fork).

**Rationale**: MIT, GDS-maintained canonical Design System (alphagov +10 trusted-org bonus); active per release notes (v6.1.0 Mar 2026) but reader did not extract last_commit_iso so activity weighted 'when_missing'. Strategic primary recommendation despite ranking 3rd numerically.

**Citation**: ALPHAGOV-GOVUK-FE-1.

---

#### Candidate 4: alphagov/govuk-prototype-kit — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk-prototype-kit |
| **Language** | javascript |
| **Framework** | govuk-prototype-kit, govuk-frontend, express |
| **License** | MIT |
| **Last Commit** | 2026-04-10 |
| **Stars / Forks** | 334 / 251 |
| **Install** | npm |

**Description**: The Prototype Kit provides a simple way to make interactive prototypes that look like pages on GOV.UK.

**Score breakdown**: licence 24, cq 20, docs 10, alignment 13, activity 15 — **total 82** (band: Fork).

**Rationale**: MIT, GDS-maintained Express+nunjucks prototype scaffolding (alphagov +10 trusted-org); active (Apr 2026). Useful for ArcKit alpha/prototype phase before production stack lock-in.

**Citation**: ALPHAGOV-PROTO-KIT-1.

---

#### Candidate 5: nhsuk/nhsuk-frontend — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | nhsuk |
| **Repository URL** | https://github.com/nhsuk/nhsuk-frontend |
| **Language** | javascript |
| **License** | MIT |
| **Stars / Forks** | 672 / 130 |
| **Install** | npm |

**Description**: NHS.UK frontend contains the code you need to start building user interfaces for NHS websites and services.

**Score breakdown**: licence 24, cq 20, docs 20, alignment 12, activity 6 — **total 82** (band: Fork).

**Rationale**: MIT, NHS England Design System frontend; only relevant for NHS-themed tenancies and as a Reference for sector-specific re-skinning patterns.

**Citation**: NHSUK-FE-1.

---

#### Candidate 6: alphagov/govuk_publishing_components — Library (74/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk_publishing_components |
| **Language** | ruby |
| **Framework** | rails, govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 88 / 30 |
| **Install** | rubygems |

**Description**: Ruby gem to document and distribute components for GOV.UK applications.

**Score breakdown**: licence 24, cq 20, docs 20, alignment 4, activity 6 — **total 74** (band: Library).

**Rationale**: MIT, Ruby gem for GOV.UK content components (alphagov +10 bonus); not relevant unless ArcKit selects Ruby/Rails which is not the project's preferred stack — Reference-only in practice.

**Citation**: ALPHAGOV-PUB-COMP-1.

---

### Capability 2: GOV.UK One Login OIDC and SAML SSO authentication middleware

**Verdict: Fork — `govuk-one-login/simulator` is the official local-dev simulator for One Login (TypeScript+Docker); use as the test harness for INT-001 in CI.**

---

#### Candidate 1: govuk-one-login/simulator — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | govuk-one-login |
| **Repository URL** | https://github.com/govuk-one-login/simulator |
| **Language** | typescript |
| **Framework** | express |
| **License** | MIT |
| **Stars / Forks** | 4 / 8 |
| **Install** | docker |

**Description**: Downloadable simulator tool for GOV.UK One Login to allow service teams to develop and test their integration locally.

**Score breakdown**: 24/20/20/12/6 — **total 82** (band: Fork).

**Rationale**: MIT, official GOV.UK One Login local-development simulator (TypeScript+Docker); use as test harness for INT-001 (NFR-SEC-001/003) without depending on the live identity service in CI.

**Citation**: GOL-SIM-1.

---

#### Candidate 2: alphagov/signon — Fork (81/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/signon |
| **Language** | ruby |
| **Framework** | rails |
| **License** | MIT |
| **Last Commit** | 2026-05-06 |
| **Stars / Forks** | 97 / 34 |
| **Install** | docker (`Use GOV.UK Docker to run any commands that follow`) |

**Description**: Centralised OAuth2 SSO provider for GDS services with username/password and 2-step verification.

**Score breakdown**: 24/20/20/2/15 — **total 81** (band: Fork).

**Rationale**: MIT, GDS-maintained centralised OAuth2/SSO provider on Rails (alphagov +10 bonus, last commit 1 day ago); use as Reference for SSO architecture even though Ruby/Rails is off-stack.

**Citation**: ALPHAGOV-SIGNON-1.

---

#### Candidate 3: govuk-one-login/onboarding-examples — Library (76/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | govuk-one-login |
| **Repository URL** | https://github.com/govuk-one-login/onboarding-examples |
| **Language** | typescript |
| **Framework** | express, govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 9 / 4 |
| **Install** | clone-only |

**Description**: Example applications demonstrating integration patterns with GOV.UK One Login authentication service.

**Score breakdown**: 24/13/20/13/6 — **total 76** (band: Library).

**Rationale**: MIT, official onboarding example apps showing TS+Express+govuk-frontend integration patterns for One Login; ideal Library reference for ArcKit's INT-001 implementation.

**Citation**: GOL-ONBOARD-EX-1.

---

#### Candidate 4: govuk-one-login/authentication-api — Library (74/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | govuk-one-login |
| **Repository URL** | https://github.com/govuk-one-login/authentication-api |
| **Language** | java |
| **Framework** | terraform |
| **License** | MIT |
| **Stars / Forks** | 17 / 10 |
| **Install** | gradle |

**Description**: Backend infrastructure for the authentication and orchestration components of GOV.UK One Login's digital identity service.

**Score breakdown**: 24/20/20/4/6 — **total 74** (band: Library).

**Rationale**: MIT, Java/Gradle backend infrastructure for the One Login authentication service; useful Reference for OIDC orchestration patterns even if Java is off-stack.

**Citation**: GOL-AUTH-API-1.

---

#### Candidate 5: alphagov/gds-sso — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/gds-sso |
| **Language** | ruby |
| **Framework** | rails |
| **License** | MIT |
| **Stars / Forks** | 25 / 16 |
| **Install** | rubygems (`gem 'gds-sso'`) |

**Description**: OmniAuth adapter to allow apps to sign in via GOV.UK signon.

**Score breakdown**: 24/20/20/2/6 — **total 72** (band: Library).

**Rationale**: MIT, OmniAuth Rails adapter for GDS Signon (alphagov +10 bonus); only useful if Ruby selected for adapter shim — Reference-grade.

**Citation**: ALPHAGOV-GDS-SSO-1.

---

#### Candidate 6: govuk-one-login/authentication-stubs — Library (65/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | govuk-one-login |
| **Repository URL** | https://github.com/govuk-one-login/authentication-stubs |
| **Language** | typescript |
| **License** | MIT |
| **Stars / Forks** | 2 / 1 |
| **Install** | npm |

**Description**: Monorepo containing four authentication stub services (ipv-stub, orchestration-stub, amc-stub, notify-stub) for GOV.UK One Login.

**Score breakdown**: 24/13/10/12/6 — **total 65** (band: Library).

**Rationale**: MIT, TypeScript stub services for One Login local dev; complement to the simulator for finer-grained CI test seams.

**Citation**: GOL-AUTH-STUBS-1.

---

#### Candidate 7: govuk-one-login/authentication-frontend — Library (63/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | govuk-one-login |
| **Repository URL** | https://github.com/govuk-one-login/authentication-frontend |
| **Language** | typescript |
| **Framework** | express, govuk-frontend |
| **License** | Unknown |
| **Stars / Forks** | 10 / 9 |
| **Install** | npm (`npm run install`) |

**Description**: Authentication frontend for the GOV.UK One Login digital identity platform.

**Score breakdown**: 4/20/20/13/6 — **total 63** (band: Library).

**Rationale**: TypeScript+Express+govuk-frontend One Login user-facing auth flows; LICENSE not located by reader so licence=Unknown forces caution despite high tech alignment.

**Citation**: GOL-AUTH-FE-1.

---

### Capability 3: Multi-tenant SaaS isolation and per-tenant RBAC framework

**Verdict: Fork — `alphagov/digitalmarketplace-api` is the closest UK-gov reference for tenant-style RBAC and per-supplier separation; fork to inform ArcKit's isolation kernel rather than to depend on at runtime.**

---

#### Candidate 1: alphagov/digitalmarketplace-api — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/digitalmarketplace-api |
| **Language** | python |
| **Framework** | flask |
| **License** | MIT |
| **Stars / Forks** | 34 / 21 |
| **Install** | clone-only (`make run-all`) |

**Description**: API application for Digital Marketplace — Flask Python interface to a PostgreSQL database.

**Score breakdown**: 24/20/20/12/6 — **total 82** (band: Fork).

**Rationale**: MIT, GDS-maintained Python/Flask Digital Marketplace API (alphagov +10 bonus); patterns for per-supplier separation, RBAC (Support/Category/Admin Manager), API-first architecture inform FR-002/NFR-SEC-002. Reference-grade — not a turnkey isolation framework.

**Citation**: ALPHAGOV-DM-API-1.

---

#### Candidate 2: ministryofjustice/cloud-platform-environments — Library (75/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/cloud-platform-environments |
| **Framework** | terraform, kubernetes-helm |
| **License** | MIT |
| **Stars / Forks** | 78 / 39 |
| **Install** | terraform-module |

**Description**: Environment configuration for the MoJ Cloud Platform — multi-tenant Kubernetes namespaces and AWS resources across clusters.

**Score breakdown**: 24/20/20/6/6 — **total 75** (band: Library).

**Rationale**: MIT, MoJ Cloud Platform multi-tenant Kubernetes namespace and AWS-resource configuration (ministryofjustice +8 bonus); Reference for namespace-per-tenant isolation patterns.

**Citation**: MOJ-CP-ENV-1.

---

#### Candidate 3: alphagov/paas-cf — Library (61/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/paas-cf |
| **Language** | go |
| **Framework** | terraform |
| **License** | MIT |
| **Stars / Forks** | 84 / 28 |
| **Archived** | yes |
| **Install** | fork-and-build |

**Description**: GOV.UK Platform as a Service deployment of Cloud Foundry on AWS (archived October 2025).

**Score breakdown**: 24/12/20/4/1 — **total 61** (band: Library).

**Rationale**: MIT, GDS Cloud Foundry PaaS — ARCHIVED Oct 2025; informative Reference for tenant-isolation orgs/spaces patterns but not adoptable code.

**Citation**: ALPHAGOV-PAAS-CF-1.

---

#### Candidate 4: alphagov/govuk-account-manager-prototype — None (19/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk-account-manager-prototype |
| **Language** | ruby |
| **Framework** | rails |
| **License** | Unknown |
| **Archived** | yes |

**Score breakdown**: 4/2/10/2/1 — **total 19** (band: None).

**Rationale**: Unknown licence and ARCHIVED Nov 2021 prototype account manager (alphagov bonus capped by archived penalty); not suitable for reuse.

**Citation**: ALPHAGOV-ACCT-MGR-1.

---

### Capability 4: Tamper-evident audit logging and structured telemetry library

**Verdict: Library — `alphagov/govuk_app_config` is the GDS-maintained structured-logging/OpenTelemetry/Prometheus reference; complement with `ministryofjustice/hmpps-audit-api` for queue-driven audit-event capture.**

---

#### Candidate 1: alphagov/govuk_app_config — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk_app_config |
| **Language** | ruby |
| **Framework** | rails |
| **License** | MIT |
| **Stars / Forks** | 10 / 3 |
| **Install** | rubygems (`gem govuk_app_config`) |

**Description**: Gem to configure GOV.UK Ruby applications — JSON structured logging, Govuk-Request-Id propagation, Prometheus metrics, OpenTelemetry instrumentation.

**Score breakdown**: 24/20/20/2/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS Ruby gem (alphagov +10 bonus); off-stack but Reference for required telemetry primitives.

**Citation**: ALPHAGOV-APP-CONFIG-1.

---

#### Candidate 2: ministryofjustice/hmpps-audit-api — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/hmpps-audit-api |
| **Language** | kotlin |
| **Framework** | spring-boot |
| **License** | MIT |
| **Stars / Forks** | 0 / 2 |
| **Install** | gradle (`./gradlew build`) |

**Description**: Audit microservice consuming AuditEvent messages from a queue and persisting to Postgres.

**Score breakdown**: 24/20/20/2/6 — **total 72** (band: Library).

**Rationale**: MIT, MoJ HMPPS audit microservice (Kotlin/Spring Boot, ministryofjustice +8 bonus); Reference for queue-driven audit-event capture pattern.

**Citation**: MOJ-HMPPS-AUDIT-API-1.

---

#### Candidate 3: ministryofjustice/hmpps-spring-boot-sqs — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/hmpps-spring-boot-sqs |
| **Language** | kotlin |
| **Framework** | spring-boot |
| **License** | MIT |
| **Stars / Forks** | 2 / 1 |
| **Install** | gradle |

**Description**: Spring Boot starter library for Amazon SQS/SNS — distributed tracing spans, telemetry events for DLQ messages, configurable trace propagation.

**Score breakdown**: 24/20/20/2/6 — **total 72** (band: Library).

**Rationale**: MIT, MoJ HMPPS Spring Boot starter (Kotlin, ministryofjustice +8 bonus); Reference for SQS/SNS-backed audit event distribution.

**Citation**: MOJ-HMPPS-SQS-1.

---

#### Candidate 4: ministryofjustice/hmpps-audit-poc-ui — Library (68/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/hmpps-audit-poc-ui |
| **Language** | typescript |
| **Framework** | express |
| **License** | MIT |
| **Archived** | yes |
| **Install** | npm |

**Description**: POC investigating capture of audit information for frontend applications.

**Score breakdown**: 24/12/20/12/1 — **total 68** (band: Library).

**Rationale**: MIT, MoJ POC TypeScript+Express UI for capturing front-end audit information (ministryofjustice +8 bonus) — ARCHIVED; informative Reference for browser-side audit-event capture.

**Citation**: MOJ-HMPPS-AUDIT-UI-1.

---

#### Candidate 5: alphagov/paas-auditor — Library (63/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/paas-auditor |
| **Language** | go |
| **License** | MIT |
| **Archived** | yes |
| **Install** | fork-and-build (`make`) |

**Description**: Stores Cloud Foundry audit events in a Postgres database.

**Score breakdown**: 24/12/20/6/1 — **total 63** (band: Library).

**Rationale**: MIT, GDS Cloud Foundry audit-event Postgres store (alphagov +10 bonus) — ARCHIVED; informative pattern for audit persistence but not adoptable code.

**Citation**: ALPHAGOV-PAAS-AUDITOR-1.

---

### Capability 5: Companies House SME verification client and onboarding workflow

**Verdict: Fork — `companieshouse/overseas-entities-web` is a ts/express/govuk-frontend reference web service that aligns with ArcKit's preferred stack; complement with `companieshouse/api-sdk-node` as the production SDK.**

---

#### Candidate 1: companieshouse/overseas-entities-web — Fork (83/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | companieshouse |
| **Repository URL** | https://github.com/companieshouse/overseas-entities-web |
| **Language** | typescript |
| **Framework** | express, govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 8 / 5 |
| **Install** | docker |

**Description**: Web front-end for the register an overseas entity service.

**Score breakdown**: 24/20/20/13/6 — **total 83** (band: Fork).

**Rationale**: MIT, Companies House TS+Express+govuk-frontend overseas-entities web service; reference implementation that aligns with ArcKit's preferred stack and demonstrates BR-003/FR-001 verification flows end-to-end.

**Citation**: CH-OE-WEB-1.

---

#### Candidate 2: companieshouse/api-sdk-node — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | companieshouse |
| **Repository URL** | https://github.com/companieshouse/api-sdk-node |
| **Language** | typescript |
| **Framework** | openapi |
| **License** | MIT |
| **Last Commit** | 2026-05-01 |
| **Stars / Forks** | 18 / 7 |
| **Install** | npm (`npm i @companieshouse/api-sdk-node`) |

**Description**: Node.js SDK that abstracts the calls to Companies House public APIs.

**Score breakdown**: 24/20/10/14/15 — **total 82** (band: Fork).

**Rationale**: MIT, official Companies House TypeScript SDK (active May 2026); first-class fit for INT-003 — `npm install @companieshouse/api-sdk-node`.

**Citation**: CH-API-SDK-NODE-1.

---

#### Candidate 3: companieshouse/confirmation-statement-web — Library (73/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | companieshouse |
| **Repository URL** | https://github.com/companieshouse/confirmation-statement-web |
| **Language** | typescript |
| **Framework** | express, govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 1 / 1 |
| **Install** | docker |

**Description**: Web front end for Confirmation Statement service.

**Score breakdown**: 24/20/10/13/6 — **total 73** (band: Library).

**Rationale**: MIT, Companies House TS+Express+govuk-frontend Confirmation Statement web service; second reference of CH onboarding patterns.

**Citation**: CH-CS-WEB-1.

---

#### Candidate 4: kevbite/CompaniesHouse.NET — Library (71/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | kevbite |
| **Repository URL** | https://github.com/kevbite/CompaniesHouse.NET |
| **Language** | csharp |
| **Framework** | dotnet-core, aspnet |
| **License** | MIT |
| **Last Commit** | 2026-04-14 |
| **Stars / Forks** | 40 / 44 |
| **Install** | nuget (`Install-Package CompaniesHouse`) |

**Description**: A simple .NET client wrapper for Companies House API.

**Score breakdown**: 24/20/10/2/15 — **total 71** (band: Library).

**Rationale**: MIT, well-maintained .NET Companies House client (community); only relevant if .NET stack adopted later — not first choice.

**Citation**: KEVBITE-CHNET-1.

---

#### Candidate 5: nicholasamorim/chuk — Library (71/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | nicholasamorim |
| **Repository URL** | https://github.com/nicholasamorim/chuk |
| **Language** | python |
| **License** | MIT |
| **Stars / Forks** | 4 / 3 |
| **Install** | pypi |

**Description**: Beta client for the Companies House Beta API.

**Score breakdown**: 24/15/10/16/6 — **total 71** (band: Library).

**Rationale**: MIT, community Python beta client for Companies House Beta API; useful if Python chosen for verification microservice.

**Citation**: NAMORIM-CHUK-1.

---

#### Candidate 6: jimsmart/chapi — Library (66/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | jimsmart |
| **Repository URL** | https://github.com/jimsmart/chapi |
| **Language** | go |
| **License** | MIT |
| **Stars / Forks** | 2 / 0 |
| **Install** | go-module (`go get github.com/jimsmart/chapi`) |

**Description**: Go package providing clients and data structures for the Companies House API.

**Score breakdown**: 24/20/10/6/6 — **total 66** (band: Library).

**Rationale**: MIT, Go Companies House client (community); off-stack — Reference only for Go services.

**Citation**: JIMSMART-CHAPI-1.

---

#### Candidate 7: mikemaccana/companies-house — Reference (44/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | mikemaccana |
| **Repository URL** | https://github.com/mikemaccana/companies-house |
| **Language** | javascript |
| **License** | (not found) |
| **Stars / Forks** | 7 / 3 |

**Score breakdown**: 4/8/10/16/6 — **total 44** (band: Reference).

**Rationale**: Licence missing on repo page; thin JS search wrapper — Reference-only pattern, not adoptable without licence verification.

**Citation**: MIKEMACCANA-CH-1.

---

### Capability 6: GOV.UK Notify transactional email and notification client

**Verdict: Fork — `alphagov/notifications-api` is the upstream Notify backend (Python/Flask); for client integration use `notifications-python-client` or `notifications-node-client` Library SDKs depending on stack.**

---

#### Candidate 1: alphagov/notifications-api — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-api |
| **Language** | python |
| **Framework** | flask |
| **License** | MIT |
| **Stars / Forks** | 76 / 32 |
| **Install** | fork-and-build |

**Description**: Public-facing REST API for GOV.UK Notify; internal Flask REST API to manage services/users/templates; async Celery workers.

**Score breakdown**: 24/20/20/12/6 — **total 82** (band: Fork).

**Rationale**: MIT, GDS Notify backend (Python/Flask, alphagov +10 bonus) — Reference for tenant-aware notification API design including per-service API keys, team RBAC, async dispatch via Celery.

**Citation**: ALPHAGOV-NOTIFY-API-1.

---

#### Candidate 2: alphagov/notifications-python-client — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-python-client |
| **Language** | python |
| **License** | MIT |
| **Stars / Forks** | 24 / 23 |
| **Install** | pypi (`pip install notifications-python-client`) |

**Description**: Use this client to send emails, text messages and letters using the GOV.UK Notify API.

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, official GOV.UK Notify Python SDK (alphagov +10 bonus); first-class fit for INT-004 if Python selected for transactional service.

**Citation**: ALPHAGOV-NOTIFY-PY-1.

---

#### Candidate 3: alphagov/notifications-node-client — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-node-client |
| **Language** | javascript |
| **License** | MIT |
| **Stars / Forks** | 18 / 14 |
| **Install** | npm (`npm install notifications-node-client`) |

**Description**: Use this client to send emails, text messages and letters using the GOV.UK Notify API.

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, official GOV.UK Notify Node.js SDK (alphagov +10 bonus); first-class fit for INT-004 on JS/TS stack.

**Citation**: ALPHAGOV-NOTIFY-NODE-1.

---

#### Candidate 4: alphagov/notifications-ruby-client — Library (62/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-ruby-client |
| **Language** | ruby |
| **License** | MIT |
| **Stars / Forks** | 12 / 15 |
| **Install** | rubygems (`gem install notifications-ruby-client`) |

**Score breakdown**: 24/20/10/2/6 — **total 62** (band: Library).

**Rationale**: MIT, official GOV.UK Notify Ruby gem (alphagov +10 bonus); only useful if Ruby chosen.

**Citation**: ALPHAGOV-NOTIFY-RB-1.

---

#### Candidate 5: alphagov/notifications-java-client — Library (62/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-java-client |
| **Language** | java |
| **License** | MIT |
| **Stars / Forks** | 8 / 31 |
| **Install** | maven |

**Score breakdown**: 24/20/10/2/6 — **total 62** (band: Library).

**Rationale**: MIT, official GOV.UK Notify Java SDK (alphagov +10 bonus); off-stack — Reference only.

**Citation**: ALPHAGOV-NOTIFY-JAVA-1.

---

#### Candidate 6: alphagov/notifications-php-client — Library (62/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-php-client |
| **Language** | php |
| **License** | MIT |
| **Stars / Forks** | 11 / 15 |
| **Install** | composer |

**Score breakdown**: 24/20/10/2/6 — **total 62** (band: Library).

**Rationale**: MIT, official GOV.UK Notify PHP SDK (alphagov +10 bonus); off-stack — Reference only.

**Citation**: ALPHAGOV-NOTIFY-PHP-1.

---

#### Candidate 7: alphagov/notifications-net-client — Reference (57/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-net-client |
| **Language** | csharp |
| **Framework** | dotnet-core |
| **License** | MIT |
| **Stars / Forks** | 25 / 22 |
| **Install** | nuget (`Install-Package GovukNotify`) |

**Score breakdown**: 24/15/10/2/6 — **total 57** (band: Reference).

**Rationale**: MIT, official GOV.UK Notify .NET SDK (alphagov +10 bonus, no has_tests in evidence reduced cq); off-stack — Reference only.

**Citation**: ALPHAGOV-NOTIFY-NET-1.

---

### Capability 7: AI and LLM provider abstraction layer for government services

**Verdict: Fork — `i-dot-ai/consult` is the highest-scored active i.AI app (last commit 2026-05-06) demonstrating AI+human-in-the-loop; complement with `i-dot-ai/lex` (FastAPI semantic search) and `i-dot-ai/i-dot-ai-utilities` (LiteLLM-based).**

---

#### Candidate 1: i-dot-ai/consult — Fork (92/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | i-dot-ai |
| **Repository URL** | https://github.com/i-dot-ai/consult |
| **Language** | python |
| **Framework** | django, terraform |
| **License** | MIT |
| **Last Commit** | 2026-05-06 |
| **Stars / Forks** | 54 / 17 |
| **Install** | clone-only (`make install && make setup`) |

**Description**: Web application combining AI with human oversight to process public consultation responses at scale.

**Score breakdown**: 24/20/20/13/15 — **total 92** (band: Fork).

**Rationale**: MIT, i.AI Cabinet Office Django+Terraform 'Consult' app (last commit 1 day ago) — extensive evidence of AI+human-in-the-loop pattern; closest UK gov reference for FR-004 even though not a turnkey provider abstraction.

**Citation**: IDOTAI-CONSULT-1.

---

#### Candidate 2: i-dot-ai/lex — Fork (91/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | i-dot-ai |
| **Repository URL** | https://github.com/i-dot-ai/lex |
| **Language** | python |
| **Framework** | fastapi |
| **License** | MIT |
| **Last Commit** | 2026-03-23 |
| **Stars / Forks** | 47 / 22 |
| **Install** | docker (`docker compose up -d`) |

**Description**: UK legal API for AI agents and researchers — semantic search and Model Context Protocol; uses Azure OpenAI.

**Score breakdown**: 24/20/20/12/15 — **total 91** (band: Fork).

**Rationale**: MIT, i.AI 'lex' FastAPI service exposing UK legislation via semantic search and Model Context Protocol; uses Azure OpenAI through pluggable seam — best Reference for INT-005 abstraction pattern in production.

**Citation**: IDOTAI-LEX-1.

---

#### Candidate 3: i-dot-ai/i-dot-ai-utilities — Fork (82/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | i-dot-ai |
| **Repository URL** | https://github.com/i-dot-ai/i-dot-ai-utilities |
| **Language** | python |
| **License** | MIT |
| **Stars / Forks** | 2 / 1 |
| **Install** | pypi (`pip install i-dot-ai-utilities`) |

**Description**: Python package providing common utilities — logging, metrics, file storage, LLM proxy via LiteLLM.

**Score breakdown**: 24/20/20/12/6 — **total 82** (band: Fork).

**Rationale**: MIT, i.AI Python utilities package including LiteLLM proxy capabilities (logging, metrics, file storage); closest UK gov library to a true LLM provider abstraction — adopt as Library for INT-005 pluggability.

**Citation**: IDOTAI-UTIL-1.

---

#### Candidate 4: i-dot-ai/redbox — Library (67/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | i-dot-ai |
| **Repository URL** | https://github.com/i-dot-ai/redbox |
| **Language** | python |
| **Framework** | django |
| **License** | MIT |
| **Last Commit** | 2025-10-27 |
| **Stars / Forks** | 137 / 51 |
| **Archived** | yes |
| **Install** | docker (`docker compose up`) |

**Description**: GenAI app to chat with and summarise civil service documents; LangGraph + AISettings.

**Score breakdown**: 24/10/20/12/1 — **total 67** (band: Library).

**Rationale**: MIT, i.AI 'redbox' civil-service GenAI doc summariser — ARCHIVED Oct 2025; informative Reference for AISettings provider-switching pattern but no active code path.

**Citation**: IDOTAI-REDBOX-1.

---

#### Candidate 5: i-dot-ai/caddy-chatbot — Library (67/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | i-dot-ai |
| **Repository URL** | https://github.com/i-dot-ai/caddy-chatbot |
| **Language** | python |
| **Framework** | fastapi |
| **License** | MIT |
| **Stars / Forks** | 24 / 9 |
| **Archived** | yes |
| **Install** | clone-only (`poetry install && poetry shell`) |

**Description**: LLM-powered customer service co-pilot using AWS Bedrock.

**Score breakdown**: 24/10/20/12/1 — **total 67** (band: Library).

**Rationale**: MIT, i.AI 'caddy-chatbot' AWS-Bedrock-backed customer service co-pilot — ARCHIVED; Reference for Bedrock provider integration patterns.

**Citation**: IDOTAI-CADDY-1.

---

#### Candidate 6: alphagov/govuk-chat — Library (66/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk-chat |
| **Language** | ruby |
| **Framework** | rails |
| **License** | MIT |
| **Last Commit** | 2026-05-07 |
| **Stars / Forks** | 13 / 3 |
| **Install** | rubygems (`bundle install`) |

**Description**: LLM-powered chat experience over GOV.UK content — integrates Anthropic Claude and AWS Bedrock.

**Score breakdown**: 24/15/10/2/15 — **total 66** (band: Library).

**Rationale**: MIT, GDS GOV.UK Chat (alphagov +10 bonus, last commit today) — integrates Anthropic Claude + AWS Bedrock; off-stack but live Reference for chat UX over GOV.UK content.

**Citation**: ALPHAGOV-CHAT-1.

---

#### Candidate 7: i-dot-ai/coding-agent-litellm-config — Reference (52/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | i-dot-ai |
| **Repository URL** | https://github.com/i-dot-ai/coding-agent-litellm-config |
| **Language** | python |
| **License** | Unknown |
| **Stars / Forks** | 0 / 1 |
| **Install** | clone-only |

**Score breakdown**: 4/20/10/12/6 — **total 52** (band: Reference).

**Rationale**: Licence not visible (Unknown); LiteLLM proxy config mapping Azure/Bedrock/Vertex/OpenAI/Anthropic/Gemini/Mistral — Reference for multi-provider routing config.

**Citation**: IDOTAI-LITELLM-1.

---

### Capability 8: AWS multi-cloud landing-zone IaC for UK-resident SaaS workloads

**Verdict: Fork — `ministryofjustice/cloud-platform-terraform-rds-instance` and `cloud-platform-terraform-s3-bucket` are first-class Terraform modules for INT-006 Postgres and object storage on AWS; cherry-pick alongside Reference repos for full landing-zone patterns.**

---

#### Candidate 1: ministryofjustice/cloud-platform-terraform-rds-instance — Fork (80/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/cloud-platform-terraform-rds-instance |
| **Framework** | terraform |
| **License** | MIT |
| **Last Commit** | 2025-10-23 |
| **Stars / Forks** | 4 / 7 |
| **Install** | terraform-module |

**Description**: Terraform module that creates an Amazon RDS database for use on the Cloud Platform.

**Score breakdown**: 24/20/20/4/12 — **total 80** (band: Fork).

**Rationale**: MIT, MoJ Cloud Platform RDS Terraform module (ministryofjustice +8 bonus); first-class Library for INT-006 Postgres provisioning on AWS UK-region.

**Citation**: MOJ-CP-RDS-1.

---

#### Candidate 2: ministryofjustice/cloud-platform-terraform-s3-bucket — Fork (80/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/cloud-platform-terraform-s3-bucket |
| **Framework** | terraform |
| **License** | MIT |
| **Last Commit** | 2025-07-10 |
| **Stars / Forks** | 2 / 12 |
| **Install** | terraform-module |

**Description**: Terraform module that creates an Amazon S3 bucket for the Cloud Platform.

**Score breakdown**: 24/20/20/4/12 — **total 80** (band: Fork).

**Rationale**: MIT, MoJ Cloud Platform S3 Terraform module (ministryofjustice +8 bonus); first-class Library for object storage provisioning per INT-006.

**Citation**: MOJ-CP-S3-1.

---

#### Candidate 3: ministryofjustice/cloud-platform-infrastructure — Library (75/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/cloud-platform-infrastructure |
| **Framework** | terraform, kubernetes-helm |
| **License** | MIT |
| **Stars / Forks** | 66 / 32 |
| **Install** | terraform-module |

**Score breakdown**: 24/20/20/6/6 — **total 75** (band: Library).

**Rationale**: MIT, MoJ Cloud Platform Kubernetes turn-up (ministryofjustice +8 bonus); Reference and partial Fork target for k8s+Terraform tenant clusters per NFR-A-001/S-001.

**Citation**: MOJ-CP-INFRA-1.

---

#### Candidate 4: ministryofjustice/modernisation-platform — Library (74/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | ministryofjustice |
| **Repository URL** | https://github.com/ministryofjustice/modernisation-platform |
| **Framework** | terraform |
| **License** | MIT |
| **Stars / Forks** | 722 / 289 |
| **Install** | terraform-module |

**Score breakdown**: 24/20/20/4/6 — **total 74** (band: Library).

**Rationale**: MIT, MoJ Modernisation Platform — 722★, well-documented Reference for AWS multi-account landing zone (member-account-per-team); inform NFR-A-001/A-002/SEC-002 design without wholesale fork.

**Citation**: MOJ-MODPLAT-1.

---

#### Candidate 5: alphagov/govuk-infrastructure — Library (70/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk-infrastructure |
| **Framework** | terraform, kubernetes-helm |
| **License** | MIT |
| **Stars / Forks** | 191 / 33 |
| **Install** | terraform-module (`brew install tfenv && cd terraform/ && tfenv install latest && tfenv use latest`) |

**Score breakdown**: 24/15/20/6/6 — **total 70** (band: Library).

**Rationale**: MIT, GDS govuk-infrastructure (alphagov +10 bonus) — Terraform + Helm for full GOV.UK platform; Reference for tfenv-managed Terraform pipeline patterns.

**Citation**: ALPHAGOV-INFRA-1.

---

#### Candidate 6: alphagov/govuk-helm-charts — Library (69/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/govuk-helm-charts |
| **Framework** | kubernetes-helm |
| **License** | MIT |
| **Stars / Forks** | 24 / 6 |
| **Install** | helm (`helm repo add govuk-helm-charts`) |

**Score breakdown**: 24/15/20/4/6 — **total 69** (band: Library).

**Rationale**: MIT, GDS GOV.UK Helm charts (alphagov +10 bonus); Reference for Argo CD-driven Helm deployment patterns supporting NFR-A-001 high availability.

**Citation**: ALPHAGOV-HELM-1.

---

#### Candidate 7: DFE-Digital/terraform-azurerm-container-apps-hosting — Library (68/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | DFE-Digital |
| **Repository URL** | https://github.com/DFE-Digital/terraform-azurerm-container-apps-hosting |
| **Framework** | terraform |
| **License** | MIT |
| **Stars / Forks** | 19 / 14 |
| **Install** | terraform-module (`source = github.com/DFE-Digital/terraform-azurerm-container-apps-hosting`) |

**Score breakdown**: 24/15/20/4/6 — **total 68** (band: Library).

**Rationale**: MIT, DfE Digital Azure Container Apps Terraform module (dfe-digital +8 bonus); useful Library for Azure UK-South alternative if multi-cloud abstraction needed (TC-3).

**Citation**: DFE-TF-AZ-CA-1.

---

#### Candidate 8: hmrc/terraform-aws-vpc — Library (67/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | hmrc |
| **Repository URL** | https://github.com/hmrc/terraform-aws-vpc |
| **Framework** | terraform |
| **License** | Apache-2.0 |
| **Stars / Forks** | 1 / 0 |
| **Install** | terraform-module |

**Score breakdown**: 24/13/20/4/6 — **total 67** (band: Library).

**Rationale**: Apache-2.0, HMRC fork of terraform-aws-vpc; minimal community traction but legitimate licence and fresh — Reference for HMRC-style VPC baselining.

**Citation**: HMRC-TF-VPC-1.

---

### Capability 9: G-Cloud Digital Marketplace listing and call-off tooling

**Verdict: Library — `alphagov/digitalmarketplace-api` is the canonical reference for the Digital Marketplace data model and supplier journey; informs INT-008 / BR-004 metadata alignment without a direct dependency.**

---

#### Candidate 1: alphagov/digitalmarketplace-api — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/digitalmarketplace-api |
| **Language** | python |
| **Framework** | flask |
| **License** | MIT |
| **Stars / Forks** | 34 / 21 |
| **Install** | fork-and-build (`make run-all`) |

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS Digital Marketplace API (alphagov +10 bonus); Reference for INT-008 — supplier registration, framework application journey, SQLAlchemy models for procurement data.

**Citation**: ALPHAGOV-DM-API-1.

---

#### Candidate 2: alphagov/digitalmarketplace-utils — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/digitalmarketplace-utils |
| **Language** | python |
| **Framework** | flask |
| **License** | MIT |
| **Stars / Forks** | 4 / 18 |
| **Install** | pypi |

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS Digital Marketplace Python utils library (alphagov +10 bonus) — Flask JSON logging, S3/Notify/Cloudwatch helpers, feature flags; Reference Library for Python-native Marketplace integration.

**Citation**: ALPHAGOV-DM-UTILS-1.

---

#### Candidate 3: alphagov/digitalmarketplace-supplier-frontend — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/digitalmarketplace-supplier-frontend |
| **Language** | python |
| **Framework** | flask |
| **License** | MIT |
| **Stars / Forks** | 11 / 20 |
| **Install** | fork-and-build |

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS Digital Marketplace Supplier Frontend (alphagov +10 bonus); Reference for supplier dashboard and framework application UX patterns aligned with BR-004.

**Citation**: ALPHAGOV-DM-SUPP-FE-1.

---

#### Candidate 4: alphagov/digitalmarketplace-buyer-frontend — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/digitalmarketplace-buyer-frontend |
| **Language** | python |
| **Framework** | flask |
| **License** | MIT |
| **Stars / Forks** | 3 / 14 |
| **Install** | fork-and-build |

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS Digital Marketplace Buyer Frontend (alphagov +10 bonus); Reference for G-Cloud buyer journey UX — relevant to BR-004 callout flows.

**Citation**: ALPHAGOV-DM-BUY-FE-1.

---

#### Candidate 5: alphagov/digitalmarketplace-frameworks — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/digitalmarketplace-frameworks |
| **Language** | python |
| **License** | MIT |
| **Stars / Forks** | 11 / 16 |
| **Install** | npm |

**Score breakdown**: 24/20/10/12/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS Digital Marketplace YAML framework definitions (alphagov +10 bonus); Reference for procurement framework data model and JSON-schema-driven validation patterns.

**Citation**: ALPHAGOV-DM-FRAMEWORKS-1.

---

### Capability 10: Subscription billing and payment processing for government SaaS

**Verdict: Fork — `alphagov/pay-frontend` and `alphagov/pay-selfservice` provide Node/Express/govuk-frontend reference implementations for FR-011 / INT-002 with GOV.UK Design System alignment; complement with Java public-API and admin-users patterns.**

---

#### Candidate 1: alphagov/pay-frontend — Fork (83/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-frontend |
| **Language** | javascript |
| **Framework** | express, govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 12 / 15 |
| **Install** | npm (`npm install && npm run compile`) |

**Score breakdown**: 24/20/20/13/6 — **total 83** (band: Fork).

**Rationale**: MIT, GDS GOV.UK Pay Frontend (Node/Express/govuk-frontend, alphagov +10 bonus); Reference for FR-011 payment UX with GOV.UK Design System alignment.

**Citation**: ALPHAGOV-PAY-FE-1.

---

#### Candidate 2: alphagov/pay-selfservice — Fork (83/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-selfservice |
| **Language** | javascript |
| **Framework** | express, govuk-frontend |
| **License** | MIT |
| **Stars / Forks** | 26 / 16 |
| **Install** | npm (`npm i`) |

**Score breakdown**: 24/20/20/13/6 — **total 83** (band: Fork).

**Rationale**: MIT, GDS GOV.UK Pay Self Service admin tool (Node/Express/govuk-frontend, alphagov +10 bonus); Reference for tenant admin self-service patterns supporting FR-011 + tenant admin UX.

**Citation**: ALPHAGOV-PAY-SS-1.

---

#### Candidate 3: alphagov/pay-publicapi — Library (74/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-publicapi |
| **Language** | java |
| **Framework** | dropwizard, openapi |
| **License** | MIT |
| **Stars / Forks** | 48 / 19 |
| **Install** | maven |

**Score breakdown**: 24/20/20/4/6 — **total 74** (band: Library).

**Rationale**: MIT, GDS GOV.UK Pay Public API (Java/Dropwizard, alphagov +10 bonus); Reference Library for OpenAPI-first payment public API design.

**Citation**: ALPHAGOV-PAY-PUBAPI-1.

---

#### Candidate 4: alphagov/pay-adminusers — Library (72/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-adminusers |
| **Language** | java |
| **Framework** | dropwizard |
| **License** | MIT |
| **Stars / Forks** | 13 / 7 |
| **Install** | maven |

**Score breakdown**: 24/20/20/2/6 — **total 72** (band: Library).

**Rationale**: MIT, GDS GOV.UK Pay Admin Users module (Java/Dropwizard, alphagov +10 bonus); Reference for billing-side user/role separation aligned with NFR-SEC-003.

**Citation**: ALPHAGOV-PAY-AU-1.

---

#### Candidate 5: alphagov/pay-js-commons — Library (67/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-js-commons |
| **Language** | javascript |
| **License** | MIT |
| **Stars / Forks** | 5 / 3 |
| **Install** | npm |

**Score breakdown**: 24/15/10/12/6 — **total 67** (band: Library).

**Rationale**: MIT, GDS reusable JS scripts for GOV.UK Pay Node projects (alphagov +10 bonus); Reference Library for shared JS utilities in payment integration.

**Citation**: ALPHAGOV-PAY-JSC-1.

---

#### Candidate 6: alphagov/pay-products — Reference (57/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-products |
| **Language** | java |
| **Framework** | dropwizard |
| **License** | MIT |
| **Stars / Forks** | 4 / 3 |
| **Install** | maven |

**Score breakdown**: 24/15/10/2/6 — **total 57** (band: Reference).

**Rationale**: MIT, GDS GOV.UK Pay 'Products' microservice (alphagov +10 bonus); Reference for product-link payment patterns — useful for ad-hoc billing URLs.

**Citation**: ALPHAGOV-PAY-PROD-1.

---

#### Candidate 7: alphagov/pay-direct-debit-connector — Reference (52/100)

| Attribute | Value |
|-----------|-------|
| **Organisation** | alphagov |
| **Repository URL** | https://github.com/alphagov/pay-direct-debit-connector |
| **Language** | java |
| **Framework** | dropwizard |
| **License** | MIT |
| **Stars / Forks** | 5 / 5 |
| **Last Commit** | 2021-09-29 |
| **Archived** | yes |
| **Install** | maven |

**Score breakdown**: 24/5/20/2/1 — **total 52** (band: Reference).

**Rationale**: MIT, GDS GOV.UK Pay Direct Debit Connector — ARCHIVED 2021; informative Reference for GoCardless integration pattern only.

**Citation**: ALPHAGOV-PAY-DDC-1.

---

## License Compatibility Matrix

| Repository | License | Compatible with MIT/Apache/OGL constraints |
|------------|---------|---------------------------------------------|
| x-govuk/govuk-eleventy-plugin | MIT | Yes |
| penx/govuk-react | MIT | Yes |
| alphagov/govuk-frontend | MIT | Yes |
| alphagov/govuk-prototype-kit | MIT | Yes |
| nhsuk/nhsuk-frontend | MIT | Yes |
| alphagov/govuk_publishing_components | MIT | Yes |
| govuk-one-login/simulator | MIT | Yes |
| alphagov/signon | MIT | Yes |
| govuk-one-login/onboarding-examples | MIT | Yes |
| govuk-one-login/authentication-api | MIT | Yes |
| alphagov/gds-sso | MIT | Yes |
| govuk-one-login/authentication-stubs | MIT | Yes |
| govuk-one-login/authentication-frontend | Unknown | Caution — verify before adoption |
| alphagov/digitalmarketplace-api | MIT | Yes |
| ministryofjustice/cloud-platform-environments | MIT | Yes |
| alphagov/paas-cf | MIT (archived) | Yes (reference only) |
| alphagov/govuk-account-manager-prototype | Unknown (archived) | No — do not adopt |
| alphagov/govuk_app_config | MIT | Yes |
| ministryofjustice/hmpps-audit-api | MIT | Yes |
| ministryofjustice/hmpps-spring-boot-sqs | MIT | Yes |
| ministryofjustice/hmpps-audit-poc-ui | MIT (archived) | Yes (reference only) |
| alphagov/paas-auditor | MIT (archived) | Yes (reference only) |
| companieshouse/overseas-entities-web | MIT | Yes |
| companieshouse/api-sdk-node | MIT | Yes |
| companieshouse/confirmation-statement-web | MIT | Yes |
| kevbite/CompaniesHouse.NET | MIT | Yes |
| nicholasamorim/chuk | MIT | Yes |
| jimsmart/chapi | MIT | Yes |
| mikemaccana/companies-house | (not found) | No — verify before adoption |
| alphagov/notifications-api | MIT | Yes |
| alphagov/notifications-python-client | MIT | Yes |
| alphagov/notifications-node-client | MIT | Yes |
| alphagov/notifications-ruby-client | MIT | Yes |
| alphagov/notifications-java-client | MIT | Yes |
| alphagov/notifications-php-client | MIT | Yes |
| alphagov/notifications-net-client | MIT | Yes |
| i-dot-ai/consult | MIT | Yes |
| i-dot-ai/lex | MIT | Yes |
| i-dot-ai/i-dot-ai-utilities | MIT | Yes |
| i-dot-ai/redbox | MIT (archived) | Yes (reference only) |
| i-dot-ai/caddy-chatbot | MIT (archived) | Yes (reference only) |
| alphagov/govuk-chat | MIT | Yes |
| i-dot-ai/coding-agent-litellm-config | Unknown | Caution — verify before adoption |
| ministryofjustice/cloud-platform-terraform-rds-instance | MIT | Yes |
| ministryofjustice/cloud-platform-terraform-s3-bucket | MIT | Yes |
| ministryofjustice/cloud-platform-infrastructure | MIT | Yes |
| ministryofjustice/modernisation-platform | MIT | Yes |
| alphagov/govuk-infrastructure | MIT | Yes |
| alphagov/govuk-helm-charts | MIT | Yes |
| DFE-Digital/terraform-azurerm-container-apps-hosting | MIT | Yes |
| hmrc/terraform-aws-vpc | Apache-2.0 | Yes |
| alphagov/digitalmarketplace-utils | MIT | Yes |
| alphagov/digitalmarketplace-supplier-frontend | MIT | Yes |
| alphagov/digitalmarketplace-buyer-frontend | MIT | Yes |
| alphagov/digitalmarketplace-frameworks | MIT | Yes |
| alphagov/pay-frontend | MIT | Yes |
| alphagov/pay-selfservice | MIT | Yes |
| alphagov/pay-publicapi | MIT | Yes |
| alphagov/pay-adminusers | MIT | Yes |
| alphagov/pay-js-commons | MIT | Yes |
| alphagov/pay-products | MIT | Yes |
| alphagov/pay-direct-debit-connector | MIT (archived) | Yes (reference only) |

**Notes**: All in-band candidates carry MIT licences except `hmrc/terraform-aws-vpc` (Apache-2.0, also compatible). Two candidates (`govuk-one-login/authentication-frontend`, `i-dot-ai/coding-agent-litellm-config`) and one None-band (`govuk-account-manager-prototype`) had Unknown/missing licences and are flagged for legal verification before any adoption. The `mikemaccana/companies-house` Reference-band entry is similarly flagged.

---

## Tech Stack Alignment

| Repository | Language | Framework | Aligns With Project Profile |
|------------|----------|-----------|------------------------------|
| x-govuk/govuk-eleventy-plugin | javascript | govuk-frontend | Yes (preferred JS+govuk-frontend) |
| penx/govuk-react | typescript | react, govuk-frontend | Yes (preferred TS+react/Next.js context) |
| alphagov/govuk-frontend | javascript | govuk-frontend | Yes |
| alphagov/govuk-prototype-kit | javascript | govuk-prototype-kit, express | Yes |
| nhsuk/nhsuk-frontend | javascript | other | Yes (NHS sector tenancies) |
| alphagov/govuk_publishing_components | ruby | rails, govuk-frontend | No (off-stack) |
| govuk-one-login/simulator | typescript | express | Yes |
| alphagov/signon | ruby | rails | No |
| govuk-one-login/onboarding-examples | typescript | express, govuk-frontend | Yes |
| govuk-one-login/authentication-api | java | terraform | No |
| alphagov/gds-sso | ruby | rails | No |
| govuk-one-login/authentication-stubs | typescript | other | Yes |
| govuk-one-login/authentication-frontend | typescript | express, govuk-frontend | Yes |
| alphagov/digitalmarketplace-api | python | flask | Yes (Python) |
| ministryofjustice/cloud-platform-environments | other | terraform, kubernetes-helm | Yes |
| alphagov/paas-cf | go | terraform | Partial (Terraform only) |
| alphagov/govuk_app_config | ruby | rails | No |
| ministryofjustice/hmpps-audit-api | kotlin | spring-boot | No |
| ministryofjustice/hmpps-spring-boot-sqs | kotlin | spring-boot | No |
| ministryofjustice/hmpps-audit-poc-ui | typescript | express | Yes |
| alphagov/paas-auditor | go | — | No |
| companieshouse/overseas-entities-web | typescript | express, govuk-frontend | Yes |
| companieshouse/api-sdk-node | typescript | openapi | Yes |
| companieshouse/confirmation-statement-web | typescript | express, govuk-frontend | Yes |
| kevbite/CompaniesHouse.NET | csharp | dotnet-core | No |
| nicholasamorim/chuk | python | — | Yes (Python) |
| jimsmart/chapi | go | — | No |
| alphagov/notifications-api | python | flask | Yes |
| alphagov/notifications-python-client | python | — | Yes |
| alphagov/notifications-node-client | javascript | — | Yes |
| alphagov/notifications-ruby-client | ruby | — | No |
| alphagov/notifications-java-client | java | — | No |
| alphagov/notifications-php-client | php | — | No |
| alphagov/notifications-net-client | csharp | dotnet-core | No |
| i-dot-ai/consult | python | django, terraform | Yes |
| i-dot-ai/lex | python | fastapi | Yes |
| i-dot-ai/i-dot-ai-utilities | python | other | Yes |
| i-dot-ai/redbox | python | django, other | Yes |
| i-dot-ai/caddy-chatbot | python | fastapi | Yes |
| alphagov/govuk-chat | ruby | rails | No |
| ministryofjustice/cloud-platform-terraform-rds-instance | other | terraform | Yes |
| ministryofjustice/cloud-platform-terraform-s3-bucket | other | terraform | Yes |
| ministryofjustice/cloud-platform-infrastructure | other | terraform, kubernetes-helm | Yes |
| ministryofjustice/modernisation-platform | other | terraform | Yes |
| alphagov/govuk-infrastructure | other | terraform, kubernetes-helm | Yes |
| alphagov/govuk-helm-charts | other | kubernetes-helm | Yes |
| DFE-Digital/terraform-azurerm-container-apps-hosting | other | terraform | Yes |
| hmrc/terraform-aws-vpc | other | terraform | Yes |
| alphagov/digitalmarketplace-utils | python | flask | Yes |
| alphagov/digitalmarketplace-supplier-frontend | python | flask | Yes |
| alphagov/digitalmarketplace-buyer-frontend | python | flask | Yes |
| alphagov/digitalmarketplace-frameworks | python | other | Yes |
| alphagov/pay-frontend | javascript | express, govuk-frontend | Yes |
| alphagov/pay-selfservice | javascript | express, govuk-frontend | Yes |
| alphagov/pay-publicapi | java | dropwizard, openapi | No |
| alphagov/pay-adminusers | java | dropwizard | No |
| alphagov/pay-js-commons | javascript | other | Yes |
| alphagov/pay-products | java | dropwizard | No |
| alphagov/pay-direct-debit-connector | java | dropwizard | No |

**Project Tech Stack**: typescript / javascript / python; nextjs, govuk-frontend, openapi, terraform, kubernetes-helm.

---

## Gap Analysis

| Capability | Status | Notes | Recommended Action |
|------------|--------|-------|--------------------|
| Tamper-evident append-only audit log library (cryptographic hash chain) | No match | No UK gov repo found that specifically implements tamper-evident hash-chained audit storage; closest active candidates are structured-logging libraries (govuk_app_config) or generic audit microservices (hmpps-audit-api). | Build new — see ARC-001-ADR for hash-chain decision |
| Multi-tenant SaaS isolation framework (per-tenant data partitioning + RBAC kernel) | No match | No purpose-built UK gov multi-tenant isolation framework located. Top candidates (alphagov/notifications-api, alphagov/digitalmarketplace-api, MoJ Cloud Platform) are reference patterns inferred from production services, not turnkey libraries. | Build new with isolation tests in CI per NFR-SEC-002 |
| Markdown / AsciiDoc renderer with GOV.UK styling | No match | Carried forward from v1.0: no UK gov library combining markdown rendering with GOV.UK styling found. | Use upstream OSS (markdown-it / Asciidoctor) styled with govuk-frontend |
| Mermaid / PlantUML rendering pipeline | No match | Carried forward from v1.0: no UK gov repo implements diagram-rendering pipelines. | Use upstream OSS (mermaid-js, plantuml) |
| EA tooling adapter (LeanIX / Ardoq / MEGA) | No match | No UK gov code found and out of scope for v1; deferred to importer roadmap. | Defer to v2 |
| True LLM provider abstraction layer (vendor-agnostic gateway) | Partial | Closest candidates are integrated apps (i-dot-ai/lex, i-dot-ai/consult, alphagov/govuk-chat) using LiteLLM/AISettings as embedded patterns, not a freestanding library. | Reference these patterns and build a thin abstraction; consider depending on upstream LiteLLM directly |

---

## Requirements Traceability

| Requirement ID | Capability | Best Candidate | Strategy | Status |
|---|---|---|---|---|
| BR-001 | GOV.UK Design System frontend components and accessible web UI | alphagov/govuk-frontend | Fork | matched |
| BR-003 | Companies House SME verification client and onboarding workflow | companieshouse/api-sdk-node | Fork | matched |
| BR-004 | G-Cloud Digital Marketplace listing and call-off tooling | alphagov/digitalmarketplace-api | Library | matched |
| BR-006 | (evidence pack — bespoke generation) | — | None | build required |
| BR-007 | (tenant export — bespoke build) | — | None | build required |
| FR-001 | Companies House SME verification client and onboarding workflow | companieshouse/overseas-entities-web | Fork | matched |
| FR-002 | Multi-tenant SaaS isolation and per-tenant RBAC framework | alphagov/digitalmarketplace-api | Reference | Reference only |
| FR-003 | (artefact authoring — bespoke build) | — | None | build required |
| FR-004 | AI and LLM provider abstraction layer for government services | i-dot-ai/i-dot-ai-utilities | Fork | matched |
| FR-005 | Tamper-evident audit logging and structured telemetry library | alphagov/govuk_app_config | Reference | Reference only |
| FR-006 | (full-fidelity export — bespoke build) | — | None | build required |
| FR-007 | GOV.UK One Login OIDC and SAML SSO authentication middleware | govuk-one-login/onboarding-examples | Library | matched |
| FR-008 | (public REST/AsyncAPI — use OpenAPI standards directly) | — | None | build required |
| FR-009 | (public status page — bespoke or upstream OSS) | — | None | build required |
| FR-010 | (tenant offboarding — bespoke build) | — | None | build required |
| FR-011 | Subscription billing and payment processing for government SaaS | alphagov/pay-frontend | Fork | matched |
| FR-012 | Tamper-evident audit logging and structured telemetry library | ministryofjustice/hmpps-audit-api | Reference | Reference only |
| FR-013 | GOV.UK Design System frontend components and accessible web UI | alphagov/govuk-frontend | Fork | matched |
| FR-014 | (admin console — bespoke build with break-glass) | — | None | build required |
| FR-015 | GOV.UK Design System frontend components and accessible web UI | x-govuk/govuk-eleventy-plugin | Fork | matched |
| NFR-SEC-001 | GOV.UK One Login OIDC and SAML SSO authentication middleware | govuk-one-login/simulator | Fork | matched |
| NFR-SEC-002 | Multi-tenant SaaS isolation and per-tenant RBAC framework | alphagov/digitalmarketplace-api | Reference | Reference only |
| NFR-SEC-003 | GOV.UK One Login OIDC and SAML SSO authentication middleware | alphagov/signon | Reference | Reference only |
| NFR-C-002 | Tamper-evident audit logging and structured telemetry library | alphagov/govuk_app_config | Library | Reference only |
| NFR-C-003 | GOV.UK Design System frontend components and accessible web UI | alphagov/govuk-frontend | Fork | matched |
| NFR-M-001 | Tamper-evident audit logging and structured telemetry library | alphagov/govuk_app_config | Library | Reference only |
| NFR-A-001 | AWS multi-cloud landing-zone IaC for UK-resident SaaS workloads | ministryofjustice/cloud-platform-infrastructure | Library | matched |
| NFR-A-002 | AWS multi-cloud landing-zone IaC for UK-resident SaaS workloads | ministryofjustice/cloud-platform-terraform-rds-instance | Fork | matched |
| NFR-S-001 | AWS multi-cloud landing-zone IaC for UK-resident SaaS workloads | alphagov/govuk-helm-charts | Library | matched |
| INT-001 | GOV.UK One Login OIDC and SAML SSO authentication middleware | govuk-one-login/simulator | Fork | matched |
| INT-002 | Subscription billing and payment processing for government SaaS | alphagov/pay-frontend | Fork | matched |
| INT-003 | Companies House SME verification client and onboarding workflow | companieshouse/api-sdk-node | Fork | matched |
| INT-004 | GOV.UK Notify transactional email and notification client | alphagov/notifications-python-client | Library | matched |
| INT-005 | AI and LLM provider abstraction layer for government services | i-dot-ai/i-dot-ai-utilities | Fork | matched |
| INT-006 | AWS multi-cloud landing-zone IaC for UK-resident SaaS workloads | ministryofjustice/cloud-platform-terraform-rds-instance | Fork | matched |
| INT-007 | Tamper-evident audit logging and structured telemetry library | alphagov/govuk_app_config | Library | matched |
| INT-008 | G-Cloud Digital Marketplace listing and call-off tooling | alphagov/digitalmarketplace-api | Library | matched |
| INT-009 | (vulnerability disclosure — security.txt + ISO 29147 process) | — | None | build required |

---

## Recommendations

### Reuse Strategy Summary

ArcKit-as-a-Service v1.1 reuse strategy under the deterministic rubric is dominated by **Fork**-band candidates (18 of 49 scored repositories) concentrated in three trusted orgs: alphagov, ministryofjustice and i.AI. The frontend story is settled — `alphagov/govuk-frontend` (npm) plus `x-govuk/govuk-eleventy-plugin` for documentation chrome and `alphagov/govuk-prototype-kit` for early-phase prototypes. The verification story is similarly settled — depend on `companieshouse/api-sdk-node` directly and use `companieshouse/overseas-entities-web` as the worked example for FR-001 onboarding flows. For email and SSO, take the official GDS clients (`notifications-python-client` / `notifications-node-client`) and the One Login `simulator` as harness.

For **infrastructure**, the recommendation is to fork the MoJ Cloud Platform Terraform modules (`cloud-platform-terraform-rds-instance`, `cloud-platform-terraform-s3-bucket`) and reference `cloud-platform-infrastructure` and `modernisation-platform` for the multi-account landing-zone patterns. AWS dominates the available reference set; for Azure UK-South, `DFE-Digital/terraform-azurerm-container-apps-hosting` is the only first-class candidate and should be used as the multi-cloud bridge if the cloud ADR adopts a portable target. For **AI**, `i-dot-ai/i-dot-ai-utilities` is the closest UK-gov LiteLLM-based abstraction; combine with `i-dot-ai/consult` and `i-dot-ai/lex` as live reference apps for Cabinet Office AI patterns.

For all **gap** capabilities (tamper-evident audit log, multi-tenant isolation kernel, Markdown / Mermaid pipelines, EA-tool adapters, true LLM gateway, classification validators), the recommendation is unchanged from v1.0: build new under MIT and publish back so the next gov programme (and the sovereign-deployment Project 002) can reuse what ArcKit produces.

### Implementation Priority

| Priority | Repository | Capability | Action |
|----------|------------|------------|--------|
| 1 | alphagov/govuk-frontend | Frontend | npm install; theme overrides |
| 2 | companieshouse/api-sdk-node | SME verification | npm dependency; INT-003 |
| 3 | alphagov/notifications-python-client (or notifications-node-client) | Email | pip / npm dependency; INT-004 |
| 4 | govuk-one-login/simulator | SSO test harness | docker compose into CI |
| 5 | ministryofjustice/cloud-platform-terraform-rds-instance | RDS Postgres | Terraform module fork |
| 6 | ministryofjustice/cloud-platform-terraform-s3-bucket | Object storage | Terraform module fork |
| 7 | i-dot-ai/i-dot-ai-utilities | LLM abstraction | pip dependency; FR-004 / INT-005 |
| 8 | x-govuk/govuk-eleventy-plugin | Docs chrome | npm; FR-015 marketing/docs site |
| 9 | alphagov/pay-frontend, pay-selfservice | Billing UX reference | Pattern lift; FR-011 / INT-002 |
| 10 | alphagov/digitalmarketplace-api | Tenant RBAC reference | Pattern lift; FR-002 / NFR-SEC-002 |
| 11 | alphagov/govuk_app_config + ministryofjustice/hmpps-audit-api | Audit/telemetry reference | Pattern lift; FR-005 / FR-012 |
| 12 | (build new) | Tamper-evident hash-chain log, tenant-isolation kernel, tenant export, admin console, status page, vulnerability disclosure | Sprint 1–6 |

### Risk Considerations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| `alphagov/govuk-frontend` breaking change mid-build | Low | Medium | Pin to a major version; track release notes |
| `penx/govuk-react` becomes stale (last commit 2024-05) | Medium | Low | Verify freshness before adoption; fall back to govuk-frontend Nunjucks bridge |
| `govuk-one-login/authentication-frontend` Unknown licence | Medium | High | Do not adopt without confirmed licence; rely on simulator + onboarding-examples |
| `i-dot-ai/redbox`, `caddy-chatbot` archived | High (already archived) | Low | Reference only; never import |
| `alphagov/paas-cf`, `paas-auditor` archived | High (already archived) | Low | Reference patterns only |
| MoJ Cloud Platform modules diverge from SaaS account model | Medium | Low | Cherry-pick modules; document deviations in ADRs |
| Companies House API rate limits on free tier | Medium | Medium | Cache with TTL; queue verification jobs |
| Notify costs at scale exceed free allowance | Low | Medium | Pluggable email provider abstraction |

---

## Spawned Knowledge

The following standalone tech-note files were created or updated from this reuse-assessment run:

### Tech Notes

- `tech-notes/x-govuk-govuk-eleventy-plugin.md` — Created
- `tech-notes/penx-govuk-react.md` — Created
- `tech-notes/alphagov-govuk-frontend.md` — Created
- `tech-notes/alphagov-govuk-prototype-kit.md` — Created
- `tech-notes/nhsuk-nhsuk-frontend.md` — Created
- `tech-notes/alphagov-govuk-publishing-components.md` — Created
- `tech-notes/govuk-one-login-simulator.md` — Created
- `tech-notes/alphagov-signon.md` — Created
- `tech-notes/govuk-one-login-onboarding-examples.md` — Created
- `tech-notes/govuk-one-login-authentication-api.md` — Created
- `tech-notes/alphagov-gds-sso.md` — Created
- `tech-notes/govuk-one-login-authentication-stubs.md` — Created
- `tech-notes/govuk-one-login-authentication-frontend.md` — Created
- `tech-notes/alphagov-digitalmarketplace-api.md` — Created
- `tech-notes/ministryofjustice-cloud-platform-environments.md` — Created
- `tech-notes/alphagov-paas-cf.md` — Created
- `tech-notes/alphagov-govuk-app-config.md` — Created
- `tech-notes/ministryofjustice-hmpps-audit-api.md` — Created
- `tech-notes/ministryofjustice-hmpps-spring-boot-sqs.md` — Created
- `tech-notes/ministryofjustice-hmpps-audit-poc-ui.md` — Created
- `tech-notes/alphagov-paas-auditor.md` — Created
- `tech-notes/companieshouse-overseas-entities-web.md` — Created
- `tech-notes/companieshouse-api-sdk-node.md` — Created
- `tech-notes/companieshouse-confirmation-statement-web.md` — Created
- `tech-notes/kevbite-companieshouse-net.md` — Created
- `tech-notes/nicholasamorim-chuk.md` — Created
- `tech-notes/jimsmart-chapi.md` — Created
- `tech-notes/alphagov-notifications-api.md` — Created
- `tech-notes/alphagov-notifications-python-client.md` — Created
- `tech-notes/alphagov-notifications-node-client.md` — Created
- `tech-notes/alphagov-notifications-ruby-client.md` — Created
- `tech-notes/alphagov-notifications-java-client.md` — Created
- `tech-notes/alphagov-notifications-php-client.md` — Created
- `tech-notes/i-dot-ai-consult.md` — Created
- `tech-notes/i-dot-ai-lex.md` — Created
- `tech-notes/i-dot-ai-i-dot-ai-utilities.md` — Created
- `tech-notes/i-dot-ai-redbox.md` — Created
- `tech-notes/i-dot-ai-caddy-chatbot.md` — Created
- `tech-notes/alphagov-govuk-chat.md` — Created
- `tech-notes/ministryofjustice-cloud-platform-terraform-rds-instance.md` — Created
- `tech-notes/ministryofjustice-cloud-platform-terraform-s3-bucket.md` — Created
- `tech-notes/ministryofjustice-cloud-platform-infrastructure.md` — Created
- `tech-notes/ministryofjustice-modernisation-platform.md` — Created
- `tech-notes/alphagov-govuk-infrastructure.md` — Created
- `tech-notes/alphagov-govuk-helm-charts.md` — Created
- `tech-notes/dfe-digital-terraform-azurerm-container-apps-hosting.md` — Created
- `tech-notes/hmrc-terraform-aws-vpc.md` — Created
- `tech-notes/alphagov-digitalmarketplace-utils.md` — Created
- `tech-notes/alphagov-digitalmarketplace-supplier-frontend.md` — Created
- `tech-notes/alphagov-digitalmarketplace-buyer-frontend.md` — Created
- `tech-notes/alphagov-digitalmarketplace-frameworks.md` — Created
- `tech-notes/alphagov-pay-frontend.md` — Created
- `tech-notes/alphagov-pay-selfservice.md` — Created
- `tech-notes/alphagov-pay-publicapi.md` — Created
- `tech-notes/alphagov-pay-adminusers.md` — Created
- `tech-notes/alphagov-pay-js-commons.md` — Created

---

## External References

### Citations

| Citation ID | URL |
|-------------|-----|
| ALPHAGOV-GOVUK-FE-1 | https://github.com/alphagov/govuk-frontend |
| ALPHAGOV-PROTO-KIT-1 | https://github.com/alphagov/govuk-prototype-kit |
| ALPHAGOV-PUB-COMP-1 | https://github.com/alphagov/govuk_publishing_components |
| PENX-GOVUK-REACT-1 | https://github.com/penx/govuk-react |
| XGOVUK-11TY-1 | https://github.com/x-govuk/govuk-eleventy-plugin |
| NHSUK-FE-1 | https://github.com/nhsuk/nhsuk-frontend |
| GOL-AUTH-API-1 | https://github.com/govuk-one-login/authentication-api |
| GOL-AUTH-FE-1 | https://github.com/govuk-one-login/authentication-frontend |
| GOL-AUTH-STUBS-1 | https://github.com/govuk-one-login/authentication-stubs |
| GOL-SIM-1 | https://github.com/govuk-one-login/simulator |
| GOL-ONBOARD-EX-1 | https://github.com/govuk-one-login/onboarding-examples |
| ALPHAGOV-SIGNON-1 | https://github.com/alphagov/signon |
| ALPHAGOV-GDS-SSO-1 | https://github.com/alphagov/gds-sso |
| ALPHAGOV-DM-API-1 | https://github.com/alphagov/digitalmarketplace-api |
| MOJ-CP-ENV-1 | https://github.com/ministryofjustice/cloud-platform-environments |
| ALPHAGOV-PAAS-CF-1 | https://github.com/alphagov/paas-cf |
| ALPHAGOV-ACCT-MGR-1 | https://github.com/alphagov/govuk-account-manager-prototype |
| ALPHAGOV-APP-CONFIG-1 | https://github.com/alphagov/govuk_app_config |
| ALPHAGOV-PAAS-AUDITOR-1 | https://github.com/alphagov/paas-auditor |
| MOJ-HMPPS-AUDIT-API-1 | https://github.com/ministryofjustice/hmpps-audit-api |
| MOJ-HMPPS-AUDIT-UI-1 | https://github.com/ministryofjustice/hmpps-audit-poc-ui |
| MOJ-HMPPS-SQS-1 | https://github.com/ministryofjustice/hmpps-spring-boot-sqs |
| CH-API-SDK-NODE-1 | https://github.com/companieshouse/api-sdk-node |
| CH-OE-WEB-1 | https://github.com/companieshouse/overseas-entities-web |
| CH-CS-WEB-1 | https://github.com/companieshouse/confirmation-statement-web |
| KEVBITE-CHNET-1 | https://github.com/kevbite/CompaniesHouse.NET |
| NAMORIM-CHUK-1 | https://github.com/nicholasamorim/chuk |
| JIMSMART-CHAPI-1 | https://github.com/jimsmart/chapi |
| MIKEMACCANA-CH-1 | https://github.com/mikemaccana/companies-house |
| ALPHAGOV-NOTIFY-API-1 | https://github.com/alphagov/notifications-api |
| ALPHAGOV-NOTIFY-PY-1 | https://github.com/alphagov/notifications-python-client |
| ALPHAGOV-NOTIFY-NODE-1 | https://github.com/alphagov/notifications-node-client |
| ALPHAGOV-NOTIFY-RB-1 | https://github.com/alphagov/notifications-ruby-client |
| ALPHAGOV-NOTIFY-JAVA-1 | https://github.com/alphagov/notifications-java-client |
| ALPHAGOV-NOTIFY-NET-1 | https://github.com/alphagov/notifications-net-client |
| ALPHAGOV-NOTIFY-PHP-1 | https://github.com/alphagov/notifications-php-client |
| IDOTAI-UTIL-1 | https://github.com/i-dot-ai/i-dot-ai-utilities |
| IDOTAI-LITELLM-1 | https://github.com/i-dot-ai/coding-agent-litellm-config |
| IDOTAI-REDBOX-1 | https://github.com/i-dot-ai/redbox |
| ALPHAGOV-CHAT-1 | https://github.com/alphagov/govuk-chat |
| IDOTAI-CONSULT-1 | https://github.com/i-dot-ai/consult |
| IDOTAI-LEX-1 | https://github.com/i-dot-ai/lex |
| IDOTAI-CADDY-1 | https://github.com/i-dot-ai/caddy-chatbot |
| MOJ-MODPLAT-1 | https://github.com/ministryofjustice/modernisation-platform |
| MOJ-CP-INFRA-1 | https://github.com/ministryofjustice/cloud-platform-infrastructure |
| MOJ-CP-RDS-1 | https://github.com/ministryofjustice/cloud-platform-terraform-rds-instance |
| MOJ-CP-S3-1 | https://github.com/ministryofjustice/cloud-platform-terraform-s3-bucket |
| ALPHAGOV-INFRA-1 | https://github.com/alphagov/govuk-infrastructure |
| ALPHAGOV-HELM-1 | https://github.com/alphagov/govuk-helm-charts |
| HMRC-TF-VPC-1 | https://github.com/hmrc/terraform-aws-vpc |
| DFE-TF-AZ-CA-1 | https://github.com/DFE-Digital/terraform-azurerm-container-apps-hosting |
| ALPHAGOV-DM-UTILS-1 | https://github.com/alphagov/digitalmarketplace-utils |
| ALPHAGOV-DM-SUPP-FE-1 | https://github.com/alphagov/digitalmarketplace-supplier-frontend |
| ALPHAGOV-DM-BUY-FE-1 | https://github.com/alphagov/digitalmarketplace-buyer-frontend |
| ALPHAGOV-DM-FRAMEWORKS-1 | https://github.com/alphagov/digitalmarketplace-frameworks |
| ALPHAGOV-PAY-PUBAPI-1 | https://github.com/alphagov/pay-publicapi |
| ALPHAGOV-PAY-FE-1 | https://github.com/alphagov/pay-frontend |
| ALPHAGOV-PAY-SS-1 | https://github.com/alphagov/pay-selfservice |
| ALPHAGOV-PAY-AU-1 | https://github.com/alphagov/pay-adminusers |
| ALPHAGOV-PAY-PROD-1 | https://github.com/alphagov/pay-products |
| ALPHAGOV-PAY-JSC-1 | https://github.com/alphagov/pay-js-commons |
| ALPHAGOV-PAY-DDC-1 | https://github.com/alphagov/pay-direct-debit-connector |

---

**Generated by**: ArcKit `/arckit:gov-reuse` agent (writer tier)
**Generated on**: 2026-05-07
**ArcKit Version**: 4.19.0
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
**Rubric**: gov-reuse-uk-gov
