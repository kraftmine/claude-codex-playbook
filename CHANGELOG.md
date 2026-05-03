# Changelog

This file tracks meaningful changes to the playbook.

For governance and update process, see [`GOVERNANCE.md`](GOVERNANCE.md).

## v1.1.0 — 2026-05-03

Added.

- `GOVERNANCE.md` — file layers, editing rules, versioning, conflict resolution, when to update vs leave alone (drafted by Claude Code, reviewed by Codex).
- `CHANGELOG.md` — this file.

Changed.

- `README.md` — trimmed the agent-facing subsection (now lives in `HOW_TO_USE.md` only). README is now humans-only. Status line bumped to v1.1.0. Added pointers to `GOVERNANCE.md` and `CHANGELOG.md`.

Process.

- Followed the Writer/Reviewer Loop on the playbook itself. Claude Code drafted, Codex reviewed (`CODEX_RESPONSE_v1_1.md`) and contributed two refinements which were folded in:
  - GOVERNANCE.md changes are not unilateral — substantive edits require Writer/Reviewer.
  - `PROPOSAL_*.md` files are editable while open, frozen after approval/rejection.
- Proposal artifact (`PROPOSAL_v1_1.md`) is now frozen as working history.

Why.

After the v1 freeze, Codex added `HOW_TO_USE.md` without a clear merge process, and the README and HOW_TO_USE began to overlap. This release codifies the editing process and resolves the duplication so future updates do not silently fork the entry points.

## v1.0.1 — 2026-05-03

Added.

- `HOW_TO_USE.md` — agent-facing activation guide with copy-paste prompt for sending the playbook to a new agent (Codex).

## v1.0.0 — 2026-05-03

Initial frozen baseline. Authored by Konstantin, Claude Code, and Codex.

Includes.

- `AI_WORKING_RULES.md` — 14 rules for Claude Code, Codex, and any future AI agent.
- `LESSONS_FROM_WK.md` — 11 named lessons from the Wild Kamchatka refactor.
- `WORKFLOW.md` — roles, default loop, Writer/Reviewer pattern, handoff contract.
- `PROJECT_TEMPLATE.md` — minimal per-project context with day 0 file requirements.
- `PLAYBOOK_CHECKPOINT.md` — short procedure before risky operations.
- `PLAYBOOK_DEPLOY.md` — deployment safety checklist.
- `README.md` — human-facing overview.
- Working history: `CLAUDE_CODE_REVIEW.md`, `CODEX_SYNTHESIS.md`, `EXTERNAL_RESEARCH_FINDINGS.md`.
