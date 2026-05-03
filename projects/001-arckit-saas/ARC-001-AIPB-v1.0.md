# UK Government AI Playbook Assessment: ArcKit as a Service (Managed SaaS)

> **Template Origin**: Official | **ArcKit Version**: 4.12.3 | **Command**: `/arckit:ai-playbook`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-AIPB-v1.0 |
| **Document Type** | UK Government AI Playbook Compliance Assessment |
| **Project** | ArcKit as a Service (Managed SaaS) (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-05-03 |
| **Last Modified** | 2026-05-03 |
| **Review Date** | 2026-08-03 (quarterly DPO review per RISK R-010 control) |
| **Owner** | [PENDING] DPO + Lead Architect (joint owners — RACI) |
| **Reviewed By** | [PENDING] Service Owner / SIRO-equivalent, Security Lead |
| **Approved By** | [PENDING] Service Owner |
| **Distribution** | Project Team, Architecture Team, CCS liaison, CDDO, ICO (on request) |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-05-03 | ArcKit AI | Initial creation from `/arckit:ai-playbook` command. Pre-GA assessment of the SaaS AI feature surface. AI use case is **drafting-only assistance** for ArcKit artefact generation (FR-004) via the pluggable provider abstraction (ADR-004). Human-in-the-loop architectural — Article 22-safe. Risk classification: **LOW**. Linked to RISK R-010 (AI Playbook scope drift), R-011 (sub-processor), R-017 (provider lock-in); DPIA-008 / DPIA-012 in DPIA. | [PENDING] | [PENDING] |

## Document Purpose

The UK Government AI Playbook compliance assessment for the AI feature surface of the managed SaaS (Project 001). Two purposes:

1. Self-assessment against the AI Playbook 10 Principles + 6 Ethical Themes.
2. **The artefact that gates AI feature evolution** — any new AI feature beyond drafting (e.g., recommendation, scoring, ranking) triggers a refresh of this assessment **and** of `ARC-001-DPIA-v1.0.md` (RISK R-010 P2 action).

This assessment is **scoped to the managed SaaS only**. Sovereign deployments (Project 002) carry their own AI assessment per deployment.

---

## 1. AI System Context

### 1.1 System Identification

- **System name**: ArcKit AI artefact-generation feature.
- **AI type**: Generative (LLM-based) drafting assistant.
- **Provider**: Pluggable (per `ARC-001-ADR-004-v1.0.md`); single live primary at GA, second provider validated quarterly in CI (Goal G-8, Outcome O-7).
- **Deployment context**: A feature within the broader ArcKit SaaS, called only on user request.

### 1.2 Use Case

**Primary use case**: When a tenant user (an architect or bid lead) creates an artefact (principles, requirements, ADR, diagram, etc.), they may optionally request an AI-generated draft using their existing project context as input. The AI returns a draft. The user reviews, edits, and saves. The user is the artefact author; the AI is a drafting assistant. AI does **not**:

- Make decisions affecting the tenant or any data subject.
- Score, rank, triage, or recommend among options or among tenants / suppliers.
- Profile data subjects.
- Use customer data for model training (contractual no-training clause in DPA).
- Auto-publish or auto-save without human review.

### 1.3 Users and Affected Population

- **Users (initiate AI)**: tenant architects, tenant bid leads — professional adults using a B2B SaaS in a work context.
- **Affected population**: same as the user — they are the artefact author and reviewer; the AI's output is theirs, edited by them, before any further use.
- **No third-party affected**: AI does not act on a citizen, customer, or applicant. It does not affect access to public services.
- **Decision authority**: 100% with the human user. Zero AI autonomy.

### 1.4 Risk Classification (UK Gov AI Playbook)

**Classification: LOW-RISK**.

Rationale:

- ❌ Not high-risk: AI does not make automated decisions affecting health, fundamental rights, access to services, legal status, employment, or financial circumstances.
- ❌ Not medium-risk: AI does not perform semi-automated decisions; it does not allocate resources; it does not score or prioritise cases.
- ✅ Low-risk: AI is a productivity / drafting feature with full human control; recommendation systems with human control as defined in the AI Playbook; document drafting is an explicit Playbook example of low-risk use.

**Threshold for upgrade**: any future feature that scores / ranks / recommends or is used to triage suppliers / artefacts re-classifies the AI use case to MEDIUM-RISK or higher and triggers a refresh of this document, the DPIA, and the ATRS record (RISK R-010 P2 action — feature-scope boundary).

---

## 2. Compliance Against the 10 Core Principles

> Scoring 0–10 per principle. LOW-RISK threshold: ≥ 60% overall, basic safeguards in place.

### Principle 1: Understanding AI — ✅ Compliant — Score 8/10

**Evidence**:

- `ARC-001-ADR-004-v1.0.md` documents AI provider selection rationale, alternatives considered, and known limitations of LLMs (hallucination, context-window limits, model deprecation).
- `ARC-001-RISK-v1.0.md` R-010 explicitly covers AI feature scope drift — the team understands that "drafting-only" is a binding boundary, not a default position.
- `ARC-001-DPIA-v1.0.md` DPIA-012 explicitly addresses hallucination risk for AI-generated content attributed to data subjects.
- AI-content lineage metadata (FR-004) is mandatory — AI output is always distinguishable from human content.
- `ARC-001-PRIN-v2.0.md` Principle 9 (Data Quality, Lineage, and Tenant Portability) requires generation source, model, and prompt to be recorded on every artefact.
- Pilot DDaT user group is the channel for receiving real-world feedback on AI output quality.

**Findings**: Team has realistic expectations of LLM capabilities. Hallucination risk is acknowledged and mitigated by lineage flagging + human-as-author architecture.

**Gaps**: None significant for LOW-RISK; ongoing knowledge maintenance via quarterly DPO review.

---

### Principle 2: Lawful and Ethical Use — ✅ Compliant — Score 8/10

**Evidence**:

- `ARC-001-DPIA-v1.0.md` completed (this is the DPIA for the SaaS — AI processing covered in §14 of DPIA + DPIA-008/012).
- UK GDPR Article 22 explicit assessment: AI does **not** make solely-automated decisions of legal or significant effect (DPIA §14.1; this document §1.2).
- Equality Act 2010: AI feature is identity-blind; not used to select / rank / triage individuals; bias risk minimal in drafting-only mode.
- Human Rights Act 1998: no AI decision-making affects rights; no surveillance / profiling.
- Data Ethics Framework: applied via Principles 5 (Security by Design), 7 (UK Sovereignty), 9 (Data Quality / Lineage / Portability) in `ARC-000-PRIN-v2.0.md`.
- Legal / compliance team engagement: DPO + Service Owner + Lead Architect joint review.

**Findings**: Lawful basis (Article 6(1)(b) Performance of contract, with legitimate-interest for service-improvement aggregates) is documented in DPIA §4. EqIA not formally produced as a separate document because risk is low and feature is drafting-only — equality assessment is captured in this document §3 (Theme 3 — Fairness).

**Gaps**:

- Standalone Equality Impact Assessment not produced — for LOW-RISK B2B SaaS this is proportionate, but noted as a gap to address if AI feature scope ever expands.
- Standalone Human Rights Assessment not produced — same proportionality reasoning.

**Action**: Inline EqIA in §3 Theme 3; refresh if AI scope changes (LOW PRIORITY).

---

### Principle 3: Security — ✅ Compliant — Score 8/10

**Evidence**:

- `ARC-001-SECD-v1.0.md` §5 threat model addresses AI-specific threats:
  - **T4** — AI sub-processor exfiltration / training-on-customer-data → no-training-on-customer-data DPA clause + provider abstraction + quarterly DPO review (RISK R-011).
  - Prompt injection — mitigated by short, scoped prompts + structured-output validation + lineage flagging of suspicious outputs.
  - Data poisoning — N/A (no fine-tuning on customer data; provider serves stock model).
  - Model theft — N/A (vendor consumes API; doesn't host model).
  - Model inversion — mitigated by no-training-on-customer-data clause.
- `ARC-001-RISK-v1.0.md` R-011 (sub-processor breach), R-017 (provider lock-in), R-014 (isolation defect) all carry through.
- `ARC-001-PRIN-v2.0.md` Principle 5 (Security by Design, NON-NEGOTIABLE).
- AI sub-processor DPA includes Article 46 SCCs + security incident notification SLA.
- ADR-004 pluggable abstraction enables ≤ 5-day provider switch (Outcome O-7 / RISK R-017 control).

**Findings**: The AI feature inherits the platform's strong security baseline. AI-specific concerns are addressed through contractual + architectural separation.

**Gaps**:

- **Red-teaming for prompt injection**: not yet executed; planned for pre-GA pen test (RISK §H Priority-1 action 1) — the pen test scope explicitly includes AI feature surface.

**Action**: Ensure pen-test scope (RISK §H) includes prompt-injection / jailbreak testing (HIGH).

---

### Principle 4: Human Control — ✅ Compliant — Score 10/10

**Evidence**:

- **Architectural human-in-the-loop**: every AI output is reviewed and edited by a human user before save (UC-2 in `ARC-001-REQ-v1.0.md`).
- AI does not auto-publish; the user is the artefact author with full edit / delete / discard control.
- Tenant administrator can disable AI feature for the tenancy (FR-004 + ADR-004) — full opt-out at tenancy level.
- Per-user AI feature toggle available (covered by tenant admin role permissions).
- Lineage metadata distinguishes AI vs human content (FR-004) — supports human review.
- AI is a **drafting assistant**, not a decision-maker — full alignment with the AI Playbook's strongest human-oversight model.

**Findings**: Human control is the architectural default — this is the AI feature's strongest dimension.

**Gaps**: None.

---

### Principle 5: Lifecycle Management — ⚠️ Partially Compliant — Score 7/10

**Evidence**:

- ADR-004 documents provider selection, alternatives, and exit strategy.
- Pluggable abstraction (ADR-004) enables provider switch within 5 working days.
- Quarterly CI on alternative provider validates portability (Goal G-8 / Outcome O-7).
- Model versioning is the provider's responsibility (vendor consumes provider's model API); vendor monitors deprecation notices and version-pinning policy.
- Decommissioning: AI feature can be disabled per-tenant or platform-wide; tenant data export (BR-007) is unaffected by AI-feature decommissioning.
- Monitoring: AI usage telemetry (per-tenant inference volume) feeds RISK R-006 (cost) and R-007 (abuse).

**Findings**: Lifecycle management is mostly delegated to the provider, with vendor controls on selection and exit.

**Gaps**:

- Model-deprecation monitoring runbook not yet documented.
- Drift detection for AI output quality not formally implemented; relies on user feedback + quarterly DPO review.
- Explicit retraining schedule: N/A (vendor doesn't fine-tune).

**Actions**:

- Document model-deprecation monitoring runbook — Lead Architect, GA + 30 days (MEDIUM).
- Add output-quality KPI to quarterly DPO review (e.g., user-reported AI-quality complaints) — DPO, GA + 60 days (MEDIUM).

---

### Principle 6: Right Tool Selection — ✅ Compliant — Score 8/10

**Evidence**:

- `ARC-001-ADR-004-v1.0.md` selection rationale: AI-assisted drafting genuinely lowers the time-to-first-bid-pack for SMEs (Goal G-2 — 5 working days target) and is the principal mechanism that makes the SME free tier (Principle 1) viable at scale.
- Alternatives considered: pure-template generation (insufficient — produces generic content); manual templating only (defeats the platform's value proposition); rules-based generators (insufficient for the long-form artefact types).
- Cost-benefit: AI inference cost (~ £X per artefact at scale, per Finance Lead model) is offset by SME activation rate (Goal G-2) and cross-subsidy economics (Outcome O-3).
- Success metrics defined: artefact-quality user-feedback score ≥ X; activation rate ≥ 60% (BR-008); free-tier productivity uplift measurable.

**Findings**: AI is the right tool for the drafting use case; alternatives genuinely considered; not "AI for AI's sake."

**Gaps**:

- AI-quality user-feedback metric not yet operationalised.

**Action**: Operationalise AI-quality user-feedback in tenant UI — Product Manager, GA + 30 days (MEDIUM).

---

### Principle 7: Collaboration — ✅ Compliant — Score 7/10

**Evidence**:

- Cross-government collaboration: CCS liaison for G-Cloud listing; CDDO engagement on TCoP / Service Standard; pilot DDaT user group (Goal G-1).
- AI Standards Hub: under consideration for community engagement post-GA.
- Knowledge sharing: ATRS publication is the principal vehicle (RISK R-010 P2 action).
- Industry / civil society: pre-GA consultation with privacy-law counsel.
- Vendor itself contributes to government AI community via the open ArcKit plugin and (potentially) public service-side OSS (TCoP Point 3 ADR pending).

**Findings**: Collaboration baseline is appropriate for a B2B SaaS. Deepening is a post-GA opportunity.

**Gaps**:

- Engagement with the AI Standards Hub not yet formalised.
- Cross-government AI community contribution channel not yet defined.

**Actions**:

- Reach out to the AI Standards Hub — Service Owner, GA + 60 days (LOW).
- Publish ATRS record — DPO, GA (HIGH; RISK R-010 P2).

---

### Principle 8: Commercial Partnership — ✅ Compliant — Score 8/10

**Evidence**:

- AI provider DPA includes the AI-Playbook-recommended terms:
  - Performance metrics and SLAs (latency, error rate).
  - Audit rights for security and processing posture.
  - Bias / fairness disclosure (provider model card requested at quarterly DPO review).
  - Data rights and ownership: tenant retains rights; no provider use of customer data for training (no-training-on-customer-data).
  - Exit strategy: data portability via open formats (Principle 9 + ADR-007); pluggable abstraction enables provider switch within 5 days (ADR-004).
  - Liability for AI failures: covered by indemnification + cyber insurance (RISK §H action 6).
  - Article 46 transfer mechanism (Standard Contractual Clauses) for non-UK processing.
- Procurement: vendor is the procurer of the AI sub-processor; tenant is not exposed to the contractual relationship beyond the published sub-processor list and sub-processor-change 30-day notice.
- Cost / margin transparency: AI-inference cost is a tracked line item in FinOps tagging (Principle 17 + RISK R-006).

**Findings**: Commercial controls on the AI sub-processor are robust and aligned with AI Playbook expectations.

**Gaps**:

- Pen-testing rights in the DPA not yet specifically validated.
- Provider-side incident notification SLA not yet stress-tested (no incidents have occurred).

**Actions**:

- Confirm pen-testing rights in DPA renewal — DPO, GA + 90 days (MEDIUM).
- Annual tabletop incident-notification drill with provider — DPO + Security Lead, GA + 12 months (LOW).

---

### Principle 9: Skills and Expertise — ⚠️ Partially Compliant — Score 6/10

**Evidence**:

- Team composition (`ARC-001-STKE-v1.0.md`):
  - Lead Architect (named [PENDING]) — AI/ML technical knowledge expected.
  - DPO (named [PENDING]) — UK GDPR + AI ethics knowledge expected.
  - Security Lead (named [PENDING]).
  - Service Owner (Mark Craddock — confirmed) — strategic AI awareness.
- Pilot DDaT user group provides domain expertise on the buyer side.
- SME architects (the customer) provide the domain expertise on the supplier / use side.

**Findings**: The vendor has identified the right roles and is staffing them; some are [PENDING] hires (vendor team is small and lean).

**Gaps**:

- Several team roles still [PENDING] in STKE.
- Formal AI ethics training for the team not yet completed.
- Bias-testing expertise: the LOW-RISK drafting-only scope minimises bias risk, but explicit expertise is not yet in-house.

**Actions**:

- Fill [PENDING] vendor roles (Lead Architect, DPO, Security Lead, Accessibility Lead) by GA – 60 days — Service Owner (HIGH).
- AI ethics training for vendor team (e.g., Government Cyber Academy + UK AI Standards Hub modules) — Service Owner, GA + 90 days (MEDIUM).
- Engage external bias-testing expertise as needed if AI scope expands (CONDITIONAL).

---

### Principle 10: Organisational Alignment — ✅ Compliant — Score 8/10

**Evidence**:

- Senior Responsible Owner: Mark Craddock, Service Owner / SIRO-equivalent (`ARC-001-STKE-v1.0.md` RACI).
- AI Governance gate: any AI feature change beyond drafting goes through ADR review + DPIA refresh + this document refresh (RISK R-010 P2 action).
- AI strategy alignment: AI feature serves Principle 1 (SME affordability) and Goal G-2 (5-day pack); strategic justification documented.
- Risk management process: `ARC-001-RISK-v1.0.md` R-010, R-011, R-017 all under quarterly review.
- Architecture Review Board (`ARC-000-PRIN-v2.0.md` §VI Exception Process): all AI ADRs subject to board review.
- Assurance team: DPO + Security Lead + Service Owner joint sign-off.

**Findings**: AI is governed within the broader ArcKit governance framework, not as a side-channel feature. SRO is the same as the platform SRO — there is no AI-specific governance vacuum.

**Gaps**:

- Formal AI Governance Board: vendor-scale-appropriate equivalent is the Service Owner + DPO + Security Lead + Lead Architect joint forum; full Board not warranted at this scale.

**Actions**: None for now; reassess at scale.

---

### Principles Score Summary

| # | Principle | Status | Score |
|---|-----------|--------|-------|
| 1 | Understanding AI | ✅ | 8 |
| 2 | Lawful and Ethical Use | ✅ | 8 |
| 3 | Security | ✅ | 8 |
| 4 | Human Control | ✅ | 10 |
| 5 | Lifecycle Management | ⚠️ | 7 |
| 6 | Right Tool Selection | ✅ | 8 |
| 7 | Collaboration | ✅ | 7 |
| 8 | Commercial Partnership | ✅ | 8 |
| 9 | Skills and Expertise | ⚠️ | 6 |
| 10 | Organisational Alignment | ✅ | 8 |
| **Subtotal** | | | **78/100** |

---

## 3. Compliance Against the 6 Ethical Themes

> Scoring 0–10 per theme.

### Theme 1: Safety, Security, and Robustness — ✅ Compliant — Score 8/10

**Evidence**:

- Safety testing: AI output is reviewed by human author before any external use — the principal safety control.
- Robustness: AI feature degrades gracefully (UC-2 Alt 3a) — if AI engine throttled or unavailable, manual authoring is unaffected.
- Fail-safe: tenant continues to function with AI disabled.
- Incident response plan: `ARC-001-SECD-v1.0.md` §1 D1 + RISK §H action 7 — incident runbook with ICO 72-h notification template.
- Pre-GA pen test scope includes prompt-injection / jailbreak testing (Principle 3 action).

**Gaps**: red-team prompt-injection testing pending (covered in Principle 3 action).

---

### Theme 2: Transparency and Explainability — ⚠️ Partially Compliant — Score 7/10

**Evidence**:

- AI-content lineage metadata (FR-004) — AI vs human content distinguishable on every artefact.
- Sub-processor list published (DPIA + this document).
- Tenant-facing AI documentation (in product help) describes what AI does, what it does not do, what data it sees, what data it does not retain.
- DPIA §14 (AI / Algorithmic Processing) provides the formal explainability narrative.

**Gaps**:

- **ATRS (Algorithmic Transparency Recording Standard)** not yet published — RISK R-010 control + this document Principle 7 action.
- Public-facing AI-feature documentation not yet on the marketing site.

**Actions**:

- Publish ATRS record at GA — DPO (CRITICAL — RISK R-010 P2 + DPIA action #4).
- Publish AI-feature documentation page on marketing site — Product Manager, GA (HIGH).

---

### Theme 3: Fairness, Bias, and Discrimination — ✅ Compliant (in scope) — Score 7/10

**Evidence**:

- Bias risk in drafting-only mode is structurally low: AI does not select / rank / triage individuals; AI's input is the user's own project context; AI's output is reviewed and edited by the user before publication.
- Equality Act 2010 protected characteristics (gender, ethnicity, age, disability, religion, sexual orientation): AI feature is identity-blind — no protected-characteristic input or output processing in the principal use case.
- Inline EqIA — AI does not deny or differentiate access to the service based on any protected characteristic.
- Provider model card review: AI provider's published model card is reviewed at provider selection and quarterly thereafter.
- Pilot DDaT user group includes diverse architecture-community representation (DDaT roles span seven specialisms; SME and large-enterprise mix).

**Gaps**:

- Formal fairness-metrics testing across protected characteristics: not applicable for drafting-only mode (no decisions to be fair / unfair about) but would be required if AI scope expanded to recommendation / scoring.
- Provider-side bias disclosures monitored but not independently audited.

**Actions**:

- Quarterly DPO review of provider model card and bias disclosures — DPO (MEDIUM; in cadence).
- Document fairness-metrics framework activation criterion (re-applied if AI scope expands to recommendation) — DPO + Lead Architect, GA + 60 days (LOW).

---

### Theme 4: Accountability and Responsibility — ✅ Compliant — Score 9/10

**Evidence**:

- SRO: Mark Craddock, Service Owner / SIRO-equivalent (`ARC-001-STKE-v1.0.md` RACI).
- DPO + Lead Architect joint owner of this document.
- Decision-making process documented: AI ADRs subject to review board (`ARC-000-PRIN-v2.0.md` §VI).
- Audit trail of AI decisions: every AI generation is logged (FR-004 + ADR-005 audit log) with command, model, prompt-version, user, tenant ID.
- Incident response procedures: `ARC-001-SECD-v1.0.md` §1 D1.
- Accountability for errors: the user is the artefact author; the vendor is accountable for the AI feature operating within scope (drafting-only) and for sub-processor controls; the AI provider is accountable for service availability and security per DPA.

**Gaps**: minor — formal RACI for an AI-specific decision (e.g., who authorises a model upgrade) embedded in §10 Principle 10 evidence but not separately tabulated. Not a meaningful gap at vendor scale.

---

### Theme 5: Contestability and Redress — ✅ Compliant — Score 8/10

**Evidence**:

- Right to contest AI output: trivially available — the AI output is a draft on the user's own screen, fully editable / discardable. There is no "decision" by the AI to contest.
- Human review process: the AI output is reviewed by the human author before any further use — it is not used to take any action against any data subject.
- Appeal mechanism: not applicable to drafting-only AI; tenant DPO mailbox available for any concerns.
- Redress: tenant DPA + UK GDPR data-subject rights (DPIA §11) + DPO complaint route + ICO complaint right (DPIA §11 row 9).
- Response times: SAR 1-month SLA per UK GDPR; service incidents per `ARC-001-OPS-v1.0.md` (pending).

**Gaps**:

- AI-specific contestation (if a tenant ever wants to formally contest an AI output's quality) handled via DPO mailbox — process exists but isn't yet documented as an AI-specific track.

**Actions**:

- Document AI-output quality-feedback channel in product help — Product Manager, GA + 30 days (LOW).

---

### Theme 6: Societal Wellbeing and Public Good — ✅ Compliant — Score 9/10

**Evidence**:

- Strategic alignment: the AI feature directly supports Procurement Act 2023 SME-spend objectives by reducing the cost of producing credible governance evidence for SMEs (Principle 1 / SD-13). It is a tool for *more equitable* access to the public-sector supply chain.
- Environmental: AI inference cost is tracked (RISK R-006); per-tenant carbon attribution is on the post-GA roadmap (TCoP Point 12 cross-link).
- Benefits distribution: the SME free tier (Principle 1) makes AI-assisted artefact generation available *without paying for an enterprise EA tool* — which is the target population most likely to be excluded from such tools.
- Negative impacts mitigated: hallucination risk → lineage flag + human review; sub-processor risk → contractual + abstraction controls; cost risk → quotas (ADR-008).
- Alignment with public values: open standards (Principle 4), open source first (Principle 16), SME-fairness (Principle 1), accessibility (Principle 12 NON-NEGOTIABLE), UK sovereignty (Principle 7) — all explicit in the architecture principles.

**Gaps**:

- Independent assessment of public-good claim not yet conducted (e.g., independent academic study). Could be commissioned post-GA when adoption volume permits.

---

### Themes Score Summary

| # | Theme | Status | Score |
|---|-------|--------|-------|
| 1 | Safety, Security, Robustness | ✅ | 8 |
| 2 | Transparency and Explainability | ⚠️ | 7 |
| 3 | Fairness, Bias, Discrimination | ✅ | 7 |
| 4 | Accountability and Responsibility | ✅ | 9 |
| 5 | Contestability and Redress | ✅ | 8 |
| 6 | Societal Wellbeing | ✅ | 9 |
| **Subtotal** | | | **48/60** |

---

## 4. Overall Score and Compliance

**Total Score**: 78 (Principles) + 48 (Themes) = **126 / 160 = 78.75%**.

**Risk Level**: **LOW**.

**LOW-RISK Threshold**: ≥ 60% with basic safeguards in place. **Threshold met.**

**Compliance Status**: ✅ **GOOD** (within the 75–84% band).

**Decision**: ✅ **GO — DEPLOY** subject to closure of Priority-1 actions in §7 (chiefly ATRS publication).

---

## 5. Mandatory Documentation Checklist

| Document | Required? | Status | Reference |
|----------|-----------|--------|-----------|
| **ATRS (Algorithmic Transparency Recording Standard)** | Yes (recommended for vendor; mandatory if a public-sector tenant operates ArcKit-AI within their own service stack) | ⚠️ Pending — to be published at GA | RISK R-010 P2 + Theme 2 action |
| **DPIA** | Yes (UK GDPR Art. 35) | ✅ Done — `ARC-001-DPIA-v1.0.md` | §15 action 4 closed at this commit |
| **EqIA (Equality Impact Assessment)** | Inline (proportionate for LOW-RISK drafting-only B2B SaaS) | ✅ Inlined in §3 Theme 3; refreshes if scope changes | Theme 3 evidence |
| **Human Rights Assessment** | Inline (proportionate) | ✅ Inlined in Principle 2; no rights-affecting decisions made | Principle 2 evidence |
| **Security Risk Assessment** | Yes | ✅ `ARC-001-SECD-v1.0.md` + `ARC-001-RISK-v1.0.md` | SbD §5 threat model |
| **Bias Audit Report** | N/A for drafting-only mode | ✅ N/A justified; reactivated if scope expands | Theme 3 action |
| **User Research Report** | Yes | ⚠️ Pilot DDaT user group ongoing; written report at GA + 30 days | STKE Goal G-1 |

---

## 6. Mapping to ArcKit Artefacts

| Source / Sibling Artefact | AI Playbook Linkage |
|---------------------------|---------------------|
| `ARC-000-PRIN-v2.0.md` | Principle 4 (Open Standards) → ADR-004 portability; Principle 5 (Security) → AI threat model; Principle 7 (UK Sovereignty) → Article 46 SCCs; Principle 9 (Lineage) → AI-content metadata |
| `ARC-001-REQ-v1.0.md` | FR-004 (AI-assisted generation); BR-006 (evidence pack scope); BR-007 (portability); INT-005 (AI provider integration) |
| `ARC-001-STKE-v1.0.md` | SD-9 (Lead Architect — pluggability); SD-11 (DPO); Goal G-8 (pluggable AI for sovereign reuse); Outcome O-7 (AI architecture validated) |
| `ARC-001-RISK-v1.0.md` | R-010 (AI Playbook scope drift), R-011 (sub-processor breach), R-017 (provider lock-in) — this assessment is a load-bearing control on each |
| `ARC-001-TCOP-v1.0.md` | AI Annex (cross-references Principle 7, Point 6 / Point 7) — this assessment is the principal evidence for the AI Annex |
| `ARC-001-SECD-v1.0.md` | §5 threat model (T4 AI-specific); §10 acceptance vehicle for R-010 |
| `ARC-001-DPIA-v1.0.md` | §14 (AI / Algorithmic Processing); DPIA-008 (AI sub-processor incident); DPIA-012 (hallucination) |
| `ARC-001-ADR-004-v1.0.md` | AI Provider Abstraction — the architectural foundation for all AI Playbook controls |

---

## 7. Action Plan

### 7.1 High Priority (Pre-GA, must-land)

| # | Action | Owner | Due | AI Playbook Ref |
|---|--------|-------|-----|------------------|
| 1 | Publish ATRS record | DPO | GA | Theme 2; RISK R-010 |
| 2 | Define AI feature-scope boundary (drafting / recommendation) | DPO + Lead Architect | 2026-07-31 | Principle 4; RISK R-010 P2 |
| 3 | Pen-test scope to include prompt-injection / jailbreak testing | Security Lead | GA – 60 days | Principle 3; RISK §H action 1 |
| 4 | Public AI-feature documentation page | Product Manager | GA | Theme 2 |
| 5 | Fill [PENDING] vendor roles (Lead Architect, DPO, Security Lead) | Service Owner | GA – 60 days | Principle 9 |

### 7.2 Medium Priority (first 90 days post-GA)

| # | Action | Owner | Due |
|---|--------|-------|-----|
| 6 | Operationalise AI-quality user-feedback metric in tenant UI | Product Manager | GA + 30 days |
| 7 | Document model-deprecation monitoring runbook | Lead Architect | GA + 30 days |
| 8 | Add output-quality KPI to quarterly DPO review | DPO | GA + 60 days |
| 9 | Document AI-output quality-feedback channel in product help | Product Manager | GA + 30 days |
| 10 | Confirm pen-testing rights in DPA renewal | DPO | GA + 90 days |
| 11 | Document fairness-metrics framework activation criterion | DPO + Lead Architect | GA + 60 days |
| 12 | Reach out to AI Standards Hub | Service Owner | GA + 60 days |
| 13 | AI ethics training for vendor team | Service Owner | GA + 90 days |

### 7.3 Low Priority (continuous)

| # | Action | Owner | Cadence |
|---|--------|-------|---------|
| 14 | Quarterly DPO review of AI feature surface area + provider model card | DPO | Quarterly |
| 15 | Annual tabletop incident-notification drill with provider | DPO + Security Lead | Annual |
| 16 | Annual AI Playbook re-assessment | DPO + Lead Architect | Annual or on material change |

---

## 8. Approval

| Role | Name | Decision | Date | Signature |
|------|------|----------|------|-----------|
| DPO | [PENDING] | [PENDING] Endorse AI Playbook compliance position | [PENDING] | _________ |
| Lead Architect | [PENDING] | [PENDING] Confirm technical AI controls | [PENDING] | _________ |
| Service Owner / SIRO-equivalent | Mark Craddock | [PENDING] Approve overall AI Playbook compliance | [PENDING] | _________ |
| Security Lead | [PENDING] | [PENDING] Confirm AI security position | [PENDING] | _________ |

---

## 9. Review and Monitoring

- **Quarterly**: DPO review of AI feature surface area, provider model card, sub-processor posture (cadence locked into RISK §J).
- **Event-based**: any AI feature change crossing the drafting / recommendation boundary triggers immediate refresh of this document, the DPIA, and the ATRS record.
- **Annual**: full AI Playbook re-assessment.

---

## External References

> No external policy documents were placed in `projects/001-arckit-saas/external/` at the time of generation. UK Government AI Playbook, ATRS guidance, and Data Ethics Framework are public-domain and cited by name.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### References

- UK Government AI Playbook: <https://www.gov.uk/government/publications/ai-playbook-for-the-uk-government>
- Algorithmic Transparency Recording Standard: <https://www.gov.uk/government/publications/guidance-for-organisations-using-the-algorithmic-transparency-recording-standard>
- Data Ethics Framework: <https://www.gov.uk/government/publications/data-ethics-framework>
- ICO AI Guidance: <https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/>

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `/arckit:ai-playbook` command
**Generated on**: 2026-05-03
**ArcKit Version**: 4.12.3
**Project**: ArcKit as a Service (Managed SaaS) (Project 001)
**AI Model**: Claude Opus 4.7 (1M context)
**Generation Context**: Sourced from ARC-000-PRIN-v2.0, ARC-001-REQ-v1.0, ARC-001-STKE-v1.0, ARC-001-RISK-v1.0 (R-010/R-011/R-017), ARC-001-TCOP-v1.0, ARC-001-SECD-v1.0, ARC-001-DPIA-v1.0, and ARC-001-ADR-004-v1.0. AI use case scoped to drafting-only assistance per FR-004 and ADR-004. Risk classification: LOW.
