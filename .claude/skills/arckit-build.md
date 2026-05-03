---
name: arckit-build
description: "This skill should be used when the user asks to bulk-build ArcKit artefacts, run an end-to-end architecture build, generate multiple /arckit:* outputs in parallel, orchestrate a wave-based build, resume an interrupted build, or rebuild a project from scratch without exhausting main-context. Triggers: arckit-build, build harness, build all artefacts, generate full project, /arckit:* in parallel, run the recipe, --plan, --resume, --target, --refresh, --recipe, state.json. The skill orchestrates parallel /arckit:* generation using subagent isolation: reads project state, computes the artefact dependency DAG, dispatches one subagent per target per wave (each subagent invokes a /arckit:* skill in its own context), validates outputs, commits the wave, and persists progress to .arckit/state.json for resumability."
paths:
  - "projects/**/.arckit/state.json"
  - "projects/**/ARC-*-*.md"
  - ".claude/skills/arckit-build.md"
---

# ArcKit Build Harness (v0.2)

You are running the ArcKit build harness. Your job is **orchestration only** — never read or write artefact content yourself. Spawn subagents for that.

## Operating principles

- **Never read or write artefact content in main context.** That's what subagents are for.
- **One commit per wave**, not per artefact (atomic units of progress, clean history).
- **Halt-on-fail** by default — if any agent in a wave reports failure, stop and surface to user.
- **State is sacred** — update `projects/{P}/.arckit/state.json` after every wave, before moving on.
- **Single message, multiple Agent calls** for parallelism within a wave. Never loop sequential Agent calls.
- **Idempotency**: if state says `complete` and the file exists at the recorded path, skip.

## Args

| Arg | Effect |
|-----|--------|
| `<project>` | Project directory name or numeric ID (e.g. `001` or `001-arckit-saas`). If absent, prompt user. |
| `--plan` | Dry run. Print the wave plan, do not dispatch any Agents, exit. |
| `--resume` | Read state.json; continue from last incomplete wave. |
| `--target NAME` | Build only NAME and its missing dependencies. |
| `--refresh NAME` | Force-rebuild NAME and everything downstream. |
| `--no-commit` | Skip the per-wave git commit. |
| `--recipe NAME` | Override recipe (default: auto-detect; UK-SaaS for now). |

## Recipe: UK-SaaS (v0.2, hardcoded)

Required artefacts. `{P}` = project ID, `{V}` = version (default `1.0`), `{N}` = sequence, `{NAME}` = project slug.

Output paths use `bash scripts/bash/generate-document-id.sh` rather than hardcoded strings — the helper is the source of truth for ArcKit naming. Argument order is **positional**: `PROJECT_ID DOC_TYPE [VERSION]` followed by flags. Multi-instance types (ADR, DIAG, DFD, WARD, DMC, RSCH, AWRS, AZRS, GCRS, DSCT, WGAM, WCLM, WVCH, GOVR, GCSR, GLND) **require** `--next-num DIR` to allocate the sequence number.

```bash
# Single-instance (REQ, STKE, RISK, HLD, ...):
bash scripts/bash/generate-document-id.sh {P} {TYPE} {V} --filename
#   → ARC-{P}-{TYPE}-v{V}.md

# Multi-instance (ADR, DIAG, ...):
bash scripts/bash/generate-document-id.sh {P} {TYPE} {V} --filename \
  --next-num projects/{P}-{NAME}/{decisions|diagrams}
#   → ARC-{P}-{TYPE}-{NNN}-v{V}.md  (NNN auto-incremented)
```

The helper returns only the *filename* (e.g. `ARC-001-REQ-v1.0.md`), not the full path — the harness composes `projects/{P}-{NAME}/[subfolder/]{filename}` using the subfolder convention from the recipe table below. The "Expected output path" column is the result for validation only; the harness itself never hand-constructs these strings outside the helper + recipe-defined subfolder.

