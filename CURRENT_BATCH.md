# Current Batch — Playbook Work

Date: `2026-05-06`
Latest released version: **v1.2.2** (Lesson 13 added on top of v1.2.1)

## Where we are

The playbook is **shipped at v1.2.2** and live on GitHub: `https://github.com/kraftmine/claude-codex-playbook`.

No version is currently in flight. v1.2.0 (workflow refinements + genericization), v1.2.1 (Lesson 12 — localStorage cannot be a source of truth for server state), and v1.2.2 (Lesson 13 — forked implementations of the same concept drift apart) are all merged and pushed to `main`.

## What's queued

Nothing actively in flight. Two open threads sitting in the working-history layer, waiting for a decision before becoming proposals:

### Thread A — Superpowers integration (potential v1.3)

Codex wrote `CODEX_POSITION_SUPERPOWERS_INTEGRATION.md` (2026-05-04). Position:

- Do **not** vendor full `obra/superpowers` into the main playbook.
- For v1.3, propose a small layered addition:
  - `BEGINNER_AI_DEVELOPMENT.md` — plain-language workflow for non-engineer builders.
  - `SUPERPOWERS_INTEGRATION.md` — bridge: if Superpowers is installed, which skills to use when; otherwise follow the manual workflow.
  - `templates/beginner-dashboard/AGENTS.md` — copyable starter for dashboard/business-tool projects.
- Reuse Superpowers ideas (brainstorming-before-code, writing-plans, systematic-debugging, verification-before-completion, code review for medium/high risk) as principles, not as copied skill files.

Open question for Claude Code: write the v1.3 proposal now, or wait for one real beginner-dashboard trial first. Codex's bias: write now, merge minimal.

Decision needed from the user before any v1.3 work begins.

### Thread B — Backlog from v1.1.0 era, still valid

Not active work, recorded for after the third real WK use (per `CODEX_SYNTHESIS.md` "automate after the third repeat" rule):

- Possible future skill: `kraftmine:checkpoint` — only after the manual procedure has been used three or more times and proves repeatable.
- Possible future skill: `kraftmine:bootstrap` — only when starting a new project from scratch and the activation procedure has matured.
- Possible future hook: lint-on-edit, tests-on-domain-change — only after manual run patterns prove repetitive.
- Telegram-based unified council via OpenClaw — discussed, not committed.

## How to resume in a new session

Open Claude Code in this folder (`~/Desktop/claude-codex-playbook/`). The local `CLAUDE.md` gives the new session context automatically.

If you want to be explicit, paste this into the new session:

```text
Read in this order:
1. CURRENT_BATCH.md (current state)
2. CHANGELOG.md (recent versions)
3. GOVERNANCE.md (how this playbook changes)
4. README.md (what this is)

Then check the open threads in CURRENT_BATCH.md before proposing new work.
```

That's enough to reload context.

## What lives elsewhere (and should not be duplicated here)

- The actual rules: `AI_WORKING_RULES.md`
- The actual workflow: `WORKFLOW.md`
- The actual lessons: `LESSONS_FROM_WK.md`
- Wild Kamchatka project work: `~/wild-kamchatka-dashboard/.planning/coordination/`

This file (`CURRENT_BATCH.md`) is a pointer to active work, not a copy of the work itself.

## Last verified

- 2026-05-03 — v1.2.0 pushed (workflow refinements + genericization).
- 2026-05-03 — v1.2.1 pushed (Lesson 12).
- 2026-05-06 — v1.2.2 pushed (Lesson 13).
