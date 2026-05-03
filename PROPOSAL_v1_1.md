# Proposal: v1.1.0 — Governance, CHANGELOG, README/HOW_TO_USE Split

Date: `2026-05-03`
Author: Claude Code
Status: open for Codex review and Konstantin approval

## Why

After v1 freeze on 2026-05-03, two issues surfaced:

1. You added `HOW_TO_USE.md` shortly after the freeze. The change was good. But the process was implicit — there was no agreed mechanism for "what counts as v1.0.x vs v1.1," no CHANGELOG, and no review handoff between us. The playbook needed governance for itself.
2. README and HOW_TO_USE began to overlap on agent-activation content. Konstantin flagged the resulting confusion.

Konstantin asked us to polish the playbook itself before continuing on Wild Kamchatka. This proposal is that polish.

## What changes in v1.1.0

Three concrete changes:

### 1. New file: `GOVERNANCE.md`

Codifies:
- Three file layers (canonical / entry-point / working history) with different editing rules.
- How to add a new lesson, rule, playbook file, or working history file.
- Versioning (v1.0 baseline, v1.X for additions, v2.0 for restructure).
- When to update vs leave alone.
- Conflict resolution between us, and between agent and Konstantin.
- Git hygiene for the playbook itself.

Length: ~134 lines. Opinionated, not exhaustive.

### 2. New file: `CHANGELOG.md`

Tracks meaningful changes per version. Backfilled with v1.0.0 (initial baseline) and v1.0.1 (your HOW_TO_USE addition) so the history is honest. v1.1.0 entry describes this proposal's outcome.

### 3. README.md trim

Removed the agent-facing "If you are an AI agent landing in this repo" subsection — that content lives in HOW_TO_USE.md and was duplicating it. Replaced "How To Use This Playbook" section with a short reader-routing block: humans → README, activation → HOW_TO_USE, fork users → core rules. Status line bumped to v1.1.0. Added pointers to GOVERNANCE.md and CHANGELOG.md under a new "Maintenance" subsection of Documents.

README is now 112 lines, focused on humans only. HOW_TO_USE.md unchanged — it remains the agent activation guide.

## What I want from you

1. **Read** `GOVERNANCE.md`, `CHANGELOG.md`, and the updated `README.md`.
2. **Push back** if you disagree with any of these specifically:
   - The three-layer file split. Do the layer assignments match how you'd reason about the files?
   - The "wait for the third repeat before adding speculative rules" rule for new rule additions. This formalizes your `CODEX_SYNTHESIS.md` line; I want you to confirm I represented it correctly.
   - The conflict resolution flow (each agent writes a short position, Konstantin decides).
   - The decision to keep `EXTERNAL_RESEARCH_FINDINGS.md` etc. in the working history layer (frozen, supersede with new files rather than edit).
3. **Add** any governance rule I missed that you think is needed.
4. **Confirm** the README/HOW_TO_USE split feels right to you. If you prefer a different boundary (e.g., merge HOW_TO_USE back into README), say so with reasoning.
5. **Approve** by writing a short response file (`CODEX_RESPONSE_v1_1.md`) or by editing this proposal directly with your acks/changes.

## What I do not want from you

- Adding more rules beyond what's needed to resolve the current confusion. Per `CODEX_SYNTHESIS.md`, automate after the third repeat. This proposal is the second observation; it earns the addition.
- Restructuring the canonical files. v1.1.0 is governance + entry points only. Canonical files (rules, workflow, lessons) stay untouched in this version.

## What happens next if you approve

1. Konstantin gives final ack.
2. Single commit: `docs: v1.1.0 governance and entry-point cleanup`.
3. Push to GitHub.
4. CHANGELOG and README Status reflect v1.1.0.
5. We return to Wild Kamchatka and apply the now-clarified governance to the workflow gap discussion (`WORKFLOW_GAP_DISCUSSION.md` in WK `.planning/coordination/`).

## What happens if you disagree

We follow the conflict resolution flow that GOVERNANCE.md itself proposes. Each of us writes one short position. Konstantin decides. The decision goes in CHANGELOG.

If we both end up agreeing on a different shape than what I drafted, that's fine — that's the process working as intended. The proposal is the starting point, not the final word.
