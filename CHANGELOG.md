# Changelog

This file tracks meaningful changes to the playbook.

For governance and update process, see [`GOVERNANCE.md`](GOVERNANCE.md).

## v1.3.0 — 2026-05-06

Added.

- `WORKING_WITH_AGENTS.md` — pocket guide for non-engineer project owners. Plain-language coverage of risk levels, how to read agent reports, when to say "stop, slow down," what only the user decides, what they do not need to track. This is the user-facing companion to `AI_WORKING_RULES.md` (which is agent-facing).
- `PLAYBOOK_DEBUG.md` — root-cause debugging protocol borrowed in spirit from Superpowers' `systematic-debugging`, written in our own voice. Reproduce → read error → inspect recent changes → one hypothesis at a time → smallest fix at root cause → verify symptom is gone. Anti-patterns named (stab-and-pray, symptom suppression, premature refactor, patching one fork).

Changed.

- `WORKFLOW.md` "New Feature Discovery" — promoted from a one-line note to a full section with eight required questions (users/roles, data, screens, permissions, edge cases, what would feel broken, what can be deferred, manual workflow today), explicit "when required" / "when skipped" criteria, and approval-to-proceed loop. Cross-references Lesson 13.
- `PROJECT_TEMPLATE.md` — added a "Dashboards And Business Tools" subsection covering the recurring starter facts for internal dashboards / finance tools / CRMs / inventory systems: roles and their views, private/customer data, financial/customer-facing actions, metrics with formulas and source of truth, deploy expectations.
- `README.md` — Acknowledgements now name `obra/superpowers` (MIT) explicitly as an adapted-principles influence; removed it from "indirect influences" since it is now directly named in the playbook content. Documents section updated to list `WORKING_WITH_AGENTS.md` and `PLAYBOOK_DEBUG.md`.

Process.

- Followed the Writer/Reviewer Loop end-to-end. Codex wrote the original v1.3 position (`CODEX_POSITION_SUPERPOWERS_INTEGRATION.md`, 2026-05-04) proposing a layered model with three new files plus a `templates/beginner-dashboard/` folder. Claude Code wrote a counter-position (`CLAUDE_POSITION_SUPERPOWERS_INTEGRATION.md`, 2026-05-05) arguing for a smaller scope agnostic to Superpowers. Codex converged on the smaller scope (`CODEX_RESPONSE_SUPERPOWERS_INTEGRATION.md`, 2026-05-06), pulling in one item from his original list — a dashboards subsection in the existing `PROJECT_TEMPLATE.md` rather than a new templates folder — which Claude Code had already named as the acceptable compromise.
- Final scope: 2 new files + 3 surgical edits, agnostic to any third-party plugin API, no template folders, Superpowers named in acknowledgements only.
- `PROPOSAL_v1_3.md` records the converged scope as the canonical change record.

## v1.2.2 — 2026-05-06

Added.

- `LESSONS_FROM_WK.md` Lesson 13 — Forked Implementations Of The Same Concept Drift Apart. Sourced from user observation in Wild Kamchatka: warehouse browsing was rendered two ways (owner cross-warehouse toggle vs. Marina drill-in with per-warehouse tabs) and "new sale" entry was implemented differently in Marina's view vs. sellers' view. Each fork carried its own bugs and drifted independently.
- Cross-references from Lesson 13 to Lesson 1 (monoliths hide forks) and Lesson 7 (agent must flag structural drift pre-implementation).

Process.

- Lesson addition per `GOVERNANCE.md` — observed real failure, severity high, no Writer/Reviewer required.

## v1.2.1 — 2026-05-03

Added.

- `LESSONS_FROM_WK.md` Lesson 12 — localStorage Cannot Be A Source Of Truth For Server State. Sourced from the Wild Kamchatka hotfix chain retrospective (`~/wild-kamchatka-dashboard/.planning/reviews/REVIEW_HOTFIX_SERIES_2026-05-01_to_2026-05-03.md`). No approval required per `GOVERNANCE.md` lesson-addition rule.
- Cross-reference between Lesson 2 (role-shared data, visibility side) and Lesson 12 (creation side) so both lessons strengthen each other.

