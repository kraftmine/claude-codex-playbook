# Current Batch — Playbook Work

Date: `2026-05-03`
Latest released version: **v1.1.0** (commit `2f921cb`, pushed to GitHub `main`)

## Where we are

The playbook is **shipped at v1.1.0** and live on GitHub: `https://github.com/kraftmine/claude-codex-playbook`.

It is being used in production for the Wild Kamchatka dashboard, which is the test bed for v1.2.0 refinements.

## What's queued for v1.2.0

Two refinements have been **proposed and accepted** in the WK project's `.planning/coordination/WORKFLOW_GAP_DISCUSSION.md` and confirmed by Codex in `CODEX_RESPONSE_WORKFLOW_GAP.md`. They are not yet merged into the playbook.

### Refinement 1 — activation is its own task

Add to `HOW_TO_USE.md` (and reference from `WORKFLOW.md`):

> When activating the playbook in a project, treat activation as its own scoped task. Start with `git status --short`. If the working tree is dirty, first classify the existing changes by provenance: pre-existing user work, prior agent work, generated artifacts, activation files, and substantive code. Commit activation files separately when safe, or write an activation note explaining why the tree cannot be cleanly committed yet. Do not mix activation files with substantive code changes.

### Refinement 2 — Writer pings Reviewer before medium/high-risk work

Add to `WORKFLOW.md` Writer/Reviewer Loop section:

> For planned medium/high-risk work, Writer creates a short handoff before substantive implementation begins: goal, risk classification, likely files, expected verification, and deploy expectation. Reviewer acknowledges or pushes back before work starts.
> Exception: urgent production hotfixes may proceed immediately, but Writer must record the reason and request retrospective review before the checkpoint/deploy is considered closed.

### Process for v1.2.0

Per `GOVERNANCE.md`, `WORKFLOW.md` is canonical and `HOW_TO_USE.md` is entry-point. Refinement 1 touches both. Refinement 2 touches canonical `WORKFLOW.md`. So:

1. Claude Code drafts both edits as `PROPOSAL_v1_2.md`.
2. Codex reviews and approves or refines.
3. The user gives final ack.
4. Single commit: `docs: v1.2.0 add activation and pre-work handoff refinements`.
5. CHANGELOG entry, version bump in README.
6. Push to GitHub.
7. Freeze v1.2.0.

## What's in the backlog

Not active work, but recorded for after v1.2.0:

- Wait for two more real WK uses before considering v1.3 refinements (per `CODEX_SYNTHESIS.md` "automate after the third repeat" rule).
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

Then continue from "What's queued for v1.2.0" in CURRENT_BATCH.md.
```

That's enough to reload context.

## What lives elsewhere (and should not be duplicated here)

- The actual rules: `AI_WORKING_RULES.md`
- The actual workflow: `WORKFLOW.md`
- The actual lessons: `LESSONS_FROM_WK.md`
- Wild Kamchatka project work: `~/wild-kamchatka-dashboard/.planning/coordination/`

This file (`CURRENT_BATCH.md`) is a pointer to active work, not a copy of the work itself.

## Last verified

- 2026-05-03 — v1.1.0 pushed; CURRENT_BATCH.md created as session-resume entry point.
