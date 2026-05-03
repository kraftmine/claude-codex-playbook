# Claude Code + Codex Playbook

A small, opinionated playbook for working with Claude Code and Codex as paired coding agents — without drifting into kitchen-sink monoliths, untracked git work, or methodology bloat.

**Status:** v1 frozen on `2026-05-03`. Authored from the lessons of a real production refactor (Wild Kamchatka dashboard). To be revised after three real uses.

**Author:** [Konstantin Gordon](https://github.com/kraftmine), with synthesis from Claude Code (Anthropic) and Codex (OpenAI).

## What This Is

A set of short, practical rails for a non-engineer founder using Claude Code + Codex to build production software:

- **rules** that prevent the most expensive mistakes (file-size hard ceilings, git neglect, mutable globals, deploy without backup)
- **lessons** named from real failures, so the same trap is recognized faster next time
- **workflow** for splitting work between two agents without making the human coordinate hand-offs
- **playbooks** for the moments where ritual saves the project (checkpoint, deploy)
- **project template** so every new project starts with healthy boundaries on day 0

The playbook is operational discipline, not methodology. It scales process to task risk. Low-risk work stays fast. Only high-risk work invokes the full ceremony.

## What This Is Not

- Not a replacement for judgment.
- Not a 100-step process before every bugfix.
- Not Claude-only — Codex follows the same rules.
- Not an excuse to slow down simple work.
- Not a way to make the founder responsible for engineering details.
- Not a methodology like Superpowers or 12-factor agents — those exist and are good. This playbook covers the operational layer they leave open: git hygiene, file-size limits, deploy ritual, role split, named project lessons.

## Core Principle

Konstantin owns product intent and business priorities.

Claude Code and Codex own engineering risk detection, architecture pushback, verification discipline, and clear explanations.

If the user asks for something that would create avoidable technical debt, the AI does not silently comply. It explains the risk, recommends a safer path, and only proceeds with the risky path if the user explicitly chooses it.

## Risk-Based Operating Model

Every coding task is classified quickly:

| Risk | Examples | Required discipline |
|---|---|---|
| **Low** | copy change, small UI tweak, obvious bugfix | `git status`, focused edit, targeted test/build if relevant |
| **Medium** | feature slice, shared component, business rule, persistence change | short plan, tests, build, smoke if UI-facing |
| **High** | deploy, redesign, migration, auth/finance/data model, multi-file refactor | checkpoint, written plan, tests, build, browser smoke, backup, rollback note |

Process scales with risk. Low-risk tasks stay fast.

## Operating Model

- **Claude Code** — orchestrator, planner, architect, reviewer.
- **Codex** — builder, debugger, verifier, shipper.
- Both agents are **peers**, not boss/subordinate. Either can challenge a plan when code reality or product risk demands it.
- **Konstantin** — product owner, not engineering dispatcher.

This split is directly modeled on Anthropic's [orchestrator-workers pattern](https://www.anthropic.com/research/building-effective-agents).

## Documents

### Rules & Lessons
- [`AI_WORKING_RULES.md`](AI_WORKING_RULES.md) — 14 rules for Claude Code, Codex, and any future agent. The source of truth.
- [`LESSONS_FROM_WK.md`](LESSONS_FROM_WK.md) — 11 concrete failures from Wild Kamchatka with cause, rule, and preventive check for each.

### Workflow & Templates
- [`WORKFLOW.md`](WORKFLOW.md) — roles, default loop, Writer/Reviewer pattern, handoff contract, deploy loop.
- [`PROJECT_TEMPLATE.md`](PROJECT_TEMPLATE.md) — minimal per-project context with day 0 file requirements (`CLAUDE.md` short, `AGENTS.md` for commands).

### Playbooks
- [`PLAYBOOK_CHECKPOINT.md`](PLAYBOOK_CHECKPOINT.md) — short procedure before risky operations.
- [`PLAYBOOK_DEPLOY.md`](PLAYBOOK_DEPLOY.md) — deployment safety checklist.

### How This Came Together (working history)
- [`CODEX_SYNTHESIS.md`](CODEX_SYNTHESIS.md) — Codex's position on keeping the system small.
- [`CLAUDE_CODE_REVIEW.md`](CLAUDE_CODE_REVIEW.md) — Claude Code's review of the initial draft, surfacing four required gaps.
- [`EXTERNAL_RESEARCH_FINDINGS.md`](EXTERNAL_RESEARCH_FINDINGS.md) — survey of existing AI-agent playbooks (Anthropic, HumanLayer, AGENTS.md, 12-factor agents, smartwhale8/claude-playbook). What we adopted, what we rejected.

## How To Use This Playbook

For a practical step-by-step setup guide, start with [`HOW_TO_USE.md`](HOW_TO_USE.md).

### If you are Konstantin
Use it on the next real task. Treat the rules as defaults, not absolutes. After three real uses, run a short retrospective: what prevented a mistake, what slowed work down, what repeated enough to deserve a hook or skill.

### If you found this repo
You are welcome to copy, fork, or adapt anything here. The playbook is shaped by one specific founder + agent setup; your context is different. Take what fits.

The most reusable pieces are likely:
- the **risk-based scaling** model
- the **named lessons from Wild Kamchatka** (most are universal)
- the **handoff contract** in `WORKFLOW.md`
- the **CLAUDE.md size discipline** (under 80 lines, under 60 if possible)

The least reusable: anything specific to Wild Kamchatka deploy mechanics, the kraftmine GitHub username, the Indonesian/Russian operational context.

### If you are an AI agent landing in this repo
Read in this order: `README.md` -> `HOW_TO_USE.md` -> `AI_WORKING_RULES.md` -> `WORKFLOW.md` -> `PROJECT_TEMPLATE.md`.

If the user asks you to activate this workflow in a project, create or update the minimal project-local entrypoints (`AGENTS.md`, short `CLAUDE.md` when relevant, and `.planning/` folders). Do not copy the whole playbook into the project by default.

## Open Questions

To be answered or removed after three real uses:

- Which rules are hard stops versus warnings?
- What should be required before every live deploy?
- How should Claude Code and Codex hand off context without duplicating work?
- Which project facts should live in every repo so new agents do not guess?
- When should we use GitHub-connected tools versus local filesystem inspection?
- When should we search for new skills/tools versus keeping the toolchain stable?
- Which checks should become deterministic hooks after they prove useful three times?

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — feel free to use, adapt, share. Attribution appreciated.

## Acknowledgements

- The lessons in this playbook come from a real production refactor sequence on the Wild Kamchatka operations dashboard, where the original authors hit every monolith / git / mutable-global trap themselves.
- Direct external influences: [Anthropic's Claude Code best practices](https://code.claude.com/docs/en/best-practices), [HumanLayer's "Writing a good CLAUDE.md"](https://www.humanlayer.dev/blog/writing-a-good-claude-md), [the AGENTS.md convention](https://agents.md/), [12-factor agents](https://github.com/humanlayer/12-factor-agents), [smartwhale8/claude-playbook](https://github.com/smartwhale8/claude-playbook).
- Indirect influences: Andrej Karpathy's coding rules, Addy Osmani's agent-skills, obra/superpowers methodology.
