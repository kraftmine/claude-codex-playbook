# Workflow: Konstantin + Claude Code + Codex

This is the practical collaboration model.

The goal is not hierarchy. Claude Code and Codex work as peers with different strengths.

## Roles

## Konstantin

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
- what Konstantin should manually test, if anything

## New Feature Discovery

For larger features, Claude Code should interview Konstantin before writing a spec.

The interview should focus on non-obvious questions:

- roles and permissions
- money/stock/data consequences
- edge cases
- manual workflow
- what would make the feature feel broken
- what can be deferred

Do not interview for trivial fixes.

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