| Target | Skill | Skill args | Expected output path | Depends on |
|--------|-------|------------|----------------------|------------|
| PRIN | `arckit:principles` | (none — global) | `projects/000-global/ARC-000-PRIN-v{V}.md` | — |
| GLOSSARY | `arckit:glossary` | `{P}` | `projects/000-global/ARC-000-GLO-v{V}.md` | PRIN |
| STRATEGY | `arckit:strategy` | (none — global) | `projects/000-global/ARC-000-STRAT-v{V}.md` | PRIN, STKE |
| WARDLEY | `arckit:wardley` | `{NAME}` | `projects/000-global/ARC-000-WARD-v{V}.md` | PRIN, REQ |
| REQ | `arckit:requirements` | `{NAME}` | `projects/{P}-{NAME}/ARC-{P}-REQ-v{V}.md` | PRIN |
| STKE | `arckit:stakeholders` | `{NAME}` | `projects/{P}-{NAME}/ARC-{P}-STKE-v{V}.md` | PRIN |
| ADR-{N} | `arckit:adr` | `{P} <topic>` (topic per recipe — see below) | `projects/{P}-{NAME}/decisions/ARC-{P}-ADR-{N}-v{V}.md` | PRIN, REQ |
| RISK | `arckit:risk` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-RISK-v{V}.md` | REQ, STKE, ADR-*, PRIN |
| SOBC | `arckit:sobc` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-SOBC-v{V}.md` | REQ, STKE, RISK |
| PLAN | `arckit:plan` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-PLAN-v{V}.md` | SOBC, RISK |
| ROADMAP | `arckit:roadmap` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-ROAD-v{V}.md` | PLAN |
| TCOP | `arckit:tcop` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-TCOP-v{V}.md` | REQ, STKE, RISK, ADR-* |
| SBD | `arckit:secure` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-SBD-v{V}.md` | TCOP, RISK, REQ, ADR-* |
| DPIA | `arckit:dpia` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-DPIA-v{V}.md` | REQ, STKE, RISK |
| AIP | `arckit:ai-playbook` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-AIP-v{V}.md` | DPIA, RISK, REQ, ADR-004 |
| SVCASS | `arckit:service-assessment` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-SVCASS-v{V}.md` | TCOP, SBD, DPIA, AIP, REQ, STKE |
| HLD | `arckit:hld-review` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-HLD-v{V}.md` | REQ, ADR-*, PRIN |
| DIAG-C4 | `arckit:diagram` | `{P} c4-context` | `projects/{P}-{NAME}/diagrams/ARC-{P}-DIAG-001-v{V}.md` | HLD |
| DIAG-SEQ | `arckit:diagram` | `{P} sequence` | `projects/{P}-{NAME}/diagrams/ARC-{P}-DIAG-002-v{V}.md` | HLD |
| DIAG-DEP | `arckit:diagram` | `{P} deployment` | `projects/{P}-{NAME}/diagrams/ARC-{P}-DIAG-003-v{V}.md` | HLD, ADR-006 |
| DEVOPS | `arckit:devops` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-DEVOPS-v{V}.md` | REQ, ADR-* |
| FINOPS | `arckit:finops` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-FINOPS-v{V}.md` | REQ, RISK |
| OPS | `arckit:operationalize` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-OPS-v{V}.md` | HLD, DEVOPS, RISK |
| TRACE | `arckit:traceability` | `{P}` | `projects/{P}-{NAME}/ARC-{P}-TRACE-v{V}.md` | REQ, STKE, ADR-*, RISK, HLD, DPIA, SBD, TCOP, PLAN, ROADMAP, AIP, SVCASS, DEVOPS, FINOPS, OPS |

**ADR topic seeding** — `arckit:adr` requires a topic. Topics are recipe-defined, not auto-discovered in v0.1. UK-SaaS default ADR set:

| ADR | Topic |
|-----|-------|
| ADR-001 | Cloud platform (AWS / Azure / GCP) |
| ADR-002 | Identity & access (GOV.UK One Login vs Entra) |
| ADR-003 | Data residency & sovereignty |
| ADR-004 | AI / LLM provider (if AI feature in scope) |
| ADR-005 | Logging & observability stack |
| ADR-006 | Deployment topology (regions, multi-tenancy) |
| ADR-007 | Build vs buy (G-Cloud framework) |
| ADR-008 | Open-source licence policy |

To override, set `recipe.adrs[]` in a future external recipe file (v0.5+). For now, edit the table inline.

**Optional targets** (omit unless project flags them in scope):
- `AIP` — only if AI feature in scope (check REQ for AI-related FRs).
- `SVCASS` — only if public-service-style (always true for UK-SaaS recipe).
- `MOD-SBD` instead of `SBD` for sovereign / MOD recipes (separate recipe).

**Post-build hooks** (run after final wave):
- `arckit:health` — diagnostic scan.
- `arckit:pages` — regenerate docs site.

## Wave plan algorithm

Standard topological sort with parallelism:

1. `pending = recipe.targets - (state.complete ∩ files-exist)`
2. `done = state.complete`
3. While pending non-empty:
   - `wave = { t ∈ pending : deps(t) ⊆ done }`
   - If wave empty → cycle / unresolvable. Halt with error.
   - Emit wave; remove its members from pending; (after dispatch + validate) add to done.

**Worked example** — for project 001 (UK-SaaS) **starting from empty state**, the algorithm above produces this wave plan. Treat it as illustrative output; the harness recomputes waves at runtime from the recipe's dependency graph rather than reading this list.

- Wave 0: PRIN (no deps)
- Wave 1: GLOSSARY, REQ, STKE (deps on PRIN only)
- Wave 2: ADR-001..ADR-008 (parallel; deps on PRIN + REQ)
- Wave 3: STRATEGY, WARDLEY, RISK, HLD, DEVOPS, FINOPS (parallel)
- Wave 4: SOBC, TCOP, SBD, DPIA, DIAG-C4, DIAG-SEQ (parallel; DIAG-DEP waits on ADR-006 which is already done in W2)
- Wave 5: DIAG-DEP, PLAN, OPS, AIP (parallel; AIP only if in scope)
- Wave 6: ROADMAP (deps on PLAN)
- Wave 7: SVCASS (deps on TCOP, SBD, DPIA, AIP)
- Wave 8: TRACE
- Wave 9 (post-build): health, pages

## Per-wave execution

For each wave, in order:

### 1. Plan dispatch

Print:
```
Wave {N}/{total}: {targets joined}
  - estimated agents: {len(wave)}
  - estimated duration: ~{2-5} min wall-clock per agent (parallel)
