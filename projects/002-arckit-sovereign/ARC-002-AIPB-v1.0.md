# UK Government AI Playbook Assessment: ArcKit as a Service (Sovereign Deployment)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:ai-playbook`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-002-AIPB-v1.0 |
| **Document Type** | UK Government AI Playbook Compliance Assessment |
| **Project** | ArcKit as a Service (Sovereign Deployment) (Project 002) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Cycle** | Per release; per sovereign customer accreditation event when AI is enabled |
| **Next Review Date** | 2026-06-02 |
| **Owner** | Mark Craddock (Service Owner) — joint with Vendor DPO and Lead Architect |
| **Reviewed By** | [PENDING] AI Ethics Reviewer, Vendor Security Lead, MOD Defence Digital liaison |
| **Approved By** | [PENDING] Service Owner |
| **Distribution** | Project Team, Architecture, Security, DPO, MOD Defence Digital liaison, NCSC liaison, pilot sovereign customer Accreditor / SIRO (when engaged) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:ai-playbook` command. Sovereign-deployment scope: AI is OPT-IN PER DEPLOYMENT (default `ai.provider = none`, fail-closed). Where enabled, inference runs against a customer-controlled on-premise endpoint per `ARC-002-ADR-004-v1.0` (TGI / vLLM / Triton / customer-internal). Vendor delivers no data, no model, no inference. Risk classification: LOW when AI enabled (drafting-only — same as SaaS); N/A when AI disabled. Inverts Principle 8 (commercial partnership) — customer owns the model, vendor does not. Theme 2 ATRS responsibility shifts: vendor publishes for the AIAdaptor abstraction; deploying authority publishes for its deployed instance. | [PENDING] | [PENDING] |

## Document Purpose

The UK Government AI Playbook compliance assessment for the AI feature surface of the **sovereign deployment** of ArcKit (Project 002). Three purposes:

1. **Self-assessment against the AI Playbook 10 Principles + 6 Ethical Themes** for the *abstraction* the vendor ships (the `AIAdaptor` interface and its sovereign provider profile, `customer-endpoint`).
2. **An evidence pack the deploying authority can inherit** when running its own `/arckit:ai-playbook` for its specific deployment instance — provenance schema, audit fields, and architectural controls are vendor-supplied; the customer adds its own model card, EqIA, and ATRS record on top.
3. **The artefact that gates AI scope evolution in sovereign mode** — any new AI feature beyond drafting (e.g., scoring, ranking, routing) triggers a refresh of this assessment, of `ARC-002-ADR-004-v1.0`, and of any deploying-authority assessments that depend on it.

This assessment is **scoped to the sovereign deployment route**. The managed SaaS AI assessment is `projects/001-arckit-saas/ARC-001-AIPB-v1.0.md`; the abstraction is shared, but sovereign and SaaS are accountable parties for different things — see §1.5 (Responsibility Matrix).

---

## Executive Summary

**Overall Compliance** (vendor scope, AIAdaptor abstraction): **126/160 (79%)** — **Good — Compliant with minor improvements needed**.

**Risk Assessment**:

- [ ] HIGH-RISK
- [ ] MEDIUM-RISK
- [x] **LOW-RISK** (when AI is enabled — drafting-only, human-in-the-loop architectural, identical use case to SaaS)
- [x] **N/A** (when AI is disabled — `ai.provider = none` default — many sovereign sites will never enable AI; this assessment then has no live obligations at the customer side)

**Status**: ⚠️ **PARTIALLY COMPLIANT (vendor scope) — pending three customer-side artefacts that are by design not in vendor scope (ATRS for the *deployed instance*, customer-side EqIA, customer-side accreditor sign-off when AI enabled).**

**Critical Issues**: 0 blocking issues at the vendor side. 3 customer-side conditions (each customer that enables AI must publish their own ATRS, run their own EqIA proportionate to use, and obtain accreditor sign-off — these are *customer* obligations; the vendor cannot complete them).

**Go/No-Go Decision**: [x] **APPROVED WITH CONDITIONS** for vendor-side bundling and shipment of the AI surface (subject to the customer-side conditions above for each deployment that turns AI on). [ ] APPROVED / [ ] REJECTED.

**Sovereign-specific framing**:

1. **AI is OPT-IN per deployment** — the default sovereign install ships with `ai.provider = none` (ADR-004 §5.1, FR-004 acceptance criterion). Many customers (especially those without an accredited on-prem model) will deploy ArcKit and never enable AI. For those deployments the AI Playbook obligations are **dormant** — manual authoring is fully functional (NFR-A-003).
2. **When enabled, inference happens entirely inside the customer-accredited boundary** — vendor never sees prompt content, never delivers the model, never delivers inference. The vendor's contribution is the `AIAdaptor` abstraction (reused unmodified from SaaS), the OpenAI-compatible wire contract, the install-time validator that refuses public-resolvable endpoints, the provenance schema, and the audit log shape (ADR-004 §5.1, §7.1).
3. **AI Playbook responsibility shifts at the boundary** — the **vendor** is accountable for the abstraction (this document); the **deploying authority** is accountable for its specific deployed instance (its own `/arckit:ai-playbook`, its own ATRS, its own EqIA, its own accreditor sign-off). This document carries the abstraction-level evidence; §1.5 names the responsibility split.
4. **Sovereign AI enables otherwise-excluded use cases** — MOD units, intelligence-community partners, accredited operators of essential services who could not lawfully use a public managed SaaS can now use AI-assisted artefact generation against their own approved model. This is a Theme 6 (Societal Wellbeing / Public Good) positive of the sovereign route specifically.

---

## 1. AI System Context

### 1.1 System Identification

- **System name**: ArcKit AI artefact-generation feature, sovereign provider profile (`customer-endpoint`).
- **AI type**: Generative (LLM-based) drafting assistant — *when enabled by the customer*.
- **Provider**: Customer-controlled on-premise model endpoint (per ADR-004) — typically HuggingFace Text Generation Inference (TGI), vLLM, NVIDIA Triton with the OpenAI-compatible front-end, or a customer-internal-hosted serving stack. Vendor does not deliver, host, or operate any model. Vendor does not deliver, host, or operate any inference engine. Vendor does not deliver weights.
- **Deployment context**: A feature within the sovereign-mode ArcKit installation. Disabled by default; activated only when the customer admin sets `ai.provider = customer-endpoint` and configures a private-network endpoint that passes the install-time validator.

### 1.2 Use Case

**Primary use case (when AI enabled)**: When a deploying-authority user (an architect or bid lead) creates an artefact (principles, requirements, ADR, diagram, etc.), they may optionally request an AI-generated draft using their existing project context as input. The model returns a draft. The user reviews, edits, and saves. The user is the artefact author; the AI is a drafting assistant. AI does **not**:

- Make decisions affecting the deploying authority, any data subject, or any other party.
- Score, rank, triage, or recommend among options or among individuals / cases / suppliers.
- Profile data subjects.
- Use customer data for model training (the customer hosts the model; no training in serving stacks like TGI / vLLM / Triton).
- Auto-publish or auto-save without human review.
- Send any data outside the customer's accredited boundary (the model endpoint is RFC1918 / customer-internal — install-time validator refuses public-resolvable hosts; CI network-deny test confirms no other outbound calls — ADR-004 §7.1).

**When AI disabled** (`ai.provider = none` — sovereign default): manual authoring is fully functional (NFR-A-003); UI badges AI features as `disabled`; the AI Playbook obligations on this deployment are dormant — there is no AI system in operation.

### 1.3 Users and Affected Population

- **Users (initiate AI)**: deploying-authority architects and bid leads — professional adults using a sovereign-deployed B2B platform in a work context.
- **Affected population**: same as the user — they are the artefact author and reviewer; the AI's output is theirs, edited by them, before any further use.
- **No third-party affected**: AI does not act on a citizen, customer, or applicant. It does not affect access to public services. (In MOD or intelligence-community use cases, the *artefacts* themselves may inform downstream operational decisions, but those decisions are made by humans through documented governance — not by the AI.)
- **Decision authority**: 100% with the human user. Zero AI autonomy.

### 1.4 Risk Classification (UK Gov AI Playbook)

**Classification**:

- **N/A** when AI is disabled (`ai.provider = none` default).
- **LOW-RISK** when AI is enabled, **for the use case scoped here (drafting-only, human-in-the-loop architectural)**.

Rationale (when enabled):

- ❌ Not high-risk: AI does not make automated decisions affecting health, fundamental rights, access to services, legal status, employment, or financial circumstances. The user is the author; the AI's output is a draft.
- ❌ Not medium-risk: AI does not perform semi-automated decisions; it does not allocate resources; it does not score or prioritise cases.
- ✅ Low-risk: AI is a productivity / drafting feature with full human control; document drafting is an explicit AI Playbook example of low-risk use.

**Threshold for upgrade**: any future feature that scores / ranks / recommends or is used to triage suppliers / artefacts / personnel re-classifies the AI use case to MEDIUM-RISK or higher and triggers a refresh of this document, of ADR-004, of any deploying-authority assessments, and of the customer-side ATRS record. This boundary is contractually preserved by the customer (they choose what to do with the model output) and architecturally preserved by the vendor (the `AIAdaptor` interface only exposes drafting endpoints).

**Sovereign-specific overlay**: even if the *use case* stays LOW-RISK, the *operating environment* in MOD or comparable accredited sites may impose stricter controls (e.g., SECRET classification ceiling, specific safety alignment requirements). Those are handled by the deploying authority's accreditation — not by re-classifying the AI Playbook risk tier. The classification of the *artefact content* is independent of the AI Playbook risk tier and is enforced separately by `ai.classification_max` (FR-012, ADR-004).

### 1.5 Responsibility Matrix — Vendor / Deploying Authority Split

> The defining sovereign-specific feature of this assessment. AI Playbook responsibilities split cleanly between the vendor (who ships the abstraction) and the deploying authority (who runs the instance). This table is the controlling reference for §2 (Principles) and §3 (Themes) — every "this is satisfied / not satisfied" call below is qualified by who owns it.

| AI Playbook obligation | Vendor (this document) | Deploying authority (per deployment, when AI enabled) |
|------------------------|------------------------|-------------------------------------------------------|
| Principle 1 — Understanding AI (abstraction limitations: hallucination, context, drafting-only) | ✅ Owns | ✅ Owns for chosen model + own user training |
| Principle 2 — Lawful and Ethical Use (UK GDPR, Equality Act, Data Ethics Framework) | ✅ Owns for the abstraction (no personal data leaves boundary by construction) | ✅ Owns for tenant content under their controllership (vendor is not a processor for tenant content in sovereign mode — ADR-004; DPIA-SOVEREIGN §3) |
| Principle 3 — Security (AI-specific threats: prompt injection, data poisoning, model theft) | ✅ Owns architecture-level controls (input validation hooks, output classification check, fail-closed default, network-deny CI test, install-time validator) | ✅ Owns runtime / model-level controls (red teaming on chosen model, weight integrity, internal network controls) |
| Principle 4 — Human Control | ✅ Owns architecturally (human-in-the-loop is enforced by the AIAdaptor — no auto-publish, no autonomous action) — **trivially satisfied** | ✅ Owns operationally (training users on AI limitations, override capability) |
| Principle 5 — Lifecycle Management | ✅ Owns abstraction lifecycle (LTS line, golden-prompt suite, supported-stack matrix) | ✅ Owns model lifecycle (selection, retraining, version tracking, retirement, decommissioning) |
| Principle 6 — Right Tool Selection | ✅ Owns ("AI as drafting assistant" was scoped through ADR-004; alternatives considered and documented) | ✅ Owns (the customer chose to enable AI on their deployment — that decision is theirs, made through their accreditation forum) |
| Principle 7 — Collaboration | ✅ Owns vendor-side (engagement with GDS, CDDO, NCSC, MOD Defence Digital liaison) | ✅ Owns deployment-side (sharing within their organisation; cross-government if appropriate) |
| Principle 8 — Commercial Partnership | **INVERTED** — vendor is *not* the AI supplier in sovereign mode; vendor is the *platform supplier*. The customer owns the AI model, not the vendor. The vendor's commercial commitments here are about the *abstraction*, not about the model. | ✅ Owns (the customer's commercial arrangement with their on-prem model supplier — if any — is between them) |
| Principle 9 — Skills | ✅ Owns vendor team skills (AI/ML literacy on engineering team, AI ethics reviewer engaged) | ✅ Owns deploying-authority team skills (their architects / bid leads need AI-literacy training; they own this) |
| Principle 10 — Organisational Alignment | ✅ Owns vendor-side governance (ARB, AI Ethics Reviewer) | ✅ Owns deploying-authority governance (their AI Governance Board if any, their SRO, their accreditation forum) |
| Theme 1 — Safety / Robustness | ✅ Owns abstraction-level (input validation, fail-closed, classification ceiling) | ✅ Owns model-level (safety alignment, red teaming) |
| Theme 2 — **Transparency / ATRS** — see §3.2 | ✅ Owns the ATRS *for the AIAdaptor abstraction* (this is published by the vendor as part of the bundle / vendor public ATRS hub) | ✅ Owns the ATRS *for the deployed instance* (each deploying authority that turns AI on publishes its own ATRS record per ATRS guidance — vendor cannot publish on their behalf because the model and use are theirs) |
| Theme 3 — Fairness / Bias | ✅ Owns abstraction-level (no triage / scoring / ranking; identity-blind drafting) | ✅ Owns model-level (the customer's chosen model may have biases the vendor cannot assess; customer accountable for their model) |
| Theme 4 — Accountability | ✅ Owns vendor accountability for the abstraction | ✅ Owns deploying-authority accountability for the deployed instance (their SRO, their incident response) |
| Theme 5 — Contestability | N/A at vendor level (no AI decisions to contest — drafting-only; user is the author) | ✅ Owns (the customer's internal complaints / appeals process if relevant — typically irrelevant for drafting-only) |
| Theme 6 — Societal Wellbeing | ✅ Owns the sovereign-availability narrative (this route enables MOD / regulated-OES use cases that the SaaS cannot reach) | ✅ Owns deployment-specific societal impact assessment if relevant |

---

## 2. Compliance Against the 10 Core Principles

> Scoring 0–10 per principle. LOW-RISK threshold: ≥ 60% overall, basic safeguards in place. Scores below evaluate the **vendor scope** (the AIAdaptor abstraction and the sovereign provider profile) — see §1.5 for vendor / deploying-authority split.

### Principle 1: Understanding AI — ✅ Compliant — Score 8/10

**Evidence**:

- `ARC-002-ADR-004-v1.0` documents AI provider selection rationale, alternatives considered (vendor-bundled model rejected; proprietary inference engine rejected; do-nothing rejected), and known limitations of LLMs (hallucination, context-window limits, model deprecation, quantisation cliff below Q4, parameter cliff below 8B).
- `ARC-002-RISK-v1.0.md` R-008 (On-premise AI model integration brittleness) explicitly addresses model-version churn, content-policy mismatch, and classification-marking errors at the model boundary.
- AI-content lineage metadata reused unchanged from SaaS — provenance schema (ADR-004 Appendix D) makes AI output always distinguishable from human content, with `model.deployment = "customer-endpoint"`.
- Minimum model spec documented (ADR-004 §5.1.1) — capability cliff acknowledged at parameter < 8B and quantisation < Q4; install-time warning and admin acknowledgement required if below spec.
- AI Ethics Reviewer engaged in the abstraction-level review (ADR-004 stakeholders).
- Hallucination risk explicitly carried into the sovereign mode and amplified into FR-004 acceptance criteria — every AI-generated artefact must be visibly badged in UI and machine-readable in provenance metadata.

**AI Limitations Documented** (vendor scope — abstraction):

| Limitation | Impact | Mitigation |
|------------|--------|------------|
| Hallucinations in LLM | May generate factually incorrect drafts | Human-as-author architecture (Principle 4); AI-content badging; provenance metadata; user trained that AI output is a *draft* |
| Below-minimum-spec model degrades | Artefact templates produce unusable output | Install-time warning; golden-prompt suite shipped in bundle for customer validation |
| Quantisation cliff (Q3 and below) | Capability collapses | Documented as unsupported; warning at install |
| Wire-format dialect drift across stacks (TGI / vLLM / Triton) | Adaptor breaks on stack version bump | Per-stack shim layer; supported-stack matrix; CI smoke tests |
| Customer-model retirement strands the deployment | AI features unavailable mid-LTS | Pluggable adaptor allows hot-swap of model; LTS does not pin a model |
| Hardware mis-sizing causes p95 latency blow-out | UX degrades | Sizing guidance in runbook; minimum model spec; UI progress indicator |

**Findings**: Vendor team has realistic expectations of LLM capabilities and of the heterogeneity of customer-accredited models. The ADR-004 minimum model spec and the golden-prompt regression suite are the load-bearing artefacts — they make "AI as drafting assistant" a falsifiable contract.

**Gaps**: Deploying-authority user training for AI literacy is the customer's obligation (see §1.5) — vendor cannot complete this; vendor ships an AI-literacy briefing template in the operator runbook (FR-011) as scaffolding.

---

### Principle 2: Lawful and Ethical Use — ✅ Compliant (vendor scope) — Score 8/10

**Evidence**:

- `ARC-002-DPIA-v1.0.md` (the sovereign DPIA — vendor-narrow scope) confirms that the **deploying authority is the data controller** for tenant content, that the vendor is a software supplier (not a processor) for that content, and that AI generation when enabled runs entirely inside the customer-accredited boundary. The vendor never sees prompt content (DPIA §1, §3).
- ICO 9-criteria screening (DPIA §1.1) returned 0/9 met for vendor-side processing — no DPIA strictly required at the vendor side; DPIA generated as a transparency artefact for accreditators and deploying-authority DPOs.
- UK GDPR Article 22: AI does **not** make solely-automated decisions of legal or significant effect — drafting-only by architecture (this document §1.2). At customer side, the customer's own DPIA evaluates Article 22 for their use; vendor architecture forecloses the harmful pattern.
- Equality Act 2010: AI feature is identity-blind; not used to select / rank / triage individuals; bias risk minimal in drafting-only mode (see Theme 3).
- Human Rights Act 1998: no AI decision-making affects rights; no surveillance / profiling.
- Data Ethics Framework: applied via Principles 5 (Security by Design — incl. MOD SbD), 7 (UK Sovereignty), 9 (Data Quality / Lineage / Portability), 21 (Sovereign and Air-Gapped Deployment) in `ARC-000-PRIN-v2.0.md`.
- MOD Secure by Design / JSP 440 / JSP 604 alignment at `ARC-002-SECD-MOD-v1.0.md` covers the AI surface explicitly as a discrete component.

**Legal and Ethical Checks** (vendor abstraction):

| Check | Status | Issues Found | Resolution |
|-------|--------|--------------|------------|
| DPIA (vendor-narrow) | ✅ | None — 0/9 ICO criteria met | Published as transparency artefact |
| DPIA (deploying-authority instance) | 🔄 | Customer-side obligation — vendor provides DPIA inputs (architecture diagrams, data-flow documentation, SBOMs, threat model) | Customer completes per their own accreditation timeline |
| EqIA — abstraction-level | ✅ | None — drafting-only is identity-blind | Inline analysis in Theme 3 |
| EqIA — deploying-authority instance | 🔄 | Customer-side obligation if their use materially affects protected characteristics | Customer completes proportionate to use |
| Human Rights — abstraction | ✅ | None — no decision-making | Inline analysis in this document |
| Human Rights — deploying-authority instance | 🔄 | Customer-side obligation in MOD / sensitive contexts | Customer's accreditor-led process |
| UK GDPR — vendor-narrow | ✅ | None — vendor is not a controller for tenant content | DPIA-SOVEREIGN §3 |
| UK GDPR — tenant content | 🔄 | Customer is controller | Customer's ROPA / DPIA |
| Equality Act — abstraction | ✅ | None — drafting-only | Inline analysis in Theme 3 |
| MOD SbD / JSP 440 | 🔄 | Per release evidence pack | `ARC-002-SECD-MOD-v1.0.md`; per-deployment authorisation by customer accreditor |
| NCSC CAF (non-MOD sites) | 🔄 | Per release CAF mapping | Per release; per deployment |

**Data Protection** (vendor-narrow scope):

- Legal basis for processing (vendor scope): **N/A for tenant content — vendor is not a controller in sovereign mode** (DPIA-SOVEREIGN §3). For vendor-narrow data (licence-management contacts, opt-in support records, opt-in engineering telemetry — default OFF), Article 6(1)(b) Performance of contract.
- Special category data: NO at vendor side — none ever leaves the deploying-authority boundary (DPIA-SOVEREIGN §1.1 #4).
- Data retention period: tenant content not held by vendor; customer manages retention inside their boundary.
- Right to object: N/A at vendor side; customer provides its own mechanism if required.

**Findings**: Lawful basis fully documented. The sovereign-specific point is that the *vendor's* AI Playbook lawful-use story is dramatically simpler than the SaaS equivalent because the vendor processes no personal data through the AI surface — by construction. The deploying authority's lawful-use story is what matters for the deployed instance, and the vendor scaffolds it (DPIA inputs, provenance schema, classification ceiling).

**Gaps**:

- Standalone Equality Impact Assessment (vendor side) not produced — for LOW-RISK B2B platform with identity-blind drafting this is proportionate; gap noted if AI feature scope ever expands.
- Standalone Human Rights Assessment (vendor side) not produced — same proportionality reasoning.
- MOD SbD evidence pack (`ARC-002-SECD-MOD-v1.0`) needs a dedicated AI-surface section — addressed in plan for §10.2 Phase 8 of ADR-004.

**Action**: No vendor-side blocking gaps. Customer-side obligations called out clearly so deploying authorities cannot inadvertently rely on the vendor for what only they can do.

---

### Principle 3: Security — ✅ Compliant — Score 9/10

**Evidence**:

- AI surface treated as a discrete component in `ARC-002-SECD-MOD-v1.0.md` (Secure by Design assessment for sovereign — MOD context).
- ADR-004 §5.1, §7.1, §8.1 enumerate the AI-specific security controls:
  - **Fail-closed default**: `ai.provider = none` — AI features are off until explicit configuration; deployments accredit with AI off then make a separate decision to enable.
  - **Install-time validator**: refuses public-resolvable hostnames; integration test against a known public hostname must reject; configuration linted.
  - **Network-deny CI test on AI flow**: outbound calls to anything other than the configured endpoint cause CI failure.
  - **Within-deployment isolation extended to AI**: prompt-context selection scoped to project / role / community-of-interest (FR-006, NFR-SEC-006); CI isolation tests cover the AI surface.
  - **Classification ceiling**: `ai.classification_max` enforced at adaptor entry; artefacts above ceiling rejected before reaching the model (FR-012); audit-logged.
  - **Auth options**: bearer / mTLS, with key material in customer KMS (INT-007).
  - **TLS to model endpoint via customer-controlled CA bundle** (INT-003).
  - **Audit logging** to customer-controlled destination (FR-010, INT-004): prompt-shape (template ID + variable schema), token counts, latency, model name, outcome — full prompt content NOT logged by default.
  - **Rate limiting**: `ai.max_concurrent_requests_per_user`, `ai.max_tokens_per_request`, `ai.timeout_ms`.
- **NCSC AI guidance** and **NCSC supply-chain security guidance** explicitly referenced in ADR-004 §9.5; supply-chain-integrity guidance for model weights shipped in operator runbook (informational — customer accountable).
- **Pen test** covers the AI surface in the sovereign profile, including install-time validator, audit logging, fail-closed behaviour (ADR-004 §8.1).
- **Risk register R-008** (AI integration brittleness, residual 8 Medium) and **R-007** (Accredited-boundary egress incident, residual 8 Medium) treat the AI surface security envelope.

**AI-Specific Security Threats**:

| Threat | Risk Level (sovereign) | Mitigation |
|--------|------------------------|------------|
| Prompt injection | LOW | Input validation hooks at adaptor entry; output classification check; user-as-author architecture means injected output never auto-acts; identity-blind drafting; no tool-use in adaptor surface |
| Data poisoning | LOW (vendor scope) | Vendor does not host the model; customer accountable for weight integrity (NCSC supply-chain guidance shipped in runbook); golden-prompt regression suite bundled for customer to run |
| Model theft | LOW (vendor scope) | Vendor does not hold the model; theft risk sits with the customer's serving stack — customer accreditation responsibility |
| Adversarial attacks | LOW | Drafting-only use case + human review; no decision automation to attack |
| Model inversion | LOW (vendor scope) | Vendor does not host; customer-side concern; advisory note in runbook |
| Public-endpoint mis-configuration (sovereign-specific) | LOW residual / CRITICAL impact | Install-time validator refuses public-resolvable hosts; CI network-deny test; admin UI displays endpoint and warns; configuration linted |
| Within-deployment isolation breach via shared prompt context | LOW residual / CRITICAL impact | Prompt-context selection scoped to project / role / community-of-interest; CI isolation tests; audit log per call |
| Classification breach via prompt content above ceiling (sovereign-specific) | LOW residual / CRITICAL impact | `ai.classification_max` ceiling enforced at adaptor entry; artefacts above ceiling rejected before model; audit-logged |

**Security Controls** (vendor scope, abstraction-level):

- [x] Input validation and sanitisation hooks at adaptor entry
- [x] Output classification check against `ai.classification_max`
- [x] Fail-closed default (`ai.provider = none`)
- [x] Install-time validator (no public-resolvable hostname allowed)
- [x] Network-deny CI test on AI flow
- [x] Rate limiting on adaptor (per user, per request, per timeout)
- [x] Access controls reused from non-AI ArcKit RBAC + community-of-interest scoping
- [x] Audit logging (customer-controlled destination — never to vendor)
- [x] Auth: bearer + mTLS via customer KMS
- [x] TLS via customer-controlled CA bundle
- [x] Provenance metadata on every output (machine-readable)
- [x] Per-stack shim layer with supported-stack smoke-test matrix (TGI / vLLM / Triton-OpenAI-front-end / customer-internal)
- [ ] Red teaming on the *abstraction* — proportionate red team test of the input-validation / output-classification path is **planned** for the alpha programme (carried as P2 action — not blocking for vendor sign-off, but should land before first customer go-live with AI on)
- [x] No outbound network calls beyond the configured endpoint (boundary protection, by construction)

**Findings**: AI-specific security envelope at the sovereign abstraction is *stronger* than the SaaS equivalent in important respects — fail-closed by default, install-time validator, network-deny test on the AI flow specifically, classification ceiling enforced before the model, and the vendor cannot exfiltrate prompt content because the vendor is not in the call path. The customer's accreditor will need their own evidence on the *model* and *serving stack* security envelope; that is structurally outside vendor scope.

**Gaps**: Red teaming of the abstraction path planned for the alpha programme (P2 — not blocking).

---

### Principle 4: Human Control — ✅ Compliant — Score 10/10 (architectural — *trivially satisfied*)

**Evidence**:

- The `AIAdaptor` interface only exposes drafting endpoints (ADR-004 §5.1; project-001 ADR-004). There is no auto-publish, auto-save, auto-submit, or auto-decide path. The user is the artefact author. The AI returns a draft; the user reviews, edits, and saves.
- Provenance metadata makes AI-generated content visibly badged in UI and machine-readable in storage (`model`, `version`, `timestamp`, `template_id`, `human_reviewer`, `approved_for_publication = false` until a human approves) — same schema as SaaS (ADR-004 Appendix D).
- AI output is **never** rendered as a system action — only as content the user can accept, edit, or discard.
- Override capability is the architectural default — the user can always discard the draft and write manually.
- Manual authoring (FR-008) works fully when AI is off and continues to work alongside AI when AI is on.
- Audit log records the human reviewer for every AI-generated artefact that is saved.
- For sovereign deployments specifically: even within MOD environments where operational decisions follow from the artefacts, the *artefacts* themselves are produced by the human author with optional AI drafting — there is no fully-automated defence-decision pathway by design.

**Human Oversight Model**:

- [x] **Human-in-the-loop**: Review EVERY AI draft before it becomes an artefact — required by architecture, not by policy.
- [ ] Human-on-the-loop (not applicable — there are no autonomous AI decisions to monitor; nothing AI-initiated reaches an artefact without explicit human accept).
- [ ] Human-in-command (subsumed — strict human-in-the-loop is stronger).
- [ ] Fully automated (forbidden by design and reaffirmed by the FR-004 acceptance criteria).

**Human Review Requirements**:

| Decision Type | Review Requirement | Reviewer Role | Escalation Path |
|---------------|-------------------|---------------|-----------------|
| Any AI-generated draft becoming an artefact | Every draft (architectural) | The user requesting the draft (architect / bid lead in deploying authority) | Customer's operator team / SRO |
| Bulk AI generation N/A | N/A — adaptor interface does not expose bulk generation that bypasses review | — | — |

**For High-Risk AI applications**: N/A — this is LOW-RISK by classification. But because Human Control is *architectural* rather than *procedural* in the AIAdaptor, the system would still satisfy human-in-the-loop requirements if the use case ever escalated to MEDIUM-RISK; any escalation beyond drafting (e.g., scoring) would require new endpoints which would re-trigger this assessment regardless.

**Findings**: Human Control is **trivially satisfied** in the sovereign sense — the design forecloses non-compliant patterns, so the principle is met as a property of the architecture rather than as a procedural commitment that could erode under operational pressure. This is the *strongest* form of compliance for this principle.

**Gaps**: None at vendor side. Customer-side training (users understand AI output is a draft, not an authoritative source) is the deploying authority's obligation; vendor ships an AI-literacy briefing template in the operator runbook.

---

### Principle 5: Lifecycle Management — ⚠️ Partial — Score 7/10

**Evidence**:

- ADR-004 §10 Implementation Plan covers selection (Phase 1: sovereign provider implementation), deployment (Phase 4: golden-prompt suite packaging), operations (Phase 7: operator runbook), and decommissioning (rollback plan §10.3).
- LTS line documented (BR-005) — sovereign customers can stay on a pinned LTS release for 24 months from each LTS release, with security patches.
- Supported-stack matrix refresh annually (TGI / vLLM / Triton); per-release smoke tests against pinned stack versions per LTS line.
- Golden-prompt regression suite shipped *with* the bundle so customers can validate their model on every release — explicit lifecycle artefact for the deploying authority.
- Per-release audit-log AI section: model name, latency, token counts, outcome (no full prompt content).
- Configuration surface (ADR-004 Appendix B) allows the customer to hot-swap model, retire model, or disable provider entirely without redeploying ArcKit.
- Decommissioning: at the abstraction level, `ai.provider = none` immediately disables AI; manual authoring continues; rollback plan §10.3 covers vendor-side hot-fix flow.

**Lifecycle Stages**:

**1. Selection and Procurement** (vendor abstraction):

- [x] Requirements defined (`ARC-002-REQ-v1.0.md` FR-004, FR-005, INT-005)
- [x] Build vs buy decision documented (ADR-004 — vendor builds the *abstraction*; customer chooses the *model*; serving stack reused from open-source)
- [x] Supplier evaluation completed for serving-stack selection (TGI / vLLM / Triton)
- [x] Contract terms with the customer cover the abstraction; customer's contract with their model supplier (if any) is between them — see Principle 8 inversion.

**2. Development and Testing** (vendor abstraction):

- [x] Training data — N/A (vendor does not train models)
- [x] Bias testing on the abstraction — drafting-only is identity-blind; no triage to test for bias
- [x] Performance benchmarks: minimum model spec (≥ 8B parameters, ≥ 32k context, ≤ Q4 quantisation, ≤ 60s p95 to first complete generation)
- [x] User acceptance testing — conducted at vendor side against representative open-weight model
- [x] Accessibility testing — abstraction inherits ArcKit accessibility envelope

**3. Deployment** (vendor abstraction → customer):

- [x] Phased rollout: alpha (first sovereign customer), beta, GA
- [x] Monitoring dashboards configured at customer-controlled destination (FR-010, INT-004)
- [x] Alert thresholds: customer-defined; vendor ships defaults in runbook
- [x] Incident response: rollback plan in ADR-004 §10.3

**4. Operation and Maintenance**:

- [x] Performance monitoring — at customer-controlled destination
- [ ] **Model drift detection** — at the *abstraction* level there is no drift to detect (the adaptor does not maintain a model); at the *model* level this is the customer's obligation. Vendor provides golden-prompt regression suite for periodic re-run; customer-side process to schedule it is operator-runbook-recommended (not vendor-enforced) — gap.
- [x] Retraining schedule — N/A at vendor; customer's call
- [x] User feedback collection — via customer's normal support channels
- [x] Per-release supported-stack smoke tests + golden-prompt re-run

**5. Decommissioning**:

- [x] Disable AI: `ai.provider = none` — immediate effect, no redeploy
- [x] Decommission deployment: standard sovereign uninstall procedure (BR-002 — operable-without-vendor)
- [x] Data deletion — customer-side (vendor never held it)
- [x] Lessons learned: feedback into next LTS line via supported-stack matrix refresh

**Model Monitoring Metrics** (customer-controlled destination — sovereign):

| Metric | Baseline | Threshold | Owner |
|--------|----------|-----------|-------|
| AI generation latency p95 | per minimum model spec | ≤ 60 s | Customer Operator Team |
| AI error rate | per release smoke test | ≤ 1% per template | Customer Operator Team |
| Above-classification-ceiling rejections | 0 expected | any non-zero is an audit event | Customer Security |
| Public-resolvable-endpoint validator triggers | 0 expected | any non-zero is an audit event | Customer Operator Team |
| Fail-closed activations (`ai_disabled` 403) | varies | usage analytics | Customer Operator Team |

**Findings**: Lifecycle management at the abstraction is solid — golden-prompt suite, supported-stack matrix, fail-closed default, hot-swap of model. The abstraction does not have a "model" to manage, so most lifecycle questions cleanly delegate to the customer.

**Gaps**:

- **Model drift detection** is a customer-side obligation that the vendor *cannot perform*. Vendor ships the golden-prompt suite as scaffolding, but operator runbook recommends — does not enforce — a periodic re-run cadence. Risk of customer-side neglect noted; mitigated by R-008 control "AI integration test harness per approved provider".
- Customer-side decommissioning notice to users (e.g., "AI is being switched off in this deployment") is a customer-runbook responsibility — vendor scaffolds with admin UI affordance.

**Action**: P2 — Tighten operator runbook to explicitly schedule golden-prompt re-runs per LTS release; add a "drift-watch" event in the audit log for customer-side dashboards.

---

### Principle 6: Right Tool Selection — ✅ Compliant — Score 9/10

**Evidence**:

- ADR-004 §5 enumerates 5 considered options with explicit pros/cons:
  - Option 1 (chosen): same `AIAdaptor`, OpenAI-compatible wire contract, customer-controlled endpoint, fail-closed default, minimum model spec, provenance parity with SaaS.
  - Option 2: ship no AI in sovereign — rejected (conflicts with BR-001, FR-004, Principle 21; pressure for fork).
  - Option 3: vendor-bundled open-weight model inside sovereign bundle — rejected (bundle size; vendor accountability for model accreditation; customer model approval policies vary; LTS pinning of model burdensome).
  - Option 4: build a proprietary on-prem inference stack — rejected outright (Principle 16 — reuse over build).
  - Option 5: do nothing — rejected (Conflict C-4 unresolved; per-customer fork pressure).
- Cost-benefit analysis (ADR-004 §5.1 Cost Analysis) covers vendor CAPEX (≈ 4 weeks engineering for sovereign provider implementation), vendor OPEX (per-stack regression maintenance), customer CAPEX (inference hardware), customer OPEX (inference power, LTS patching).
- AI is genuinely value-adding when enabled (artefact drafting at speed); AI is **not** required (manual authoring fully functional — NFR-A-003); the customer makes their own enable/disable call.
- Success metrics are defined at the abstraction level (provider-call-site lint at 0; AI calls reaching public internet at 0; sovereign deployments shipped with `ai.provider = none` by default at 100%; supported open-weight serving-stack matrix ≥ 3 at GA).
- Pilot/proof-of-concept: alpha sovereign customer engagement is the validation gate (ADR-004 §11.1 — initial review).

**Alternatives Considered** (already assessed in ADR-004):

| Solution | Pros | Cons | Why Not Chosen |
|----------|------|------|----------------|
| Manual authoring only (no AI) | Smallest attack surface, no model accreditation | Conflicts with BR-001, FR-004, Principle 21 — feature gap with SaaS | Rejected — fork pressure |
| Vendor-bundled model | Vendor regression evidence applies directly | Bundle size; vendor accountability; LTS pinning | Rejected — vendor cannot accredit models on customer behalf |
| Proprietary on-prem inference engine | Maximum vendor control | Conflicts with Principle 16 (reuse); not in team's wheelhouse | Rejected outright |
| Pluggable to customer-controlled endpoint (chosen) | Single codebase; no outbound calls; customer-chosen and customer-accredited model; AI Playbook portability | De facto wire-format standard; customer hardware variability | **Chosen** — Option 1 in ADR-004 |

**Use Case Appropriateness** (sovereign):

- [x] Problem is well-suited to AI (artefact drafting from existing project context — large surface area, repetitive structure, high cognitive load reduction)
- [x] Sufficient quality training data — N/A at vendor (customer's chosen model has its own training data; vendor does not curate)
- [x] Success can be measured — provenance metadata + golden-prompt suite enable objective measurement
- [x] Acceptable trade-offs — explainability traded for fluency, mitigated by provenance metadata + human review
- [x] NOT using AI just because trendy — the alternative (manual authoring) is fully supported and many sovereign deployments will use only that

**Inappropriate Use Cases (foreclosed by design)**:

- [x] No fully automated decisions on life-changing matters (architecture forbids decision endpoints)
- [x] No high-stakes decisions (drafting-only)
- [x] No 100%-accuracy use cases (drafting tolerates hallucination because the human reviews)
- [x] Simpler solutions are adequate where they suffice — manual authoring always available

**Success Metrics** (vendor scope — abstraction):

| Metric | Baseline | Target | Status |
|--------|----------|--------|--------|
| Provider-specific call sites in app code | 0 | 0 (lint-enforced) | ✅ |
| AI calls reaching public internet from sovereign deployment | 0 | 0 (network-deny CI test) | ✅ |
| Sovereign deployments shipped with `ai.provider = none` default | 100% | 100% | ✅ |
| Generation events with provenance metadata when AI on | 100% | 100% | ✅ |
| AI calls without project / role / community scope check | 0 | 0 | ✅ |
| Install-time refusal of public-resolvable endpoints | 100% | 100% | ✅ |
| Supported open-weight serving-stack matrix at GA | ≥ 3 | ≥ 3 | ✅ |
| Golden-prompt regression suite shipped in bundle | yes | yes | ✅ |

**Findings**: Right-tool decision is the strongest part of the assessment — every alternative was considered and documented in ADR-004 with a clear rationale. The decision is not "AI is great" — the decision is "where AI helps and the customer agrees, here is the safest possible way to do it; otherwise manual authoring works fine."

**Gaps**: None significant. P3 — capture customer-side success metrics (artefact authoring time saved, draft acceptance rate) once a deploying authority enables AI; vendor cannot collect these; deploying-authority feedback channel is the input.

---

### Principle 7: Collaboration — ⚠️ Partial — Score 7/10

**Evidence**:

- Cross-government collaboration (vendor side):
  - **MOD Defence Digital liaison** in ADR-004 stakeholders (consulted) — AI surface specifically called out in liaison engagement.
  - **NCSC liaison** consulted on supply-chain security guidance for model artefacts.
  - **GDS / CDDO** engagement at the platform level (`ARC-002-REQ-v1.0.md` distribution list).
  - **AI Standards Hub** — engagement planned but not yet executed (gap).
- Open-source ecosystem reuse: TGI (HuggingFace), vLLM, NVIDIA Triton — vendor does not fork or re-implement; customer benefits from community support of serving stacks.
- OpenAI-compatible wire contract aligns with the de facto open standard for chat completions (Principle 4 — Open standards in `ARC-000-PRIN-v2.0.md`).
- Knowledge-sharing: the AIAdaptor abstraction is shared between project 001 (SaaS) and project 002 (sovereign); the same `/arckit:ai-playbook` and `/arckit:atrs` commands work in both modes — the *deploying authority* can run them.
- Pilot sovereign customer engagement (ADR-004 §11.1) — accreditator-in-the-loop alpha programme is the primary collaboration channel for the AI surface (R-001 mitigation).

**Collaboration Activities**:

| Stakeholder | Engagement Type | Purpose | Outcome |
|-------------|-----------------|---------|---------|
| MOD Defence Digital | Liaison consultation (ADR-004) | Guidance on model approval routes within MOD | ADR-004 stakeholders list — pending PENDING confirmation |
| NCSC | Liaison consultation (ADR-004) | Supply-chain security guidance for model artefacts | Informational guidance shipped in operator runbook — pending |
| GDS | Cross-government channel (project distribution) | Platform-level engagement | Aligned with TCoP and Service Standard |
| CDDO | Cross-government channel | Cross-gov AI playbook signal | Engaged at platform level |
| AI Standards Hub | Planned engagement | Cross-gov AI assurance practice | **Gap** — to be initiated |
| Pilot sovereign customer Accreditor | Alpha engagement | Accreditation feasibility at AI surface | Pending — R-001 mitigation |
| Pilot sovereign customer SIRO | Alpha engagement | Information risk acceptance for AI on/off | Pending |
| HuggingFace TGI / vLLM / Triton communities | Open-source ecosystem | Wire-format compatibility, supported-stack matrix maintenance | Indirect via release notes / issues |

**Knowledge Sharing**:

- [x] AIAdaptor abstraction shared with project 001 (cross-project knowledge transfer within vendor)
- [x] Provenance schema documented for customer-side reuse (ADR-004 Appendix D)
- [x] Operator runbook AI section is a customer-facing knowledge artefact
- [ ] Cross-government forum presentation on the sovereign AI architecture — **gap** (planned post-alpha)
- [ ] Public case study (where appropriate) — **gap** (planned post-GA)

**Findings**: Vendor-side collaboration with MOD Defence Digital and NCSC is set up; the pilot-customer alpha programme is the primary live channel. The AI Standards Hub engagement is the most material gap.

**Gaps**:

- AI Standards Hub formal engagement not yet initiated.
- Cross-government forum presentation pending.

**Action**: P2 — initiate AI Standards Hub engagement before GA; commit to a cross-gov forum presentation within 6 months of GA.

---

### Principle 8: Commercial Partnership — ✅ Compliant — Score 9/10 (**INVERTED — vendor is not the AI supplier**)

**Sovereign-specific framing — the inversion**:

> In the SaaS, the vendor procures AI capacity from a third-party provider (OpenAI / Anthropic / etc. via the AIAdaptor) on behalf of tenants. The vendor's AI Playbook Principle 8 obligations there are about *that procurement* — performance SLAs, audit rights, data rights, exit clauses.
>
> In **sovereign mode the relationship is inverted**: the **customer** procures and operates the model; the **vendor** ships the abstraction. The vendor is no longer the AI supplier — the vendor is the *platform supplier into which the customer's AI feeds*. The vendor's Principle 8 obligations here are therefore about the *abstraction contract* (what the customer can rely on the AIAdaptor to do) and about *not interfering with the customer's commercial relationship with their model* (whatever that is — open-weight self-hosted, internal-only inference, or a customer-side commercial arrangement is between them).
>
> This is a *cleaner* commercial position for the customer than the SaaS — the customer fully controls their AI supply chain.

**Evidence (vendor-as-platform-supplier commitments)**:

- The customer's contract with the vendor for the sovereign deployment includes:
  - **Performance metrics on the abstraction**: install-time validator accuracy, fail-closed default, supported-stack matrix at GA ≥ 3, golden-prompt suite shipped with bundle. *No* SLA on AI generation latency, accuracy, or quality (those are properties of the customer's model on the customer's hardware — not vendor responsibility — ADR-004 §7.2).
  - **Explainability of the abstraction**: ADR-004 is publicly documented; provenance schema is publicly documented; the customer can inspect and reason about every artefact attached to the AI flow.
  - **Audit rights**: the customer can audit the vendor's AI surface code at any time (open-source, vendor's own audit logs accessible to vendor's auditors; the *customer's* audit log is in the customer's environment — vendor-side audit log access is for vendor incidents only).
  - **Data rights**: the customer owns their tenant content, prompts, outputs, and audit logs. The vendor never holds any of these in sovereign mode.
  - **Exit strategy**: standard sovereign uninstall (BR-002) — set `ai.provider = none`, then run uninstall; the model and serving stack are the customer's, untouched.
  - **Liability**: vendor liable for the abstraction (e.g., a defect in the install-time validator that lets a public hostname through); the customer is liable for their model's outputs (e.g., a hallucination from the customer's model — vendor is not in the loop).
  - **Security**: NCSC supply-chain guidance for the bundle; HSM-backed signing of releases (mitigates R-004).
- Vendor commits **not to** mandate a specific model, charge per-call AI fees, or take a margin on the customer's inference costs (sovereign commercial model is a flat sovereign licence; AI on/off is *commercially neutral* at the vendor side).
- Vendor does **not** require the customer to share prompt content, audit logs, or model details with the vendor — by construction.

**Contract Requirements for AI** (sovereign-specific):

| Requirement | In contract? | Sovereign verification method |
|-------------|--------------|------------------------------|
| Performance metrics on the abstraction | ✅ Yes | Install-time validator + golden-prompt suite shipped with bundle |
| Explainability of the abstraction | ✅ Yes | Public ADR-004 + provenance schema |
| Bias audits — abstraction-level | ✅ Yes (drafting-only is identity-blind) | Inline analysis in this document Theme 3 |
| Bias audits — model-level | ❌ Not in vendor contract — **customer obligation** | Customer's accreditation forum |
| Retraining — model | ❌ Not in vendor contract — **customer obligation** | Customer's model lifecycle |
| Data rights | ✅ Yes — customer owns all of it | Vendor never holds tenant content |
| Audit rights | ✅ Yes | Customer's own audit log; vendor source code auditable |
| Security — bundle | ✅ Yes | HSM signing; SBOM; supply-chain guidance |
| Security — model and serving stack | ❌ Not in vendor contract — **customer obligation** | Customer accreditation |
| Liability — abstraction defect | ✅ Yes — vendor liable | Standard contract liability clauses |
| Liability — model output | ❌ Not in vendor contract — **customer obligation** | Customer accountability for model selection |
| Exit | ✅ Yes — `ai.provider = none` + standard uninstall | BR-002, ADR-004 §10.3 |
| Pricing — flat sovereign licence; no per-call AI fees | ✅ Yes | Commercial model in SOBC |

**Vendor (as platform supplier) responsible-AI commitments**:

| Commitment | Contractual? | Verification |
|------------|--------------|--------------|
| AIAdaptor will not exfiltrate prompt content | ✅ | Network-deny CI test; pen test |
| Fail-closed default ships in every release | ✅ | CI test; release validation |
| Provenance metadata on every AI output | ✅ | CI test; audit-log spec |
| Within-deployment isolation extended to AI | ✅ | CI isolation tests |
| Classification ceiling enforced before model | ✅ | Adaptor-entry check; CI test |
| Supported-stack matrix maintained per LTS line | ✅ | Per-release matrix refresh |

**Findings**: Principle 8 is satisfied through *inversion* — the vendor is not the AI supplier, so the standard SaaS Principle 8 worries (vendor lock-in to AI provider, vendor data flowing to AI provider, vendor-side AI cost pressure) do not apply. The vendor's commitments are about the *platform abstraction*, and they are tighter than typical SaaS commitments because they are architectural rather than procedural.

**Gaps**: Customer-side procurement (when the customer procures their model commercially) is between the customer and their model supplier; vendor cannot complete it; vendor scaffolds with NCSC supply-chain guidance and the operator runbook supply-chain-integrity note.

---

### Principle 9: Skills and Expertise — ✅ Compliant — Score 8/10

**Evidence (vendor team — for the abstraction)**:

- AI/ML technical expertise: present on the engineering team (ADR-004 stakeholders include Lead Architect — accountable for AI integration).
- Data science / ML literacy: minimum model spec drafting, golden-prompt suite design require this — present.
- Ethics: AI Ethics Reviewer engaged in ADR-004 (consulted) — provenance schema parity check; further engagement at alpha gate.
- Domain expertise: Service Owner + Lead Architect have deep ArcKit / artefact-template knowledge; this is what makes "drafting" an appropriate scoping.
- User research: AI surface user research conducted at vendor side against representative model; deploying-authority user research is the customer's obligation.
- Legal / compliance: vendor DPO engaged on DPIA (sovereign); MOD Defence Digital liaison provides the cross-domain legal/compliance lens.
- Cyber security: Vendor Security Lead engaged on AI surface as discrete component in MOD SbD assessment.

**Team Composition** (vendor, abstraction):

| Role | Filled? | Scope |
|------|---------|-------|
| AI/ML Specialist (Lead Architect carries this) | ✅ | Abstraction design, minimum model spec, supported-stack matrix |
| Ethics Advisor | ✅ (consulted) | ADR-004 + Theme 3 inline analysis |
| Domain Expert | ✅ (Service Owner + Lead Architect) | Artefact templates suitability |
| User Researcher | ⚠️ Gap (vendor scope) — customer's obligation in deployment | Vendor side: representative testing only |
| Legal / DPO | ✅ | Vendor-narrow DPIA; AI Playbook |
| Security Specialist | ✅ | MOD SbD AI section; pen test |
| Product Manager (sovereign track) | ✅ (per project 002 stakeholder list) | LTS line; sovereign commercial model |
| MOD Defence Digital liaison | ✅ Consulted | Cross-domain legal/compliance |

**Training Provided** (vendor team):

- [x] AI fundamentals — engineering team
- [x] Ethical AI considerations — at AI Ethics Reviewer touchpoints
- [x] Bias recognition (relevant to drafting)
- [x] AI system limitations — minimum model spec, hallucination, dialect drift
- [x] Incident response for AI failures — runbook + ADR-004 §10.3 rollback

**Findings**: Vendor team has the skills required for the abstraction. The deploying authority's team needs AI literacy for their use of the deployed instance — this is the customer's obligation, scaffolded by the AI-literacy briefing template in the operator runbook (FR-011).

**Gaps**:

- Vendor-side user research is representative only; deployment-specific user research is the customer's.
- Standalone certified AI ethics qualification on vendor team — gap; mitigated by AI Ethics Reviewer engagement at gates.

**Action**: P3 — formalise AI Ethics Reviewer engagement schedule (per release, per alpha gate, per scope-expansion trigger).

---

### Principle 10: Organizational Alignment — ✅ Compliant — Score 8/10

**Evidence (vendor)**:

- ArcKit Architecture Review Board (ARB) approval pathway documented for ADR-004; same ARB has approved the AIAdaptor abstraction in project 001.
- AI strategy alignment: the dual-deployment model in `ARC-000-PRIN-v2.0.md` (Principle 21) is the strategic anchor; this assessment evidences that the sovereign route honours Principle 21's "AI / model dependencies are pluggable; sovereign mode supports approved on-premise model endpoints" mandate.
- Senior Responsible Owner (vendor): Mark Craddock (Service Owner) — same SRO as project 001.
- Risk management: `ARC-002-RISK-v1.0.md` R-008 (AI integration brittleness, residual 8 Medium — exceeds technology appetite ≤ 6 by 2 points; treated). R-007 (egress incident) and R-002 (MOD SbD fail) also touch the AI surface.
- Assurance: Vendor Security Lead engaged; AI Ethics Reviewer engaged.
- Governance forum: ArcKit ARB + AI Ethics review at vendor side; customer accreditation forum (per deployment) for go-live with AI on (ADR-004 §2.4).

**Governance Structure**:

- **AI Governance Board**: ArcKit ARB (vendor side) — for the abstraction. Customer-side governance is *the customer's accreditation forum* and possibly their own AI Governance Board.
- **Senior Responsible Owner**: Mark Craddock (Service Owner) — vendor side. Customer SRO is the deploying authority's own SRO (per ADR-004 §2.4).
- **Product Owner**: Service Owner + Product Manager (sovereign track).
- **Assurance Lead**: Vendor Security Lead (vendor side) + customer Accreditor (per deployment).

**Governance Checkpoints**:

| Phase | Review Required (vendor side) | Status | Notes |
|-------|-------------------------------|--------|-------|
| ADR-004 approval | ARB + AI Ethics Reviewer | ⏳ Pending | ADR is DRAFT — alpha gate target |
| Pre-alpha AI surface review | ARB + Vendor Security Lead | ⏳ Pending | Before first sovereign customer enables AI |
| Per-release AI surface re-review | ARB on triggered events (ADR-004 §11.2) | 🔄 Standing | Wire-format drift, AI Playbook update, EU AI Act, parent ADR change |
| Per-deployment customer-side approval | Customer accreditation forum | ⏳ Pending per customer | Vendor cannot conduct on customer's behalf |

**Organizational AI Principles**:

- [x] Aligns with ArcKit principles (PRIN v2.0 — Principles 4, 5, 7, 8, 16, 21)
- [x] Aligns with cross-government AI principles (UK AI Playbook 10 + 6 — this document)
- [x] No conflicts with organisational values

**Findings**: Vendor-side governance is in place at the abstraction level, with a clear cross-over point to customer-side governance per deployment. The dual SRO model (vendor SRO for the abstraction; customer SRO for the deployed instance) is the right pattern for sovereign delivery.

**Gaps**: Customer-side AI Governance Board may not exist at smaller deploying authorities; mitigated by the runbook decision template for the accreditator (ADR-004 §10.2 Phase 7).

**Action**: P3 — refresh runbook decision template for accreditator-without-AI-board so smaller deploying authorities have a tractable approval path.

---

## 3. Six Ethical Themes Assessment

> Scoring 0–10 per theme. Same vendor-scope qualifier as §2.

### Theme 1: Safety, Security, and Robustness — ✅ Compliant — Score 9/10

**Evidence**:

- Safety: drafting-only architecture forecloses harmful-output autonomy at the abstraction level (Principle 4); content-classification ceiling enforced at adaptor entry rejects above-ceiling artefacts; output classification check in audit log.
- Security: Principle 3 controls (fail-closed default; install-time validator; network-deny CI test; within-deployment isolation; classification ceiling; bearer / mTLS auth via customer KMS; TLS via customer-controlled CA bundle; audit logging to customer-controlled destination).
- Robustness: minimum model spec; supported-stack matrix; per-stack shim layer; per-release smoke tests; golden-prompt regression suite shipped in bundle.
- Fail-safe mechanisms: `ai.provider = none` immediately disables AI without redeploy; manual authoring continues; install-time refusal to start when `ai.endpoint.url` resolves publicly; classification-ceiling rejection at adaptor entry.
- Incident response plan tested: rollback plan in ADR-004 §10.3 covers vendor hot-fix flow and customer-side config flip.

**Safety Measures**:

| Risk | Safeguard | Testing | Status |
|------|-----------|---------|--------|
| Harmful content from customer model | Drafting-only + human review + provenance metadata + classification ceiling | Pen test on AI surface; CI tests | ✅ |
| Above-classification-ceiling content | `ai.classification_max` rejection at adaptor entry | CI test against above-ceiling artefacts | ✅ |
| Public-endpoint mis-configuration | Install-time validator; CI network-deny test | Integration test against known public hostname | ✅ |
| Within-deployment isolation breach via prompt | Project / role / community scope check on prompt context | CI isolation tests | ✅ |
| Wire-format drift breaks adaptor | Per-stack shim; supported-stack matrix; per-release smoke tests | CI matrix | ✅ |
| System failures | Graceful degradation: AI off → manual authoring works | Disconnected-mode CI test | ✅ |

**Findings**: Sovereign safety/security envelope is *stronger* than the SaaS equivalent on the load-bearing controls — fail-closed default, network-deny test on AI flow, no vendor-side prompt visibility, classification ceiling enforced before the model. Customer-side controls (model safety alignment, weight integrity, internal network controls) are out of vendor scope by design.

**Gaps**: Red teaming of the abstraction path planned for alpha (P2 — not blocking).

---

### Theme 2: Transparency and Explainability — ⚠️ **Partial — Score 7/10 — *responsibility shifts at sovereign boundary***

**Sovereign-specific framing — the ATRS shift**:

> In the SaaS the vendor publishes one ATRS record covering the whole AI feature surface (one model, one provider, one deployment context). In **sovereign mode** the AIAdaptor is the same abstraction, but the **model**, the **provider**, the **deployment context**, the **affected population**, and the **decision authority** are all *the deploying authority's*. ATRS responsibility therefore splits in two:
>
> - **Vendor publishes an ATRS record for the AIAdaptor abstraction** (the platform-level transparency record covering: the abstraction's purpose, the drafting-only scope, the human-in-the-loop architecture, the fail-closed default, the provenance metadata schema, the supported-stack matrix). This record is general — it applies to every deployment that uses the abstraction.
> - **Each deploying authority that turns AI on publishes its own ATRS record** for the *deployed instance* — naming their model, their hardware, their use case, their decision authority, their affected users. The vendor cannot publish on their behalf because the model, the use, and the population are theirs.
>
> A deploying authority that *does not enable AI* (`ai.provider = none`) has no ATRS record to publish — the AI Playbook obligations on their deployment are dormant.

**Evidence**:

- ADR-004 publicly documented (the abstraction-level transparency artefact).
- Provenance metadata schema documented (ADR-004 Appendix D) — every AI output carries `model.deployment = "customer-endpoint"`, `model.name`, `model.version`, `template_id`, `human_reviewer`, `approved_for_publication`.
- AI-content lineage badging in UI — every AI-generated artefact visibly distinguishable.
- This document (ARC-002-AIPB-v1.0) is the AI Playbook abstraction-level transparency artefact for sovereign mode.
- Operator runbook (FR-011) includes a "publish your ATRS" walkthrough for the deploying authority — scaffolded by the same `/arckit:atrs` command at the customer's end.
- `/arckit:atrs` command in the ArcKit toolkit produces a deployment-specific ATRS record using the provenance schema as input — same template both vendor and customer can run.

**ATRS Compliance** (vendor scope — abstraction):

- **ATRS URL** (vendor abstraction): [PENDING — to be published on the vendor's public hub before GA]
- **Publication date**: [PENDING — alpha gate target]
- **Last updated**: N/A
- **Scope of vendor ATRS**: the AIAdaptor abstraction, *not* any specific deployment.

**ATRS Compliance** (deploying authority scope — per deployment, when AI enabled):

- **Customer's obligation**: each deploying authority that turns AI on must publish its own ATRS record on its own organisational publication route (gov.uk for central government departments; departmental publication for ALBs; customer-specific publication for MOD).
- **Vendor scaffolding**: `/arckit:atrs` command with the provenance schema and adaptor-level facts pre-populated; runbook walkthrough.

**Explainability Level**:

- [x] **Partial explainability** — at the abstraction level: the user can see what model produced the draft (provenance metadata), what template was used, what context was attached. The model itself is a black box (LLM); the abstraction wrapping it is fully transparent.
- For the customer's instance, explainability depends on the chosen model; vendor cannot guarantee.

**Public Communication** (vendor side):

- [x] Public ADR-004 informs technically literate readers
- [x] Public provenance schema
- [ ] Public ATRS record on vendor hub — **gap** (planned)
- [ ] Plain-language statement for non-technical readers — **gap** (planned at GA)

**Public Communication** (customer side, per deployment):

- Customer obligation: their privacy notice must include AI use; their ATRS record must be published; their internal users must be told AI is being used.

**Findings**: Transparency *for the abstraction* is well-served — public ADR-004, public provenance schema, and the AI-literacy briefing template in the operator runbook. **Transparency *for the deployed instance* is the deploying authority's obligation** — the vendor cannot complete it; the vendor scaffolds it. This is a *clean* split, but two artefacts need to land before GA: vendor-side public ATRS record on the abstraction; vendor-side plain-language transparency statement.

**Gaps**:

- Vendor-side public ATRS record on the abstraction not yet published — **P1, planned before GA**.
- Plain-language transparency statement for non-technical readers not yet drafted — **P2**.
- Customer-side ATRS publication is a per-deployment obligation; vendor cannot complete; vendor scaffolds via `/arckit:atrs` template.

**Action**: P1 — Publish the vendor-side ATRS record on the abstraction before GA (Service Owner accountable; Vendor DPO consulted). P2 — Plain-language statement for non-technical readers.

---

### Theme 3: Fairness, Bias, and Discrimination — ✅ Compliant (vendor scope, abstraction) — Score 7/10

**Sovereign-specific framing**:

> Bias at the *abstraction* is what the vendor can assess. Bias at the *model* is what the customer can assess on their chosen model. The vendor's posture is:
>
> - The abstraction is identity-blind — the AIAdaptor does not score, rank, triage, or recommend among individuals or groups; it drafts content from project context.
> - The drafting use case is identity-blind in a substantively meaningful way — there is no protected-characteristic input feature; outputs are reviewed by the human author before any further use; the AI is not in the path of any decision affecting people.
> - The customer's chosen model may carry biases from its training data; vendor cannot assess those without knowing the model. Vendor scaffolds with a "model card walkthrough" advisory in the operator runbook — the customer should review the model card before enabling.

**Evidence**:

- Drafting-only use case = no demographic-impact pathway at the abstraction level.
- Human-in-the-loop review = bias in a draft is caught and corrected by the human author before the artefact is published.
- Identity-blind input = prompts are derived from project context (principles, requirements, ADR text), not from personal data of individuals.
- Equality Act 2010 inline assessment: the AI feature does not select / rank / triage / decide for individuals. It does not allocate access to services or resources. It does not employ protected-characteristic features.
- Public Sector Equality Duty: in MOD / sensitive-site use, the AI's role is content drafting for governance artefacts, not for personnel or operational decisions. The deploying authority's wider PSED compliance is its own obligation — vendor scaffolds with `/arckit:atrs` (which captures equality information) and the operator runbook EqIA template.

**Fairness Testing** (abstraction-level, drafting-only):

| Protected Characteristic | Metric | Sovereign abstraction | Note |
|-------------------------|--------|----------------------|------|
| Gender | Demographic parity | N/A — no triage / scoring | Drafting-only is identity-blind |
| Ethnicity | Equal opportunity | N/A — no triage / scoring | Drafting-only is identity-blind |
| Age | Equalised odds | N/A — no triage / scoring | Drafting-only is identity-blind |
| Disability | Calibration | N/A — accessibility envelope is the relevant lens | Inherits ArcKit accessibility envelope (Principle 12) |
| Religion / belief | — | N/A | Identity-blind |
| Sexual orientation | — | N/A | Identity-blind |
| Pregnancy / maternity | — | N/A | Identity-blind |

**Bias Mitigation** (vendor scope):

- [x] Use case scoping forecloses bias-affecting pathways (no triage)
- [x] Provenance metadata makes AI output traceable and auditable
- [x] Human-as-author architecture catches biased drafts before publication
- [x] Customer-side mitigation scaffolded: model-card walkthrough in operator runbook; advisory note that the customer should review their model's known biases before enabling

**Findings**: Bias risk at the vendor abstraction is **minimal by design** — drafting-only is identity-blind. The customer's chosen model may carry training-data biases; that is the customer's obligation, with vendor scaffolding. Score 7 (not 9–10) reflects honest acknowledgement that *somebody* (the customer) needs to do model-card due diligence and the vendor cannot do it.

**Gaps**:

- Customer-side model-card walkthrough in operator runbook needs to be tightened with a checklist (P3).
- Drift in customer-model behaviour over time (e.g., customer applies their own fine-tuning) is the customer's problem; vendor cannot detect.

**Action**: P3 — Tighten model-card walkthrough checklist in operator runbook for the deploying authority.

---

### Theme 4: Accountability and Responsibility — ✅ Compliant — Score 8/10

**Evidence**:

- **Vendor accountability for the abstraction**:
  - Service Owner (Mark Craddock) — overall vendor accountability
  - Lead Architect — AI surface technical accountability (ADR-004 stakeholders)
  - Vendor DPO — data-protection / DPIA accountability (sovereign scope)
  - Vendor Security Lead — AI surface security accountability
  - AI Ethics Reviewer — abstraction-level ethics accountability
- **Deploying-authority accountability for the deployed instance**:
  - Customer SRO — strategic oversight of the customer's AI use
  - Customer Accreditor — issues authorisation to operate
  - Customer SIRO — information-risk acceptance for AI on/off
  - Customer Operator Team — day-to-day operation
  - Customer's own DPO — data-protection / DPIA for tenant content
- **Audit trail**: every AI call to the customer-controlled audit destination with prompt-shape, token counts, latency, model, outcome (FR-010, INT-004). Vendor-side audit trail is irrelevant for tenant content because the vendor never sees it.
- **Incident response**: ADR-004 §10.3 rollback plan covers vendor hot-fix flow; customer Operator Team executes local config flip (`ai.provider = none`).
- **Decision-making process**: ADR-004 §6 Y-statement documents the abstraction-level decision; per-deployment AI-on/off decision is the customer's accreditation forum (ADR-004 §2.4).

**Accountability Structure**:

- **Senior Responsible Owner (vendor)**: Mark Craddock — Strategic oversight at vendor side
- **Senior Responsible Owner (deploying authority)**: Customer SRO — Strategic oversight at deployment side (per ADR-004 §2.4)
- **Product Owner**: Service Owner + Product Manager (sovereign track)
- **Technical Lead**: Lead Architect — vendor side; Customer Operator Team — customer side
- **Ethics Lead**: AI Ethics Reviewer — vendor side; customer's own ethics function — customer side

**Incident Response**:

- [x] Process for reporting AI errors — vendor-side via standard support; customer-side via internal incident management
- [x] Root cause analysis procedure — vendor-side standard; customer-side per their accreditation
- [x] Corrective action tracking — vendor LTS patch flow; customer hot-fix
- [x] Learning and improvement loop — supported-stack matrix refresh; lessons learned shared across LTS lines

**Findings**: Accountability is clearly partitioned. The vendor SRO is accountable for the abstraction; the customer SRO is accountable for the deployed instance. This is a strong sovereign-specific accountability story — neither party can hide behind the other.

**Gaps**: Customer SRO accountability template (a standard form the deploying authority can use to document their accountability when AI is on) — gap; mitigated by the operator runbook decision template.

**Action**: P3 — Customer SRO accountability template tightened in operator runbook.

---

### Theme 5: Contestability and Redress — ⚠️ N/A at abstraction — Score 6/10 (proportionate)

**Sovereign-specific framing**:

> Contestability applies when an AI decision affects a person who can contest it. In the AIAdaptor abstraction there is **no AI decision** — the AI produces a draft, the human accepts/edits/rejects. The human decision is contestable through the customer's normal governance routes (employment grievances, ALB complaints, etc.), but the AI is not in the contested loop. Score 6 (not 10) reflects proportionate handling — there is little to contest, but the customer should still ensure their internal users know how to flag concerns about AI drafts.

**Evidence**:

- Use case is drafting-only — no AI decisions to contest.
- Right to contest a *draft* is the user's freedom to discard or edit it — built into the architecture (Principle 4).
- Right to contest the *customer's decision* (e.g., a strategic decision documented in an AI-drafted artefact) follows the customer's normal contestability routes — this is *not* an AI Playbook obligation per se because the AI was not the decider.
- Where AI hallucination materially affects an artefact, the human author is responsible for catching it before publication; if missed, the customer's internal review chain catches it; if still missed, the artefact's normal correction process applies.
- For UK GDPR Article 22 explicit assessment: AI does NOT make solely-automated decisions of legal or significant effect (this document §1.2; DPIA §3) — Article 22 contestability does not apply by construction.
- For sovereign-specific MOD use: operational decisions follow from the artefacts via documented MOD governance — those decisions are contestable through the relevant MOD process, not through the vendor's AI surface.

**Contestability Process** (proportionate):

| Path | Owner | Mechanism |
|------|-------|-----------|
| Concern about an AI-generated draft | Deploying-authority user | Discard / edit / re-prompt — built into UI |
| Concern that a customer's published artefact is wrong | Deploying authority's normal artefact review chain | Customer's internal governance |
| Concern about AI feature being enabled at all | Customer SRO / Accreditor / SIRO | Customer's accreditation forum (ADR-004 §2.4) — `ai.provider = none` flips it off |
| Article 22 automated-decision concern | N/A | No automated decisions in scope |

**Testing**:

- [x] Architecture forecloses Article 22 patterns
- [x] User can override draft trivially (architectural)
- [ ] Customer-side process tested with deploying-authority users — customer obligation; vendor cannot test

**Findings**: Contestability obligations at the vendor abstraction are *minimal* because there are no AI decisions to contest. Vendor scaffolds the customer's responsibilities (their internal users' concerns, their accreditation-forum decision to enable/disable AI) but cannot complete them.

**Gaps**: None at vendor side beyond the proportionate scoring. Customer-side process is the customer's.

---

### Theme 6: Societal Wellbeing and Public Good — ✅ Compliant — Score 9/10 (**sovereign route enables otherwise-excluded use cases**)

**Sovereign-specific framing**:

> The sovereign route is itself a Public Good intervention. The managed SaaS cannot reach MOD, intelligence-community partners, or accredited operators of essential services — these populations operate inside accredited boundaries with no internet egress. Without the sovereign route they would either:
>
> 1. Not adopt ArcKit at all (loss of governance consistency that the platform exists to deliver), or
> 2. Adopt fragmented in-house alternatives (duplicate effort, divergent standards).
>
> Sovereign mode unlocks use of the AI-assisted artefact-generation feature for these populations on the customer's own approved model — they get the productivity benefit of AI drafting without compromising sovereignty, classification handling, or accreditation. This is a Theme 6 positive *of the sovereign route specifically*.

**Evidence**:

- Sovereign route addresses MOD and comparable sensitive sites that the SaaS cannot reach (`ARC-002-REQ-v1.0.md` §Business Context).
- Sovereign-specific commercial model contributes margin to the SME tier of the SaaS (BR-006 — cross-subsidy) — Public Good benefit also flows back to the SaaS' SME-affordability commitment.
- Environmental impact considered: customer uses their own hardware; vendor does not pay carbon cost; minimum model spec recommends ≥ 8B parameter open-weight models which are *much* less carbon-intensive than frontier proprietary models (Q4 quantisation reduces inference cost; SSE streaming reduces wasted generation).
- Accessibility: ArcKit accessibility envelope (Principle 12 in PRIN v2.0) inherited; AI feature does not create new accessibility barriers (drafting is a productivity feature, not a service-access feature).
- Benefits distributed fairly: AI is opt-in per deployment; customers without an approved model can still use ArcKit; the AI feature does not become a wedge that excludes customers.
- Maintains human dignity and autonomy: drafting-only architecture keeps humans as authors; AI does not replace professional judgement.
- Strengthens democratic values: open-source serving stacks (TGI, vLLM, Triton); OpenAI-compatible wire format (de facto open); public ADR-004; publishable provenance schema; publishable ATRS records — *sovereign* AI is more transparent than typical proprietary AI in important respects.

**Societal Impact**:

| Impact | Positive/Negative | Magnitude | Mitigation/Enhancement |
|--------|-------------------|-----------|------------------------|
| MOD / sensitive-site populations gain access to AI-assisted artefact generation that the SaaS cannot reach | **Positive** | High | This is the strategic point of the sovereign route |
| Cross-subsidy to SME tier of SaaS (BR-006) | **Positive** | Medium | Sovereign margin contributes to SME affordability |
| Customer hardware energy cost (inference) | Negative | Low to Medium per deployment | Minimum model spec recommends Q4-quantised ≥ 8B open-weight models — much lower cost than frontier proprietary; customer chooses |
| Customer model-weight integrity supply chain risk | Negative | Low residual | NCSC supply-chain guidance shipped; HSM-backed bundle signing; customer-side audit |
| Customer team learning curve on serving stacks | Negative | Low | Open-source TGI / vLLM / Triton have community support; runbook scaffolding |
| Customer with no approved model gets no AI capability | Negative | Low | By design — manual authoring fully functional (NFR-A-003); AI is opt-in |
| Open standards (OpenAI-compatible wire) reinforces government's open-standards commitment | Positive | Medium | Principle 4 honoured; alternative serving stacks remain hot-swappable |
| Sovereign route normalises customer-controlled AI in regulated public sector | Positive | High (long-term) | Demonstrates that AI can be deployed at OFFICIAL-SENSITIVE+ without vendor lock-in |

**Public Good**:

- [x] Solves real problem for citizens (indirectly — better-governed public-sector architecture means better-delivered public services)
- [x] Accessible to all customer populations (MOD, intelligence community, OES, sensitive civilian sites — *otherwise excluded*)
- [x] Maintains human dignity and autonomy (drafting-only)
- [x] Strengthens democratic values (open standards; public ADR; transparent provenance)

**Findings**: Sovereign route is the *strongest* Public Good story in the AIP — it delivers AI-assisted productivity to populations that the SaaS cannot reach, at no compromise on sovereignty, classification handling, or accreditation, and on open-source / open-standard infrastructure that reinforces public-sector technology principles. Score 9 (not 10) reflects honest acknowledgement that the customer hardware energy cost and the customer-side learning curve are real (if proportionate) negatives.

**Gaps**: None significant.

---

## 4. Overall Assessment Summary

### Compliance Scorecard

| Assessment Area | Score /10 | Status |
|-----------------|-----------|--------|
| **10 Core Principles** | | |
| 1. Understanding AI | 8 | ✅ |
| 2. Lawful and Ethical Use | 8 | ✅ |
| 3. Security | 9 | ✅ |
| 4. Human Control | 10 | ✅ (architectural — trivially satisfied) |
| 5. Lifecycle Management | 7 | ⚠️ (customer-side drift detection) |
| 6. Right Tool Selection | 9 | ✅ |
| 7. Collaboration | 7 | ⚠️ (AI Standards Hub gap) |
| 8. Commercial Partnership | 9 | ✅ (**inverted — customer owns the model**) |
| 9. Skills and Expertise | 8 | ✅ |
| 10. Organizational Alignment | 8 | ✅ |
| **Principles Subtotal** | **83/100** | |
| | | |
| **6 Ethical Themes** | | |
| 1. Safety, Security, Robustness | 9 | ✅ |
| 2. Transparency, Explainability | 7 | ⚠️ (vendor ATRS publication gap; **ATRS responsibility shifts** to deploying authority for deployed instance) |
| 3. Fairness, Bias, Discrimination | 7 | ✅ |
| 4. Accountability, Responsibility | 8 | ✅ |
| 5. Contestability, Redress | 6 | ⚠️ (proportionate — no AI decisions to contest at abstraction) |
| 6. Societal Wellbeing, Public Good | 9 | ✅ (**sovereign route enables otherwise-excluded use cases**) |
| **Ethics Subtotal** | **46/60** | |
| | | |
| **TOTAL SCORE** | **129/160** | |

**Percentage Score**: **81%**

### Compliance Levels

- **90-100%** (144-160 points): Excellent
- **75-89%** (120-143 points): **Good — Compliant with minor improvements needed** ← **129/160 = 81% sits here**
- **60-74%** (96-119 points): Adequate
- **< 60%** (< 96 points): Poor

### Risk-Based Decision

**For LOW-RISK AI** (drafting-only, human-in-the-loop architectural — when AI is enabled):

- [x] SHOULD score ≥ 60% to proceed — **achieved at 81%**
- [x] Basic safeguards in place — fail-closed default; install-time validator; network-deny CI test; classification ceiling; provenance metadata; within-deployment isolation
- [x] Periodic review (per release for the abstraction; per accreditation event for each deployment)

**For deployments where AI remains disabled** (`ai.provider = none`):

- AI Playbook obligations are dormant on those deployments. The customer should still be aware of the obligations *if they later choose to enable AI*; vendor scaffolds with the operator runbook decision template.

### Critical Issues (Blocking)

**Vendor side**: None — the abstraction is shippable.

**Customer side (each deployment that turns AI on)**:

1. Customer must publish their own ATRS record for the deployed instance — vendor cannot complete (Theme 2).
2. Customer must conduct an EqIA proportionate to use — vendor cannot complete (Theme 3).
3. Customer must obtain accreditor sign-off for AI on (ADR-004 §2.4) — vendor cannot complete.

These are not vendor-blocking; they are customer-side conditions clearly delineated in §1.5 Responsibility Matrix.

### Recommendations

#### High Priority (P1 — before vendor GA)

1. **Publish vendor-side ATRS record on the AIAdaptor abstraction** on the public ATRS hub (Service Owner accountable; Vendor DPO consulted). Theme 2.
2. **Initiate accreditator-in-the-loop alpha programme** (mitigates R-001, R-002, R-013 simultaneously per RISK §Recommendations) — primary collaboration channel for the AI surface.

#### Medium Priority (P2 — within 3 months of GA)

1. **Red team test of the abstraction's input-validation / output-classification path** — Vendor Security Lead. Principle 3.
2. **Plain-language transparency statement** for non-technical readers — covering what the AIAdaptor does and does not do. Theme 2.
3. **AI Standards Hub formal engagement** — Service Owner + Lead Architect. Principle 7.
4. **Operator runbook tightening**: golden-prompt re-run schedule per LTS release; "drift-watch" event in audit log for customer dashboards. Principle 5.
5. **MOD SbD evidence pack AI-surface section** — Vendor Security Lead, in `ARC-002-SECD-MOD-v1.0`. Principle 2.

#### Low Priority (P3 — continuous improvement)

1. **Cross-government forum presentation on sovereign AI architecture** within 6 months of GA. Principle 7.
2. **Customer SRO accountability template** tightened in operator runbook. Theme 4.
3. **Customer-side model-card walkthrough checklist** tightened in operator runbook. Theme 3.
4. **AI Ethics Reviewer engagement schedule** formalised (per release, per alpha gate, per scope-expansion trigger). Principle 9.
5. **Customer-side AI Governance Board template** for smaller deploying authorities without an existing AI Governance Board. Principle 10.

---

## 5. Action Plan

| Action | Principle/Theme | Owner | Due Date | Status |
|--------|----------------|-------|----------|--------|
| Publish vendor ATRS record on AIAdaptor abstraction | Theme 2 | Service Owner | Before GA | ⏳ |
| Accreditator-in-the-loop alpha programme | Principles 7, 10 | Sovereign Delivery Lead | Alpha | ⏳ |
| Red team abstraction input-validation / output-classification path | Principle 3 | Vendor Security Lead | Within 3 months of GA | ⏳ |
| Plain-language transparency statement | Theme 2 | Service Owner + Vendor DPO | Within 3 months of GA | ⏳ |
| AI Standards Hub formal engagement | Principle 7 | Service Owner | Before GA | ⏳ |
| Operator runbook tightening (drift-watch, model-card checklist, customer SRO template) | Principles 5, 10; Themes 3, 4 | Documentation Lead | Within 3 months of GA | ⏳ |
| MOD SbD AI-surface section in `ARC-002-SECD-MOD-v1.0` | Principle 2 | Vendor Security Lead | Per release | 🔄 |
| Cross-government forum presentation | Principle 7 | Service Owner | Within 6 months of GA | ⏳ |
| AI Ethics Reviewer engagement schedule formalised | Principle 9 | Service Owner | Before GA | ⏳ |

---

## 6. Mandatory Documentation

### Required Assessments (vendor scope, abstraction)

- [x] **AI Playbook self-assessment** (this document)
- [ ] **ATRS — abstraction-level**: PENDING vendor publication (P1)
- [x] **DPIA — vendor-narrow**: `ARC-002-DPIA-v1.0.md`
- [x] **EqIA — abstraction-level**: inline in §3 Theme 3 (proportionate; standalone gap noted)
- [x] **Human Rights — abstraction-level**: inline in §2 Principle 2 (proportionate)
- [x] **Security Risk Assessment — AI surface**: `ARC-002-SECD-MOD-v1.0.md` (AI section pending tightening — P2); RISK R-007, R-008
- [x] **Bias Audit — abstraction-level**: inline in §3 Theme 3 (drafting-only is identity-blind)
- [x] **User Research Report — vendor-side representative testing**: at vendor; deploying-authority instance is customer's

### Required Assessments (deploying authority — per deployment, when AI enabled)

The following are NOT vendor obligations and CANNOT be completed by the vendor — the deploying authority must complete them per deployment:

- [ ] **Deploying-authority DPIA** (controllership for tenant content sits with customer)
- [ ] **Deploying-authority ATRS** (for the deployed instance, naming the customer's model, hardware, use case, decision authority, affected users)
- [ ] **Deploying-authority EqIA** (proportionate to actual use)
- [ ] **Deploying-authority Human Rights Assessment** (where relevant in MOD / sensitive context)
- [ ] **Deploying-authority security accreditation** (MOD SbD authorisation to operate; NCSC CAF for non-MOD)
- [ ] **Deploying-authority AI feature on/off decision** (accreditation forum)

Vendor scaffolds via: operator runbook decision template; `/arckit:atrs` and `/arckit:ai-playbook` and `/arckit:dpia` toolkit commands the customer can run; provenance schema; audit log fields.

### Governance Approvals

- [ ] ArcKit ARB approval (vendor side): [PENDING]
- [ ] AI Ethics Reviewer sign-off (vendor side): [PENDING]
- [ ] Service Owner (SRO) sign-off (vendor side): [PENDING]
- [ ] Vendor Security Lead review: [PENDING]
- [ ] Vendor DPO review: [PENDING]
- [ ] Customer Accreditor sign-off (per deployment, when AI enabled): [PENDING per customer]
- [ ] Customer SRO sign-off (per deployment, when AI enabled): [PENDING per customer]
- [ ] Customer SIRO sign-off (per deployment, when AI enabled): [PENDING per customer]

---

## 7. Go/No-Go Decision

**Decision**: [x] **APPROVED WITH CONDITIONS** for vendor-side bundling and shipment of the AI surface.

**Vendor-side conditions for full approval (P1 — before GA)**:

1. Publish ATRS record on the AIAdaptor abstraction.
2. Confirm accreditator-in-the-loop alpha programme initiation.
3. AI Standards Hub formal engagement opened.

**Customer-side conditions** (each deployment that turns AI on must complete before flipping `ai.provider = customer-endpoint`):

1. Deploying-authority ATRS record published.
2. Deploying-authority EqIA proportionate to use completed.
3. Customer Accreditor + SRO + SIRO sign-off captured (per ADR-004 §2.4).

**Deployment Approval (vendor abstraction)**: [x] Yes (with conditions above)

**Deployment Approval (per customer instance with AI on)**: per-deployment — vendor cannot pre-grant.

**Ongoing Monitoring Required**:

- [x] Per-release AI-surface re-review (vendor side)
- [x] Per-customer accreditation event (when AI enabled)
- [x] Annual review of minimum model spec against open-weight model state-of-the-art
- [x] Triggered re-review on: project 001 ADR-004 changes; serving-stack major version with wire-format change; AI Playbook update; EU AI Act guidance update relevant to UK extra-territorial reach; customer-reported AI-surface defect

---

## 8. External References

> No external documents at time of generation. Public-domain UK Government, MOD, and NCSC policies are cited by name.

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

### Internal Cross-References (within this project — sovereign deployment)

- `ARC-000-PRIN-v2.0.md` — Principles 4 (Open standards), 5 (Security by design — incl. MOD SbD), 7 (UK sovereignty), 8 (Within-deployment isolation), 16 (Reuse / open source), 21 (Sovereign and Air-Gapped Deployment — anchor)
- `ARC-002-REQ-v1.0.md` — BR-001/002/003/004/005, FR-004 (primary — pluggable AI), FR-005, FR-006, FR-008, FR-010, FR-011, FR-012, FR-014, INT-003, INT-004, INT-005, INT-007, NFR-A-003, NFR-P-002, NFR-SEC-003/004/005/006, NFR-I-001
- `ARC-002-RISK-v1.0.md` — R-007 (egress), R-008 (AI integration brittleness), R-002 (MOD SbD fail), R-004 (signed-bundle compromise)
- `ARC-002-DPIA-v1.0.md` — vendor-narrow scope; deploying authority is the data controller for tenant content; no vendor data flow through AI surface
- `ARC-002-ADR-004-v1.0.md` — On-premise AI model integration (sovereign mode); the architectural source of truth for this assessment
- `ARC-002-SECD-MOD-v1.0.md` — MOD Secure by Design assessment; AI surface treated as discrete component (P2 tightening recommended)
- `ARC-002-TCOP-v1.0.md` — TCoP review; Point 13 (AI ethics) aligns with this document

### Cross-Project References

- `projects/001-arckit-saas/ARC-001-AIPB-v1.0.md` — SaaS AI Playbook assessment. **Different scope** (SaaS-specific deployment context); the AIAdaptor abstraction is shared, but this sovereign assessment is the *vendor-narrow* counterpart for the sovereign route.
- `projects/001-arckit-saas/decisions/ARC-001-ADR-004-v1.0.md` — Parent ADR. Defines the AIAdaptor interface and provenance schema reused unchanged by sovereign mode.

### Public Sources Cited By Name

- UK Government AI Playbook — https://www.gov.uk/government/publications/ai-playbook-for-the-uk-government
- Algorithmic Transparency Recording Standard (ATRS) — https://www.gov.uk/government/collections/algorithmic-transparency-recording-standard-hub
- Data Ethics Framework — https://www.gov.uk/government/publications/data-ethics-framework
- ICO AI guidance — https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/
- NCSC AI guidance — https://www.ncsc.gov.uk/collection/ai-and-cyber-security
- NCSC supply-chain security guidance — https://www.ncsc.gov.uk/collection/supply-chain-security
- HMG Government Security Classifications Policy — https://www.gov.uk/government/publications/government-security-classifications
- MOD Secure by Design (assess via `/arckit:mod-secure`)
- HuggingFace Text Generation Inference — https://huggingface.co/docs/text-generation-inference
- vLLM — https://docs.vllm.ai/
- NVIDIA Triton — https://github.com/triton-inference-server/server

---

## Sign-Off

**Assessed By**: ArcKit AI (`/arckit:ai-playbook`)
**Date**: 2026-05-03

**Service Owner / SRO (vendor)**:
Name: Mark Craddock
Date: ________________
Signature: ________________

**Lead Architect (vendor)**:
Name: [PENDING]
Date: ________________
Signature: ________________

**Vendor Security Lead**:
Name: [PENDING]
Date: ________________
Signature: ________________

**AI Ethics Reviewer (vendor)**:
Name: [PENDING]
Date: ________________
Signature: ________________

**ArcKit ARB**:
Forum: ARB
Date: ________________
Signature: ________________

**Customer Accreditor (per deployment, when AI enabled)**:
Per deployment — recorded in customer's accreditation forum minutes.

**Customer SRO (per deployment, when AI enabled)**:
Per deployment — recorded in customer's accreditation forum minutes.

---

## Review Schedule

**Next Review**: 2026-06-02 (or earlier on triggered events).

**Review Frequency**:

- [x] Per release (abstraction-level review)
- [x] Per customer accreditation event (when AI enabled)
- [x] Annually (minimum model spec, supported-stack matrix)
- [x] Triggered (AI Playbook update; EU AI Act update; serving-stack wire-format change; project 001 ADR-004 change; customer-reported defect)

---

**Template Version**: 1.0
**Last Updated**: 2026-05-03
**Source**: https://www.gov.uk/government/publications/ai-playbook-for-the-uk-government

---

**Generated by**: ArcKit `/arckit:ai-playbook` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Sovereign Deployment) (Project 002)
**AI Model**: claude-opus-4-7
**Generation Context**: Inputs: PRIN v2.0 (Principles 4, 5, 7, 8, 16, 21 — sovereign anchor); ARC-002-REQ-v1.0 (BR-001/002/003/004/005, FR-004 primary, FR-005/006/008/010/011/012/014, INT-003/004/005/007, NFR-P-002/A-003/SEC-003/004/005/006/I-001, UC-1/2, Conflict C-4); ARC-002-RISK-v1.0 (R-007 egress, R-008 AI integration brittleness, R-002 MOD SbD, R-004 supply-chain); ARC-002-DPIA-v1.0 (vendor-narrow scope confirms 0/9 ICO criteria, no vendor data flow through AI surface); ARC-002-ADR-004-v1.0 (architectural source of truth — AIAdaptor reuse, customer-endpoint provider profile, OpenAI-compatible wire contract, fail-closed default, minimum model spec, network-deny CI test, classification ceiling); ARC-002-SECD-MOD-v1.0 (security framing). Reference (NOT copied): ARC-001-AIPB-v1.0 (SaaS-side AIP — distinct scope). User input: ai-mode = opt-in-per-deployment-on-premise (override of default auto-detect-from-REQ-FRs because sovereign-specific). Risk classification: LOW (when AI enabled — drafting-only) / N/A (when AI disabled — many sovereign sites). Sovereign-specific framings: Principle 4 trivially satisfied (architectural human-in-the-loop); Principle 8 INVERTED (customer owns the model, not vendor); Theme 2 ATRS responsibility shifts (vendor publishes for the AIAdaptor abstraction; deploying authority publishes for the deployed instance); Theme 6 sovereign route enables MOD/regulated-OES use cases otherwise excluded.
