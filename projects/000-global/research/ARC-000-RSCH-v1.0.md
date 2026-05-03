# Target-Organisation Research: ArcKit as a Service — UK Public-Sector Adopter Landscape

> **Template Origin**: Official | **ArcKit Version**: 4.13.1 | **Command**: `/arckit:research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-RSCH-v1.0 |
| **Document Type** | Research Findings (Target Organisation) |
| **Project** | ArcKit as a Service — Wave 1 cross-project context (Project 000-global) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Annual (refresh each year of the SOBC outlook) |
| **Next Review Date** | 2027-05-03 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project 001 team, downstream Wave-2 research subagents (RESEARCH / AWS / AZURE / GCP / GOV_REUSE), CCS liaison, GDS, CDDO, MOD Defence Digital |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:research` (target-organisation scope, Wave 1 of `/arckit:build` for ArcKit as a Service). Synthesises strategy, organisational structure and existing-systems posture across UK central government, MOD, NHS, ALBs and local government as the prospective adopter base. | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document is the **Wave-1 target-organisation research** for ArcKit as a Service. It does not research technology vendors. Instead, it characterises the **UK public-sector organisations that would adopt** ArcKit-as-a-Service — central government departments, arm's-length bodies (ALBs), the Ministry of Defence (MOD), the NHS, devolved administrations and local government — together with the SMEs that supply them. Wave-2 technology research (`/arckit:research`, `/arckit:aws-research`, `/arckit:azure-research`, `/arckit:gcp-research`, `/arckit:gov-reuse`) will inherit this profile so that downstream vendor and platform recommendations are anchored in the actual buyer/operator estate, not a generic SaaS market.

The output answers, for the prospective adopter base:

- What is the **strategy** — the digital, data, security, procurement and SME-spend mandates that drive demand for managed EA tooling?
- What is the **organisational structure** — who decides, who pays, who accredits, who assures?
- What are the **existing systems** — what does the technology estate look like that ArcKit-as-a-Service must coexist with, integrate with, or land alongside?
- What are the **procurement and sovereignty constraints** that gate adoption?

**Requirements informing the research** (from `ARC-001-REQ-v1.0.md`):

- Business: BR-001 (free SME tier), BR-002 (transparent pricing), BR-003 (SME verification), BR-004 (G-Cloud listing), BR-005 (cross-subsidy), BR-006 (UK public-sector evidence pack), BR-007 (portability/exit), BR-008 (≥ 200 SME adoption).
- Functional: FR-001–FR-015 (multi-tenant authoring, AI generation, SSO, API, audit, status page, GOV.UK Design System alignment).
- Principles drivers (from `ARC-000-PRIN-v2.0.md`): Principle 1 (SME affordability), Principle 5 (Security by Design — incl. NCSC CAF and MOD Secure by Design / JSP 440), Principle 7 (UK data sovereignty), Principle 12 (Accessibility), Principle 21 (Sovereign and Air-Gapped Deployment).
- Stakeholder driver clusters (from `ARC-001-STKE-v1.0.md`): DDaT architecture community (SD-1–SD-5), SME suppliers (SD-6–SD-7), HMG bodies and regulators (SD-12–SD-14).

**Research approach**: Synthesis of UK Government published policy and operating-model artefacts (Procurement Act 2023, GovS 005 Digital, GovS 007 Security, TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, MOD Secure by Design, JSP 440, JSP 604, HMG Government Security Classifications Policy, Digital Marketplace G-Cloud framework, DDaT Capability Framework), enriched by the project's own principle/requirement/stakeholder/SOBC artefacts. No vendor pricing was researched in this Wave-1 step — that is Wave 2's job.

### Key Findings

- **Target-organisation strategic posture is bimodal**: a *managed-SaaS-friendly* segment (most central-civil departments, ALBs, NHS England, devolved administrations and local government) operating predominantly at OFFICIAL with OFFICIAL-SENSITIVE caveats and using public-cloud landing zones; and a *sovereign-only* segment (MOD, parts of HMG security/intelligence community, NHS national-security adjuncts) operating at OFFICIAL-SENSITIVE and above inside accredited boundaries with no internet egress. The platform's **dual deployment model** in Principle 21 maps directly onto this bimodality. ArcKit-as-a-Service Project 001 lands in the first segment; Project 002 (sovereign deployment) is engineered for the second.
- **Existing-systems constraint is "GOV.UK Design System + landing zones + GitHub-flavoured authoring"** for the SaaS-friendly segment. Public-sector buyers expect the UI to match GOV.UK Design System (FR-013), data to live in the UK on hyperscaler landing zones operated against the NCSC Cloud Security Principles, identity to ride on GOV.UK One Login for citizen-facing services and on departmental Entra-ID / federated OIDC for staff-facing services, and procurement to come through G-Cloud. For MOD and sensitive sites the constraint is fundamentally different: signed offline bundles, local model endpoints, and acceptance through the deploying authority's own JSP 604-style accreditation.
- **Procurement and sovereignty stance is mandatory not negotiable**: G-Cloud listing (BR-004) is the single highest-leverage adoption lever for the SaaS-friendly segment because the alternative — bespoke OJEU/Find-a-Tender procurement — costs SMEs and small commands more than the tooling itself. UK data residency (Principle 7) is the floor, not the ambition. For MOD, "sovereignty" means the platform itself runs inside the accredited boundary; SaaS is structurally inadmissible at OFFICIAL-SENSITIVE-and-above, regardless of vendor assurance.

### Build vs Buy Summary (Target-Organisation Adoption)

The "build vs buy" question at the *target-organisation* level is not the vendor question. It is: **does the prospective adopter currently have, build, or buy an architecture-governance capability?** This frames how ArcKit-as-a-Service is positioned to them.

