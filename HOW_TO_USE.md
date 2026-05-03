# How To Use This Playbook

This repository is a portable playbook for working with AI coding agents.

It is designed so a user can send the repository link to Codex, Claude Code, GPT-5.5, Opus, or another capable coding agent and ask it to activate the workflow inside a project.

## Quick Start For Humans

Send the agent this prompt:

```text
Use this AI collaboration playbook:
<PASTE_GITHUB_REPO_URL>

Project path or project repo:
<PASTE_PROJECT_PATH_OR_REPO_URL>

Goal:
<DESCRIBE_THE_TASK>

First read README.md, HOW_TO_USE.md, AI_WORKING_RULES.md, WORKFLOW.md, and PROJECT_TEMPLATE.md.
Then activate the workflow in the project by creating or updating the minimal project agent files.
Do not copy the whole playbook into the project unless there is a specific reason.
```

## Quick Start For Agents

When a user gives you this repository and asks to use it for a project:

1. Read `README.md`.
2. Read `HOW_TO_USE.md`.
3. Read `AI_WORKING_RULES.md`.
4. Read `WORKFLOW.md`.
5. Read `PROJECT_TEMPLATE.md`.
6. If the task involves deploys, read `PLAYBOOK_DEPLOY.md`.
7. If the task involves risky refactor/migration/redesign, read `PLAYBOOK_CHECKPOINT.md`.
8. Use `LESSONS_FROM_WK.md` for background patterns, not as a mandatory checklist.

Then inspect the target project and create or update only the minimal local files it needs.

## What To Create In A Project

For each project, create:

- `AGENTS.md` - commands, tests, build, deploy, architecture notes, critical invariants
- `CLAUDE.md` - short Claude Code context if Claude Code is used
- `.planning/coordination/` - current plans, handoffs, work notes
- `.planning/decisions/` - ADRs and decision notes
- `.planning/reviews/` - cross-agent reviews

Optional:

- `CLAUDE.local.md` - personal local notes, gitignored

Also update `.gitignore` to ignore local-only agent notes and filesystem backups where appropriate.

## What Not To Do

Do not copy every playbook file into every project by default.

Reason: copied playbooks drift. The repository should remain the source of truth, while each project contains only a small local entrypoint.

Do not create hooks or skills immediately.

Reason: hooks and skills are useful only after repeated pain proves the workflow should be automated.

Do not make the user coordinate technical process.

The agent should decide when to checkpoint, test, smoke check, write a decision note, or ask for review.

## Minimal Project Activation Checklist

Before meaningful work in a project:

1. Check `git status --short`.
2. Identify project commands from package/config files.
3. Create or update `AGENTS.md`.
4. Create or update short `CLAUDE.md` if Claude Code is part of the workflow.
5. Ensure `.planning/coordination/`, `.planning/decisions/`, and `.planning/reviews/` exist.
6. Classify the user's task as low, medium, or high risk.
7. For medium/high risk, use the Writer/Reviewer loop.
8. Verify before reporting done.

## Recommended Agent Roles

Default split:

- Claude Code: orchestrator, planner, architect, reviewer
- Codex: builder, debugger, verifier, shipper
- GPT-5.5 / Opus: high-level design critique, strategy, expensive disagreement resolution
- User: product intent, business priority, final taste, final business decision

This is not hierarchy. Agents work as peers with different strengths.

Any agent may push back when it sees engineering risk.

## Ready-To-Send Prompt

```text
I want to use this AI collaboration playbook:
<PASTE_GITHUB_REPO_URL>

Please read README.md, HOW_TO_USE.md, AI_WORKING_RULES.md, WORKFLOW.md, and PROJECT_TEMPLATE.md.

Then inspect my project:
<PASTE_PROJECT_PATH_OR_REPO_URL>

Activate the workflow by creating/updating AGENTS.md, CLAUDE.md if relevant, and .planning folders.

After that, classify this task by risk and continue according to the playbook:
<DESCRIBE_TASK>
```

## How To Share This With Another Person

Send them:

1. The GitHub repository link.
2. The ready-to-send prompt above.

If they use a capable coding agent, they should not need a long explanation.

The repository should explain itself.
