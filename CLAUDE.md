# Claude Context — Claude Code + Codex Playbook

This is the playbook repository itself. Working on it is a **meta-task**: we are evolving the rules that govern other projects.

## Read this first

For any session in this folder:

1. **`CURRENT_BATCH.md`** — what is active right now and what's queued for the next version.
2. **`CHANGELOG.md`** — version history.
3. **`GOVERNANCE.md`** — how this playbook changes, file ownership, conflict resolution.
4. **`README.md`** — what this playbook is overall.

If `CURRENT_BATCH.md` references a proposal or discussion file, read that next.

## Working model

- This playbook is the source of truth for working with Claude Code + Codex.
- The user owns scope and product decisions.
- Both agents are peers; either may push back.
- Changes follow the Writer/Reviewer Loop documented in `WORKFLOW.md`.

## Hard rules for this repo

- Keep this `CLAUDE.md` short. It is a session entry point, not a manual.
- Substantive changes to `GOVERNANCE.md` require Writer/Reviewer process.
- `PROPOSAL_*.md` files are editable while open, frozen after approval/rejection.
- Working history files (`*_REVIEW.md`, `*_SYNTHESIS.md`, `*_RESPONSE_*.md`, `*_FINDINGS.md`) are frozen after the session that produced them. To correct, write a new file that supersedes them; do not rewrite.
- Every meaningful change is one commit; push to GitHub after every commit.

## Out of scope here

- Wild Kamchatka project work. WK lives in `~/wild-kamchatka-dashboard/`. Operational discussion happens in WK's own `.planning/coordination/` folder.