| Adopter Class | Current State | Plausible Action on ArcKit-as-a-Service | Adoption Lever |
|----------------|---------------|------------------------------------------|----------------|
| **UK Central-Civil Department / ALB (DDaT EA function present)** | Mix of bespoke EA wikis (Confluence, SharePoint), commercial EA tooling (LeanIX, Ardoq, MEGA, Bizzdesign) and Office-document templates. Often partial coverage; assurance-evidence quality variable. | **BUY (G-Cloud)** ArcKit-as-a-Service paid-tier for departmental EA function; **REUSE artefacts produced by SME suppliers** on the free tier. | DDaT EA recognition (Goal G-1); G-Cloud listing (BR-004); evidence-pack alignment (BR-006). |
| **NHS Trust / NHS England** | Limited dedicated EA tooling; Microsoft 365-centric estate; clinical-system focus. Architecture-governance capability typically thin outside national bodies. | **BUY (G-Cloud)** for national bodies; **ADOPT (free tier)** for trusts under SME-spend equivalents. | NHS DTAC, DSPT, Cyber Assessment Framework (NHS profile) alignment. |
| **MOD Command / Defence Digital** | Strong existing assurance machinery (JSP 440, JSP 604, MOD Secure by Design via CAAT). Architecture artefacts often classified above the SaaS ceiling. | **OUT-OF-SCOPE for managed SaaS**; route is sovereign deployment (Project 002). | Principle 21 — signed bundle, accredited deployment. |
| **Devolved administration / Local authority** | Variable; smaller teams; heavy reliance on suppliers. Often no dedicated EA tooling. | **ADOPT free tier** for direct authoring; **REUSE supplier artefacts** otherwise. | Affordability (Principle 1); WCAG 2.2 AA (Principle 12). |
| **UK SME supplying the public sector** | No commercial EA tooling at SME prices. Bespoke / Office-document governance. | **ADOPT free tier**; convert to **paid SME tier** as growth permits. | Free tier credibility (BR-001); 5-day bid-pack (Goal G-2). |

Vendor-level Build/Buy/Adopt analysis (per category, with 3-year TCO) is **deferred to the Wave-2 technology research targets**. This document deliberately stops at the adopter-class level so that the Wave-2 outputs can use a shared adopter profile.

### Top Three Findings to Pass Forward to Wave 2

1. **Anchor SaaS-route research on UK-region hyperscaler landing zones operated under the NCSC Cloud Security Principles**. The buyer's mental model is "must run in UK region, must produce CAF / Cloud Security Principles / TCoP evidence, must list on G-Cloud, must support GOV.UK One Login or departmental OIDC, must export in open formats". Wave-2 (RESEARCH / AWS / AZURE / GCP) should evaluate against that mental model, not a generic SaaS shopping list.
2. **Hold the sovereign-deployment branch separate**. MOD and sensitive-site adopters cannot consume managed SaaS at all for the artefacts they care most about. Wave-2 should treat sovereign-deployment infrastructure (offline bundle, local model endpoint, customer-controlled telemetry) as a parallel research branch with different evaluation criteria — *not* a footnote on the SaaS pages.
3. **Treat code reuse from existing UK Government repositories as a first-class option**. The GovReposcrape-backed `/arckit:gov-reuse` discovery should run for every Wave-2 category before any commercial recommendation hardens, because (a) reuse is mandated by TCoP and the Service Manual, (b) it materially reduces SME tier cost-to-serve, and (c) sovereign-deployment customers prefer publicly-published government code on supply-chain grounds.

### Requirements Coverage

This is a target-organisation research, not a per-requirement vendor mapping. Coverage is measured against the **adopter classes** the requirements need to serve:

- ✅ **100%** of the adopter classes implied by `ARC-001-REQ-v1.0.md` are characterised here (central-civil, NHS, MOD, devolved, local, SME-supplier).
- 📌 **Per-requirement vendor coverage** is the responsibility of the Wave-2 research outputs (`ARC-001-RSCH-*`, AWS / Azure / GCP / GOV-REUSE), not of this document.

---

## Research Categories

> **Note**: Categories below are framed around the *target organisation*, not technology categories. Each category profiles a class of UK public-sector adopter (or supplier-to-public-sector) and surfaces the strategy, structure, and existing-systems facts that shape how ArcKit-as-a-Service must show up in front of them.

---

## Category 1: UK Central-Civil Departments and ALBs

**Requirements Addressed**: BR-001, BR-002, BR-004, BR-006, FR-007, FR-013, NFR-A-001, NFR-C-* (compliance), Principles 1, 5, 7, 12.

**Why This Category**: Central-civil departments and their arm's-length bodies are the largest single class of UK public-sector adopter and the dominant consumer of supplier-side governance evidence. Whether they buy ArcKit-as-a-Service for their own DDaT EA function or whether they merely *receive* artefacts produced by SME suppliers using ArcKit, their format conventions, security controls and procurement routes set the floor that the platform has to meet. This category is also where the SOBC's cross-subsidy revenue ultimately comes from (large-tenant tier per BR-005).

### Strategy

UK central-civil digital strategy is published and stable enough to design against:

- **Procurement Act 2023** sets the procurement frame — including the SME-spend objective and the duty to consider SMEs (drives BR-004 G-Cloud listing as the path of least resistance for buyers).
- **Government Functional Standard for Digital (GovS 005)** defines the mandatory digital governance roles (SRO, Service Owner, Product Manager, Delivery Manager) and the handful of artefacts those roles must produce. ArcKit's artefact set is engineered to match.
- **Government Functional Standard for Security (GovS 007)** defines mandatory protective-security roles (SIRO, DSO) and forms the spine of the security-evidence pack BR-006 has to produce.
- **Technology Code of Practice (TCoP)** — 13 points; ArcKit's `/arckit:tcop` aligns to it, and the Wave-2 vendor selection must demonstrate TCoP alignment for adopter departments to procure without exception.
- **GDS Service Standard** (14 points) — assessed via `/arckit:service-assessment`; assessor-friendly artefact format is a Goal G-1 input.
- **NCSC Cyber Assessment Framework (CAF)** — used in GovAssure for OES; the dominant assurance language buyers expect (driver SD-3).
- **NCSC Cloud Security Principles (14)** — the cloud-security frame the SaaS-route platform must demonstrate against (Principle 5 / NFR-SEC-* in REQ).
- **HMG Government Security Classifications Policy** — defines OFFICIAL, OFFICIAL-SENSITIVE handling caveats, and SECRET. The SaaS route's classification ceiling (OFFICIAL with OFFICIAL-SENSITIVE handling caveats) is set against it.
- **CDDO digital spend controls** — once material spend triggers the threshold, business-case scrutiny intensifies; ArcKit-produced SOBC/OBC/FBC artefacts must be assessor-grade.

