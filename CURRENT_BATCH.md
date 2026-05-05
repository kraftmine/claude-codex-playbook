# Current Batch — Playbook Work

Date: `2026-05-06`
Latest released version: **v1.3.0** (beginner layer + brainstorming + debug protocol)

## Where we are

The playbook is **shipped at v1.3.0** and live on GitHub: `https://github.com/kraftmine/claude-codex-playbook`.

No version is currently in flight.

Released so far:

- **v1.3.0** (2026-05-06) — added `WORKING_WITH_AGENTS.md` (user-facing pocket guide), `PLAYBOOK_DEBUG.md` (root-cause debugging protocol), expanded `WORKFLOW.md` brainstorming section to 8 required questions, added Dashboards subsection to `PROJECT_TEMPLATE.md`, named `obra/superpowers` in README acknowledgements.
- **v1.2.2** (2026-05-06) — Lesson 13: forked implementations of the same concept drift apart.
- **v1.2.1** (2026-05-03) — Lesson 12: localStorage cannot be a source of truth for server state.
- **v1.2.0** (2026-05-03) — workflow refinements (activation as own task; pre-work handoff for medium/high risk) and genericization (removed personal-name framing).
- **v1.1.0** (2026-05-03) — governance, changelog, README/HOW_TO_USE split.
- **v1.0.x** (2026-05-03) — initial frozen baseline.

## What's queued

Nothing actively in flight.

The playbook now has its first complete user-facing layer (`WORKING_WITH_AGENTS.md`), brainstorming protocol, and debug protocol. Wait for real-use feedback before the next round of changes.

### Backlog — wait for real evidence

Per `CODEX_SYNTHESIS.md` "automate after the third repeat" rule, none of the items below have earned merge yet:

- Possible future skill: `kraftmine:checkpoint` — only after the manual procedure has been used three or more times and proves repeatable.
- Possible future skill: `kraftmine:bootstrap` — only when starting a new project from scratch and the activation procedure has matured.
- Possible future hook: lint-on-edit, tests-on-domain-change — only after manual run patterns prove repetitive.
- Telegram-based unified council via OpenClaw — discussed, not committed.
- Beginner-dashboard starter (folder of files copy-pasteable into a new project) — only after two or more real beginner activations show the same starter pattern.

## How to resume in a new session

Open Claude Code in this folder (`~/Desktop/claude-codex-playbook/`). The local `CLAUDE.md` gives the new session context automatically.

If you want to be explicit, paste this into the new session:

```text
Read in this order:
1. CURRENT_BATCH.md (current state)
2. CHANGELOG.md (recent versions)
3. GOVERNANCE.md (how this playbook changes)
4. README.md (what this is)

The playbook is at v1.3.0. No version in flight.
Before proposing new work, check whether observed evidence justifies it
(per GOVERNANCE.md "When To Update vs When To Leave Alone").
```

That's enough to reload context.

## What lives elsewhere (and should not be duplicated here)

- The actual rules: `AI_WORKING_RULES.md`
- The actual workflow: `WORKFLOW.md`
- The actual lessons: `LESSONS_FROM_WK.md`
- The actual user-facing guide: `WORKING_WITH_AGENTS.md`
- Wild Kamchatka project work: `~/wild-kamchatka-dashboard/.planning/coordination/`

This file (`CURRENT_BATCH.md`) is a pointer to active work, not a copy of the work itself.

## Last verified

- 2026-05-03 — v1.2.0 pushed (workflow refinements + genericization).
- 2026-05-03 — v1.2.1 pushed (Lesson 12).
- 2026-05-06 — v1.2.2 pushed (Lesson 13).
- 2026-05-06 — v1.3.0 pushed (beginner layer, brainstorming, debug protocol).
