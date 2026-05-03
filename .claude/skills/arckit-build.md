---
name: arckit-build
description: ArcKit build harness — orchestrates parallel /arckit:* artefact generation using subagent isolation. Reads project state, computes the artefact dependency DAG, dispatches one subagent per target per wave (each subagent invokes a /arckit:* skill in its own isolated context), validates outputs, commits the wave, and persists state to .arckit/state.json for resumability. Use this when you need to build/rebuild a substantial set of ArcKit artefacts and don't want to run /arckit:* skills sequentially in main context (which exhausts context and fails past ~5 artefacts). Args: <project> (e.g. 001 or 001-arckit-saas) | --plan (dry run) | --resume (pick up from state) | --target NAME (specific target + deps) | --refresh NAME (force rebuild) | --no-commit | --recipe NAME.
---

# ArcKit Build Harness (v0.1)

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

## Recipe: UK-SaaS (v0.1, hardcoded)

Required artefacts. `{P}` = project ID, `{V}` = version (default `1.0`), `{N}` = sequence.

| Target | Skill | Output path | Depends on |
|--------|-------|-------------|------------|
| PRIN | `arckit:principles` | `projects/000-global/ARC-000-PRIN-v{V}.md` | — |
| GLOSSARY | `arckit:glossary` | `projects/000-global/ARC-000-GLO-v{V}.md` | PRIN |
| STRATEGY | `arckit:strategy` | `projects/000-global/ARC-000-STRAT-v{V}.md` | PRIN, STKE-any |
| WARDLEY | `arckit:wardley` | `projects/000-global/ARC-000-WARD-v{V}.md` | PRIN, REQ-any |
| REQ | `arckit:requirements` | `projects/{P}/ARC-{P}-REQ-v{V}.md` | PRIN |
| STKE | `arckit:stakeholders` | `projects/{P}/ARC-{P}-STKE-v{V}.md` | PRIN |
| ADR-{N} | `arckit:adr` | `projects/{P}/decisions/ARC-{P}-ADR-{N}-v{V}.md` | PRIN, REQ |
| RISK | `arckit:risk` | `projects/{P}/ARC-{P}-RISK-v{V}.md` | REQ, STKE, ADR-*, PRIN |
| SOBC | `arckit:sobc` | `projects/{P}/ARC-{P}-SOBC-v{V}.md` | REQ, STKE, RISK |
| PLAN | `arckit:plan` | `projects/{P}/ARC-{P}-PLAN-v{V}.md` | SOBC, RISK |
| ROADMAP | `arckit:roadmap` | `projects/{P}/ARC-{P}-ROAD-v{V}.md` | PLAN |
| TCOP | `arckit:tcop` | `projects/{P}/ARC-{P}-TCOP-v{V}.md` | REQ, STKE, RISK, ADR-* |
| SBD | `arckit:secure` | `projects/{P}/ARC-{P}-SBD-v{V}.md` | TCOP, RISK, REQ, ADR-* |
| DPIA | `arckit:dpia` | `projects/{P}/ARC-{P}-DPIA-v{V}.md` | SBD, REQ, STKE, RISK |
| AIP | `arckit:ai-playbook` | `projects/{P}/ARC-{P}-AIP-v{V}.md` | DPIA, RISK, REQ, ADR-004 |
| SVCASS | `arckit:service-assessment` | `projects/{P}/ARC-{P}-SVCASS-v{V}.md` | TCOP, SBD, DPIA, AIP, REQ, STKE |
| HLD | `arckit:hld-review` | `projects/{P}/ARC-{P}-HLD-v{V}.md` | REQ, ADR-*, PRIN |
| DIAG-C4 | `arckit:diagram` | `projects/{P}/diagrams/ARC-{P}-DIAG-001-v{V}.md` | HLD |
| DIAG-SEQ | `arckit:diagram` | `projects/{P}/diagrams/ARC-{P}-DIAG-002-v{V}.md` | HLD |
| DIAG-DEP | `arckit:diagram` | `projects/{P}/diagrams/ARC-{P}-DIAG-003-v{V}.md` | HLD, ADR-006 |
| DEVOPS | `arckit:devops` | `projects/{P}/ARC-{P}-DEVOPS-v{V}.md` | REQ, ADR-* |
| FINOPS | `arckit:finops` | `projects/{P}/ARC-{P}-FINOPS-v{V}.md` | REQ, RISK |
| OPS | `arckit:operationalize` | `projects/{P}/ARC-{P}-OPS-v{V}.md` | HLD, DEVOPS, RISK |
| TRACE | `arckit:traceability` | `projects/{P}/ARC-{P}-TRACE-v{V}.md` | (everything) |

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

For project 001 (UK-SaaS) **starting from empty state**, the wave plan is:

- Wave 0: PRIN, REQ, STKE (and any ADRs whose deps are met)
- Wave 1: ADR-001..ADR-N (parallel)
- Wave 2: RISK
- Wave 3: SOBC, TCOP, HLD, DEVOPS, FINOPS (parallel)
- Wave 4: SBD, PLAN, DIAG-C4, DIAG-SEQ, DIAG-DEP (parallel)
- Wave 5: DPIA, ROADMAP, OPS (parallel)
- Wave 6: AIP
- Wave 7: SVCASS
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
Output path: {OUTPUT_PATH}

Inputs you may read (only these):
{INPUT_PATHS_BULLETED}

Steps:
1. Use the Skill tool to invoke `{SKILL}` with these args verbatim:
   ```
   {SKILL_ARGS}
   ```
2. Follow the skill's instructions exactly. Read inputs. Write the file at {OUTPUT_PATH}.
3. Sanity check via Bash: `wc -l {OUTPUT_PATH}` returns > 100; `grep -c '^## Document Control' {OUTPUT_PATH}` returns ≥ 1.
4. Do NOT git commit. Do NOT modify other files. The orchestrator handles version control.

Report back ≤ 200 words:
- File path written + exact line count
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
- Do NOT commit (don't half-commit).
- Surface to user: error summary, suggested remediation.
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
4. **Compute work list**: recipe targets minus `state.targets` whose `status: complete` AND file exists.
5. **If `--plan`**: print plan (each wave + targets + line `(skip|build) target ← deps`), exit.
6. **For each wave** (sequential outer loop):
   - Print wave header.
   - Build the per-agent prompt for each target in wave.
   - **Send a single assistant message containing N Agent tool calls** (one per target, all parallel).
   - Collect summaries when all complete.
   - Validate each output.
   - Update state.json (Write tool).
   - git commit (Bash) unless `--no-commit`.
   - Halt if any fail.
7. **Post-build hooks**: spawn 2 parallel agents — one for `arckit:health`, one for `arckit:pages`.
8. **Final report**:
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
