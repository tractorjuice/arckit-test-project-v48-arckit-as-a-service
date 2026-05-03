# GDS Service Assessment Preparation Report: ArcKit as a Service (Managed SaaS) — Beta-Target Readiness

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:service-assessment`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SVCASS-v1.0 |
| **Document Type** | GDS Service Assessment Preparation Report (Beta-target) |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Weekly until pre-assessment walkthrough; then per release |
| **Next Review Date** | 2026-05-10 |
| **Owner** | Mark Craddock (ArcKit as a Service Owner) |
| **Reviewed By** | [PENDING] Product Manager, Lead Architect, DPO, Security Lead, Accessibility Lead |
| **Approved By** | [PENDING] Service Owner |
| **Distribution** | Project Team, Architecture Team, CCS liaison, prospective Service Assessor, pilot DDaT Enterprise Architect |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:service-assessment` command. Pre-Beta readiness artefact for the pre-assessment walkthrough required by RISK §H Priority-1 action 5 (R-009). All 14 GDS Service Standard points assessed with phase-appropriate (Beta) criteria. | [PENDING] | [PENDING] |

---

## Executive Summary

**Assessment Phase**: Beta (pre-GA, targeting public Beta on the path to Live)
**Target Audience for the Pre-Assessment Walkthrough**: One Service Assessor + one pilot DDaT Enterprise Architect (per `ARC-001-RISK-v1.0.md` §H Priority-1 action 5)
**Assessment Date**: Not yet booked. Formal Beta assessment targeted at GA – 30 days; pre-assessment walkthrough at GA – 60 days. GA target date pending `ARC-001-PLAN-v1.0.md` generation.

**Overall Readiness**: 🔴 Red (Not Ready for formal Beta assessment yet — 4 Red gaps must close before booking; on track for GA – 60 days walkthrough)

**Readiness Score**: 4/14 Green, 6/14 Amber, 4/14 Red

**Breakdown**:

- 🟢 Green: 4 points (2 Solve a whole problem, 7 Agile, 8 Iterate, 13 Open standards)
- 🟡 Amber: 6 points (1 Users, 3 Joined-up, 4 Simple, 6 Multidisciplinary team, 11 Right tools, 14 Reliable)
- 🔴 Red: 4 points (5 Accessibility, 9 Secure and private, 10 Performance data, 12 Open source)

**Summary**:

Project 001 has invested heavily in design-stage governance evidence: principles, requirements, ADRs, stakeholders, risk register, TCoP, Secure by Design, DPIA, and AI Playbook artefacts are all produced and internally consistent. The intellectual foundation for a Beta assessment is unusually strong for an Alpha-stage project — particularly on Points 7 (Agile), 8 (Iterate), and 13 (Open standards) where the platform's own purpose (governance tooling for SMEs) means the team works with their own product on the SaaS build itself.

However, the project is **pre-GA Alpha-stage with no live tenants**. Critical Beta-phase evidence — independent penetration test (R-008/R-014), Accessibility Statement and manual assistive-technology audit (TCoP Point 2 / NFR-C-003), production performance data, public source code repository, and pilot user research with diverse users including assistive-technology users — is committed but not yet delivered. The four Red ratings all reflect "evidence committed by GA but not yet produced", not "evidence absent and unplanned". This is consistent with what `ARC-001-TCOP-v1.0.md` Section 13 already records.

The pre-assessment walkthrough is **the right tool to use now**: it surfaces format, framing, and evidence-coverage issues *before* booking the formal Beta assessment, and gives the team room to land RISK §H Priority-1 actions 1, 5, 6, and 7 before incurring G-Cloud-listing-blocking Red findings (R-009).

**Critical Gaps** (Must address before formal Beta booking):

- **Point 5 (Everyone can use)** — WCAG 2.2 AA manual AT audit not done; Accessibility Statement not published; testing with disabled users not evidenced. Beta requires *completed and passed* audit, not just CI-automated checks. Cross-reference TCoP Point 2 critical issue.
- **Point 9 (Secure and private)** — Independent penetration test not yet completed (£40k–£60k, GA – 60 days). Cross-reference RISK R-008 / R-014, TCoP Point 6, and SBD §9.1 Critical Issue 2.
- **Point 10 (Performance data)** — No production telemetry yet (no live service); public status page committed but not implemented; no published Beta KPIs against which performance can be measured.
- **Point 12 (Open source)** — Service-side code-publication strategy not yet decided (ADR pending per TCoP Point 3 actions). The ArcKit *plugin* is open source; the *service* multi-tenancy / billing / FinOps code is not currently scoped for publication.

**Key Strengths**:

- **Decision traceability is exemplary** (Point 7, 8, 13). Eight ADRs (`ARC-001-ADR-001` through `008`) capture every material architectural choice with alternatives and consequences. The `/arckit:adr`-driven workflow demonstrates the agile + iterative posture the assessment panel will look for.
- **Open-standards posture is genuinely strong** (Point 13). OIDC / OAuth 2.x / SAML 2.0 (ADR-003), OCI containers + Kubernetes (ADR-006), Markdown / JSON / YAML for tenant export (ADR-007), OpenAPI + AsyncAPI (Principle 4 / FR-008). Buyer DDaT architects will recognise the conventions.
- **The product solves a real, well-defined whole problem** (Point 2). SMEs lacking enterprise EA tooling for UK government bid work — backed by 14 stakeholder drivers, 8 goals, and 7 outcomes in `ARC-001-STKE-v1.0.md` with explicit DDaT Capability Framework anchoring.

**Recommended Timeline**:

- **Weeks 1–2 (now to 2026-05-17)**: Critical-action prep — book independent pen test (R-008/R-014); commission manual AT audit; draft Accessibility Statement; ADR for service-side OSS publication strategy.
- **Weeks 3–6 (to 2026-06-14)**: Critical actions land — pen test executed; AT audit completed; Accessibility Statement published; pilot recruitment for DDaT user research; recruit Service Assessor + pilot DDaT EA for walkthrough.
- **Weeks 7–8 (to 2026-06-28)**: Pre-assessment walkthrough — RISK §H action 5 lands.
- **Weeks 9–12**: Address walkthrough feedback; book formal Beta assessment for GA – 30 days (pending `ARC-001-PLAN-v1.0.md` GA date confirmation).

---

## Service Standard Assessment (14 Points)

### 1. Understand Users and Their Needs

**Status**: 🟡 Amber

**What This Point Means**: The team must demonstrate deep understanding of users and their needs through ongoing user research, with research informing service iterations. For a Beta service, research must include diverse users and assistive-technology users.

**Why It Matters**: The single most common reason services fail Beta assessment is shallow or non-diverse user research. Buyer DDaT architects will probe research breadth and direct quotation from research participants.

**Evidence Required for Beta**:

- Ongoing user research throughout Beta with documented findings.
- Testing with diverse users including assistive-technology users.
- User research informing iterations (visible audit trail of research → change).
- Analytics data showing user behaviour.
- Evidence of continuous user engagement.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-STKE-v1.0.md`** (lines 79–214) — DDaT Capability Framework anchoring with all seven architecture roles individually addressed (Enterprise, Solution, Data, Security, Business, Technical, Network); 14 stakeholder drivers (SD-1..SD-14) with explicit Power/Interest grid; conflict and synergy analysis.

✅ **`ARC-001-REQ-v1.0.md`** (Personas section) — Four user personas (SME Architect, SME Founder/Bid Lead, Buying Authority Architect, ArcKit Service Operator) with goals, pain points, and proficiency. Three end-to-end use cases UC-1..UC-3.

✅ **`ARC-001-STKE-v1.0.md`** (Goal G-1, lines 596–615) — DDaT-recognisable artefacts goal commits to ≥3 buying-authority pilots before GA – 60 days. Goal G-2 commits to a 5-working-days time-to-first-bid-pack target with telemetry from FR-004.

⚠️ **Weak**: User research is committed (pilot DDaT user group, SME architect panel) but **no live research findings** are recorded yet — Project 001 is pre-GA Alpha-stage. RISK R-003 (DDaT pilot recognition failure) explicitly flags "alpha + private beta cycles with at least one buying-authority EA in the loop".

❌ **Missing**: No documented research with assistive-technology users (required for Beta).
❌ **Missing**: No analytics from a live service (cannot exist pre-GA).
❌ **Missing**: No user research repository / synthesis document yet.

**Gap Analysis**: The *plan* for user research is excellent and explicitly anchored to DDaT roles — better than most Beta submissions. The *delivery* is at risk because research has not yet started. The pilot DDaT user group (Goal G-1, ≥3 buying authorities) is a Priority-1 mitigation in RISK §H and must be executed before the formal Beta assessment.

**Readiness Rating**: 🟡 Amber

**Strengths**:

- Persona / driver / goal / outcome traceability anchored to DDaT Capability Framework — assessment panel will recognise this immediately.
- Conflict analysis (Conflicts C-1..C-4) shows the team understands competing user needs.
- Goal G-1 metric explicit: ≥3 pilots, ≥80% pass-without-rework, 0 instances of bespoke verification required.

**Weaknesses**:

- No live user-research findings yet (Alpha-stage).
- AT-user research not yet conducted.
- Research synthesis document (typically a "user research repository" link or playback slides) does not exist yet.

**Recommendations**:

1. **Critical**: Recruit and complete first round of pilot DDaT user research before the pre-assessment walkthrough (3 buying authority EAs + 5 SME architects, mix of organisation sizes).
   - Timeline: 4 weeks
   - Owner: Product Manager + User Researcher (to be hired or contracted — see Point 6)
   - Evidence to create: User-research synthesis document; participant diversity log; quoted findings.

2. **Critical**: Conduct first AT-user research session before the formal Beta assessment.
   - Timeline: 6 weeks
   - Owner: Accessibility Lead with User Researcher
   - Evidence to create: AT-user testing report (≥2 participants using screen reader / keyboard-only / voice control), feeds Point 5.

3. **High**: Stand up a public user-research repository (or summary) link that survives demo failures.
   - Timeline: 2 weeks
   - Owner: User Researcher
   - Evidence to create: Living research repository with version history.

**Assessment Day Guidance**:

- **Prepare**: User-research synthesis (3–5 pages); participant-diversity log; quoted findings linking research → service iterations.
- **Show**: Two or three short anonymised research clips or quotes; the persona / DDaT-role-mapping table from STKE.
- **Bring**: Lead User Researcher (mandatory); Product Manager.
- **Materials**: `ARC-001-STKE-v1.0.md` SD-1..SD-14 + Goal G-1; user-research synthesis; AT-user findings.
- **Likely Questions**:
  - "Tell us about a research finding that changed your service design."
  - "How are you researching with disabled users? Show the participant log."
  - "How will you keep researching after Beta assessment?"

---

### 2. Solve a Whole Problem for Users

**Status**: 🟢 Green

**What This Point Means**: The service must address the user's full problem, not just the digital touchpoint with government. Users must reach the end of their journey without having to re-enter the analogue or unsupported world.

**Why It Matters**: Half-services that solve a fragment of the problem are the dominant Beta failure mode for digitisation projects.

**Evidence Required for Beta**:

- Service covers complete user journey end-to-end.
- Integration with other services / channels.
- Assisted digital support for those who need it.
- Clear service boundaries with rationale.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-REQ-v1.0.md`** (Use Cases UC-1, UC-2, UC-3) — End-to-end SME journey: self-service onboarding → AI-assisted artefact generation → tenant data export and exit. The "5-working-days time-to-first-bid-pack" target (Goal G-2) is a measurable end-to-end outcome.