```

### 2. Single message, multiple Agent calls — all in parallel

Use the **Agent tool** with `subagent_type: "general-purpose"`. One Agent call per target. **All in the same assistant message** so they run in parallel.

Per-agent prompt template (substitute `{...}` placeholders):

```
You are an ArcKit artefact worker subagent (orchestrated by /arckit-build, wave {WAVE_N}).

Project: {PROJECT_ID} ({PROJECT_NAME})
Target: {TARGET_NAME}
Skill to invoke: {SKILL}
Skill args: {SKILL_ARGS}
Expected output path: {EXPECTED_OUTPUT_PATH}

Inputs you may read (only these):
{INPUT_PATHS_BULLETED}

Steps:
1. Use the Skill tool to invoke `{SKILL}` with the args above verbatim. Do not ask interactive
   questions — if the skill calls AskUserQuestion, supply sensible defaults and continue.
2. Follow the skill's instructions exactly. Resolve the output filename via the ArcKit helper —
   **positional args first, flags last**:
     - Single-instance: `bash scripts/bash/generate-document-id.sh {PROJECT_ID} {TYPE} {VERSION} --filename`
     - Multi-instance (ADR/DIAG/...): `bash scripts/bash/generate-document-id.sh {PROJECT_ID} {TYPE} {VERSION} --filename --next-num projects/{PROJECT_ID}-{NAME}/{decisions|diagrams}`
   The helper returns only the bare filename; compose the full path against the recipe-defined
   subfolder. Do not hardcode. The expected path above is for validation only.
3. Sanity check via Bash:
   - `test -f "$ACTUAL_PATH"` returns success
   - `wc -l < "$ACTUAL_PATH"` returns > 100
   - `grep -c '^## Document Control\|^| Document ID' "$ACTUAL_PATH"` returns ≥ 1
4. Do NOT git commit. Do NOT modify other files. The orchestrator handles version control.

Report back ≤ 200 words:
- Actual file path written (resolved by the skill) + exact line count
- Top 3 findings, scores, or RAG ratings (whatever the skill produces as headline result)
- Validation result: PASS or FAIL (with reason)
- Any failures, partial completions, or warnings

Do NOT include the document content in your report. Just the summary.
```

### 3. Wait for all agents

When all return, collect summaries.

### 4. Validate

For each target in wave:
- File exists at expected path: `Bash test -f {OUTPUT_PATH}` returns success.
- Line count > 100: `wc -l < {OUTPUT_PATH}`.
- Document control header present: `grep -c '^## Document Control' {OUTPUT_PATH}` ≥ 1.

### 5. Update state.json

Read `projects/{P}/.arckit/state.json`, update each target with:

```json
{
  "<TARGET>": {
    "status": "complete",
    "path": "{OUTPUT_PATH}",
    "built_at": "{ISO_TIMESTAMP}",
    "wave": {WAVE_N},
    "line_count": {LC},
    "skill": "{SKILL}",
    "agent_summary": "{≤200-word agent report}"
  }
}
```

For failures: `status: "failed"`, `error: "..."`, `wave: {WAVE_N}`.

Write back to state.json.

### 6. Git commit

If `--no-commit` not set:
```bash
git add {OUTPUT_PATHS} projects/{P}/.arckit/state.json
git commit -m "$(cat <<'EOF'
Build wave {N}: {targets joined} via /arckit-build

{One-line per target with line count and headline result}

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### 7. Halt-on-fail