**Strategic implication for ArcKit-as-a-Service**: This adopter class is the *primary* SaaS audience and the *primary* consumer of artefacts produced *by* SaaS users. The Wave-2 research must therefore aim every SaaS-route shortlist at "fits inside a CDDO-spend-controlled, TCoP-assessed, CAF-aligned, G-Cloud-procured environment".

### Organisational Structure (Decision Rights)

The decision rights ArcKit-as-a-Service must navigate inside an adopter department:

| Role (GovS 005 / GovS 007 / DDaT) | Authority Relevant to ArcKit Adoption | Engagement Implication |
|------------------------------------|---------------------------------------|------------------------|
| Permanent Secretary / Director-General | Strategic spend approval at threshold; rare direct touch | Briefed-only; do not target |
| CDIO / CTO | Departmental digital strategy; technology stack decisions | Quarterly briefing; G-Cloud awareness |
| SRO (per service) | Accountable for spend / outcomes on a specific service | Receives the SOBC / OBC; owns spend-control sign-off |
| Service Owner | End-to-end service quality; consumes Service Standard evidence | Direct user of ArcKit assessor-grade outputs |
| Enterprise Architect (DDaT) | Departmental architecture coherence | **Manage-Closely** — pilot and reference partner |
| Solution Architect (DDaT) | Programme/project design and review | **Manage-Closely** — primary reviewer of supplier ArcKit artefacts |
| Security Architect (DDaT) / SIRO / DSO | Security architecture, CAF, classification handling | **Manage-Closely** — receives security evidence pack |
| Data Architect (DDaT) | Data model / DPIA / governance | Consumer of `/arckit:data-model`, `/arckit:dpia` |
| Technical / Network Architect (DDaT) | Platform / topology / segmentation | Consumer of `/arckit:diagram` deployment views |
| Procurement / Commercial / GCF | G-Cloud call-off; framework compliance | Consumer of BR-004 listing |
| DPO | UK GDPR posture | Consumer of `/arckit:dpia` and sub-processor list |
| Accessibility champion | PSBAR conformance | Consumer of `/arckit:diagram` and accessibility statement |

**Structural implication for ArcKit-as-a-Service**: A buying department has at least seven distinct evaluator roles. The platform's evidence pack (BR-006) and artefact set must serve each of them out of the same artefacts. Wave-2 research must check that any third-party component selected does not force the adopter to introduce *another* evaluator role.

### Existing Systems Estate (Today's State)

The dominant patterns inside a typical UK central-civil department's existing estate, shaped by published policy and stable procurement behaviour:

- **End-user productivity**: Microsoft 365 (Exchange Online, Teams, SharePoint Online, OneDrive) at almost-universal scale. Some departments dual-stack with Google Workspace.
- **Document and knowledge stores**: SharePoint Online; Confluence / Jira (where Atlassian is on the menu); shared file stores; bespoke wikis.
- **Identity and access**: Microsoft Entra ID (Azure AD) for staff; GOV.UK One Login for citizen-facing services; OIDC / SAML 2.0 federation; departmental MFA.
- **Cloud landing zones**: AWS (UK regions eu-west-2 London), Microsoft Azure (UK South / UK West), Google Cloud (europe-west2 London). Most departments are dual-cloud at minimum; some have an explicit cloud-first / hyperscaler-of-choice posture, but few are single-cloud in practice.
- **Delivery tooling**: GitHub.com (and GitHub Enterprise Cloud), Azure DevOps, GitLab; CI/CD via GitHub Actions, Azure Pipelines, GitLab CI. Heavy reliance on GitHub-flavoured Markdown for documentation.
- **Enterprise architecture tooling**: Variable. Common entries: Microsoft Visio, draw.io / diagrams.net, Confluence pages, SharePoint document libraries, occasional commercial EA tooling (LeanIX, Ardoq, MEGA, Bizzdesign, BiZZdesign Horizzon, Sparx Enterprise Architect). Most departments do *not* have a single coherent EA platform.
- **Service management**: ServiceNow at scale in larger departments; Jira Service Management or freshservice in smaller ones; bespoke workflows where neither has been chosen.
- **Observability**: Splunk, Elastic, Datadog (cloud-native), Prometheus / Grafana for new builds, Microsoft Sentinel for SIEM in Azure-leaning departments.
- **Public-sector platforms (GDS-built)**: GOV.UK One Login (identity), GOV.UK Pay (payments), GOV.UK Notify (notifications), GOV.UK Forms (forms). TCoP point 8 and the Service Manual mandate consideration of these before bespoke build.
- **Compliance tooling**: Bespoke spreadsheets and SharePoint sites for CAF and Cloud Security Principles posture in many departments; some use commercial GRC (ServiceNow GRC, Archer, OneTrust).

**Existing-systems implication for ArcKit-as-a-Service**: The platform must **co-exist** with this estate, not displace it. Practically:

- It must produce GitHub-friendly outputs (Markdown, JSON, YAML, Mermaid, PlantUML) that drop into the customer's existing repos and wikis. (Already a Principle 4 / FR-006 commitment.)
- It must SSO with the customer's existing IdP (Entra ID is the dominant case). (FR-007.)
- Its UI must follow the GOV.UK Design System wherever it interacts with public-sector users so that the cognitive load on those users stays low. (FR-013.)
- It must not require introducing a new EA "platform" displacing Visio / draw.io / Confluence; it must add value alongside them and feed back into them on export.

### Sovereignty and Procurement Posture

- **Data residency**: UK only by default; cross-border processing is a per-tenant negotiation. Aligns directly with Principle 7 / NFR-C-001.
- **Classification ceiling for SaaS adoption**: OFFICIAL with OFFICIAL-SENSITIVE handling caveats where the tenant opts in. Above that, the adopter must not be able to push content into the SaaS — sovereign route only.
- **Procurement route**: G-Cloud framework call-off (BR-004) is the path of least resistance. Direct procurement, DOS framework, or bespoke OJEU/Find-a-Tender competitions are all available but commercially heavier.
- **Spend controls**: CDDO and HM Treasury spend controls activate on material spend; the platform's transparent published pricing (BR-002) keeps customers below the painful thresholds for as long as possible.