✅ **`ARC-001-REQ-v1.0.md`** (BR-007 Tenant Portability and Exit) — One-click full export in open formats; no governance-critical feature paywalled (BR-001). The service does not lock SMEs in.

✅ **`ARC-001-STKE-v1.0.md`** (Goal G-1, Outcome O-1) — Buyer-side outcome explicit: DDaT architects accept ArcKit-produced artefacts at face value, reducing assurance time per supplier engagement by 30–50%. The service solves *both* the SME's problem (produce credible governance evidence cheaply) and the buyer's problem (less translation work).

✅ **`ARC-001-REQ-v1.0.md`** (Out of Scope section) — Explicit boundaries: sovereign deployment is Project 002; classifications above OFFICIAL-SENSITIVE explicitly out; Welsh / non-English deferred. Boundaries are not hidden.

✅ **TCoP Point 13 mapping** (TCOP §13, line 544) — "End-to-end ArcKit pack covers TCoP / SbD / DPIA / Service-Assessment in one tool" — the platform is itself an integrated whole.

**Gap Analysis**: The whole-problem case is genuinely strong. The product lives within the SME's bid-and-deliver workflow, integrates upstream (Companies House, INT-003) and downstream (G-Cloud), and explicitly avoids paywalling exit (BR-007).

**Readiness Rating**: 🟢 Green

**Strengths**:

- Two-sided whole-problem statement (SME and buyer) — clearer than most Beta services.
- Explicit out-of-scope statement; service boundaries documented with rationale.
- Tenant exit / portability is first-class (BR-007, ADR-007), not a paywalled afterthought.

**Weaknesses**:

- Assisted digital is N/A (per TCoP Point 13 checklist) because this is B2B SaaS for high-tech-proficiency users — the team must be able to defend that framing under questioning.

**Recommendations**:

1. **Medium**: Prepare a one-slide user journey end-to-end diagram showing the SME journey from "considering bidding for UK gov work" to "submitting a bid backed by ArcKit pack" — useful for assessment day even though the artefacts already cover it.
   - Timeline: 1 week
   - Owner: Product Manager
   - Evidence to create: Journey diagram (Mermaid sequence or BPMN-lite).

**Assessment Day Guidance**:

- **Prepare**: One-page journey diagram; the BR-001..008 "outcomes" from REQ.
- **Show**: A live walk-through of UC-1 → UC-2 → UC-3 (sign-up → generate artefact → export).
- **Bring**: Product Manager (lead); Lead Architect (for boundaries).
- **Materials**: `ARC-001-REQ-v1.0.md` Use Cases; `ARC-001-STKE-v1.0.md` Goal G-1, G-2.
- **Likely Questions**:
  - "What happens if a user gets stuck mid-journey?"
  - "Why no assisted digital? How do you justify that for users with low confidence?"
  - "How does an SME know when their pack is good enough to submit?"

---

### 3. Provide a Joined Up Experience Across All Channels

**Status**: 🟡 Amber

**What This Point Means**: Users encounter the service consistently across whatever channel they use. Government services rarely have a single channel — there is usually a phone line, a paper form, an in-person option, or another digital service that hands off.

**Why It Matters**: Channel disconnects are where users drop out of public-service journeys.

**Evidence Required for Beta**:

- All channels implemented and working.
- Data synchronised across channels.
- Consistent user experience across channels.
- Channel switching works seamlessly.
- Testing completed across all channels.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-REQ-v1.0.md`** (FR-008 Public API and Event Interfaces) — REST + AsyncAPI as a deliberate "second channel" alongside the web UI. Same operations achievable via API (NFR-U-001 browser support; NFR-U-002 accessibility for the web channel).

✅ **`ARC-001-REQ-v1.0.md`** (FR-009 Public Status Page and Tenant Notifications) — Cross-channel notification (email + webhook) for incidents and maintenance.

⚠️ **Web-only in v1** (per TCoP Point 13 mapping, line 545) — Mobile native deferred; responsive web only. This is a deliberate scoping decision, not an oversight, but it limits the "channel" story.

❌ **Missing**: G-Cloud / Digital Marketplace listing not yet live (BR-004) — that is a "channel" for buyer-side procurement and is on the GA-blocking critical path (R-009 secondary effect).

❌ **Missing**: No documented channel-switching test (e.g., user starts on web, switches to API mid-journey, picks up state).

**Gap Analysis**: The service has two genuine channels (web UI + API) plus G-Cloud as a procurement channel. The Beta panel will accept this as "joined up" if the team can demonstrate the API and UI are equivalent for tenant operations. The framing — "this is a B2B SaaS, not a citizen service with telephone fallback" — needs to be made explicit so the panel does not penalise the absence of phone / paper channels that genuinely do not apply.

**Readiness Rating**: 🟡 Amber

**Strengths**:

- API + UI parity is a deliberate first-class commitment (FR-008): "All UI operations achievable via API."
- Status page + email + webhook notification covers cross-channel signalling.
- Open-standards interfaces (OpenAPI / AsyncAPI) make it straightforward for tenants to integrate ArcKit into their own toolchains.

**Weaknesses**:

- No mobile-native channel — must defend as deliberate B2B-context decision.
- G-Cloud listing not yet live (BR-004).
- No documented channel-switching test (pick up state from UI session in API).

**Recommendations**:

1. **High**: Document a channel-switching test scenario (UI session → API → UI) and demonstrate it during the walkthrough.
   - Timeline: 2 weeks
   - Owner: Lead Architect
   - Evidence to create: Test plan + recorded demonstration.

2. **High**: Land the G-Cloud listing pre-Beta-assessment (BR-004) so the procurement channel is live.
   - Timeline: 4 weeks (CCS framework iteration dependent)
   - Owner: Service Owner with CCS liaison
   - Evidence to create: Active Digital Marketplace listing URL.

**Assessment Day Guidance**:

- **Prepare**: Channel matrix (Web UI / API / Webhook / Email / Status page / G-Cloud) with parity claims.
- **Show**: Live demo of the same operation via UI then via API.
- **Bring**: Lead Architect; Product Manager.
- **Materials**: FR-008 (Public API), FR-009 (Status page), BR-004 (G-Cloud).
- **Likely Questions**:
  - "Why no mobile native?"
  - "How do you keep UI and API in sync for new features?"
  - "What's the user journey if the API goes down but the UI is up?"

---

### 4. Make the Service Simple to Use

**Status**: 🟡 Amber

**What This Point Means**: Users can succeed first time. Plain language. Minimal cognitive load. No jargon. Clear feedback at every step.

**Why It Matters**: Simplicity is the difference between a service that scales and one that needs hand-holding support — a real cost in public-sector economics.

**Evidence Required for Beta**:

- Usability testing with diverse users.
- Task completion >85% on first attempt.
- Content design reviewed by GDS content designers.
- Plain language, no jargon.
- Forms and interactions simplified.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-REQ-v1.0.md`** (NFR-U-001) — Usable without dedicated training; responsive design covering desktop / tablet / mobile breakpoints.

✅ **`ARC-001-REQ-v1.0.md`** (UC-1) — Self-service onboarding with "onboarding tour" on first sign-in; the user lands on an empty tenant dashboard with guidance, not a blank page.

✅ **`ARC-001-STKE-v1.0.md`** (Goal G-2) — 5-working-days time-to-first-bid-pack target with telemetry (≥60% of new SME tenants reach 5 saved artefacts within 5 working days).

✅ **`ARC-001-REQ-v1.0.md`** (FR-013) — GOV.UK Design System alignment as a SHOULD_HAVE — the team has at least considered the standard public-sector design vocabulary.

❌ **Missing**: No usability-testing results yet (no live users; pilot research not started).
❌ **Missing**: No content-design review by GDS content designers documented.
❌ **Missing**: No measured task-completion rate (cannot exist pre-GA).

**Gap Analysis**: The simplicity *target* is set (5-working-days, ≥60% activation, NPS ≥30 at 30 days). The *evidence* of meeting it does not yet exist. For the pre-assessment walkthrough this is acceptable; for the formal Beta assessment, the panel will want to see at least a small sample of usability-testing findings.

**Readiness Rating**: 🟡 Amber

**Strengths**:

- Goal G-2 measurable target (5 days, ≥60%, NPS ≥30) — better than vague "easy to use" claims.
- GOV.UK Design System alignment considered (FR-013).
- Onboarding tour is first-class in UC-1 (not a post-MVP afterthought).

**Weaknesses**:

- No usability-testing data yet.
- No content-designer review evidenced.
- No task-completion measurement.

**Recommendations**:

1. **Critical**: Run usability-testing sessions on the Alpha prototype with at least 5 SME architects and 3 buying-authority architects before the pre-assessment walkthrough; record task completion rate.
   - Timeline: 4 weeks
   - Owner: User Researcher with Product Manager
   - Evidence to create: Usability findings report; task-completion rate.

2. **High**: Engage a content designer (contractor if not on team) to review onboarding flow and AI-generation prompt UI; aligned with FR-013.
   - Timeline: 3 weeks
   - Owner: Product Manager
   - Evidence to create: Content-design review notes; revised microcopy.

**Assessment Day Guidance**:

- **Prepare**: Usability findings (5 + 3 sessions); content-design review notes; Goal G-2 measurement plan.
- **Show**: Live demo of UC-1 onboarding tour with deliberate "first time user" framing.
- **Bring**: User Researcher; Content Designer (if engaged); Product Manager.
- **Materials**: NFR-U-001, UC-1, Goal G-2.
- **Likely Questions**:
  - "Show us where you simplified something based on user testing."
  - "How is your content reviewed?"
  - "What's the task-completion rate target and where are you against it?"

---

### 5. Make Sure Everyone Can Use the Service

**Status**: 🔴 Red

**What This Point Means**: Disabled people, including those using assistive technologies, can use the service equally well. This is a non-negotiable legal duty under the Equality Act 2010 and the Public Sector Bodies Accessibility Regulations 2018, and a non-negotiable Beta-pass criterion.

**Why It Matters**: Beta services that fail Point 5 cannot proceed to Live. WCAG 2.2 AA is the explicit, audit-able standard.

**Evidence Required for Beta**:

