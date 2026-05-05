# Codex Position: Superpowers Integration For Beginner Development

Date: `2026-05-04`
Author: Codex
Status: position for discussion with Claude Code

## Context

The user wants to turn this playbook into a universal beginner-friendly software development system for himself, his sister, and friends.

The current question is whether to fully copy `obra/superpowers` into this playbook, partially copy/adapt it, or keep Superpowers as an optional external plugin while this playbook remains a compact safety/process layer.

My position: do not copy all of Superpowers into the main playbook. Create a beginner workflow layer that adopts the useful Superpowers principles, plus a small integration guide for when Superpowers is installed as a real plugin/skills system.

## Recommendation

Use a layered model:

1. `BEGINNER_AI_DEVELOPMENT.md` — one plain-language workflow for non-engineer builders.
2. `AI_WORKING_RULES.md` — compact safety rules: risk, verification, structure, rollback, privacy, reporting.
3. `SUPERPOWERS_INTEGRATION.md` — when Superpowers is installed, which skills to use and when.
4. `templates/beginner-dashboard/AGENTS.md` — copyable project entrypoint for dashboards and business tools.
5. Project docs such as `docs/project-brief.md`, `docs/mvp-plan.md`, `docs/domain-rules.md`, and `docs/safety-rules.md`.

The beginner should experience this as one simple instruction:

> Work through discovery, design, planning, implementation, verification, and review. If Superpowers is installed, use its skills at the right moments. If it is not installed, follow the manual workflow in this playbook.

## Why Not Copy All Of Superpowers

Full copy has benefits:

- It is MIT licensed, so copying is allowed if copyright/license terms are preserved.
- It provides a mature methodology for brainstorming, planning, TDD, debugging, review, worktrees, and branch completion.
- It already supports multiple agent environments, including Codex and Claude Code.

But full copy also creates costs:

- It changes this repo from a small operational playbook into a larger methodology distribution.
- It risks duplication drift against upstream Superpowers.
- It may overwhelm beginners with worktrees, subagents, plugin bootstrap details, PR discipline, and meta-skills.
- Merely copying skill files is not the same as having a real Superpowers installation; the value comes from skills being triggered at the right time by the agent environment.

For this playbook, full copy should be reserved for a separate `vendor/superpowers/` or submodule-style decision, not placed into the main beginner workflow by default.

## What To Reuse From Superpowers

Reuse these ideas directly in beginner language:

### 1. Brainstorming Before Code

For new products, features, dashboards, automations, or behavior changes:

- do not jump into code
- inspect current project context
- restate the goal in plain language
- ask only necessary clarifying questions
- identify users, data, screens, permissions, and risks
- propose 2-3 approaches when there is a meaningful choice
- present a short design and get user approval before implementation

This is the most valuable Superpowers principle for beginners.

### 2. Writing Plans Before Implementation

Before coding a medium/high-risk task:

- map files to create or modify
- define one clear responsibility per file
- prefer small focused files over giant files
- break the work into small independently verifiable tasks
- include verification steps for each task
- checkpoint or commit at meaningful boundaries

This overlaps strongly with our existing anti-monolith and git-hygiene rules.

### 3. Systematic Debugging

For bugs and test failures:

- reproduce the problem
- read the error carefully
- inspect recent changes
- trace the failing data or behavior to root cause
- form one hypothesis at a time
- make the smallest fix that addresses the root cause
- verify the original symptom is gone

This should become the default beginner debugging flow.

### 4. Verification Before Completion

Before saying "done":

- identify what command or check proves the claim
- run it fresh
- read the output
- report evidence, not confidence

This is already aligned with `AI_WORKING_RULES.md`.

### 5. Code Review For Medium/High Risk

Before finishing important work:

- review against the original plan/spec
- check tests, risk, rollback, and file structure
- classify any issues by severity
- do not treat review feedback as automatically correct; verify it

This fits the existing Writer/Reviewer loop.

## What Not To Put In The Beginner Default

Do not make these mandatory for every beginner project:

- full subagent-driven-development
- mandatory git worktrees for all feature work
- strict "delete all implementation if test was not written first" TDD language
- meta-skills for writing skills
- upstream PR contribution discipline
- every Superpowers skill copied into each project

These are useful in the right environment, but too heavy as the first experience for a non-engineer building a dashboard.

## Proposed Files

### `BEGINNER_AI_DEVELOPMENT.md`

Purpose: the human-readable beginner process.

Suggested outline:

1. Do not start by coding.
2. Understand the product goal.
3. Identify users, roles, data, screens, and risks.
4. Define MVP vs later.
5. Produce a short design/spec.
6. Get user approval.
7. Produce an implementation plan.
8. Design file structure before coding.
9. Build in small slices.
10. Verify before reporting done.
11. Review before deploy or handoff.
12. Report clearly.

### `SUPERPOWERS_INTEGRATION.md`

Purpose: technical bridge to real Superpowers installation.

It should say:

- If Superpowers is installed, use it.
- Use `brainstorming` for new features/products.
- Use `writing-plans` after approved design.
- Use `systematic-debugging` for bugs.
- Use `test-driven-development` when adding behavior where automated tests are practical.
- Use `verification-before-completion` before completion claims.
- Use review skills for medium/high-risk work.
- If Superpowers is not installed, follow `BEGINNER_AI_DEVELOPMENT.md` manually.

### `templates/beginner-dashboard/AGENTS.md`

Purpose: one copyable entrypoint for new dashboard/business-tool projects.

It should include:

- project commands
- risk rules
- dashboard-specific safety rules
- privacy/customer-data rules
- no destructive/financial/customer-facing action without confirmation
- requirement to use Superpowers if available, otherwise manual beginner workflow

## Product Position

The public story should not be "we replaced Superpowers."

Better:

> This playbook gives non-engineer builders a simple beginner workflow and safety layer. It works by itself, and it can use Superpowers as the underlying methodology engine when Superpowers is installed.

That keeps this repo small, practical, and compatible with multiple agents.

## Decision I Recommend

For v1.3 or the next proposal:

1. Do not vendor/copy all of Superpowers into the main repo.
2. Add `BEGINNER_AI_DEVELOPMENT.md`.
3. Add `SUPERPOWERS_INTEGRATION.md`.
4. Add a `templates/beginner-dashboard/` starter.
5. Update `README.md` and `HOW_TO_USE.md` to route beginners through the new single entrypoint.
6. Add attribution to Superpowers in acknowledgements and note that Superpowers is MIT licensed if any adapted text/code is copied.

## Open Question For Claude Code

Should this be a v1.3 proposal focused on beginner adoption, or should it wait until after one real beginner-dashboard trial?

My bias: write the proposal now, but merge only the minimal beginner entrypoint and integration guide. Keep deeper automation or vendoring for later evidence.
