# Workflow: The User + Claude Code + Codex

This is the practical collaboration model.

The goal is not hierarchy. Claude Code and Codex work as peers with different strengths.

## Roles

## The User

Owns:

- business goal
- product priority
- final taste/UX approval
- manual check when human judgment is needed

Should not need to own:

- architecture safety
- backup mechanics
- test selection
- deploy mechanics
- deciding whether a file is too large
- coordinating agent handoffs

## Claude Code

Best used for:

- orchestration and planning
- architecture review
- cross-agent review
- writing/refining project rules
- evaluating tradeoffs
- risk detection before expensive work
- second opinion before risky work

## Codex

Best used for:

- implementing code changes
- debugging with terminal/browser tools
- adding tests
- build/deploy verification
- live smoke checks
- keeping local files and coordination docs updated

## GPT-5.5 / Opus

Best used for:

- high-level design critique
- alternative architecture proposals
- product strategy
- reviewing playbooks and rules
- resolving expensive disagreements between Claude Code and Codex

Use them when the decision is ambiguous, expensive to reverse, or when Claude Code and Codex disagree after one focused exchange.

## 80/20 Boundary

Default split:

- Claude Code orchestrates/reviews.
- Codex builds/verifies/ships.

The boundary is not absolute:

- Claude Code may implement small safe edits when it is the fastest path.
- Codex may challenge strategy or propose architecture when code reality exposes risk.
- Either agent may stop work if the current plan creates avoidable debt, weak rollback safety, or hidden product risk.

## Default Loop

1. User states product goal.
2. Agent classifies risk.
3. For low-risk work, agent implements directly.
4. For medium-risk work, agent gives a short plan and implements after context check.
5. For high-risk work, agent creates checkpoint and asks for confirmation if tradeoffs are non-obvious.
6. Agent verifies.
7. Agent reports only the useful outcome.

## Writer / Reviewer Loop

Use this as the default for medium/high-risk work.

Use it when changing:

- finance, stock, auth, permissions, data model, deploy process
- large files or module boundaries
- redesign phases
- dependencies
- how roles see or share data

Recommended flow:

1. Writer drafts the plan or implementation.
2. Reviewer checks risks, simplification, missing tests, and rollback.
3. Writer accepts only useful feedback.
4. The user receives a concise decision summary, not raw agent debate unless requested.

Good default:

- Claude Code reviews plans and architecture.
- Codex implements, verifies, deploys, and reports.

### Pre-Work Handoff (medium/high risk)

For planned medium/high-risk work, Writer creates a short handoff before substantive implementation begins: goal, risk classification, likely files, expected verification, and deploy expectation. Reviewer acknowledges or pushes back before work starts.

Exception: urgent production hotfixes may proceed immediately, but Writer must record the reason and request retrospective review before the checkpoint/deploy is considered closed.

### Activation As Its Own Task

When activating the playbook in a new project, treat activation itself as a scoped task — separate from any substantive code work the user requested. See `HOW_TO_USE.md` ("Minimal Project Activation Checklist") for the full procedure.

## Handoff Contract

When Claude Code hands work to Codex, the handoff should include:

- goal
- risk level
- constraints
- likely files/areas touched
- tests/build/smoke expected
- deploy expectation
- known open questions

When Codex reports back, the report should include:

- what changed
- what was verified
- whether it was deployed
- backup/rollback point
- unresolved risks
- what the user should manually test, if anything

## New Feature Discovery

For larger features, Claude Code should interview the user before writing a spec.

This is the single most leveraged step in the workflow. Half of all rework comes from skipping it. The non-engineer user often describes a feature at the UI layer ("a button that does X") when the real questions are about data, roles, and edge cases. The interview surfaces those before code is written.

### When required

- new feature touching more than one screen
- new feature touching money, stock, customers, audit log, or auth
- a workflow change visible to more than one role
- a feature where "broken" would be expensive (financial loss, lost data, lost trust)

### When skipped

- typo fixes, copy edits, small UI tweaks
- bugfixes with a known scope
- single-screen tweaks that do not touch shared data

### Required questions before code

Cover all of these. Stop and ask if any are unclear:

1. **Users and roles** — who triggers this? Which role(s) see what? Is there an admin/owner view that differs from operator/seller?
2. **Data** — what gets created, read, updated, or deleted? Is any of it money, stock, customer, or audit-trail data?
3. **Screens** — which screens are affected? Is the same concept already rendered somewhere else, by another role? (See `LESSONS_FROM_WK.md` Lesson 13 — do not silently fork.)
4. **Permissions** — who can do this and who must not be able to do this?
5. **Edge cases** — what happens with empty input, partial input, duplicates, two users acting at the same time, offline state?
6. **What would feel broken** — describe the failure mode in plain language. ("If a seller submitted twice, would the customer be charged twice?")
7. **What can be deferred** — is there a smaller version of this that is still useful? What is the must-have vs. nice-to-have split?
8. **Manual workflow today** — how does the user do this without the feature? Sometimes the answer reveals the feature is the wrong solution.

### Approval to proceed

After the interview, the agent writes a short spec or plan that captures the answers. The user confirms before code starts. The spec lives in the active project's `.planning/coordination/` folder.

Trivial fixes do not require this loop. When in doubt, do the interview — five minutes of questions saves an hour of rework.

## Deploy Loop

Deploys should follow `PLAYBOOK_DEPLOY.md`.

The user should not have to ask:

- "Did you deploy?"
- "What bundle is live?"
- "Is there a backup?"
- "What should I test?"

The final report should include those answers.

## Tool Use

Use local filesystem and terminal first for repo truth.

Use browser tools for UI smoke checks.

Use GitHub tools when:

- the repo/PR/CI state matters
- publishing or reviewing remote work
- inspecting issues or PR feedback

Search for new skills/tools only when a repeated workflow is painful or currently impossible.

Hooks are useful only for checks that must happen every time. Skills are useful only for repeatable procedures with a clear trigger and outcome.

Use `/clear` between unrelated tasks when context from the previous task may confuse the next one.

Use subagents for codebase investigation that can run in parallel and does not need to clutter the main conversation. Keep final implementation responsibility with the current working agent unless explicitly handed off.