If any agent in the wave reported `FAIL` or validation failed:
- **DO write state.json** — record `status: "failed"`, `error: "..."`, `wave: {WAVE_N}` for each failed target, and `status: "complete"` for the targets in the wave that *did* succeed. State is needed for `--resume` to work.
- **Do NOT git commit** (don't half-commit a wave). Successfully-written artefact files are left in the working tree; they will be picked up on `--resume` and committed with the rest of the (then-complete) wave.
- Surface to user: per-target outcome, error summary, suggested remediation.
- Suggest `--resume` once fixed.
- Stop the build.

### 8. Move to next wave

Otherwise, proceed.

## State file shape

`projects/{P}/.arckit/state.json`:

```json
{
  "version": "0.1",
  "project_id": "001",
  "project_name": "001-arckit-saas",
  "recipe": "uk-saas",
  "started_at": "2026-05-03T16:00:00Z",
  "last_wave_completed": 5,
  "current_wave": 6,
  "targets": {
    "PRIN":   {"status": "complete", "path": "projects/000-global/ARC-000-PRIN-v2.0.md", "wave": 0, "source": "pre-existing"},
    "REQ":    {"status": "complete", "path": "...", "wave": 0, "source": "pre-existing"},
    "RISK":   {"status": "complete", "path": "...", "wave": 2, "skill": "arckit:risk"},
    "SVCASS": {"status": "pending"}
  },
  "waves": [
    {"n": 0, "targets": ["PRIN", "REQ", "STKE", "ADR-001..008"], "status": "complete", "completed_at": "...", "source": "pre-existing"},
    {"n": 2, "targets": ["RISK"], "status": "complete", "completed_at": "..."},
    {"n": 3, "targets": ["TCOP"], "status": "complete"}
  ]
}
```

## When invoked, perform these steps in order

1. **Parse arguments** from skill input (project, --plan, --resume, etc.). If project not specified, ask user.
2. **Detect project**: resolve `<project>` arg → `projects/{P}-{slug}/`. Confirm directory exists.
3. **Load state.json** at `projects/{P}/.arckit/state.json`. If absent, scan project dir for existing `ARC-{P}-*-v*.md` files and infer initial state.
4. **Subagent capability smoke-test** (first wave only, skip on `--resume`): before dispatching the real wave, spawn one throwaway `general-purpose` Agent with the prompt *"Use the Skill tool to list whether `arckit:principles` is available. Return one line: AVAILABLE or NOT_AVAILABLE."* If the response is `NOT_AVAILABLE`, halt with a clear error: subagents in this session do not have access to plugin skills (Failure mode #1). Suggest enabling the plugin at user-scope or running the harness from a session where `claude --print '/skill list'` shows the `arckit:*` family.
5. **Compute work list**: recipe targets minus `state.targets` whose `status: complete` AND file exists.
6. **If `--plan`**: print plan (each wave + targets + line `(skip|build) target ← deps`), exit.
7. **For each wave** (sequential outer loop):
   - Print wave header.
   - Build the per-agent prompt for each target in wave.
   - **Send a single assistant message containing N Agent tool calls** (one per target, all parallel).
   - Collect summaries when all complete.
   - Validate each output.
   - Update state.json (Write tool).
   - git commit (Bash) unless `--no-commit`.
   - Halt if any fail.
8. **Post-build hooks**: spawn 2 parallel agents — one for `arckit:health`, one for `arckit:pages`.
9. **Final report**:
   - Targets built (with line counts) / skipped / failed.
   - Total wall-clock.
   - Health + pages outcome.
   - Next recommended action (e.g., "review pre-GA blockers in TCOP §Critical Issues").

## Failure modes to watch for

- **Subagent doesn't have access to `arckit:*` skills** — if Skill tool returns "skill not found", surface clearly. Workaround: load the skill prompt in main context once, pass as plain text to agent (not implemented in v0.1).
- **Skill expects interactive Q&A** — some skills (e.g., `/arckit:dpia`) ask AskUserQuestion. The agent prompt must pre-resolve those by spelling them out in `{SKILL_ARGS}`. The recipe's Skill-args column should be specific enough to skip interaction.
- **Output path collision** — two skills writing to same path. Recipe must have unique paths per target.
- **State drift** — user manually deletes/edits artefacts after build. Detect via `test -f` validation + optional file-hash check (v0.3+).
- **Cycle in dependencies** — wave algorithm halts with "unresolvable cycle" error and lists the involved targets.

## Future versions

- v0.2: full DAG resolver (currently uses hardcoded wave hints).
- v0.3: input-hash-based change detection — skip if all inputs unchanged.
- v0.4: cross-reference + schema validators between waves.
- v0.5: external recipe YAML files (not hardcoded in skill).
- v0.6: CI mode (`--validate-only` for GitHub Actions).
- v1.0: skills declare I/O in frontmatter; harness reads frontmatter directly; dedicated `arckit:artefact-worker` subagent type.
