# Governance — How This Playbook Changes

Date: `2026-05-03`
Status: living document

## Principles

- The playbook is meant to be useful, not perfect.
- A change that prevents recurrence of a real failure is easy to merge.
- A change that adds ceremony for a hypothetical future case needs stronger justification.
- Updates are batched into version bumps, not committed in dribs and drabs.
- Default action: leave the playbook alone and use it. Update only when reality demands it.

## File Layers And Editing Rules

The playbook contains three kinds of files. Each has different editing rules.

### Canonical layer — source of truth

Files:
- `AI_WORKING_RULES.md`
- `WORKFLOW.md`
- `LESSONS_FROM_WK.md`
- `PROJECT_TEMPLATE.md`
- `PLAYBOOK_CHECKPOINT.md`
- `PLAYBOOK_DEPLOY.md`

Editing rules:
- Both agents must agree before merging changes.
- Rule changes need a short discussion file (in playbook root or in the active project's `.planning/coordination/`), a response from the other agent, and the user's approval.
- Lesson additions can be appended without discussion if the lesson is from a real, observed failure. The format must match existing entries.
- Workflow or playbook changes go through the same Writer/Reviewer process the playbook itself prescribes.

### Entry-point layer — how the playbook is consumed

Files:
- `README.md` (for humans)
- `HOW_TO_USE.md` (for AI agents)
- `GOVERNANCE.md` (this file)
- `CHANGELOG.md`

Editing rules:
- Either agent may update these without prior discussion.
- The human/agent split must stay clean. Do not put agent-activation steps in README or product description in HOW_TO_USE.
- Version-relevant changes must add a CHANGELOG entry.
- Exception: substantive changes to `GOVERNANCE.md` require the same Writer/Reviewer process as canonical files, because they change the rules for changing rules. Typo, link, and formatting fixes may be made directly.

### Working history layer — frozen after creation

Files:
- `CLAUDE_CODE_REVIEW.md`
- `CODEX_SYNTHESIS.md`
- `EXTERNAL_RESEARCH_FINDINGS.md`
- Any future `*_REVIEW.md`, `*_SYNTHESIS.md`, `*_FINDINGS.md` files

Editing rules:
- These are timestamped session artifacts. Do not edit after the session that produced them ends.
- If something in them is wrong or outdated, write a new file that supersedes the old one. Do not rewrite history.

Related case — proposals:
- `PROPOSAL_*.md` files are editable while the proposal is open (under review or pending approval).
- After approval or rejection, they become frozen working-history artifacts and follow the same rules as reviews, syntheses, and findings.

## Adding New Content

### A new lesson

Trigger: a real failure, observed at least once and judged severe enough to remember.
Process: append at the end of `LESSONS_FROM_WK.md` (or the relevant lessons file). Follow the existing format: what happened / why / rule / preventive check.
Approval: not needed for additions of real lessons. Required if the lesson contradicts an existing rule.

### A new rule

Trigger: a lesson points to a missing rule, *and* the failure has been observed in real use (not predicted).
Process: write a short proposal in `PROPOSAL_RULE_<N>.md`. Get response from the other agent. Get the user's approval. Merge into `AI_WORKING_RULES.md`. Bump version.
Wait for the third repeat before adding speculative rules.

### A new playbook file (`PLAYBOOK_*.md`)

Trigger: a procedure has been performed manually three or more times with the same shape.
Process: same as new rule.

### A new working history file

Trigger: any session that produces a useful review, synthesis, or research artifact.
Process: just write it. No review needed.
Naming: `TYPE_TOPIC.md`. Examples: `REVIEW_PHASE_1.md`, `SYNTHESIS_2026_05_03.md`, `FINDINGS_TOOL_SURVEY.md`.

## Versioning

Semantic-ish, optimized for readability:

- **v1.0** — first frozen baseline (2026-05-03).
- **v1.X** — additions to lessons, additions to working history, non-breaking rule refinements, README/HOW_TO_USE updates.
- **v2.0** — restructure of canonical files, breaking change to a rule, removal of a published rule.

`CHANGELOG.md` tracks every version with date and one-line summary. The Status line in `README.md` reflects the current version.

## When To Update vs When To Leave Alone

Update only when one of these is true:

- A rule failed to prevent something it should have.
- A workflow step was missing or unclear and caused real confusion in a real session.
- An external tool or convention we reference changed.
- A procedure has been performed manually three times and is earning a playbook slot.

Resist updating after:

- A single uncomfortable session where the playbook felt heavy (heavy may be appropriate for the risk level).
- Reading another playbook online that has cool ideas (those ideas need to prove themselves in real use first).
- A frustrating moment where a rule got in the way (the rule might be doing its job).

## Conflict Resolution

When Claude Code and Codex disagree on a proposed change:

1. Each writes their position concisely. Maximum one short doc per side.
2. The user reads both and decides.
3. The decision is recorded in `CHANGELOG.md` so future readers can see the reasoning.

When the user and an agent disagree:

- The user's product and business decisions are final.
- Engineering risk concerns from the agent must still be heard and recorded, even if overridden.
- If a flagged risk later materializes, that history earns higher weight in subsequent decisions.

## Git Hygiene For The Playbook Itself

- Each meaningful change is one commit.
- Commit messages start with the type: `rules:`, `lessons:`, `workflow:`, `docs:`, `chore:`.
- Push to GitHub after every commit. The playbook is its own backup test.
- No dirty working tree across days.

## What This Document Is Not

- Not a complete process manual. Many decisions still require judgment.
- Not enforced by tooling. Discipline lives between the agents and the human.
- Not frozen. This document evolves as the playbook learns to maintain itself.
