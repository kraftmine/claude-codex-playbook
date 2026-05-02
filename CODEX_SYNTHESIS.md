# Codex Synthesis: Keep The System Small And Useful

Date: `2026-05-03`
Author: Codex
Context: response to Claude Code review and external research findings.

## Position

Claude Code and Codex should not work as boss and subordinate.

The better model is peer collaboration with different defaults:

- Claude Code is the default orchestrator, planner, architect, and reviewer.
- Codex is the default builder, debugger, verifier, and shipper.
- Konstantin owns product intent, priority, taste, and final business decisions.
- Both agents own engineering risk detection and may push back.

This gives Konstantin leverage without making him manage technical process.

## What To Adopt Now

Adopt these immediately:

- verification-first discipline
- meaningful git checkpoints
- hard pressure against adding feature logic to huge files
- `AGENTS.md` as project-level commands/context for agents
- short `CLAUDE.md`, not a bloated instruction manual
- Writer/Reviewer loop for medium/high-risk work
- ADRs or decision notes before expensive choices
- explicit handoff contracts between Claude Code and Codex

These are small rails with high leverage.

## What To Delay

Delay these until repeated pain proves they are worth it:

- many custom skills
- many hooks
- complex Claude-only infrastructure
- broad GitHub tool hunting
- heavyweight Superpowers-style methodology

The rule of thumb: automate after the third repeat, not after the first idea.

## Hooks Policy

Hooks are powerful because they are deterministic. That also makes them risky if installed too early.

Good hook candidates:

- show `git status` at session start
- run lint after relevant edits
- run domain tests after `src/domain/` changes

Bad hook candidates:

- anything that surprises the user
- anything that slows every tiny edit
- anything that changes files automatically without clear consent

Start with one hook only after the workflow proves repetitive.

## Skills Policy

Skills should be narrow.

Good future skills:

- `kraftmine:checkpoint` - creates a safe recovery point before risky work
- `kraftmine:bootstrap` - starts a new project with healthy structure

Bad skills:

- mega-skills that plan, implement, review, deploy, and document everything
- vague skills with broad triggers
- skills that replace judgment with ceremony

## Operating Rule

The playbook is successful only if work becomes faster and safer.

If the playbook makes simple tasks feel heavy, simplify the playbook.

If the playbook misses the same risk twice, strengthen the rule or automate the check.

## Recommended Next Use

Use this playbook on the next Wild Kamchatka task without adding new automation.

After three real uses, review:

- what prevented a mistake
- what slowed us down
- what the user still had to coordinate manually
- what repeated enough to deserve a hook or skill