- WCAG 2.2 AA audit completed and passed (CRITICAL).
- Testing with screen readers, voice control, magnification.
- Testing with disabled users.
- Accessibility statement published.
- Alternative formats available.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-000-PRIN-v2.0.md`** Principle 12 (Accessibility) marked **NON-NEGOTIABLE**: WCAG 2.2 AA minimum, assistive-technology testing, Accessibility Statement aligned with PSBAR 2018.

✅ **`ARC-001-REQ-v1.0.md`** NFR-C-003 (Accessibility — PSBAR 2018 / WCAG 2.2 AA) — All tenant-facing UI MUST meet WCAG 2.2 AA, MUST be tested with assistive technologies, MUST publish an Accessibility Statement.

✅ **`ARC-001-STKE-v1.0.md`** Goal G-6 (WCAG 2.2 AA / PSBAR Conformance) with success metrics: automated CI green; manual AT testing per release; zero critical regressions.

✅ **Automated a11y in CI** committed (TCoP Point 2 checklist line 112; Principle 19; NFR-T-002).

❌ **Missing**: WCAG 2.2 AA manual audit not yet conducted (TCoP Point 2 checklist line 109).
❌ **Missing**: Accessibility Statement not published (TCoP Point 2 checklist line 111; explicit critical issue in TCOP §"Critical Issues" #4).
❌ **Missing**: Manual AT (screen reader / voice control / magnification) testing not yet performed (TCoP Point 2 checklist line 110).
❌ **Missing**: Testing with disabled users not yet performed (links to Point 1 weakness above).

**Gap Analysis**: The accessibility *commitment* is the strongest in the artefact set — non-negotiable in PRIN, codified in REQ, with a goal and success metrics in STKE. Yet the *delivery* is unambiguously incomplete: no manual audit, no published statement, no AT-user testing. `ARC-001-TCOP-v1.0.md` already lists this as one of four pre-GA blocking issues. For Beta assessment, this is the single most likely cause of a Red rating.

**Readiness Rating**: 🔴 Red

**Strengths**:

- Strongest possible commitment (Principle 12 marked NON-NEGOTIABLE).
- Automated CI accessibility checks committed (NFR-T-002).
- Goal G-6 metrics measurable (CI green; per-release manual AT; statement reviewed annually).

**Weaknesses**:

- Manual WCAG 2.2 AA audit outstanding (BLOCKING per TCoP §Critical Issues #4).
- Accessibility Statement unpublished (BLOCKING).
- AT-user research and AT testing not yet conducted.

**Recommendations**:

1. **Critical**: Procure independent manual WCAG 2.2 AA audit before the pre-assessment walkthrough.
   - Timeline: 4 weeks (procure + execute)
   - Owner: Accessibility Lead
   - Evidence to create: Audit report with findings + remediation plan.

2. **Critical**: Publish Accessibility Statement aligned with PSBAR 2018 by GA – 30 days.
   - Timeline: 2 weeks
   - Owner: Accessibility Lead with Communications
   - Evidence to create: Public Accessibility Statement URL.

3. **Critical**: Conduct AT-user research session (screen reader, keyboard-only, voice control — at least one user per category) before formal Beta assessment.
   - Timeline: 6 weeks
   - Owner: User Researcher with Accessibility Lead
   - Evidence to create: AT-user research report.

4. **High**: Establish vulnerability-disclosure-equivalent channel for accessibility regressions (TCoP Point 2 action; STKE Risk SR-5 contingency).
   - Timeline: 3 weeks
   - Owner: Accessibility Lead
   - Evidence to create: Public reporting URL.

**Assessment Day Guidance**:

- **Prepare**: Audit report (with findings categorised as Critical / Major / Minor); Accessibility Statement URL; AT-user testing notes; CI a11y dashboard screenshot.
- **Show**: Live screen-reader walk-through of UC-1; CI a11y test failing → fixed → passing.
- **Bring**: Accessibility Lead (mandatory); User Researcher (for AT-user testing).
- **Materials**: `ARC-000-PRIN-v2.0.md` Principle 12; NFR-C-003; Goal G-6; manual audit report; statement.
- **Likely Questions**:
  - "Walk me through your service using a screen reader."
  - "What did the manual audit find that the automated tests missed?"
  - "How will users in scope of the Equality Act 2010 reasonable-adjustment duty raise an issue?"

---

### 6. Have a Multidisciplinary Team

**Status**: 🟡 Amber

**What This Point Means**: A sustainable team with all the disciplines needed (delivery management, user research, design, content, technology, security, accessibility) and enough autonomy to make decisions.

**Why It Matters**: Skill gaps in the team show up as evidence gaps in the assessment. Beta panels routinely ask team members directly about their role and how they made specific decisions.

**Evidence Required for Beta**:

- Team stable and sustainable.
- All required skills represented.
- Specialists available (accessibility, security, content, etc.).
- Team has autonomy to make decisions.
- Career development for team members.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-STKE-v1.0.md`** (lines 67–78) — Internal stakeholders table identifies all required vendor roles: Service Owner, Lead Architect / CTO, Product Manager, Delivery Manager, Security Lead / SIRO-equivalent, DPO, Accessibility Lead, Finance Lead, SRE / Operations Lead, Customer Success / Support.

✅ **`ARC-001-RISK-v1.0.md`** (RACI matrix line 1049 — Service Owner heavy load — and Section H actions) — Decision rights documented.

✅ **`ARC-001-STKE-v1.0.md`** (Governance & Decision Rights section, RACI matrix) — Decision authority codified per decision type (pricing, ADR, security control, DPIA, AI provider, free-tier limit, incident response, GA go/no-go).

⚠️ **Weak**: Most internal-stakeholder roles are **[PENDING]** — only Service Owner (Mark Craddock) is named. The Lead Architect, Security Lead, DPO, Accessibility Lead, Finance Lead, SRE Lead, and Customer Success roles are unfilled or unidentified.

⚠️ **Weak** (per TCoP Point 13 mapping line 548): "Vendor team partially staffed — STKE internal stakeholders; some [PENDING] roles". The team is not yet stable for a Beta assessment by GDS standards.

❌ **Missing**: User Researcher role not in the internal-stakeholder list. Critical gap given Points 1, 4, and 5 all depend on user research.
❌ **Missing**: Content Designer role not in the internal-stakeholder list.

**Gap Analysis**: The role taxonomy is right and the RACI matrix is unusually well-formed for an Alpha-stage project. The problem is straightforward: most roles are unfilled. A Service Assessor will ask "who is your User Researcher?" on day one. Without a named person, Points 1, 4, and 5 weaken further.

**Readiness Rating**: 🟡 Amber

**Strengths**:

- Role taxonomy comprehensive and aligned to GovS 005 (Government Functional Standard for Digital).
- Decision-rights matrix codified (RACI in STKE).
- Service Owner named and active (Mark Craddock).

**Weaknesses**:

- Most internal-stakeholder roles **[PENDING]** — Lead Architect, Security Lead, DPO, Accessibility Lead, etc.
- No User Researcher in the role taxonomy.
- No Content Designer.

**Recommendations**:

1. **Critical**: Fill or contract the User Researcher role before the pre-assessment walkthrough — without one, Points 1, 4, and 5 cannot reach Green.
   - Timeline: 4 weeks
   - Owner: Service Owner
   - Evidence to create: Named role + first research output.

2. **Critical**: Fill or contract the Accessibility Lead and Content Designer roles before the formal Beta assessment.
   - Timeline: 6 weeks
   - Owner: Service Owner
   - Evidence to create: Named roles + first deliverables (audit, content review).

3. **High**: Update `ARC-001-STKE-v1.0.md` revision to add User Researcher and Content Designer to the internal-stakeholders table.
   - Timeline: 1 week
   - Owner: Service Owner
   - Evidence to create: STKE v1.1.

4. **High**: Generate `ARC-001-PLAN-v1.0.md` (Project Plan) via `/arckit:plan` to capture team timeline and sustainability.
   - Timeline: 2 weeks
   - Owner: Delivery Manager (when filled) or Service Owner
   - Evidence to create: PLAN artefact.

**Assessment Day Guidance**:

- **Prepare**: Named team list with roles; updated RACI; brief CV-style bios for the day.
- **Show**: Each presenter introduces themselves with role and one thing they decided this sprint.
- **Bring**: All Manage-Closely roles from STKE Power-Interest grid (lines 154–214).
- **Materials**: `ARC-001-STKE-v1.0.md` internal stakeholders + RACI; PLAN (when generated).
- **Likely Questions**:
  - "Who's your User Researcher? How many days a week?"
  - "Who has the authority to stop a release for an accessibility issue?"
  - "If your Lead Architect leaves, who's next?"

---

### 7. Use Agile Ways of Working

**Status**: 🟢 Green

**What This Point Means**: The team works in short cycles, delivers working software frequently, learns from each cycle, and adapts. Backlog visible, ceremonies running, retrospectives leading to change.

**Why It Matters**: Agile is the operating system of GDS-aligned services. Panel members will ask the team how they decided what to build last sprint and what they will build next.

**Evidence Required for Beta**:

- Mature agile practices.
- Regular releases to production.
- Retrospectives leading to improvements.
- Team velocity tracked.
- Continuous improvement culture.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-000-PRIN-v2.0.md`** Principle 20 (Continuous Deployment / release-on-merge) — establishes the release cadence default.

✅ **`ARC-001-TCOP-v1.0.md`** Point 13 mapping (line 549) — "Vendor product cadence; sprint reviews; release-on-merge" — agile is operating mode, not aspiration.

✅ **`ARC-001-RISK-v1.0.md`** §H Priority-1, Priority-2, Priority-3 action plan — phased delivery with explicit pre-GA / first-90-days / continuous cadence.

✅ **Eight ADRs (`ARC-001-ADR-001` to `008`)** — each captures a decision, alternatives considered, and consequences. The ADR pattern is a hallmark of agile architecture.

✅ **`ARC-001-STKE-v1.0.md`** (RACI matrix) — Product Manager + Delivery Manager + Service Owner are all named accountable parties.

⚠️ **Weak**: Sprint cadence not explicitly documented (no PLAN artefact yet).
⚠️ **Weak**: No retrospective output documented (would be in PLAN or DEVOPS).

**Gap Analysis**: The team is using ArcKit (its own product) to build ArcKit-as-a-Service, including running the `/arckit:adr` and `/arckit:risk` commands iteratively. That is *evidence-of-agile-by-construction* — the kind of self-eating-its-own-dogfood story that Beta panels respond well to. The missing PLAN artefact is the only material gap.

**Readiness Rating**: 🟢 Green

**Strengths**:

- Eight ADRs with alternatives and consequences — exemplary decision traceability.
- Continuous deployment as a Principle (Principle 20).
- Phased action plan with cadence (RISK §H Priority 1 / 2 / 3).
- Self-evidencing: the team builds the platform using the platform's own governance tooling.

**Weaknesses**:

- No explicit sprint-cadence document.
- No retrospective log shared.

**Recommendations**:

1. **High**: Generate `ARC-001-PLAN-v1.0.md` via `/arckit:plan` documenting sprints, gates, and review cadence.
   - Timeline: 2 weeks
   - Owner: Delivery Manager (when filled) or Service Owner
   - Evidence to create: PLAN artefact.

2. **Medium**: Maintain a public-or-shared retrospective log with last 6 retros showing what changed.
   - Timeline: Continuous
   - Owner: Delivery Manager
   - Evidence to create: Retrospective notes (anonymised).

**Assessment Day Guidance**:

- **Prepare**: Sprint board screenshot; one retrospective with "we changed X because Y" example; ADR list with dates.
- **Show**: The team's actual sprint board (Trello / Jira / GitHub Projects); a recent ADR walk-through.
- **Bring**: Delivery Manager (lead); any team member to demonstrate process.
- **Materials**: `ARC-001-RISK-v1.0.md` §H; ADR-001..008.
- **Likely Questions**:
  - "What did your last retrospective change?"
  - "Show us your backlog."
  - "How often do you release to production?"

---

### 8. Iterate and Improve Frequently

**Status**: 🟢 Green

**What This Point Means**: The service evolves based on user feedback, with the team having capacity and flexibility to ship changes regularly. Iteration is not a one-off Alpha activity; it persists into Beta and Live.

**Why It Matters**: Services that don't iterate ossify and stop meeting user needs as those needs evolve.

**Evidence Required for Beta**:

- Service iterations in production.
- A/B testing or controlled rollouts.
- Feature flags for experimentation.
- Monitoring and feedback loops.
- Regular releases (at least monthly).

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-000-PRIN-v2.0.md`** Principle 20 (Continuous Deployment) — release-on-merge is the default; weekly or more frequent releases.

✅ **`ARC-001-RISK-v1.0.md`** R-009 (line 657) — "Pre-assessment with `/arckit:service-assessment` skill (existing tooling)" + iterative pilot programme. The platform's own tooling is being run iteratively against the platform's own artefacts.

