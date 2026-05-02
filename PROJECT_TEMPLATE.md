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
