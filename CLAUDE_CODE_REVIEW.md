# Claude Code Review of Initial Playbook Draft

Date: `2026-05-03`
Reviewer: Claude Code
Reviewing: `README.md`, `AI_WORKING_RULES.md`, `LESSONS_FROM_WK.md`, `WORKFLOW.md`, `PLAYBOOK_CHECKPOINT.md`, `PLAYBOOK_DEPLOY.md`, `PROJECT_TEMPLATE.md`
Status: `accepted with four required additions`

## Overall

The vision is solid and structurally better than my own initial draft. Specifically:

- **Risk-based operating model** (low / medium / high) is the right backbone. It scales process to task size and avoids the Superpowers failure mode of triggering heavyweight discovery for every typo.
- **"Konstantin owns product, AI owns engineering risk"** is a clean separation of responsibility.
- **Twelve short rules** in `AI_WORKING_RULES.md` are actionable and free of fluff.
- **`README.md` recommendation** to stabilize rules before building skills or searching for tools is correct sequencing.

I accept the playbook as-is, with four required additions before it should be considered complete.

## Orchestrator / Builder Framing

Konstantin proposed: Claude Code = orchestrator, Codex = builder.

This matches what `WORKFLOW.md` already encodes and is the right default split:

- **Konstantin**: product intent, business priority, final taste, manual smoke when human judgment is needed.
- **Claude Code**: orchestration, planning, architecture review, cross-agent review, writing/refining rules, risk detection, second opinion before risky work.
- **Codex**: implementation, terminal/browser debugging, tests, build/deploy verification, keeping coordination docs in sync.

One nuance worth recording: the boundary is **not absolute**. There are legitimate handoffs — Claude Code occasionally implements small things (e.g. checkpoint commits, `.gitignore` edits, vitest config patches) and Codex occasionally proposes architectural directions. The 80/20 rule holds; the remaining 20% is honest work where the line shifts.

This nuance should be a one-line mention in `WORKFLOW.md`, not a new section.

## Required Additions

Four gaps weaken the playbook against the actual lessons of Wild Kamchatka. All four are short additions, not rewrites.

### Gap 1 — Git hygiene is not a rule

`AI_WORKING_RULES.md` has twelve rules and **none about git**. Yet the largest single failure on Wild Kamchatka was git neglect: HEAD on a commit from April 9, three weeks of untracked work, no remote, recovery dependent on filesystem snapshots only.

**Add Rule 13: Commit at meaningful boundaries.**

> Commit after phase completion, after deploy, and before risky operations. If the working tree has more than 200 untracked lines or has been dirty for more than 24 hours, propose a checkpoint commit. Push to remote after every commit so a single device failure cannot lose work.

This belongs in `AI_WORKING_RULES.md` as a first-class rule and should also surface as Lesson 8 in `LESSONS_FROM_WK.md`.

### Gap 2 — File-size pre-flight is a check, not a rule

`LESSONS_FROM_WK.md` Lesson 1 captures monolith risk and proposes a "preventive check": *"Before substantial edits, inspect target file size and ask: 'Am I adding logic that belongs somewhere else?'"*

This is too soft. It is exactly the kind of soft check that drifted Wild Kamchatka's `App.jsx` to 10,000+ lines. The check existed in spirit; the rule did not.

**Promote to a hard rule in `AI_WORKING_RULES.md`:**

> **Rule 14: File-size hard ceiling.** If the target file exceeds 1500 lines, do not add code. Stop and propose extraction first. Proceed inline only after the user explicitly chooses speed over structure with full information about the cost.

The rule must be a hard stop, not a question phrased as a check.

### Gap 3 — Folder structure on day 0 is preference, not rule

`PROJECT_TEMPLATE.md` mentions preferred folder structure under "Agent Notes":

> avoid growing monolithic files, prefer `src/domain`, `src/ui`, `src/features`, `src/hooks`

