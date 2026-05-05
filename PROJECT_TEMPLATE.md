# Project Template

Copy this into a new project's planning folder or project-specific agent instructions.

## Project

Name:

Purpose:

Stage:

- prototype
- MVP
- production

## Stack

Frontend:

Backend/API:

Database:

Hosting/deploy:

Auth:

Payments/finance:

## Commands

Install:

```bash

```

Dev:

```bash

```

Test:

```bash

```

Build:

```bash

```

Deploy:

```bash

```

## Day 0 Agent Files

Required:

- `CLAUDE.md` - short project-specific context and hard rules
- `AGENTS.md` - commands, tests, build, deploy, architecture, invariants
- `.gitignore` - includes local backups, generated build output, secrets, and `CLAUDE.local.md`

Optional:

- `CLAUDE.local.md` - personal notes, not committed
- `.planning/decisions/` - ADRs and decision notes

`CLAUDE.md` target: under 80 lines, ideally under 60.

If it grows beyond that, move commands and stable project facts into `AGENTS.md`, or use Claude Code native `@` imports for specialized context.

Example:

```markdown
See @AGENTS.md for commands and deploy notes.
See @docs/git-workflow.md for commit conventions.
```

## Invariants

Things agents must not break:

- 

## Shared Truth

Where durable data lives:

- 

Data that must not be only local/browser state:

- 

## Risk Areas

- auth
- permissions
- money/finance
- inventory/stock
- migrations
- deploy/rollback

Project-specific risks:

- 

## Known Debt

| Debt | Impact | Cleanup trigger |
|---|---|---|
|  |  |  |

## Manual Smoke Tests

Critical flows the user or agent should verify:

- 

## Agent Notes

Preferred architecture:

- `src/domain` for business logic
- `src/ui` for reusable UI primitives
- `src/features` for feature slices
- `src/views` or `src/pages` for route/page composition
- `src/hooks` for reusable stateful behavior
- `src/constants` for named business constants
- `src/lib` for infrastructure helpers
- avoid growing monolithic files

Project-specific rules:

- 

## Decision Records

Use ADRs for high-risk or expensive-to-reverse choices:

- new dependency
- data model or data flow change
- module boundary change
- auth, permissions, finance, inventory, or deploy behavior

Use short decision notes for medium-risk choices that future agents should not rediscover.

## Dashboards And Business Tools

Internal dashboards and operational business tools (the most common project shape for non-engineer founders) share a recurring set of starter facts worth capturing on day 0. If your project is a dashboard, finance tool, CRM, inventory system, or ops console, fill in this subsection in addition to the generic sections above.

### Roles And Their Views

List every role that uses the system, and the shape of UI each one sees:

- 

For each role, note: what they can read, what they can write, what is hidden from them, and which screens are role-specific vs. shared.

### Private And Customer Data

Data the system handles that has legal, financial, or trust weight:

- 

Mark which of these must never appear in logs, error messages, screenshots, or unencrypted backups.

### Financial / Customer-Facing Actions

Actions that move money, change stock, send a message to a customer, or commit to a delivery:

- 

These actions require explicit user confirmation before the agent triggers them programmatically. Never auto-fire.

### Metrics And Reports

Numbers shown on dashboards. For each one, name:

- 

The formula (in plain language), the source of truth (which table, which calculation), and how stale the displayed value can be before it is misleading.

### Source Of Truth

For each piece of operational data, name where it lives:

- 

If a value is shown in two places, only one is the source of truth and the other is derived. Do not allow two writeable versions of the same number.

### Deploy Expectations

Who deploys, how often, and what counts as a "safe" deploy window for the customers using the tool:

- 

If the tool is used live during business hours, deploy is a higher-risk operation than a generic web app deploy.