### Recommendation for Wave 2 (Target-Organisation Anchor)

When Wave-2 research evaluates third-party services, components and platforms for the SaaS route, it should:

1. **Filter to UK-region availability** (Principle 7 hard constraint).
2. **Demand TCoP and NCSC Cloud Security Principles posture evidence** from any candidate.
3. **Demand G-Cloud listing or a credible plan to list**.
4. **Treat GOV.UK Design System compatibility** (UI components reusable) as a tiebreaker.
5. **Treat GitHub-friendly outputs** (Markdown, JSON, YAML) as a hard requirement, not a nice-to-have.

---

## Category 2: UK Ministry of Defence and Sensitive-Site Adopters

**Requirements Addressed**: Principle 21 (Sovereign and Air-Gapped Deployment); upstream of Project 002 (sovereign-route SOBC).

**Why This Category**: A material portion of ArcKit's intended audience cannot lawfully or operationally use the SaaS route for some or all of their work. Treating MOD and sensitive-site adopters as a footnote on the SaaS pages is exactly the failure mode Principle 21 was added to prevent. Wave-2 sovereign-route research must inherit a clean profile of what these adopters look like.

### Strategy

- **MOD Digital Strategy** and the **Defence Digital** function set the cross-MOD digital direction (target architectures, common platforms such as **Defence as a Platform** / DaaP, and the move toward common identity and cloud landing zones at OFFICIAL).
- **MOD Secure by Design** (mandatory; assessed via the MOD Continuous Assurance and Assessment Tool — CAAT) is the dominant security framework. ArcKit's `/arckit:mod-secure` and `/arckit:secure` are deliberately aligned.
- **JSP 440 (Defence Manual of Security)**, **JSP 604 (Information Systems Authorisation)**, and JSP 936 (AI assurance) define the policy floor.
- **HMG Government Security Classifications Policy** sets the classification frame; MOD operates routinely at OFFICIAL, OFFICIAL-SENSITIVE and SECRET, with TS networks separate.
- **Defence-specific procurement** runs through the **Defence and Security Accelerator (DASA)**, **Defence Equipment & Support (DE&S)** and **Defence Digital procurement routes** — not (typically) through G-Cloud as the primary path. SMEs serving MOD often go through specific defence frameworks rather than the civilian G-Cloud framework.
- **NCSC** is not the formal accreditor for MOD systems; the deploying authority's own accreditor (a formal role under JSP 604) is. NCSC guidance still informs control selection.

**Strategic implication for ArcKit-as-a-Service**: MOD and sensitive-site adopters consume the **sovereign deployment** (Project 002), not the SaaS. Their evaluation criteria are not "fits in a UK-region AWS landing zone" but "ships as a signed offline bundle, runs in our accredited boundary, accepts our keys, our model endpoint, our package mirror, our telemetry destination, and our decommission process". The Wave-2 sovereign-route research has to be engineered against that.

### Organisational Structure (Decision Rights)

| Role | Authority Relevant to ArcKit Sovereign Adoption | Engagement Implication |
|------|---------------------------------------------------|------------------------|
| Senior Information Risk Owner (SIRO) — Command | Owns information risk on the deploying system | Manage-Closely; receives sovereign release evidence |
| Information Asset Owner (IAO) | Day-to-day asset risk | Receives operator runbooks |
| Accreditor (per JSP 604) | Formal authority to operate (ATO) | Manage-Closely; receives MOD Secure by Design evidence pack and supply-chain integrity manifest |
| Departmental Security Officer (DSO) | Implements security policy | Keep-Informed |
| MOD Defence Digital Architecture Authority | Sets cross-MOD architecture | Strategic engagement; not transactional |
| Cleared engineering staff | Day-to-day operation of the deployment | Operator runbook audience |
| Industry partner / SI inside the boundary | May host or operate the platform | Receives the same signed bundle and supplier-cleared documentation |

**Structural implication**: There is no single "MOD-wide" buying decision. Each accredited deployment is a *separate* customer. ArcKit-as-Sovereign must therefore be packaged so a single command, capability or programme can deploy it inside their own boundary without needing the *vendor* present. That is exactly what Principle 21 commits to.

### Existing Systems Estate

- **Multi-tier classified networks**: separate networks at OFFICIAL, OFFICIAL-SENSITIVE, SECRET; cross-domain transfers are formal and slow. Internet egress from OFFICIAL-SENSITIVE-and-above is typically prohibited.
- **MOD common platforms**: Defence as a Platform (DaaP) for OFFICIAL workloads; Microsoft 365 (MODNET) for productivity; DII-F historic estate still present in some commands; Defence-grade clouds for specific sensitive workloads.
- **Identity**: MOD's own identity stack (departmental Entra ID-backed for OFFICIAL; bespoke directories at higher classifications). External federated identity is generally not available inside the accredited boundary.
- **Build / supply chain**: Internal package mirrors; signed builds; SBOM / provenance increasingly demanded. Many commands operate their own DevSecOps pipeline behind the boundary.
- **AI / model endpoints**: Approved on-premise model deployments are appearing; assumption of "default to a public-internet model API" is not safe at OFFICIAL-SENSITIVE-and-above.
- **Time / certificate authority / package mirror**: All controlled by the host environment, not the vendor. Hard-coded outbound calls to public CAs / mirrors / NTP fail acceptance.

**Existing-systems implication for ArcKit-as-a-Service**: Every assumption that holds for the SaaS route has to be re-tested for the sovereign route. The **Validation Gates of Principle 21** are the literal acceptance test:

- Disconnected installation walkthrough, validated end-to-end on a representative isolated environment.
- Disconnected upgrade and rollback.
- Backup / restore / decommission within the boundary.
- AI / model integration documented as pluggable; default sovereign profile points at no external provider.
- No critical-path dependency requires outbound internet connectivity (network-deny test).

### Sovereignty and Procurement Posture

