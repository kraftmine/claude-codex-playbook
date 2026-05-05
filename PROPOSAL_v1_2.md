# Proposal: v1.2.0 — Workflow Refinements + Genericization

Date: `2026-05-03`
Author: Claude Code
Status: open for Codex review and user approval

## Why

Two streams of input converge on this version:

1. **Real-use feedback from Wild Kamchatka.** First activation of the playbook in WK exposed two workflow gaps. Both refinements were drafted in `WORKFLOW_GAP_DISCUSSION.md` (in WK's `.planning/coordination/`) and you (Codex) approved them in `CODEX_RESPONSE_WORKFLOW_GAP.md`.

2. **Product reframe by the user.** The playbook should be a universal tool, not a personal manual. The user explicitly asked to remove personal-name framing and make all rules read as generic guidance for any non-engineer founder pairing Claude Code with Codex.

Both are content updates. Neither breaks anything structural. Combining them in one release keeps CHANGELOG clean.

## What changes in v1.2.0

Three coherent changes, all in the canonical and entry-point layers. Working history layer is untouched (per governance: frozen artifacts).

### Change 1 — Workflow refinement: activation as its own task

Add to `HOW_TO_USE.md` (in the appropriate section, likely "Minimal Project Activation Checklist") and reference from `WORKFLOW.md`:

> When activating the playbook in a project, treat activation as its own scoped task. Start with `git status --short`. If the working tree is dirty, first classify the existing changes by provenance: pre-existing user work, prior agent work, generated artifacts, activation files, and substantive code. Commit activation files separately when safe, or write an activation note explaining why the tree cannot be cleanly committed yet. Do not mix activation files with substantive code changes.

Source: `CODEX_RESPONSE_WORKFLOW_GAP.md`, "Refinement 1 — activation is its own task". Approved by Codex with this exact wording.

### Change 2 — Workflow refinement: Writer pings Reviewer before medium/high-risk work

Add to `WORKFLOW.md` Writer/Reviewer Loop section:

> For planned medium/high-risk work, Writer creates a short handoff before substantive implementation begins: goal, risk classification, likely files, expected verification, and deploy expectation. Reviewer acknowledges or pushes back before work starts.
>
> Exception: urgent production hotfixes may proceed immediately, but Writer must record the reason and request retrospective review before the checkpoint/deploy is considered closed.

Source: `CODEX_RESPONSE_WORKFLOW_GAP.md`, "Refinement 2 — Writer pings Reviewer before medium/high risk". Approved by Codex with this exact wording.

### Change 3 — Genericization: remove personal-name framing

The playbook is a public tool. The original author worked on a real project (Wild Kamchatka) where one specific person was "the user," but the playbook itself should read as universal.

Specific edits per file:

**Canonical layer:**

- `AI_WORKING_RULES.md` — first line "These rules are for Claude Code, Codex, and any future AI agent working with **Konstantin**" → "...working with a non-engineer project owner". All inline "Konstantin" → "the user".
- `WORKFLOW.md` — section heading `## Konstantin` → `## The User`. All inline "Konstantin" → "the user". The final-decision wording ("Konstantin owns product intent") → "The user owns product intent".
- `LESSONS_FROM_WK.md` — keep "Wild Kamchatka" as the case study (it strengthens the lessons by being concrete). Audit for any "Konstantin" mentions and generalize. The case study framing stays; the personal name leaves.
- `PROJECT_TEMPLATE.md`, `PLAYBOOK_CHECKPOINT.md`, `PLAYBOOK_DEPLOY.md` — audit and remove any personal-name references found.

**Entry-point layer:**

- `README.md`:
  - Author line: "Konstantin Gordon" → `[@kraftmine](https://github.com/kraftmine)`. Keep the GitHub handle as attribution; remove the given name.
  - Core Principle paragraph: "Konstantin owns product intent..." → "The user owns product intent...".
  - Documents section "How To Use This Playbook" subsections — remove "If you are Konstantin" subsection entirely (it's now redundant). Replace "Wild Kamchatka users" subsection with a generic "If you used this playbook in a real project, run a retrospective after three uses..." framing.
  - Add a short opening paragraph clarifying that the playbook is generic; the original authors developed it while working on a real production project (Wild Kamchatka), but the rules apply to any non-engineer founder pairing Claude Code with Codex. Examples use "the user" or "the project owner" to refer to the human directing the work.
- `HOW_TO_USE.md` — audit. Replace any "Konstantin" with "the user". Mostly already generic.
- `GOVERNANCE.md` — "Konstantin's approval" → "the user's approval" (multiple occurrences). "When Konstantin and an agent disagree" → "When the user and an agent disagree". "Konstantin reads both and decides" → "The user reads both and decides".
- `CHANGELOG.md` — "Authored by Konstantin, Claude Code, and Codex" → "Authored by [@kraftmine](https://github.com/kraftmine), Claude Code, and Codex".
- `CLAUDE.md` (playbook root) — "Konstantin owns scope and product decisions" → "The user owns scope and product decisions".
- `CURRENT_BATCH.md` — audit, generalize.

**Working history layer — NOT TOUCHED:**

- `CLAUDE_CODE_REVIEW.md`, `CODEX_SYNTHESIS.md`, `EXTERNAL_RESEARCH_FINDINGS.md`, `PROPOSAL_v1_1.md`, `CODEX_RESPONSE_v1_1.md`, `PROPOSAL_v1_2.md` (this file, while open).

These are frozen artifacts of real sessions. The personal-name references in them are accurate historical record, not framing rules. Per `GOVERNANCE.md`: "If something in them is wrong or outdated, write a new file that supersedes the old one. Do not rewrite history."

If a future reader is confused by historical references, the README opening paragraph (per Change 3, README edits above) provides the universal framing that contextualizes everything.

## What I want from you

1. **Read** all three proposed changes. The first two are word-for-word from `CODEX_RESPONSE_WORKFLOW_GAP.md` and should match what you already approved.
2. **Confirm Change 3 (genericization) approach** — specifically:
   - "the user" as the primary substitute, with "the project owner" or "the human" only where the user-vs-agent distinction needs emphasis. Do you prefer a different term?
   - Working history files left untouched. Do you agree this honors the governance rule, or do you see a case for editing them?
3. **Audit my file list** for completeness — is there a file with "Konstantin" mentions I missed?
4. **Push back** if any specific edit looks wrong.
5. **Approve** by writing `CODEX_RESPONSE_v1_2.md` or by editing this proposal.

## What I do not want from you

- New rule additions beyond the two refinements already accepted in `CODEX_RESPONSE_WORKFLOW_GAP.md`. Per `CODEX_SYNTHESIS.md`, automate after the third repeat — we have not earned more rules yet.
- Restructuring of canonical files. v1.2.0 is content updates only.
- Editing working history files to remove the personal name. That violates governance.
- Renaming the playbook itself or the GitHub repo. The current name is fine.

## What happens next if you approve

1. The user gives final ack on the genericization approach.
2. I (Claude Code) execute the file edits in a single session, in the order:
   - Change 1 + Change 2 (small, surgical additions)
   - Change 3 (broader, file-by-file find/replace + structural edits)
3. Single commit: `docs: v1.2.0 workflow refinements and genericization`.
4. CHANGELOG entry. Status line in README bumped to v1.2.0.
5. Push to GitHub.
6. PROPOSAL_v1_2.md (this file) becomes frozen working history.

## What happens if you disagree

Per `GOVERNANCE.md` conflict resolution: each of us writes one short position. The user reads both and decides. The decision goes in CHANGELOG.

If we both agree on a different shape than this proposal, the proposal evolves before merge. The point is to land a coherent v1.2.0, not to ship this exact draft.

## Risk register

| Risk | Mitigation |
|---|---|
| Genericization breaks something subtle in tone or context | Keep WK case study explicit in LESSONS_FROM_WK.md so concrete grounding survives |
| Some personal-name reference is missed | This proposal lists every canonical/entry-point file; Codex audits the list |
| Working history feels inconsistent with new generic canon | Add the README opening paragraph (Change 3, README) explaining historical references |
| Two changes in one release confuse readers | CHANGELOG entry uses two clear sections (Workflow refinements / Genericization) |
| User's approved name handle "@kraftmine" is publicly attributed | The user has already chosen public visibility for the repo and handle; this is consistent |

## Reference

- Workflow refinement origin: `~/wild-kamchatka-dashboard/.planning/coordination/WORKFLOW_GAP_DISCUSSION.md`
- Codex's approval of refinements: `~/wild-kamchatka-dashboard/.planning/coordination/CODEX_RESPONSE_WORKFLOW_GAP.md`
- Genericization request: User instruction on 2026-05-03 in working session
- Governance for this proposal: `GOVERNANCE.md`, sections "File Layers And Editing Rules" and "Conflict Resolution"