But `AI_WORKING_RULES.md` has nothing about it, and a new project bootstrapped from this playbook could legally start without any of those folders.

**Add Rule 15: Day 0 folder structure for new projects.**

> New projects start with `src/ui/`, `src/features/`, `src/domain/`, `src/views/` (or `src/pages/`), `src/hooks/`, `src/constants/`, `src/lib/`. Code outside this structure requires an ADR explaining why. The 30 minutes spent on day 0 saves months of monolith pain.

Wild Kamchatka's monolith would have been impossible if this rule had been followed at project start.

### Gap 4 — ADR triggers are not codified

During Wild Kamchatka redesign planning, three ADRs were written: typography (`Golos Text` + `Unbounded`), i18n (keep RU/EN), AppDataContext (hybrid context + explicit args). Each closed a decision that would otherwise have drifted. ADR discipline was valuable.

The current playbook does not mention ADRs anywhere.

**Add Rule 16: Write ADRs before implementation for non-trivial decisions.**

> Required ADR triggers: a new dependency, a pattern repeated 3+ times, a change to module boundaries, a change to data flow shape, a decision that affects more than 3 files. Save as `.planning/decisions/ADR-NNN-<short-name>.md` before code. The ADR contains: context, decision, alternatives considered, consequences.

This explicit list eliminates ambiguity about when to write one and prevents the documentation gap that hides design decisions inside commit messages.

## Optional Improvements (non-blocking)

These are smaller and can be folded in if convenient:

- **Stage awareness rule.** `PROJECT_TEMPLATE.md` lists prototype/MVP/production but `AI_WORKING_RULES.md` does not differentiate by stage. Production should require all rules; prototype can relax some (no CI required, looser test coverage).
- **Session-start pre-flight.** Worth saying in `WORKFLOW.md` that a new working session should begin with `wc -l` on hot files and `git status`. This is the macro temperature reading that prevents drift between sessions.
- **GPT-5.5 / Opus trigger.** `WORKFLOW.md` lists their use cases but does not specify when Claude Code should escalate to them. Suggested trigger: "when the design decision is reversible only at high cost, or when Claude Code and Codex disagree after one exchange."
- **Context handoff between agents.** Codex updates `CODEX_NOTES.md` after work; Claude Code writes `*_REVIEW.md` files. Worth a short subsection in `WORKFLOW.md` so this convention is explicit, not implicit.

## Sequencing

`README.md` says: *"Do not start by building skills or searching GitHub for more tools. First, make the rules and lessons crisp."*

Strongly agreed. The sequence should be:

1. Close the four required gaps in this review (30 minutes of editing).
2. Resolve the open questions in `README.md` ("Open Questions" section).
3. Use the playbook on the next real task (Wild Kamchatka Phase 1 implementation).
4. After three concrete uses, identify which procedures repeat and would benefit from being skills.
5. Only then design `kraftmine:checkpoint` and `kraftmine:bootstrap` skills.

The point of the playbook is not to be perfect on first draft. It is to be **good enough to use immediately** and **honest enough to adjust** based on real experience.

## Recommended Next Step

I propose Codex applies the four gap additions (Rules 13–16, plus a new Lesson 8 for git hygiene), and updates `LESSONS_FROM_WK.md` with two more concrete lessons from our recent work:

- **Lesson 8: Git neglect costs more than it saves.** Wild Kamchatka was three weeks ahead of HEAD with no remote.
- **Lesson 9: Mutable module-level globals defeat extraction later.** `WAREHOUSES`, `PRODUCTS`, `STAFF_DIRECTORY` blocked Phase 2 of the redesign and required a dedicated Phase 1.5 to migrate.
- **Lesson 10: i18n in a half-state is dead code.** Infrastructure existed but nothing used it; the right move was to either commit fully or delete fully.

After those edits, the playbook is ready to be the working reference for Phase 1 implementation and beyond.
