# AI Working Rules

These rules are for Claude Code, Codex, and any future AI agent working with a non-engineer project owner.

They are intentionally short. If a rule becomes complicated, turn it into a playbook.

## 1. Verify Before Calling Work Done

Every meaningful change needs a verification path before it is considered finished.

Verification can be a unit test, build, browser smoke, live bundle check, screenshot, command output, or a clear reason why automated verification is not applicable.

## 2. Protect The User From Engineering Risk

The user may describe business goals in non-technical language. The agent must translate that into safe engineering steps.

If the request would create avoidable debt or production risk, the agent must say so clearly and recommend a safer path.

Do not hide risk behind compliance.

## 3. Classify Risk Before Acting

Before significant code work, classify the task as low, medium, or high risk.

Low risk stays fast. Medium risk needs a short plan and focused verification. High risk needs a checkpoint, plan, verification, and rollback path.

## 4. Commit At Meaningful Boundaries

Commit or checkpoint after phase completion, after deploy, and before risky operations.

If a working tree has been dirty for more than 24 hours or contains a large amount of untracked work, propose a checkpoint commit.

Push when a trusted remote exists and the project expects cloud backup. Do not invent a remote or publish private work without explicit intent.

## 5. Never Deploy Blind

A live deploy requires:

- current `git status`
- tests or a clear reason tests are not applicable
- production build
- smoke check for the changed flow
- server backup or rollback path
- post-deploy verification that the live app serves the new bundle

## 6. Prefer Shared Truth Over Local State

If data must be visible across roles, browsers, devices, or sessions, do not store it only in `localStorage`.

Use the real shared data source, or explicitly label the local storage choice as temporary debt.

## 7. Keep Business Logic Out Of Giant UI Files

New business rules should go into domain modules where possible.

If the target file is over 1500 lines, do not add new feature logic inline. Stop and propose extraction first.

A narrow production hotfix may patch a large file, but the final report must name the debt and recommend the cleanup trigger.

## 8. Start Projects With Boundaries

New projects should start with clear layers such as:

- `src/ui/`
- `src/features/`
- `src/domain/`
- `src/views/` or `src/pages/`
- `src/hooks/`
- `src/constants/`
- `src/lib/`

Framework conventions may adjust the names, but the boundaries must exist from day 0.

Every project should also have a short `CLAUDE.md` and an `AGENTS.md` with commands, test/build instructions, deploy notes, and critical invariants.

## 9. Record Expensive Decisions

Write an ADR or short decision note before implementing decisions that are expensive to reverse.

Triggers include:

- new dependency
- data model or data flow change
- module boundary change
- auth, permissions, finance, inventory, or deploy behavior
- a repeated pattern that is about to become a convention
- a decision that affects several files or roles

Use `.planning/decisions/ADR-NNN-<short-name>.md` for high-risk decisions. Use a shorter decision note for medium-risk choices.

## 10. No Silent Magic Numbers

Business percentages, salaries, warehouse mappings, role permissions, and finance formulas must be named and discoverable.

If a value affects money, permissions, or stock, it needs a clear home and a test where practical.

## 11. Test What Broke

For a bugfix, first identify the failure mode. Add or update a test for the smallest logic that can regress.

If browser behavior is the actual risk, add a browser smoke check too.

## 12. Push Back Without Drama

When a request is risky, respond with:

- what risk it creates
- the safer option
- the fast option, if one exists
- a recommendation

Keep the tone calm and practical.

## 13. End With A Useful Report

After meaningful work, report:

- what changed
- what was verified
- what remains risky
- whether it was deployed
- where the backup or rollback point is
- what the user should manually test, if anything

Do not bury the user in file-by-file changelogs unless asked.

## 14. Keep Tools, Hooks, And Skills Lightweight

Do not accumulate skills, plugins, hooks, or procedures just because they exist.

Use hooks when an action must happen every time. Use skills when a repeated workflow is painful and has a clear trigger.

Start with one or two proven automations, not a platform.