- **Sovereignty**: Total. The platform runs inside the customer's boundary. The vendor has no remote access unless contractually agreed *and* accredited by the deploying authority's accreditor.
- **Procurement**: Defence-specific frameworks; DOS where applicable; long lead times; supplier security cleared where required by the SAL.
- **Classification ceiling**: As accredited per deployment. Anything above OFFICIAL is out of scope of the SaaS, period.

### Recommendation for Wave 2 (Sovereign-Route Anchor)

Wave-2 research for the sovereign route must:

1. **Treat any third-party component that requires phone-home licensing or internet egress as a hard reject**, not a "with mitigations" candidate.
2. **Prefer open-source components with on-premise distribution rights** so the licence does not block sovereign distribution.
3. **Demand SBOM + signed-builds + supply-chain provenance** as a baseline, not a tiebreaker.
4. **Score each candidate on offline operability** (offline install, offline upgrade, offline licence verification, offline telemetry).
5. **Score AI / model endpoints separately** for the sovereign route — only on-premise-deployable model options qualify for the default sovereign profile.

---

## Category 3: NHS Bodies (NHS England, NHS Trusts, ICBs, Devolved NHS)

**Requirements Addressed**: BR-001, BR-004, BR-006, FR-007, FR-013, NFR-C-001, Principles 1, 5, 7, 12.

**Why This Category**: NHS England, NHS trusts and Integrated Care Boards (ICBs) are a substantial sub-segment of UK public-sector adopters with their own assurance frameworks (DSPT, DTAC, NHS-profile CAF) and procurement quirks (NHS frameworks alongside G-Cloud). Many NHS organisations are themselves *suppliers* of digital services to government and to citizens, so the same artefact-quality expectation applies.

### Strategy

- **NHS Long Term Plan and the Federated Data Platform agenda** keep digital and data architecture at strategic prominence.
- **Data Security and Protection Toolkit (DSPT)** is the dominant NHS information-governance assessment.
- **Digital Technology Assessment Criteria (DTAC)** is the NHS supplier assessment for digital health technologies.
- **NHS England Cyber Strategy** mandates a CAF-aligned posture (NHS-profile CAF).
- **NHSX legacy work** consolidated under NHS England Transformation Directorate; standards continuity is broadly stable.
- **Procurement** runs through NHS Shared Business Services frameworks, the NHS Workforce Alliance, and G-Cloud where appropriate.

**Strategic implication for ArcKit-as-a-Service**: NHS adopters consume essentially the same SaaS route as central-civil departments, but the evidence pack must additionally demonstrate **DSPT** alignment and (for any tenant using ArcKit to author DTAC submissions) **DTAC** alignment. ArcKit's existing SbD / TCoP / CAF assessments cover most of the ground; Wave 2 should check that the chosen vendor stack is also DSPT- and DTAC-friendly.

### Organisational Structure

NHS structure is more federated than central-civil. Decision rights distribute across:

- **NHS England Transformation Directorate** (national digital architecture);
- **ICB digital leadership** (regional aggregation);
- **NHS Trusts** (autonomous IT and EA functions, of varying maturity);
- **Caldicott Guardian / DPO** (information-governance equivalent of the SIRO/DSO pattern);
- **Clinical Safety Officer (DCB0129/DCB0160 compliance)** for any change touching clinical decision-making.

**Implication**: An NHS adopter's "buyer" is rarely a single role — pilots typically need both IG sign-off (Caldicott / DPO / DSPT lead) and clinical-safety sign-off if any AI generation touches clinical content.

### Existing Systems Estate

- **Microsoft 365 NHSmail and NHS-Microsoft tenancies** dominate productivity.
- **Clinical systems**: Cerner Millennium (now Oracle Health), Epic, EMIS, SystmOne, Lorenzo (legacy). These are not ArcKit's target estate, but ArcKit's outputs may describe their integrations.
- **Integration**: HL7 v2 / FHIR; NHS Spine; the Federated Data Platform.
- **Cloud**: Microsoft Azure with strong NHS-focused offerings; AWS UK regions also present; Google Cloud less common but present.
- **Identity**: NHS CIS2 / Care Identity Service for clinical SSO; Entra ID for staff productivity.
- **Architecture tooling**: Variable; some larger trusts have commercial EA tooling, most do not.

**Implication**: ArcKit-as-a-Service's SaaS route fits naturally for *NHS staff-side digital architecture* work (strategy, supplier reviews, programme assurance), provided the vendor stack chosen in Wave 2 is reachable from an NHS network and supports NHS-grade SSO.

### Sovereignty and Procurement Posture

- **Data residency**: UK only by default; specific patient data has additional handling requirements outside ArcKit's scope.
- **Classification**: ArcKit content is OFFICIAL with OFFICIAL-SENSITIVE handling caveats — same as central civil. Patient data is *not* the platform's content domain, but tenants must be able to opt out of putting patient identifiers into ArcKit.
- **Procurement**: G-Cloud is acceptable; NHS-specific frameworks are routinely preferred for clinical-system buys but applicable to EA-tooling buys too.

### Recommendation for Wave 2

Wave-2 SaaS-route research should:

1. Confirm chosen components are reachable from NHSmail networks and standard NHS network egress patterns.
2. Verify SSO support extends to **NHS CIS2 / OIDC** in addition to Entra ID and Google Workspace.
3. Confirm DSPT-friendly evidence (sub-processor lists, breach notifications, retention policies) is producible from the platform's outputs.

---

## Category 4: Devolved Administrations and Local Government

**Requirements Addressed**: BR-001, BR-004, BR-008, FR-013, NFR-C-001, Principles 1, 12.

**Why This Category**: Devolved administrations (Scottish Government, Welsh Government, Northern Ireland Executive) and local authorities (English unitary / county / district / metropolitan; Welsh principal authorities; Scottish councils; Northern Ireland councils) are net-affordability-sensitive adopters. They have small or zero in-house EA capability and are the *primary* beneficiaries of Principle 1's free tier. They also have specific framework loyalties (e.g., LGA / LGfL frameworks; Crown Commercial Service still dominant).

### Strategy