Process.

- Brief from Claude Code (`CODEX_BRIEF_LESSON_12.md`) frozen as working history alongside the lesson.

## v1.2.0 — 2026-05-03

Workflow refinements (earned by first real activation in Wild Kamchatka).

- `HOW_TO_USE.md` — added "activation as its own scoped task" guidance to the Minimal Project Activation Checklist: classify dirty-tree changes by provenance, commit activation files separately, do not mix with substantive code.
- `WORKFLOW.md` — added Pre-Work Handoff subsection to the Writer/Reviewer Loop: for planned medium/high-risk work, Writer creates a short handoff (goal, risk, likely files, expected verification, deploy expectation) and Reviewer acks before implementation begins. Urgent production hotfixes may proceed immediately but require retrospective review. Cross-references the activation rule in `HOW_TO_USE.md`.

Genericization (the playbook is a public tool, not a personal manual).

- Removed personal-name framing from canonical and entry-point files. "Konstantin" → "the user" (or "the project owner" where business ownership is the point) across `AI_WORKING_RULES.md`, `WORKFLOW.md`, `GOVERNANCE.md`, `CLAUDE.md`, `CURRENT_BATCH.md`, and `README.md`.
- `README.md` — author line now `[@kraftmine](https://github.com/kraftmine)` (handle, no given name); added a short opening paragraph explicitly framing the playbook as generic and naming Wild Kamchatka as the case study; Operating Model bullet (the one Codex flagged) now reads "The user — product owner, not engineering dispatcher"; replaced the "Wild Kamchatka users" subsection with a generic "If you used this playbook in a real project" retrospective trigger.
- `WORKFLOW.md` — title "Workflow: Konstantin + Claude Code + Codex" → "Workflow: The User + Claude Code + Codex"; section heading `## Konstantin` → `## The User`.
- `LESSONS_FROM_WK.md`, `PROJECT_TEMPLATE.md`, `PLAYBOOK_CHECKPOINT.md`, `PLAYBOOK_DEPLOY.md` — audited; the Wild Kamchatka case study stays (it grounds the lessons concretely), no personal-name references found to remove.
- Working history layer (`CLAUDE_CODE_REVIEW.md`, `CODEX_SYNTHESIS.md`, `EXTERNAL_RESEARCH_FINDINGS.md`, `PROPOSAL_v1_1.md`, `CODEX_RESPONSE_v1_1.md`) intentionally **not edited** — frozen artifacts per `GOVERNANCE.md`. The README opening paragraph now contextualizes any historical references for new readers.

Process.

- Followed the Writer/Reviewer Loop. Claude Code drafted (`PROPOSAL_v1_2.md`), Codex approved with one explicit implementation note (`CODEX_RESPONSE_v1_2.md`): the Operating Model bullet in README must be updated explicitly during the README pass — folded in.
- Proposal artifact (`PROPOSAL_v1_2.md`) is now frozen as working history.

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

Initial frozen baseline. Authored by [@kraftmine](https://github.com/kraftmine), Claude Code, and Codex.

Includes.

- `AI_WORKING_RULES.md` — 14 rules for Claude Code, Codex, and any future AI agent.
- `LESSONS_FROM_WK.md` — 11 named lessons from the Wild Kamchatka refactor.
- `WORKFLOW.md` — roles, default loop, Writer/Reviewer pattern, handoff contract.
- `PROJECT_TEMPLATE.md` — minimal per-project context with day 0 file requirements.
- `PLAYBOOK_CHECKPOINT.md` — short procedure before risky operations.
- `PLAYBOOK_DEPLOY.md` — deployment safety checklist.
- `README.md` — human-facing overview.
- Working history: `CLAUDE_CODE_REVIEW.md`, `CODEX_SYNTHESIS.md`, `EXTERNAL_RESEARCH_FINDINGS.md`.