✅ **Eight ADRs over short timeframe** — ADR-001 through ADR-008 produced during Alpha (decisions visible).

✅ **`ARC-001-STKE-v1.0.md`** (Goal G-1) — Pilot programme with ≥3 buying authorities is the iteration vehicle pre-GA.

✅ **`ARC-001-TCOP-v1.0.md`** Point 13 mapping (line 550) — "Continuous deployment (Principle 20); feature flags; pilot-driven iteration".

⚠️ **Weak**: Feature-flag implementation not yet evidenced (no DEVOPS artefact yet).
⚠️ **Weak**: Pilot iteration not yet started (Alpha-stage).

**Gap Analysis**: Iteration is part of the team's DNA — they iterate on the platform using the platform. Once pilots start, the iteration evidence will accumulate quickly. The only soft spot is the lack of a DEVOPS artefact documenting feature-flag and controlled-rollout machinery.

**Readiness Rating**: 🟢 Green

**Strengths**:

- Continuous deployment as a Principle.
- Pilot programme is the explicit iteration vehicle (Goal G-1).
- Eight ADRs in a short window demonstrate decision velocity.

**Weaknesses**:

- No DEVOPS artefact yet.
- Pilot iteration not yet started — *will* be evidence-rich once running.

**Recommendations**:

1. **High**: Generate `ARC-001-DEVOPS-v1.0.md` via `/arckit:devops` covering CI/CD, feature flags, controlled rollout.
   - Timeline: 3 weeks
   - Owner: Lead Architect with SRE Lead (when filled)
   - Evidence to create: DEVOPS artefact.

2. **Medium**: Maintain a "what changed in this release" changelog visible in the product (FR-009 status page already covers incidents — extend to feature releases).
   - Timeline: 2 weeks
   - Owner: Product Manager
   - Evidence to create: In-product changelog.

**Assessment Day Guidance**:

- **Prepare**: Release-frequency stat (releases per week / month); feature-flag inventory; changelog screenshot.
- **Show**: Recent ADR demonstrating an iteration; pilot-feedback example (when pilots running).
- **Bring**: Delivery Manager; Lead Architect.
- **Materials**: ADR-001..008; Principle 20; Goal G-1.
- **Likely Questions**:
  - "Show me a release that you backed out."
  - "How do you know if your last change made things better or worse?"
  - "What's a hypothesis you tested that turned out to be wrong?"

---

### 9. Create a Secure Service Which Protects Users' Privacy

**Status**: 🔴 Red

**What This Point Means**: Security is in the design, not bolted on; user privacy is a first-class concern; the team can demonstrate the controls that protect tenants and tenant users.

**Why It Matters**: A multi-tenant SaaS handling OFFICIAL data with AI processing as a sub-processor relationship is *security and privacy heavy*. Beta assessment cannot pass without independent security testing and a completed DPIA.

**Evidence Required for Beta**:

- Security testing completed (pen test, vulnerability scanning) — CRITICAL.
- GDPR compliance implemented.
- Privacy policy published.
- Data retention policies defined.
- Security monitoring in place.
- Incident response plan documented.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-SBD-v1.0.md`** — Comprehensive Secure by Design assessment covering NCSC CAF (all four objectives A/B/C/D), Cyber Essentials, NCSC Cloud Security Principles (14), threat model, and the UK Government Cyber Security Standard (Cabinet Office July 2025).

✅ **`ARC-001-DPIA-v1.0.md`** — DPIA produced for AI processing (FR-004) with ICO 9-criteria screening, data inventory, lawful-basis register, retention table, sub-processor inventory, transfer assessment, and Article 22 statement (no solely-automated decisions).

✅ **`ARC-001-AIP-v1.0.md`** — UK Government AI Playbook compliance assessment (10 principles + 6 ethical themes scored).

✅ **`ARC-001-RISK-v1.0.md`** R-008 (cross-tenant data leakage, residual 5/25) and R-014 (isolation defect, residual 8/20) — defence-in-depth controls articulated; appetite-acceptance position documented in §H action 8.

✅ **`ARC-001-ADR-001-v1.0.md`** — Tenant Isolation Model (namespace-per-tenant, default-deny network policy, tenant-ID enforcement at every data boundary). `ARC-001-ADR-005-v1.0.md` — Observability with signed, immutable per-tenant audit log.

✅ **`ARC-001-REQ-v1.0.md`** — NFR-SEC-001..009 + NFR-C-001..007 cover authentication, isolation, authorisation, encryption, secrets, vulnerability management, mTLS, NCSC CAF posture, NCSC Cloud Security Principles, UK GDPR, audit retention, accessibility, TCoP, GDS Service Standard, ISO 27001, classifications.

❌ **Missing**: Independent penetration test not yet completed — RISK §H Priority-1 action 1, due GA – 60 days, £40k–£60k. **CRITICAL BLOCKING ISSUE per TCoP §Critical Issues #2 and SBD §9.1 Critical Issue 2.**
❌ **Missing**: Privacy policy not yet published (DPIA completed but privacy notice / publication still pending — TCoP §Critical Issues #1).
❌ **Missing**: Incident-response runbook with ICO-72h-notification template not yet finalised — RISK §H Priority-1 action 7.
❌ **Missing**: First NCSC CAF self-assessment + first NCSC Cloud Security Principles assessment not yet baselined (Goal G-4 commits to first by GA).
⚠️ **Weak**: Cyber Essentials Plus committed but not yet certified (TCoP Point 6 actions).

**Gap Analysis**: The *design* is unusually thorough — three full assessments (SBD, DPIA, AIP) plus a comprehensive risk register with explicit defence-in-depth on the existential R-008. The *delivery gap* is the Beta-required independent pen test and the absence of live security telemetry. The Service Assessment panel will accept the design but not pass Point 9 without the pen-test report and the live monitoring.

**Readiness Rating**: 🔴 Red

**Strengths**:

- Three complete security/privacy artefacts (SBD, DPIA, AIP) — most Beta services have one.
- R-008 / R-014 defence-in-depth explicitly articulated; appetite-acceptance position planned.
- DPIA covers AI sub-processor case explicitly (Article 46 transfer, no-training assurance, no Article 22 decisions).
- Tenant-isolation testing in CI mandated (NFR-SEC-002).

**Weaknesses**:

- Independent pen test outstanding (BLOCKING).
- Privacy policy / privacy notice not published (BLOCKING).
- No live security monitoring (cannot exist pre-GA, but the panel will want to see the SIEM design from ADR-005 with sample data).
- NCSC CAF + Cloud Security Principles not yet baselined.

**Recommendations**:

1. **Critical**: Procure and execute independent pen test (RISK §H action 1) — £40k–£60k, due GA – 60 days.
   - Timeline: 6 weeks (procure + execute + remediate)
   - Owner: Security Lead (when filled) — interim Service Owner
   - Evidence to create: Pen-test report + remediation evidence.

2. **Critical**: Publish privacy notice / policy aligned with the DPIA findings.
   - Timeline: 2 weeks
   - Owner: DPO (when filled) — interim Service Owner
   - Evidence to create: Public privacy policy URL.

3. **Critical**: Complete the first NCSC CAF self-assessment and first NCSC Cloud Security Principles assessment (Goal G-4).
   - Timeline: 4 weeks
   - Owner: Security Lead
   - Evidence to create: CAF + CSP self-assessment artefacts.

4. **Critical**: Finalise incident-response runbook with ICO-72h-notification template (RISK §H action 7).
   - Timeline: 4 weeks
   - Owner: DPO with Security Lead
   - Evidence to create: Runbook + tabletop-exercise outcome.

5. **High**: Land the Compliance Acceptance Register entries for R-008, R-009, R-010, R-011 (RISK §H action 8) before GA – 14 days.
   - Timeline: 6 weeks (post-pen-test)
   - Owner: Service Owner with DPO + Security Lead
   - Evidence to create: Acceptance register signatures in SBD §10.

**Assessment Day Guidance**:

- **Prepare**: Pen-test executive summary; DPIA extract (data inventory + lawful basis); incident-runbook walk-through; ADR-001 (tenant isolation); SBD §1 CAF scorecard.
- **Show**: Tenant-isolation CI test running (NFR-SEC-002); audit-log integrity demo (ADR-005).
- **Bring**: Security Lead (mandatory); DPO (mandatory); Lead Architect.
- **Materials**: `ARC-001-SBD-v1.0.md`, `ARC-001-DPIA-v1.0.md`, `ARC-001-AIP-v1.0.md`, `ARC-001-ADR-001-v1.0.md`, `ARC-001-ADR-005-v1.0.md`, NFR-SEC-001..009, RISK R-008 / R-014.
- **Likely Questions**:
  - "Walk me through how a defect in your AI provider would surface in a tenant-data leak."
  - "Show me your CAF self-assessment."
  - "How would you notify the ICO inside 72 hours of a confirmed breach?"
  - "Why did the pen test find no critical issues — were the testers competent?"

---

### 10. Define What Success Looks Like and Publish Performance Data

**Status**: 🔴 Red

**What This Point Means**: The team has clear KPIs aligned to user needs and publishes performance data so the public, peers, and auditors can see how the service is doing.

**Why It Matters**: Public accountability is a structural feature of UK Government services. Live services *must* publish performance data (4 mandatory KPIs at Live: cost per transaction, user satisfaction, completion rate, digital take-up). Beta services should be collecting and starting to publish.

**Evidence Required for Beta**:

- Performance data being collected.
- Dashboard showing key metrics.
- Performance data published (at least internally).
- Metrics reviewed regularly by team.
- Targets set for live service.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-STKE-v1.0.md`** Goals G-1..G-8 + Outcomes O-1..O-7 — Eight goals and seven outcomes with explicit KPIs (e.g., G-2: ≥60% of new SME tenants reach 5 saved artefacts within 5 working days; O-2: ≥200 SMEs onboarded in 12 months; O-4: zero cross-tenant incidents).

✅ **`ARC-001-REQ-v1.0.md`** NFR-A-001 (≥99.9% rolling-30-day availability), NFR-P-001..003 (response-time, AI-generation, export latency), NFR-S-001..002 (scaling).

✅ **`ARC-001-REQ-v1.0.md`** FR-009 (Public Status Page) — Externally accessible status page committed.

✅ **`ARC-000-PRIN-v2.0.md`** Principle 6 (Observability / Public Status Page) — committed as a non-negotiable.

❌ **Missing**: No live performance data (cannot exist pre-GA).
❌ **Missing**: No performance dashboard yet — neither tenant-facing nor public.
❌ **Missing**: No baseline measurement (Goal G-2 target: ≥60%, current: 0).
❌ **Missing**: No documented "where we publish performance data" plan (e.g., "we will publish on the public site monthly from GA + 90 days").

**Gap Analysis**: The *targets* are well-defined and quantitative; the *measurement* and *publication* infrastructure does not exist yet. For a Beta assessment, the panel will accept "we will publish from GA + 90 days" provided the dashboard design and data collection are demonstrably in place. As of now, even the design of the dashboard is implicit in NFRs rather than documented as a tangible artefact.

**Readiness Rating**: 🔴 Red

**Strengths**:

- 8 goals × 7 outcomes with measurable KPIs (Goal G-1..G-8).
- Public status page committed (FR-009; Principle 6).
- ≥99.9% availability target codified (NFR-A-001).

**Weaknesses**:

- No live performance data.
- No dashboard implementation evidenced.
- No publication plan / cadence documented.

**Recommendations**:

