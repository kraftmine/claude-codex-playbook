# Proposal: v1.3.0 — Beginner Layer + Brainstorming + Debug Protocol

Date: `2026-05-06`
Author: Claude Code
Status: approved on arrival (converged via prior Writer/Reviewer round)

## Why

Two converging needs:

1. **The user's framing**: the playbook should be usable by non-engineers (the user, his sister, friends). It needs a short doc the human can read to understand how to drive AI coding agents safely — not another procedure manual for the agent.
2. **Observed gaps from Wild Kamchatka**: the hotfix series (2026-05-01 to 2026-05-03) showed debugging without a fixed protocol becomes ad-hoc and slow; the 24 dorabotki batch (2026-03-29) showed half the items were re-specified post-facto because no upfront discovery happened.

Codex independently raised whether to vendor `obra/superpowers` into the playbook. Both positions filed; converged on a smaller scope.

## What's converged

The Writer/Reviewer round produced three artifacts in working history:

- `CODEX_POSITION_SUPERPOWERS_INTEGRATION.md` (2026-05-04) — original layered model with three new files plus a `templates/beginner-dashboard/` folder.
- `CLAUDE_POSITION_SUPERPOWERS_INTEGRATION.md` (2026-05-05) — counter-position arguing for a smaller agent-agnostic scope, no third-party API translation layer, no templates folder, beginner doc rewritten for the human user.
- `CODEX_RESPONSE_SUPERPOWERS_INTEGRATION.md` (2026-05-06) — Codex converged on the smaller scope, pulling in one item from his original list (dashboards subsection in existing `PROJECT_TEMPLATE.md`) which Claude Code had already named as the acceptable compromise.

This proposal documents the converged scope. No further round of debate.

## What changes in v1.3.0

Two new files plus three surgical edits.

### Add 1 — `WORKING_WITH_AGENTS.md` (new, user-facing)

Audience: the project owner, not the agent.

Coverage: what the user is actually doing (not "managing developers"); risk levels in plain language; how to read an agent report; when to say "stop, slow down" (signs of flailing); what only the user decides (product intent, money, taste); what the user does not need to track; two habits that save hours; trust calibration; recovery path when things go wrong.

This is the doc the user can hand to his sister, to a friend, or read himself when the agent's behavior feels off.

### Add 2 — `PLAYBOOK_DEBUG.md` (new)

Borrowed in spirit from Superpowers' `systematic-debugging`, written in our own voice. No dependency on any plugin or skill name.

Steps: reproduce → read the error carefully → inspect recent changes → form one hypothesis at a time → make the smallest fix at the root cause → verify the original symptom is gone.

Includes a named anti-patterns section (stab-and-pray, symptom suppression, premature refactor, patching one fork — cross-references `LESSONS_FROM_WK.md` Lesson 13, "Looks fine to me") and an escalation step (hand the problem to the other agent with what is known) so the agent does not flail in the same context.

### Modify 1 — `WORKFLOW.md` "New Feature Discovery"

Promote from a one-line note to a full section. Explicit "when required" / "when skipped" criteria. Eight required questions (users/roles, data, screens, permissions, edge cases, what would feel broken, what can be deferred, manual workflow today). Approval-to-proceed step. Cross-reference to Lesson 13 to prevent silent forking when a concept is rendered for multiple roles.

This is the brainstorming-before-code value from Superpowers, captured in our own voice and grounded in a real WK observation (24 dorabotki where half were re-specified).

### Modify 2 — `PROJECT_TEMPLATE.md` "Dashboards And Business Tools"

A new subsection in the existing template, not a new file or folder. Captures the recurring starter facts for the most common project shape a non-engineer founder builds: internal dashboards, finance tools, CRMs, inventory systems, ops consoles.

Sections: roles and their views, private/customer data, financial/customer-facing actions, metrics with formulas and source-of-truth pointers, deploy expectations during business hours.

This is Codex's one carry-over from his original position: dashboard guidance does belong somewhere, just not in a `templates/` folder.

### Modify 3 — `README.md` Acknowledgements

`obra/superpowers` (MIT licensed) is now explicitly named as an adapted-principles influence (lifted from "indirect influences" to direct, with a link). The README's Documents section is updated to list `WORKING_WITH_AGENTS.md` and `PLAYBOOK_DEBUG.md`.

### What is **not** in v1.3

- No vendored Superpowers.
- No `SUPERPOWERS_INTEGRATION.md` (would tie us to a third-party API surface).
- No `templates/` folder (template sprawl risk).
- No 12-step beginner methodology document distinct from `WORKING_WITH_AGENTS.md`.
- No mandatory Superpowers skill-name references in canonical workflow.

## Risk register

| Risk | Mitigation |
|---|---|
| `WORKING_WITH_AGENTS.md` reads as too informal or too short | Iterate on real reader feedback (the user, then a non-engineer reader); easy to refine in v1.3.1 |
| `PLAYBOOK_DEBUG.md` overlaps with PLAYBOOK_CHECKPOINT.md/PLAYBOOK_DEPLOY.md | Each playbook has a different trigger condition stated up front, so the agent can pick correctly |
| Brainstorming questions feel heavy for medium-risk work | Section is explicit about "when required" vs "when skipped"; trivial fixes do not invoke it |
| Dashboards subsection invites copying-by-default | Subsection explicitly says "fill in if your project is a dashboard" — opt-in, not auto |

## What happens next

1. Single commit: `docs: v1.3.0 beginner layer, brainstorming, debug protocol`.
2. CHANGELOG entry, README status bumped to v1.3.0.
3. Push to GitHub `main`.
4. `PROPOSAL_v1_3.md` (this file) and the three Writer/Reviewer artifacts (`CODEX_POSITION...`, `CLAUDE_POSITION...`, `CODEX_RESPONSE...`) freeze as working history.
5. After v1.3 is live, wait for one real beginner-dashboard activation (e.g., Handara or a sister/friend project) before considering v1.4.

## Reference

- Codex original position: `CODEX_POSITION_SUPERPOWERS_INTEGRATION.md`
- Claude Code counter-position: `CLAUDE_POSITION_SUPERPOWERS_INTEGRATION.md`
- Codex convergence response: `CODEX_RESPONSE_SUPERPOWERS_INTEGRATION.md`
- WK observations grounding the gaps: hotfix retrospective (`~/wild-kamchatka-dashboard/.planning/reviews/REVIEW_HOTFIX_SERIES_2026-05-01_to_2026-05-03.md`), 24 dorabotki batch (memory `wk-24-tasks.md`)
- Governance: `GOVERNANCE.md` sections "File Layers And Editing Rules" and "Conflict Resolution"