- **Scottish Government Digital Strategy** and the **Welsh Government Digital Strategy** broadly mirror UK central digital strategy with regional variations and bilingual obligations.
- **Local Digital Declaration** (a sector-led initiative) sets a common digital direction for English local authorities.
- **GOV.WALES / GOV.SCOT / GOV.UK** all use GOV-style design systems; Welsh services have a statutory bilingual requirement.
- **Cyber Assessment Framework** is increasingly being applied to local public sector by NCSC.

**Strategic implication**: These adopters are a natural fit for the SaaS *free tier* (Principle 1 / BR-001) and the SME paid tier. Welsh Government adopters require Welsh-language UI consideration in time (currently out of v1 scope per REQ §"Out of Scope").

### Organisational Structure

- **Devolved CDIO / CTO functions** (smaller than central-civil but with full functional standards reach).
- **Local-authority IT director / Head of Digital** — typically combined with operational IT leadership; rarely a dedicated EA function.
- **Local-authority procurement**: framework-led (CCS, NEPO, ESPO, YPO, SBS, Procurement for Housing); G-Cloud broadly accepted.

### Existing Systems Estate

- **Productivity**: Microsoft 365 dominant; Google Workspace minority.
- **Line-of-business**: Civica, Capita, Northgate, Liberata, IDOX, Granicus (housing, revs and bens, planning, electoral, FOI, comms).
- **Identity**: Entra ID; smaller authorities sometimes still on AD on-prem.
- **Cloud**: AWS and Azure UK regions; some authorities still substantially on-prem in 2026.
- **Architecture tooling**: Sparse. Visio and SharePoint dominate; commercial EA tooling rare.

**Implication**: ArcKit-as-a-Service's free tier is *uniquely positioned* for this segment — the alternative is "no EA tooling at all". Wave-2 should make sure the SaaS route does not assume a level of network or identity sophistication that smaller authorities lack.

### Sovereignty and Procurement Posture

- **Data residency**: UK only.
- **Classification**: Predominantly OFFICIAL.
- **Procurement**: G-Cloud + specific local-government frameworks. Crown Commercial Service spend rules still apply.

### Recommendation for Wave 2

Wave-2 research should ensure:

1. **No mandatory minimum tenant size** is imposed by chosen components — small councils with two-person digital teams must still be supportable.
2. **Welsh-language considerations** are noted as a future-roadmap item, not an architectural blocker (the platform's i18n must not be designed out).

---

## Category 5: UK SMEs Supplying the Public Sector

**Requirements Addressed**: BR-001, BR-002, BR-003, BR-008, FR-001, FR-004, FR-006, Principles 1, 17.

**Why This Category**: The SME-supplier community is the **primary commercial audience** for the SaaS free and paid SME tiers (per stakeholder driver SD-6 / SD-7). Their existing-systems estate is shaped by being small, by being multi-customer, and by being cost-sensitive.

### Strategy

- **Procurement Act 2023 / SME Action Plans** create a demand-side incentive — the supplier-side capability gap (driver SD-13) is what ArcKit-as-a-Service exists to close.
- **SME suppliers tend to be cloud-native**, GitHub-native, AI-native by default; they cannot afford on-premise estate.
- **Their strategic problem is bid economics** (driver SD-7): every pound spent on bid infrastructure is loss-making until a bid wins.

### Organisational Structure

- 1–250 employees; flat hierarchy; a single "senior architect" often doubles as bid lead and tech lead.
- Founder / MD often signs procurement; finance lead may not exist as a dedicated role.
- DPO is usually an outsourced or fractional role.
- ICO registration is in place; UK GDPR / DPA 2018 obligations are owned by the founder and/or the DPO of record.

### Existing Systems Estate

- **Productivity**: Google Workspace or Microsoft 365 — roughly even split.
- **Source control**: GitHub.com almost universally.
- **Authoring**: Markdown-first in repos; Notion / Confluence Cloud / Google Docs for less technical artefacts.
- **Cloud**: AWS dominant among SMEs; Azure significant; GCP smaller share.
- **Identity**: Google Workspace SSO or Entra ID; sometimes Okta / Auth0.
- **EA tooling**: None, generally. Office documents and Visio-equivalents.
- **Compliance tooling**: None or fractional; often spreadsheets and signed PDFs.

**Implication for ArcKit-as-a-Service**: The SaaS must be plug-and-play for a small SME — sign up, verify against Companies House (FR-001), produce a bid pack in 5 working days (Goal G-2). The Wave-2 research must avoid components that require dedicated SRE / DevOps capacity inside the customer to operate; the platform must absorb that operational burden, not push it down to SMEs.

### Sovereignty and Procurement Posture

- **Data residency**: UK preference is strong (because their public-sector customers will require it of them), but SMEs have practical ability to use non-UK regions for non-customer data. Principle 7's UK default protects them.
- **Procurement**: SMEs *consume* G-Cloud (BR-004) and *appear on* G-Cloud as suppliers themselves. Both flows benefit from ArcKit's outputs.

### Recommendation for Wave 2

Wave-2 SaaS-route research should:

1. Treat operational simplicity for the small-SME customer as a primary evaluation criterion.
2. Ensure on-boarding does not require integrations the SME does not yet have (no mandatory enterprise IdP for the free tier; FR-007).
3. Ensure the AI-generation cost envelope (FR-004) lets a fully-active SME produce a bid pack within the SOBC's tenant cost-to-serve assumptions (BR-005).

---

## Cross-Category Summary: What Wave 2 Inherits

| Property | SaaS-Route Adopters (Categories 1, 3, 4, 5) | Sovereign-Route Adopters (Category 2) |
|----------|---------------------------------------------|---------------------------------------|
| **Classification ceiling** | OFFICIAL with OFFICIAL-SENSITIVE handling caveats | Up to deployment-accredited classification (SECRET on accredited deployments) |
| **Data residency** | UK by default | Customer-controlled inside accredited boundary |
| **Identity / SSO** | Entra ID, OIDC, SAML 2.0, GOV.UK One Login (citizen), NHS CIS2 (NHS) | Customer-internal directories; no external federation |
| **Procurement route** | G-Cloud (primary), NHS frameworks, local-gov frameworks, direct procurement | Defence frameworks (DASA, DE&S, Defence Digital procurement); long lead times |
| **Assurance language** | TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, UK GDPR / DPA 2018, PSBAR / WCAG 2.2 AA, NHS DSPT / DTAC | MOD Secure by Design (CAAT), JSP 440, JSP 604, JSP 936, Site Security Aspects Letter |
| **Telemetry destination** | Vendor-controlled (managed SaaS) | Customer-controlled inside boundary |
| **AI / model endpoint** | Public-internet provider (with no-training assurances and DPIA) | Customer-approved on-premise model endpoint; default no external provider |
| **Operational model** | Vendor-operated multi-tenant SaaS | Customer-operated single-tenant deployment from signed offline bundle |
| **Update / patching** | Continuous delivery, SaaS standard | Signed bundle airdropped across air-gap; long-term support release line |
| **GOV.UK Design System adoption expected?** | Yes (FR-013) — SaaS UI matches public-sector visual language | Optional — sovereign-deployment UIs may follow the deploying authority's own conventions |
| **G-Cloud listing required?** | Yes (BR-004) — primary procurement path | No — sovereign deployments procure through defence-specific routes |

---

## Total Cost of Ownership Implications (Pass-Through to Wave 2)

Vendor TCO will be calculated by Wave-2 research. The target-organisation findings here change the **TCO assumptions** Wave 2 must use:

- **UK-region pricing only** for the SaaS route. Multi-region failover within the UK (eu-west-2 + a second UK option, where available) is acceptable; cross-border is not.
- **Cross-subsidy economics** (BR-005) mean per-tenant cost-to-serve must be calculable per Principle 17. Wave-2 SaaS-route candidates that hide pricing or charge by features critical to the free tier are non-starters.
- **Sovereign-route TCO** must include packaging effort (signed bundle, SBOM, provenance), accreditation evidence, long-term support cost — all carried by the vendor — and the customer-side cost of operating inside their boundary.
- **Reuse from existing UK Government repositories** (via `/arckit:gov-reuse` and govreposcrape) reduces both routes' TCO and should be evaluated *first* per TCoP and Principle 16.

> **Concrete TCO numbers** are deferred to Wave-2 outputs.

---

## Requirements Traceability

This Wave-1 target-organisation research traces against requirement *contexts*, not specific vendor selections.

| Requirement | Adopter-Class Context Set Here |
|-------------|--------------------------------|
| BR-001 (Free SME tier) | Categories 4, 5 are the primary beneficiaries; Category 1 receives artefacts produced under it. |
| BR-002 (Transparent pricing) | Category 1 / 5 — both procurement-sensitive and bid-cost-sensitive. |
| BR-003 (SME verification) | Category 5 — Companies House interaction is the operational dependency. |
| BR-004 (G-Cloud listing) | Categories 1, 3, 4 — primary procurement route. |
| BR-005 (Cross-subsidy) | Funded predominantly by Category 1 large-tenant adopters. |
| BR-006 (Evidence pack) | Categories 1, 3 set the assurance language; pack must speak it. |
| BR-007 (Portability / exit) | All categories, especially Category 2 (precondition for sovereign acceptance). |
| BR-008 (Adoption) | Volume sourced from Categories 4, 5; revenue from Category 1. |
| FR-001 (Tenant provisioning) | Category 5 driver — Companies House check. |
| FR-004 (AI generation) | All categories; differential model-endpoint behaviour for Category 2. |
| FR-007 (SSO) | Entra ID / OIDC / SAML 2.0 / GOV.UK One Login / NHS CIS2 — covered by `Identity / SSO` row above. |
| FR-013 (GOV.UK Design System) | Categories 1, 3, 4 — public-sector UI convention. |
| NFR-A-001 (≥ 99.9% availability) | All categories; UK-region multi-AZ. |
| NFR-C-* (Compliance) | Categories 1, 3 demand the most evidence; Category 2 demands different evidence. |
| Principle 21 (Sovereign deployment) | Category 2 only. |

---

## UK Government Considerations

### Technology Code of Practice (TCoP) Posture (Adopter-Side)

Buyers in Categories 1, 3 and 4 expect any platform they procure to *demonstrate* TCoP alignment. ArcKit-as-a-Service's TCoP review (`/arckit:tcop`) is intended to satisfy this. The Wave-2 research must not select components that *break* the platform's overall TCoP posture (e.g., proprietary lock-in violating Point 3 / Point 8).

### GOV.UK Common Platforms in the Adopter Estate

| Platform | Where ArcKit-as-a-Service Touches It | Decision |
|----------|---------------------------------------|----------|
| GOV.UK One Login | Citizen-facing services typically use it. ArcKit-as-a-Service is **staff-and-supplier-facing**, not citizen-facing, so One Login is not on the critical path for tenant SSO. | Evaluate as an *option* for tenants whose own service uses One Login, not as a requirement. |
| GOV.UK Pay | ArcKit-as-a-Service paid tiers are commercial. **Not in scope** — commercial payment processor (INT-002) handles billing. | Not used. |
| GOV.UK Notify | Free for central government. The platform's tenant notifications can use a commercial provider (INT-004) for SaaS, but tenants in central government may want their own GOV.UK Notify integration for *their* downstream services. | Evaluate as a tenant-side integration option in Wave 2 only if relevant. |
| GOV.UK Forms | Out of scope for ArcKit-as-a-Service itself. | Not used. |
| GOV.UK Design System | UI alignment per FR-013. | Required for SaaS UI; optional for sovereign UI. |

### Digital Marketplace Procurement Strategy (for ArcKit-as-a-Service Itself)

The platform must list on **G-Cloud 14 (or current iteration)** under categories such as Software-as-a-Service / Cloud Software (Lot 2 in the G-Cloud taxonomy). Pricing must be published on Digital Marketplace. SFIA-rated rates apply for any associated specialist support engagement.

### Government Cloud and Data Residency Posture

For ArcKit-as-a-Service Project 001 (managed SaaS): UK-region public-cloud hosting is acceptable and expected, against the NCSC Cloud Security Principles. For Project 002 (sovereign deployment): residency is the deploying authority's choice, inside their accredited boundary.

---

## Integration With Wardley Mapping

The target-organisation research feeds the value-chain decomposition (`/arckit:wardley.value-chain`) by identifying *who consumes the value*. Cross-category summary positions:

| Adopter Class | Position on the Buyer Value Chain |
|---------------|-----------------------------------|
| Central-civil department | Primary consumer of ArcKit artefacts; primary funder via large-enterprise tier |
| MOD command | Primary consumer of sovereign deployment; downstream value to defence delivery |
| NHS body | Mixed — both supplier (digital health services) and consumer of supplier evidence |
| Local authority | Consumer; affordability-sensitive; benefits from free tier + supplier-side evidence |
| SME supplier | Producer of evidence using the platform; primary user of free tier |

Wave-2 research will use this positioning to assess **evolution stage** of supporting components (commodity hosting on hyperscalers vs custom EA tooling vs novel AI-assisted artefact generation).

---

## Integration With SOBC Economic Case

The SOBC at `ARC-001-SOBC-v1.0.md` already embeds the cross-subsidy economic case for the SaaS route. This research confirms the **adopter-class assumption set** that case rests on:

- Cross-subsidy revenue source: predominantly Category 1 (central-civil departments and large ALBs) buying paid large-tenant tier.
- Cost-to-serve majority: Categories 4, 5 on the free or low-paid SME tier.
- Sovereign-route revenue: Project 002 has its own SOBC; out of scope here.

This research does **not** revise the SOBC's £4.5M baseline TCO or +£0.54M optimism-bias uplift; it merely confirms the adopter-class mix that produces them.

---

## Vendor Shortlist (Deferred)

Vendor-level shortlisting is **out of scope** of this Wave-1 target-organisation research. Wave-2 outputs (`ARC-001-RSCH-*`, AWS / Azure / GCP / GOV-REUSE) own that work and will inherit the adopter-class profile here.

---

## Risks and Mitigations (Target-Organisation Level)

### TR-A1: Adopter-Class Mismatch with Vendor Shortlist

- **Risk**: Wave-2 picks vendors well-suited to a generic SaaS market but poorly suited to the UK public-sector buyer mental model documented here.
- **Impact**: HIGH — failure of Goal G-1 (DDaT-recognisable artefacts) and G-7 (G-Cloud reach).
- **Likelihood**: MEDIUM if Wave-2 is run without this anchor; LOW with this anchor.
- **Mitigation**: This document; explicit Wave-2 evaluation criteria reuse.

### TR-A2: Sovereign-Route Treated as a Footnote

- **Risk**: Wave-2 SaaS-route subagents include MOD as "with caveats" instead of producing a clean parallel branch for the sovereign route.
- **Impact**: HIGH — Principle 21 violation; MOD adopter-class effectively unsupported.
- **Likelihood**: MEDIUM unless explicitly signalled.
- **Mitigation**: This document's Category 2 and Cross-Category Summary make the bifurcation explicit.

### TR-A3: NHS / Devolved / Local-Government Specifics Missed

- **Risk**: Wave-2 SaaS-route candidates pass for central-civil but fail NHS DSPT/DTAC, Welsh-language, or small-authority operability checks.
- **Impact**: MEDIUM — restricts adopter-base size; risks BR-008 adoption target.
- **Likelihood**: MEDIUM.
- **Mitigation**: Categories 3, 4 above flag these explicitly.

### TR-A4: SME Operational Capacity Overestimated

- **Risk**: Wave-2 picks components that assume customer-side SRE / DevOps capacity that small SMEs do not have.
- **Impact**: MEDIUM — hurts Goal G-2 (5-day bid pack) and BR-008 (adoption).
- **Likelihood**: MEDIUM.
- **Mitigation**: Category 5 above; Wave-2 evaluation criterion "operational simplicity for small SMEs".

---

## Next Steps and Recommendations

### Immediate (Wave 1 → Wave 2 handoff)

1. **Pass this document forward to all Wave-2 research subagents** as the shared adopter-class profile. The subagents should not re-derive it.
2. **Pre-tag categories** in the Wave-2 outputs by which adopter-classes the recommended option serves (Category 1 / 2 / 3 / 4 / 5 from this document).
3. **Sovereign branch**: Wave-2 sovereign-route research should produce a *separate* output, not annotations on the SaaS pages.

### Short-term (post Wave-2)

4. **Reconcile Wave-2 vendor TCO** against the SOBC baseline (`ARC-001-SOBC-v1.0.md` Option 2 — £4.50M before optimism bias, £5.04M risk-adjusted).
5. **Run `/arckit:wardley`** with this adopter-class context as the buyer value-chain seed.
6. **Run `/arckit:sow`** to produce the supplier-facing RFP using the constraints documented here.

---

## Spawned Knowledge

The following standalone knowledge files were created or updated from this research:

### Vendor Profiles

- *None* — this is target-organisation research, not vendor research. Vendor profiles are produced by Wave-2 outputs.

### Tech Notes

- *None* — this is target-organisation research. Wave-2 outputs will spawn tech notes for technology categories.

---

## AskUserQuestion Choices Made

This subagent did not invoke `AskUserQuestion`. No interactive prompts arose; defaults from the wave-1 dispatch instructions were not needed.

---

## External References

> No external policy documents were placed under `projects/000-global/external/` or `projects/001-arckit-saas/external/` at the time of generation. UK Government policies referenced (Procurement Act 2023, GovS 005 Digital, GovS 007 Security, TCoP, GDS Service Standard, NCSC CAF, NCSC Cloud Security Principles, MOD Secure by Design, JSP 440, JSP 604, JSP 936, HMG Government Security Classifications Policy, Digital Marketplace G-Cloud framework, DDaT Capability Framework, NHS DSPT, NHS DTAC, Local Digital Declaration) are public-domain and cited by name. Place authoritative copies in `projects/000-global/policies/` to embed inline citations on the next refresh.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:research` agent (Wave 1 of `/arckit:build`, target-organisation scope)
**Generated on**: 2026-05-03
**ArcKit Version**: 4.13.1
**Project**: ArcKit as a Service — cross-project context (Project 000-global)
**AI Model**: Claude Opus 4.7 (1M context)