1. **Critical**: Design and stand up the performance dashboard (internal first, external by GA + 90 days) covering Goal G-2 (time-to-first-bid-pack), G-3 (cross-subsidy KRIs), G-4 (CAF posture), G-6 (a11y CI green), and the 4 mandatory Live KPIs (cost per transaction, user satisfaction, completion rate, digital take-up).
   - Timeline: 6 weeks
   - Owner: Product Manager with SRE Lead (when filled)
   - Evidence to create: Dashboard URL + Beta-phase data sample.

2. **Critical**: Publish performance-data publication plan: where, when, what cadence, what reviewers.
   - Timeline: 2 weeks
   - Owner: Product Manager
   - Evidence to create: Performance-data publication plan section in PLAN (when generated) or in BR-006 evidence pack.

3. **High**: Stand up the public status page (FR-009) before the formal Beta assessment.
   - Timeline: 4 weeks
   - Owner: SRE Lead with Lead Architect
   - Evidence to create: Public status-page URL.

**Assessment Day Guidance**:

- **Prepare**: KPI matrix (Goal-to-KPI mapping); dashboard design / mockup; publication-cadence plan.
- **Show**: Dashboard in development; status-page mockup; STKE Goal G-1..G-8 KPI table.
- **Bring**: Product Manager; SRE / Performance Analyst.
- **Materials**: `ARC-001-STKE-v1.0.md` Goals/Outcomes; NFR-A-001; FR-009; Principle 6.
- **Likely Questions**:
  - "Where will users see your performance data?"
  - "What's your baseline today?"
  - "Show me one metric you intend to be transparent about even when it's bad news."

---

### 11. Choose the Right Tools and Technology

**Status**: 🟡 Amber

**What This Point Means**: Technology choices are deliberate, justified, cost-aware, and proportionate. Build vs buy is conscious. Avoiding vendor lock-in is a first-class concern. Skills match the choices.

**Why It Matters**: Public-sector technology choices are durable; expensive lock-in or wrong-fit choices have multi-year cost consequences.

**Evidence Required for Beta**:

- Technology choices working in production.
- Technology scalable and fit for purpose.
- Total cost of ownership understood.
- Technology risks managed.
- Team has skills for chosen technology.

**Evidence Found in ArcKit Artefacts**:

✅ **Eight ADRs (`ARC-001-ADR-001` to `008`)** — every material technology choice has an ADR with alternatives and consequences. ADR-002 (Cloud Region and Storage Selection), ADR-003 (Identity Provider Integration and SSO), ADR-004 (AI Provider Abstraction), ADR-005 (Observability), ADR-006 (Deployment Topology), ADR-007 (Data Portability and Export Format), ADR-008 (Per-Tenant Quotas, Rate Limits, and Fair Use).

✅ **`ARC-001-RISK-v1.0.md`** R-015 (managed K8s vendor lock-in, residual 6/9 with quarterly portability rehearsal) and R-017 (AI provider, residual 4/9 with pluggable abstraction) — vendor-concentration risks explicitly tracked with portability mitigations.

✅ **`ARC-001-STKE-v1.0.md`** Goal G-8 (Pluggable AI Provider for Future Sovereign Reuse) — "AI provider integrated through a pluggable abstraction with a second provider validated in CI quarterly; provider switchable in days not weeks".

✅ **`ARC-001-TCOP-v1.0.md`** Point 11 (Define Your Purchasing Strategy, line 431) — vendor-side procurement strategy assessed Compliant; Point 5 (Use Cloud First) Compliant.

⚠️ **Weak**: No `ARC-001-RSCH-v*.md` (Research) artefact yet — TCoP-aligned research / proof of concept evidence not separately documented.
⚠️ **Weak**: No total-cost-of-ownership / SOBC artefact yet (REQ Document Purpose explicitly notes SOBC is pending).
⚠️ **Weak**: Live evidence of "technology choices working in production" cannot exist pre-GA.

**Gap Analysis**: Decision quality is high (eight ADRs with alternatives; portability rehearsals planned for R-015 and R-017). The gap is the missing SOBC (cost-of-ownership) and the missing RSCH (technology research) — both are *committed* in REQ Document Purpose but not yet produced.

**Readiness Rating**: 🟡 Amber

**Strengths**:

- Eight ADRs covering all material choices with explicit alternatives.
- Vendor-lock-in mitigated by portability ADRs (ADR-004, ADR-006, ADR-007).
- Quarterly portability rehearsals explicit (RISK §H Priority-2 action 12).

**Weaknesses**:

- No RSCH artefact (technology research not separately captured).
- No SOBC (TCO not formalised).
- No live evidence (pre-GA).

**Recommendations**:

1. **High**: Generate `ARC-001-SOBC-v1.0.md` via `/arckit:sobc` to formalise TCO and Five Case Model.
   - Timeline: 4 weeks
   - Owner: Service Owner with Finance Lead (when filled)
   - Evidence to create: SOBC artefact with quantified TCO.

2. **High**: Generate `ARC-001-RSCH-v1.0.md` (or AWS / Azure / GCP research as appropriate) to document technology research and proof-of-concept findings.
   - Timeline: 3 weeks
   - Owner: Lead Architect
   - Evidence to create: RSCH artefact.

3. **High**: Execute the portability rehearsal on alternative cloud profile (RISK §H Priority-1 action 3) and the AI-provider failover drill (action 4) before Beta assessment.
   - Timeline: 4 weeks
   - Owner: Lead Architect
   - Evidence to create: Rehearsal report + portability evidence.

**Assessment Day Guidance**:

- **Prepare**: ADR-001..008 summaries; TCO summary (when SOBC done); portability rehearsal report.
- **Show**: ADR-004 (AI Provider Abstraction) demo of provider switch.
- **Bring**: Lead Architect (mandatory).
- **Materials**: ADR-001..008; RISK R-015, R-017; Goal G-8.
- **Likely Questions**:
  - "What's your three-year cost forecast?"
  - "How would you switch off your AI provider tomorrow?"
  - "Why managed Kubernetes and not [alternative]?"

---

### 12. Make New Source Code Open

**Status**: 🔴 Red

**What This Point Means**: Source code for the service is open by default, under an OSI-approved licence, in a public repository, with secrets kept out and contribution guidelines in place. Exceptions are documented and justified.

**Why It Matters**: GDS expects open source as the default. Closed source must be defended.

**Evidence Required for Beta**:

- Source code repository exists (GitHub / GitLab).
- Code published under appropriate licence (MIT, Apache 2.0, etc.).
- Secrets and credentials not in source code.
- README and documentation for developers.
- Contribution guidelines if accepting contributions.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-000-PRIN-v2.0.md`** Principle 16 (Open Source First and Reuse Before Build) — mandates `/arckit:gov-reuse` and equivalent searches before new builds; ADRs to capture build-vs-reuse decisions; SBOM produced; OSI-approved licences for reusable cross-cutting components.

✅ **The underlying ArcKit plugin (`arc-kit/arckit/4.12.3`) is open source** (publicly distributed) — TCoP Point 3 line 135.

✅ **`ARC-001-ADR-006-v1.0.md`** mandates OCI-standard containers and GitOps using open-source orchestration (Kubernetes).

✅ **`ARC-001-REQ-v1.0.md`** NFR-SEC-005 (no secrets in code).

⚠️ **Partial** (per TCoP Point 3 line 141): "service-side code-publication strategy is partial: the ArcKit plugin/templates are open; service-side multi-tenancy code, SME-verification workflow, and FinOps dashboards are not currently scoped for full open release given they encode commercial cross-subsidy logic. Build-vs-publish decision recorded as future ADR."

❌ **Missing**: ADR for service-side open-source publication strategy — TCoP Point 3 action, due 2026-07-31 (Lead Architect).
❌ **Missing**: Public service-side repository.
❌ **Missing**: Documented justification for non-publication of cross-subsidy / commercial logic — at the moment, the rationale exists in TCoP but not in a standalone ADR.
❌ **Missing**: SBOM published per release (TCoP Point 3 HIGH action — committed but not evidenced).

**Gap Analysis**: This is the most contentious of the four Red points. The team has a credible argument for partial closure (cross-subsidy logic encodes commercial-model details) but has *not yet documented it as an ADR with explicit justification*. The Service Assessment panel will pull on this thread: "Why isn't the multi-tenancy code public?" without a clear ADR answer, the team will struggle.

**Readiness Rating**: 🔴 Red

**Strengths**:

- Underlying ArcKit plugin is genuinely open source.
- Open-source-first is a Principle (Principle 16).
- Open-formats-only for tenant export (ADR-007) — tenant-facing data is non-proprietary.

**Weaknesses**:

- No ADR for service-side OSS publication strategy.
- No public service-side repository.
- SBOM not yet evidenced.

**Recommendations**:

1. **Critical**: Generate `ARC-001-ADR-009-v1.0.md` (or similar) for service-side open-source publication strategy: which components release (e.g., reusable libraries, CLI plumbing, tenant-facing OpenAPI specs), which retain (e.g., billing / FinOps / SME-verification logic).
   - Timeline: 3 weeks
   - Owner: Lead Architect
   - Evidence to create: Service-side OSS publication ADR with explicit justification.

2. **Critical**: Stand up a public service-side repository for the components the ADR commits to publish (even if minimal).
   - Timeline: 4 weeks
   - Owner: Lead Architect
   - Evidence to create: Public GitHub / GitLab repository under an OSI-approved licence (MIT or Apache 2.0).

3. **High**: Maintain SBOM in CI on every release (TCoP Point 3 HIGH action).
   - Timeline: 4 weeks
   - Owner: Lead Architect
   - Evidence to create: SBOM artefact published per release.

**Assessment Day Guidance**:

- **Prepare**: Service-side OSS publication ADR; public repository link; SBOM example.
- **Show**: The repository + a recent commit; the OSI licence file.
- **Bring**: Lead Architect.
- **Materials**: Principle 16; TCoP Point 3 evidence; new ADR.
- **Likely Questions**:
  - "What is open and what is closed, and why?"
  - "Show me the licence on your repository."
  - "How would another government team reuse your work?"

---

### 13. Use and Contribute to Open Standards, Common Components and Patterns

**Status**: 🟢 Green

**What This Point Means**: The service uses GOV.UK Design System, common components (Notify, Pay, One Login / Verify), open data standards, and recognised API standards rather than reinventing them.

**Why It Matters**: Open standards adoption reduces friction for the public, increases interoperability, and reduces rework.

**Evidence Required for Beta**:

- GOV.UK Design System implemented.
- Common components integrated (Notify, Pay, etc., where applicable).
- APIs follow government API standards.
- Open standards used for data formats.
- Contributing patterns back to community (if novel).

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-000-PRIN-v2.0.md`** Principle 4 (Open Standards and Interoperability) — HTTP APIs documented with OpenAPI; events documented with AsyncAPI; tenant content stored in open, human-readable formats; authentication via OIDC / OAuth 2.x / SAML 2.0; full-fidelity export in open formats.

✅ **`ARC-001-REQ-v1.0.md`** FR-008 (Public API and Event Interfaces) — OpenAPI + AsyncAPI specifications published.

✅ **`ARC-001-ADR-003-v1.0.md`** (Identity Provider Integration and SSO) — OIDC and SAML 2.0 standards-based.

✅ **`ARC-001-ADR-007-v1.0.md`** (Data Portability and Export Format) — Markdown / JSON / YAML / SBOM open standards.

✅ **`ARC-001-ADR-006-v1.0.md`** — OCI-standard containers (open standard) and Kubernetes API.

✅ **`ARC-001-REQ-v1.0.md`** FR-013 (GOV.UK Design System Alignment) — SHOULD_HAVE; "Components selected from the GOV.UK Design System where a suitable pattern exists. Where bespoke components are used, they are documented with accessibility evidence."

✅ **`ARC-001-TCOP-v1.0.md`** Point 4 (Make Use of Open Standards) — assessed **Compliant**.

⚠️ **Weak**: GOV.UK Notify / Pay / One Login integration not documented (B2B SaaS — likely N/A for Notify/Pay; may apply for One Login if buyer-side users sign in to verify supplier evidence).
⚠️ **Weak**: OpenAPI / AsyncAPI not yet *publicly* published (TCoP Point 4 HIGH action: "Publish OpenAPI specs publicly at GA").

**Gap Analysis**: The standards story is genuinely strong and aligned to public-sector expectations. The two soft spots (Notify/Pay/One Login applicability and not-yet-public API specs) are addressable with documentation rather than rework.

**Readiness Rating**: 🟢 Green

**Strengths**:

- OIDC / OAuth 2.x / SAML 2.0 (ADR-003); OpenAPI + AsyncAPI (FR-008); OCI + Kubernetes (ADR-006); Markdown / JSON / YAML (ADR-007).
- GOV.UK Design System alignment SHOULD_HAVE (FR-013).
- Open-formats-only for tenant export (ADR-007).

**Weaknesses**:

- Public OpenAPI / AsyncAPI URL not yet committed.
- GOV.UK Notify / Pay / One Login applicability not explicitly scoped (likely N/A but should say so).

**Recommendations**:

1. **High**: Publish OpenAPI specifications publicly at GA on a documented stable URL (TCoP Point 4 action).
   - Timeline: 3 weeks
   - Owner: Lead Architect
   - Evidence to create: Public OpenAPI URL.

2. **Medium**: Document GOV.UK common-component applicability (Notify / Pay / One Login) — which apply, which do not, and why.
   - Timeline: 1 week
   - Owner: Product Manager
   - Evidence to create: Note in TCoP §4 or in PLAN.

**Assessment Day Guidance**:

- **Prepare**: Standards inventory (OIDC / OAuth / SAML / OpenAPI / AsyncAPI / OCI / K8s / Markdown / JSON / YAML / GOV.UK Design System); common-component applicability note.
- **Show**: GOV.UK Design System component in the UI; an OpenAPI spec.
- **Bring**: Lead Architect.
- **Materials**: ADR-003, ADR-006, ADR-007; FR-008, FR-013; Principle 4.
- **Likely Questions**:
  - "Why didn't you use GOV.UK One Login?"
  - "Show me your OpenAPI spec."
  - "What patterns are you contributing back?"

---

### 14. Operate a Reliable Service

**Status**: 🟡 Amber

**What This Point Means**: The service is up when users need it; incidents are handled well; there is a credible plan for resilience, capacity, and disaster recovery.

**Why It Matters**: Beta services that fall over routinely fail to progress to Live.

**Evidence Required for Beta**:

- Service uptime meeting targets (typically 99.9%).
- Monitoring and alerting in place.
- Incident response procedures documented.
- On-call rota established.
- Disaster recovery plan tested.
- Load testing completed.

**Evidence Found in ArcKit Artefacts**:

✅ **`ARC-001-REQ-v1.0.md`** NFR-A-001 (≥99.9% rolling-30-day availability ≈ 43 minutes downtime per month).

✅ **`ARC-001-REQ-v1.0.md`** NFR-A-002 (DR — RPO < 15 min, RTO < 4 h, daily off-site backups within UK region; backup retention 35 days; annual full DR drill).

✅ **`ARC-001-REQ-v1.0.md`** NFR-A-003 (Fault Tolerance — circuit breaker, retry with exponential backoff, timeout on all network calls, bulkhead isolation between tenants, graceful degradation).

✅ **`ARC-001-REQ-v1.0.md`** NFR-S-001..002 (horizontal scaling, data-volume scaling).

✅ **`ARC-001-ADR-005-v1.0.md`** (Observability Stack — Logging, Metrics, Tracing, SIEM).

✅ **`ARC-001-ADR-006-v1.0.md`** (Deployment Topology) — managed Kubernetes; cell-per-tier; multi-zone failover.

✅ **`ARC-001-RISK-v1.0.md`** §J Monitoring and Review Framework — risk-review cadence + KRI dashboard.

✅ **`ARC-001-REQ-v1.0.md`** FR-009 (Public Status Page).

⚠️ **Weak**: No live uptime data (cannot exist pre-GA).
⚠️ **Weak**: No load-testing report.
⚠️ **Weak**: No DR drill executed yet (annual cadence committed; first one will be GA + 12 months unless brought forward).
⚠️ **Weak**: On-call rota not yet established (SRE Lead role [PENDING] in STKE).
⚠️ **Weak**: Incident-response runbook with ICO-72h-notification template not yet finalised (RISK §H Priority-1 action 7).

**Gap Analysis**: Reliability *design* is solid (NFR-A-001..003 + NFR-S-001..002 + ADR-005 + ADR-006). The *delivery and rehearsal* gaps are typical of pre-GA Alpha-stage projects: no live data, no load test, no DR drill, no on-call rota. The Beta panel will accept "design is good and rehearsal is scheduled pre-GA" provided the incident-response runbook is finalised and at least a synthetic load test is on record.

**Readiness Rating**: 🟡 Amber

**Strengths**:

- ≥99.9% availability codified (NFR-A-001).
- DR / RPO / RTO codified with annual drill (NFR-A-002).
- Defence-in-depth resilience patterns (NFR-A-003: circuit breaker, retry, timeout, bulkhead, graceful degradation).
- Observability stack ADR (ADR-005).

**Weaknesses**:

- No live data.
- No load test.
- No first DR drill.
- On-call not established (SRE Lead [PENDING]).
- Incident runbook outstanding.

**Recommendations**:

1. **Critical**: Finalise incident-response runbook with ICO-72h-notification template (RISK §H Priority-1 action 7).
   - Timeline: 4 weeks
   - Owner: DPO with Security Lead
   - Evidence to create: Runbook + tabletop-exercise outcome.

2. **Critical**: Execute first synthetic load test against Beta environment before formal Beta assessment.
   - Timeline: 4 weeks
   - Owner: SRE Lead with Lead Architect
   - Evidence to create: Load-test report.

3. **Critical**: Stand up the SRE on-call rota (minimum 2 named engineers + escalation to Lead Architect / Service Owner).
   - Timeline: 4 weeks
   - Owner: Service Owner / Lead Architect
   - Evidence to create: On-call rota document + escalation chain.

4. **High**: Bring forward the first DR drill to Beta (rather than annual from GA).
   - Timeline: 6 weeks
   - Owner: Lead Architect with SRE Lead
   - Evidence to create: First DR drill report.

**Assessment Day Guidance**:

- **Prepare**: NFR-A-001..003 summary; ADR-005 + ADR-006 architecture; load-test report; on-call rota; runbook example.
- **Show**: Status page mockup; observability dashboard sample; bulkhead-pattern test.
- **Bring**: SRE Lead (when filled); Lead Architect.
- **Materials**: NFR-A-001..003; ADR-005; ADR-006; FR-009; RISK §J.
- **Likely Questions**:
  - "What was your last incident, and what did you learn?"
  - "Walk me through your DR plan."
  - "Show me your load-test results."

---

## Evidence Inventory

**Complete Traceability**: Service Standard Point → ArcKit Artefacts

| Service Standard Point | ArcKit Artefacts | Status | Critical Gaps |
|------------------------|------------------|--------|---------------|
| 1. Understand users | `ARC-001-STKE-v1.0.md` (DDaT roles + drivers SD-1..SD-14 + Goal G-1, G-2); `ARC-001-REQ-v1.0.md` (4 personas + UC-1..UC-3) | 🟡 Amber | No live research; no AT-user testing |
| 2. Solve whole problem | `ARC-001-REQ-v1.0.md` (UC-1..UC-3, BR-001..008, out-of-scope); `ARC-001-STKE-v1.0.md` (Goal G-1, G-2, Outcome O-1) | 🟢 Green | None |
| 3. Joined up experience | `ARC-001-REQ-v1.0.md` (FR-008, FR-009); `ARC-001-ADR-003-v1.0.md` (SSO) | 🟡 Amber | G-Cloud listing not yet live; no channel-switching test |
| 4. Simple to use | `ARC-001-REQ-v1.0.md` (NFR-U-001, FR-013); `ARC-001-STKE-v1.0.md` (Goal G-2 5-day target) | 🟡 Amber | No usability testing yet; no content-design review |
| 5. Everyone can use | `ARC-000-PRIN-v2.0.md` Principle 12 (NON-NEGOTIABLE); `ARC-001-REQ-v1.0.md` NFR-C-003; `ARC-001-STKE-v1.0.md` Goal G-6; `ARC-001-TCOP-v1.0.md` Point 2 | 🔴 Red | Manual WCAG 2.2 AA audit; Accessibility Statement; AT-user testing |
| 6. Multidisciplinary team | `ARC-001-STKE-v1.0.md` (internal stakeholders + RACI matrix) | 🟡 Amber | Most roles [PENDING]; no User Researcher; no Content Designer |
| 7. Agile ways of working | `ARC-000-PRIN-v2.0.md` Principle 20; `ARC-001-RISK-v1.0.md` §H phased actions; ADR-001..008 | 🟢 Green | None (PLAN missing but not blocking) |
| 8. Iterate frequently | `ARC-000-PRIN-v2.0.md` Principle 20; `ARC-001-STKE-v1.0.md` Goal G-1 pilot programme; ADR-001..008 | 🟢 Green | DEVOPS artefact not yet generated |
| 9. Secure and private | `ARC-001-SBD-v1.0.md`; `ARC-001-DPIA-v1.0.md`; `ARC-001-AIP-v1.0.md`; `ARC-001-RISK-v1.0.md` R-008/R-014; ADR-001, ADR-005; NFR-SEC-001..009 + NFR-C-001..007 | 🔴 Red | Independent pen test; privacy notice; CAF + CSP baseline; incident runbook |
| 10. Success metrics | `ARC-001-STKE-v1.0.md` Goals G-1..G-8 + Outcomes O-1..O-7; `ARC-001-REQ-v1.0.md` NFR-A-001, NFR-P-001..003, FR-009 | 🔴 Red | No live data; no dashboard; no public status page |
| 11. Right tools | ADR-001..008; `ARC-001-RISK-v1.0.md` R-015, R-017; `ARC-001-STKE-v1.0.md` Goal G-8; `ARC-001-TCOP-v1.0.md` Point 5, 11 | 🟡 Amber | No SOBC (TCO); no RSCH; portability rehearsal pending |
| 12. Open source | `ARC-000-PRIN-v2.0.md` Principle 16; ADR-006 (Kubernetes/OCI); ADR-007 (open formats); `ARC-001-TCOP-v1.0.md` Point 3 | 🔴 Red | Service-side OSS publication ADR; public repo; SBOM evidence |
| 13. Open standards | `ARC-000-PRIN-v2.0.md` Principle 4; `ARC-001-REQ-v1.0.md` FR-008, FR-013; ADR-003, ADR-006, ADR-007; `ARC-001-TCOP-v1.0.md` Point 4 | 🟢 Green | Public OpenAPI URL pending |
| 14. Reliable service | `ARC-001-REQ-v1.0.md` NFR-A-001..003, NFR-S-001..002, FR-009; ADR-005, ADR-006; `ARC-001-RISK-v1.0.md` §J | 🟡 Amber | Incident runbook; load test; DR drill; on-call rota |

**Summary**:

- ✅ Strong evidence: Points 2 (Whole problem), 7 (Agile), 8 (Iterate), 13 (Open standards)
- ⚠️ Adequate but needs strengthening: Points 1 (Users), 3 (Joined-up), 4 (Simple), 6 (Multidisciplinary), 11 (Right tools), 14 (Reliable)
- ❌ Critical gaps: Points 5 (Accessibility), 9 (Secure/Private), 10 (Performance data), 12 (Open source)

---

## Assessment Preparation Checklist

### Critical Actions (Complete within 2–6 weeks — must complete before formal Beta booking; address Red ratings)

- [ ] **Action 1**: Procure and execute independent penetration test (RISK §H action 1)
  - Point: 9 (Secure and private)
  - Timeline: 6 weeks (procure + execute + remediate)
  - Owner: Security Lead — interim Service Owner
  - Outcome: Pen-test report + remediation evidence; validates R-008 / R-014 residual scores

- [ ] **Action 2**: Procure and complete manual WCAG 2.2 AA audit
  - Point: 5 (Everyone can use)
  - Timeline: 4 weeks
  - Owner: Accessibility Lead
  - Outcome: Audit report; closes TCoP §Critical Issues #4

- [ ] **Action 3**: Publish Accessibility Statement aligned with PSBAR 2018
  - Point: 5 (Everyone can use)
  - Timeline: 2 weeks
  - Owner: Accessibility Lead
  - Outcome: Public Accessibility Statement URL

- [ ] **Action 4**: Conduct AT-user research session (screen reader, keyboard-only, voice control)
  - Point: 1 (Users) + 5 (Accessibility)
  - Timeline: 6 weeks
  - Owner: User Researcher with Accessibility Lead
  - Outcome: AT-user research report

- [ ] **Action 5**: Generate `ARC-001-ADR-009-v*.md` (or similar) for service-side OSS publication strategy + stand up public repository
  - Point: 12 (Open source)
  - Timeline: 4 weeks
  - Owner: Lead Architect
  - Outcome: ADR + public GitHub / GitLab repository under OSI-approved licence

- [ ] **Action 6**: Publish privacy notice / privacy policy
  - Point: 9 (Secure and private)
  - Timeline: 2 weeks
  - Owner: DPO — interim Service Owner
  - Outcome: Public privacy policy URL

- [ ] **Action 7**: Stand up performance dashboard (internal first)
  - Point: 10 (Success metrics)
  - Timeline: 6 weeks
  - Owner: Product Manager with SRE Lead
  - Outcome: Dashboard URL + Beta-phase data sample

- [ ] **Action 8**: Stand up public status page (FR-009)
  - Point: 10 (Success metrics) + 14 (Reliable)
  - Timeline: 4 weeks
  - Owner: SRE Lead with Lead Architect
  - Outcome: Public status-page URL

- [ ] **Action 9**: Pre-assessment evidence-pack walkthrough with one Service Assessor + one pilot DDaT EA (RISK §H action 5)
  - Point: All 14
  - Timeline: 8 weeks
  - Owner: Product Manager
  - Outcome: Walkthrough notes + format/coverage feedback

### High Priority Actions (Complete within 4–8 weeks — Amber → Green)

- [ ] **Action 10**: Recruit and complete first round of pilot DDaT user research (3 buying-authority EAs + 5 SME architects)
  - Point: 1 (Users)
  - Timeline: 4 weeks
  - Owner: Product Manager + User Researcher
  - Outcome: User-research synthesis document

- [ ] **Action 11**: Run usability-testing sessions on Alpha prototype with at least 5 SME architects + 3 buying-authority architects
  - Point: 4 (Simple)
  - Timeline: 4 weeks
  - Owner: User Researcher with Product Manager
  - Outcome: Usability findings report; task-completion-rate baseline

- [ ] **Action 12**: Fill or contract User Researcher, Accessibility Lead, Content Designer, Security Lead, DPO, SRE Lead roles
  - Point: 6 (Multidisciplinary team)
  - Timeline: 6 weeks
  - Owner: Service Owner
  - Outcome: Named team

- [ ] **Action 13**: Generate `ARC-001-PLAN-v1.0.md` (Project Plan) via `/arckit:plan`
  - Point: 6 (Team) + 7 (Agile) + 14 (Reliable)
  - Timeline: 2 weeks
  - Owner: Delivery Manager — interim Service Owner
  - Outcome: PLAN artefact

- [ ] **Action 14**: Generate `ARC-001-SOBC-v1.0.md` via `/arckit:sobc`
  - Point: 11 (Right tools)
  - Timeline: 4 weeks
  - Owner: Service Owner with Finance Lead
  - Outcome: SOBC artefact with quantified TCO

- [ ] **Action 15**: Generate `ARC-001-DEVOPS-v1.0.md` via `/arckit:devops`
  - Point: 8 (Iterate) + 14 (Reliable)
  - Timeline: 3 weeks
  - Owner: Lead Architect with SRE Lead
  - Outcome: DEVOPS artefact

- [ ] **Action 16**: Execute portability rehearsal on alternative cloud profile + AI-provider failover drill (RISK §H actions 3 + 4)
  - Point: 11 (Right tools)
  - Timeline: 4 weeks
  - Owner: Lead Architect
  - Outcome: Rehearsal reports

- [ ] **Action 17**: Finalise incident-response runbook with ICO-72h-notification template (RISK §H action 7)
  - Point: 9 (Secure) + 14 (Reliable)
  - Timeline: 4 weeks
  - Owner: DPO with Security Lead
  - Outcome: Runbook + tabletop-exercise outcome

- [ ] **Action 18**: Stand up SRE on-call rota
  - Point: 14 (Reliable)
  - Timeline: 4 weeks
  - Owner: Service Owner / Lead Architect
  - Outcome: On-call rota + escalation chain

- [ ] **Action 19**: Land G-Cloud listing (BR-004)
  - Point: 3 (Joined-up channels)
  - Timeline: 4 weeks (CCS-iteration dependent)
  - Owner: Service Owner with CCS liaison
  - Outcome: Active Digital Marketplace listing URL

- [ ] **Action 20**: Execute first synthetic load test
  - Point: 14 (Reliable)
  - Timeline: 4 weeks
  - Owner: SRE Lead with Lead Architect
  - Outcome: Load-test report

### Medium Priority Actions (Nice to have — improve confidence)

- [ ] **Action 21**: Maintain SBOM in CI on every release (TCoP Point 3 HIGH action)
  - Point: 12 (Open source)
  - Timeline: 4 weeks
  - Owner: Lead Architect
  - Outcome: SBOM published per release

- [ ] **Action 22**: Publish OpenAPI specifications publicly at GA
  - Point: 13 (Open standards)
  - Timeline: 3 weeks
  - Owner: Lead Architect
  - Outcome: Public OpenAPI URL

- [ ] **Action 23**: Document GOV.UK common-component applicability (Notify / Pay / One Login)
  - Point: 13 (Open standards)
  - Timeline: 1 week
  - Owner: Product Manager
  - Outcome: Applicability note in TCoP §4 or PLAN

- [ ] **Action 24**: One-page user journey diagram (UC-1 → UC-2 → UC-3)
  - Point: 2 (Whole problem)
  - Timeline: 1 week
  - Owner: Product Manager
  - Outcome: Journey diagram (Mermaid)

- [ ] **Action 25**: Generate `ARC-001-DIAG-001-v*.md` (C4 context + container) via `/arckit:diagram`
  - Point: 9 (Secure) + 11 (Right tools) + 14 (Reliable)
  - Timeline: 2 weeks
  - Owner: Lead Architect
  - Outcome: Architecture diagrams

- [ ] **Action 26**: Generate `ARC-001-TRAC-v1.0.md` (Traceability Matrix) via `/arckit:traceability`
  - Point: 7 (Agile) + 8 (Iterate)
  - Timeline: 2 weeks
  - Owner: Lead Architect
  - Outcome: Traceability matrix

- [ ] **Action 27**: Compliance Acceptance Register for R-008 / R-009 / R-010 / R-011 (RISK §H action 8)
  - Point: 9 (Secure)
  - Timeline: 6 weeks (post-pen-test)
  - Owner: Service Owner with DPO + Security Lead
  - Outcome: Acceptance entries in SBD §10

---

## Assessment Day Preparation

### Timeline and Booking

**Current Readiness**: 🔴 Red — not ready to book formal Beta assessment yet. Pre-assessment walkthrough first (RISK §H Priority-1 action 5).

**Recommended Booking Timeline**:

- Complete critical actions (Actions 1–9): 6 weeks
- Pre-assessment walkthrough with 1 Service Assessor + 1 pilot DDaT EA: 8 weeks (= GA – 60 days target)
- Address walkthrough feedback: 2 weeks
- Complete high-priority actions (Actions 10–20): 8 weeks
- Buffer: 1 week
- **Ready to book formal Beta assessment after**: 11–12 weeks from now (GA – 30 days target)

**How to Book**:

1. Contact GDS Central Digital & Data Office assessment team via the Service Manual booking process.
2. Book at least 5 weeks in advance.
3. Assessments typically Tuesday–Thursday.
4. Duration: 4 hours.
5. Provide: Service name (ArcKit as a Service — Managed SaaS), department / sponsor (vendor — supplier of UK Government via G-Cloud), phase (Beta), preferred dates.

**Note on procurement-side framing**: ArcKit as a Service is a *commercial supplier service* (B2B SaaS) rather than a citizen-facing departmental service. Service assessment for supplier services accessed via G-Cloud is non-standard; the team must clarify with CDDO at booking whether the formal GDS Service Standard route applies, or whether equivalent assurance evidence (the artefacts in this report) is the right vehicle. The pre-assessment walkthrough is the right place to have this conversation.

### Documentation to Share with Panel (Send 1 Week Before)

**Required documentation**:

- [ ] Project overview (1–2 pages — extract from `ARC-001-STKE-v1.0.md` Executive Summary).
- [ ] User research repository / synthesis (when generated — Action 10).
- [ ] Service architecture diagrams (when generated — Action 25).
- [ ] Demo / prototype environment URL.

**Recommended documentation — Key ArcKit artefacts**:

- [ ] `ARC-001-STKE-v1.0.md` — Stakeholders, DDaT roles, drivers, goals, outcomes
- [ ] `ARC-001-REQ-v1.0.md` — Requirements (BR-001..008, FR-001..015, NFRs)
- [ ] `ARC-001-RISK-v1.0.md` — Risk register (especially R-008, R-009, R-014; §H action plan)
- [ ] `ARC-001-TCOP-v1.0.md` — TCoP review (especially Point 13 mapping table)
- [ ] `ARC-001-SBD-v1.0.md` — Secure by Design (CAF, threat model, Cloud Security Principles)
- [ ] `ARC-001-DPIA-v1.0.md` — DPIA (data inventory, AI processing, transfers)
- [ ] `ARC-001-AIP-v1.0.md` — AI Playbook compliance
- [ ] `ARC-000-PRIN-v2.0.md` — Architecture Principles (especially 1, 5, 7, 12, 16)
- [ ] `decisions/ARC-001-ADR-001-v1.0.md` through `008` — ADRs

**Optional supplementary**:

- [ ] Pen-test executive summary (when complete — Action 1)
- [ ] Manual WCAG 2.2 AA audit report (when complete — Action 2)
- [ ] Accessibility Statement URL (when published — Action 3)
- [ ] AT-user research findings (when complete — Action 4)
- [ ] Service-side OSS publication ADR + repository link (when complete — Action 5)
- [ ] Public status page URL (when live — Action 8)
- [ ] Performance dashboard sample (when live — Action 7)

### Who Should Attend

**Core Team** (required):

- ✅ **Service Owner** (Mark Craddock) — overall service vision and decision authority
- ✅ **Product Manager** — backlog, prioritisation, user-need delivery
- ✅ **Lead User Researcher** — user needs, research findings, AT testing (recruit / contract — Action 12)
- ✅ **Technical Architect / Lead Developer** — technology choices, ADRs, security design (recruit — Action 12)
- ✅ **Delivery Manager** — agile practices, team dynamics, on-call (recruit — Action 12)

**Phase-Specific Additions for Beta**:

- ✅ **Accessibility Lead / Specialist** — WCAG audit, AT testing, statement (recruit — Action 12)
- ✅ **Security Lead** — pen test, threat model, NCSC CAF, incident response (recruit — Action 12)
- ✅ **DPO** — DPIA, ICO posture, sub-processor chain (recruit — Action 12)
- ✅ **Content Designer** — onboarding flow, plain-language review (recruit — Action 12)

**Optional**:

- Senior Responsible Owner (Service Owner doubles as SRO in vendor context)
- CCS liaison (for G-Cloud questions)
- Pilot DDaT EA participant (if convenient — adds buyer-side credibility on Point 1)

### Show and Tell Structure (4-Hour Pre-Assessment Walkthrough)

**0:00–0:15 — Introductions and Context**:

- Team introductions (name, role, days/week, recent decision they made)
- Service overview: "We help UK SMEs produce credible architecture-governance evidence for UK Gov bids" (2 minutes)
- Project context: pre-GA Alpha-stage, targeting Beta-eligible state at GA – 30 days; this walkthrough = RISK §H Priority-1 action 5

**0:15–1:00 — User Research and Needs (Points 1, 2, 3, 4)**:

- User Researcher presents:
  - DDaT-role-anchored personas (`ARC-001-STKE-v1.0.md` SD-1..SD-14)
  - First-round pilot research findings (Action 10 output)
  - AT-user research findings (Action 4 output) — also flagged as Point 5 evidence
  - Goal G-1 / G-2 / G-6 KPI baselines

**1:00–1:45 — Service Demonstration (Points 2, 3, 4, 5)**:

- Live walk-through of UC-1 (sign-up) → UC-2 (AI-assisted artefact) → UC-3 (export)
- Screen-reader walk-through of UC-1 (Point 5 evidence)
- API + UI parity demo (Point 3 evidence — channel switching)

**1:45–2:30 — Technical Architecture and Security (Points 9, 11, 12, 13, 14)**:

- Lead Architect walks through:
  - C4 context + container diagrams (when generated — Action 25)
  - ADR-001 (Tenant Isolation Model)
  - ADR-004 (AI Provider Abstraction) + portability-rehearsal demo (Action 16)
  - ADR-006 (Deployment Topology)
  - ADR-007 (Data Portability)
  - Service-side OSS publication ADR (Action 5)
- Security Lead walks through:
  - SBD §1 NCSC CAF self-assessment baseline (Action when CAF baselined)
  - DPIA findings (data inventory, transfers, Article 22)
  - Pen-test executive summary (Action 1 output)
  - Incident-response runbook + ICO-72h template (Action 17 output)

**2:30–3:00 — Team and Ways of Working (Points 6, 7, 8, 10)**:

- Delivery Manager presents:
  - Team composition + RACI (`ARC-001-STKE-v1.0.md` internal stakeholders + STKE Governance section)
  - Sprint cadence and ceremonies (PLAN — Action 13)
  - One retrospective with "we changed X because Y"
  - Performance dashboard (Action 7) + status page (Action 8) + KPI matrix (Goal G-1..G-8)

**3:00–3:45 — Open Q&A**:

- Panel asks questions on any of the 14 points; team responds with artefact references
- Particular preparation for likely Red-rating drill-downs: Points 5, 9, 10, 12

**3:45–4:00 — Panel Deliberation and Format Feedback**:

- Walkthrough panel (1 Service Assessor + 1 pilot DDaT EA) shares format / coverage feedback
- Team captures feedback for action before formal Beta assessment

### Tips for Success

**Do**:

- ✅ Show the artefacts directly (the team builds with their own tooling — that *is* the demo)
- ✅ Have the people who did the work present it (not the Service Owner alone)
- ✅ Be honest about Red ratings — name them, name the action, name the date
- ✅ Reference ArcKit artefacts by ID (assessors will recognise this as good governance hygiene)
- ✅ Show the iteration story — eight ADRs, three security artefacts, one risk register with §H action plan

**Don't**:

- ❌ Hide the [PENDING] roles — be honest about what's filled and what's hiring
- ❌ Over-rely on the Service Owner — Beta panels want to hear from doers
- ❌ Use jargon ("DDaT" / "TCoP" / "NCSC CAF" — define on first use)
- ❌ Argue the Reds — accept and present the action plan
- ❌ Pretend live data exists — Alpha-stage means no live data; say so

**Materials to Have Ready**:

- Demo environment with test data loaded (UC-1 sign-up + UC-2 AI generation + UC-3 export)
- Backup screenshots / screen recordings if demo breaks
- Links to all artefacts above
- Pen-test executive summary (when complete)
- Manual WCAG audit report (when complete)
- Accessibility Statement URL (when published)
- Public status page URL (when live)

---

## After the Assessment

### If You Pass (Green / Beta-Ready)

**Immediate Actions**:

- [ ] Celebrate
- [ ] Share the assessment report with stakeholders + CCS liaison
- [ ] Book formal Beta GDS assessment (5+ weeks lead time)
- [ ] Land remaining critical actions before formal assessment
- [ ] Update `ARC-001-RISK-v1.0.md` R-009 residual to reflect new evidence

### If You Get Amber (Most Likely Outcome of First Walkthrough)

**Understanding Amber**:

- The walkthrough panel is informal; their finding is non-binding feedback
- Track each Amber concern in this report's checklist
- Address before booking formal Beta assessment

**Immediate Actions**:

- [ ] Capture each Amber finding from walkthrough notes
- [ ] Assign owner + deadline per finding
- [ ] Schedule a follow-up walkthrough at GA – 45 days if substantial change

### If You Fail (Red — Walkthrough Recommends Postponement)

**Understanding Red**:

- The walkthrough panel may recommend postponing the formal Beta assessment
- This is a feature, not a bug — better to delay 4 weeks than to fail formally and lose 3 months
- Update `ARC-001-RISK-v1.0.md` R-009 status (return to "Open" with delayed action 5)

**Immediate Actions**:

- [ ] Review walkthrough notes carefully with full team
- [ ] Identify root causes per Red point
- [ ] Build remediation plan with weekly cadence
- [ ] Re-run `/arckit:service-assessment` after 4 weeks to track progress
- [ ] Re-book walkthrough once root-cause Red ratings closed

---

## Next Steps

### This Week (to 2026-05-10)

1. Service Owner to recruit / contract User Researcher, Accessibility Lead, Security Lead, DPO, SRE Lead, Content Designer (Action 12).
2. Procure independent pen test (Action 1).
3. Procure manual WCAG 2.2 AA audit (Action 2).
4. Confirm pre-assessment walkthrough date (target: 2026-06-28 ≈ 8 weeks from now, i.e., GA – 60 days target per RISK §H).

### Next 2 Weeks (to 2026-05-17)

1. Stand up service-side OSS publication ADR + public repository skeleton (Action 5).
2. Publish privacy notice (Action 6).
3. Generate `ARC-001-PLAN-v1.0.md` (Action 13).
4. Generate `ARC-001-DIAG-001-v*.md` (Action 25) — C4 context + container.

### Next 4–6 Weeks (to 2026-06-14)

1. Pen test executes (Action 1).
2. Manual WCAG audit completes (Action 2).
3. AT-user research session (Action 4).
4. Pilot DDaT user research first round (Action 10).
5. Performance dashboard and public status page live (Actions 7 + 8).
6. Generate SOBC, DEVOPS, TRAC artefacts (Actions 14, 15, 26).

### Next 8 Weeks — Pre-Assessment Walkthrough (target: 2026-06-28)

1. Walkthrough with 1 Service Assessor + 1 pilot DDaT EA (RISK §H Priority-1 action 5).
2. Capture format / coverage feedback.
3. Decide whether to book formal Beta assessment (target: 2026-08-XX, GA – 30 days).

### Continuous Improvement

- [ ] Re-run `/arckit:service-assessment PHASE=beta` weekly to track readiness change
- [ ] Update this report as each checklist action lands
- [ ] Sprint planning includes Service Standard preparation tasks
- [ ] Share Amber / Red trend with steering group

---

## Resources

### GDS Service Standard Resources

**Official Guidance**:

- [Service Standard](https://www.gov.uk/service-manual/service-standard) — All 14 points
- [What happens at a service assessment](https://www.gov.uk/service-manual/service-assessments/how-service-assessments-work)
- [Book a service assessment](https://www.gov.uk/service-manual/service-assessments/book-a-service-assessment)
- [Service Standard Reports](https://www.gov.uk/service-standard-reports)

**Phase-Specific Guidance**:

- [Alpha phase](https://www.gov.uk/service-manual/agile-delivery/how-the-alpha-phase-works)
- [Beta phase](https://www.gov.uk/service-manual/agile-delivery/how-the-beta-phase-works)
- [Live phase](https://www.gov.uk/service-manual/agile-delivery/how-the-live-phase-works)

### Related ArcKit Commands

**Complementary analysis**:

- `/arckit:analyze` — Comprehensive governance quality analysis
- `/arckit:traceability` — Requirements traceability matrix (Action 26)
- `/arckit:tcop` — TCoP self-assessment (already complete: `ARC-001-TCOP-v1.0.md`)
- `/arckit:secure` — Secure by Design assessment (already complete: `ARC-001-SBD-v1.0.md`)
- `/arckit:dpia` — DPIA (already complete: `ARC-001-DPIA-v1.0.md`)
- `/arckit:ai-playbook` — AI Playbook compliance (already complete: `ARC-001-AIP-v1.0.md`)

**Generate missing evidence**:

- `/arckit:plan` — Project plan (Action 13)
- `/arckit:sobc` — Strategic Outline Business Case (Action 14)
- `/arckit:devops` — DevOps strategy (Action 15)
- `/arckit:diagram` — Architecture diagrams (Action 25)
- `/arckit:hld-review` / `/arckit:dld-review` — Design reviews (post-Beta)

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government policies referenced are public-domain and cited by name.

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

**Generated by**: ArcKit `/arckit:service-assessment` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**Model**: Claude Opus 4.7 (1M context)

**Next Actions**:

1. Review this report with Service Owner + Product Manager + Lead Architect (when filled).
2. Prioritise Critical Actions 1–9 in the next sprint planning.
3. Re-run `/arckit:service-assessment PHASE=beta` weekly to track progress.
4. Use the checklist (Actions 1–27) to track completion of preparation tasks.
5. Confirm pre-assessment walkthrough date with Service Assessor and pilot DDaT EA (RISK §H Priority-1 action 5; target GA – 60 days).

---

*Good luck with the pre-assessment walkthrough. Show the artefacts, name the gaps, and present the action plan with dates. Beta assessors want to see honest progress, not polished presentations.*
