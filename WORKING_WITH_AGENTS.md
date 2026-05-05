# Working With AI Coding Agents — A Pocket Guide For Non-Engineers

This document is for **you**, the project owner, not for the agent.

If you have never built software, working with Claude Code or Codex can feel either too fast (the agent moves before you understand what it is doing) or too slow (the agent asks for things you do not know how to give). This guide is the short version of how to drive the relationship without becoming an engineer.

## What You Are Actually Doing

You are not "managing developers." You are giving an agent enough product context to make good engineering decisions on your behalf, and reading its reports critically enough to catch the moments where it is heading the wrong way.

Three things are only yours to decide:

- **Product intent** — what the thing should do, who it is for, and what would make it feel broken.
- **Money** — what gets spent, what gets paid, what gets refunded.
- **Taste** — what feels right or wrong in the user experience, even if you cannot articulate why.

Everything else (file structure, test selection, deploy mechanics, backup paths, library choices) is the agent's job. If the agent pushes those decisions onto you, push back: "Recommend the safer option and explain it."

## Risk Levels — Plain Language

Every task has a risk level. The agent should classify it before starting work.

- **Low risk** — copy change, small UI tweak, obvious bugfix. The agent just does it. You see the result. Done in minutes.
- **Medium risk** — a new feature slice, a shared component, a business rule change, anything touching how data is saved. The agent gives you a short plan first, then implements. You should be able to read the plan in under 60 seconds.
- **High risk** — deploy, redesign, data migration, anything touching money/auth/inventory, multi-file refactor. The agent creates a checkpoint, writes a plan, asks for confirmation if anything is non-obvious, and gives you a rollback path.

If a task feels like it should be low risk but the agent is treating it as high risk, ask why. Sometimes the agent sees a complication you don't. Sometimes it is over-ceremonying — your call.

## How To Read An Agent Report

After meaningful work, the agent should give you a short report. A good report answers:

- **What changed** — one line, not a file-by-file list.
- **What was verified** — which check, what the output said.
- **What was deployed (if anything)** — and which bundle is live.
- **Where the backup is** — if a deploy or risky change happened.
- **What you should manually test** — if anything. Often the answer is "nothing, I checked it."

If the report is missing any of these and the work was non-trivial, ask. The agent should not make you guess whether a deploy actually happened or whether tests passed.

## When To Say "Stop, Slow Down"

The agent is flailing if you see any of these patterns. Stop the work and ask the agent to step back.

- The agent is making the same kind of fix in three places. (It should have refactored, not patched.)
- The agent says "I think this should work" without running anything. (Verification is missing.)
- The agent jumps to a different problem mid-task without resolving the first. (Lost focus.)
- A simple-sounding request has produced a 10-file changeset. (Scope creep.)
- You are being asked to make engineering judgment calls. (Wrong handoff.)
- The same error keeps coming back after each "fix." (No root cause yet — see `PLAYBOOK_DEBUG.md`.)

The right response is not panic; it is a short pause: "Stop. Tell me in plain language what you are actually trying to fix and what the smallest safe step looks like."

## What You Do Not Need To Track

You do not need to memorize:

- File paths or module names
- Whether a file is "too big"
- Test framework choices
- Build commands or deploy commands
- Where the backup directory lives
- Git branch names
- Whether to use a hook or a skill

If any of these become your problem, the agent's process broke. The fix is to surface it ("you are pushing engineering details onto me again") and let the agent fix the process.

## Two Habits That Save You Hours

**Before agreeing to a feature, answer these out loud or in writing:**

1. Who uses this? (which role, which device)
2. What data does it touch? (money, stock, customers, audit log)
3. What would make it feel broken to a real user?
4. What is the smallest version that is still useful?

If the agent has not asked these, you should volunteer them. They unlock 80% of the design choices.

**After meaningful work, ask one verification question:**

- "What did you actually run, and what did it say?"

If the answer is "I made the change and it looks right," the work is not done yet. Ask for evidence.

## When Things Go Wrong

You will hit moments where:

- A deploy goes out and something breaks in production.
- The agent insists a fix is correct but you can see it is not.
- A change you approved last week comes back to bite you.

These are not failures of the playbook. They are the reason the playbook exists. The recovery path:

1. Get the most recent backup live (the agent should know where it is).
2. Reproduce the broken state in a controlled way.
3. Use `PLAYBOOK_DEBUG.md` to find the root cause, not the next plausible patch.
4. Add a `LESSONS_FROM_WK.md`-style entry so the same trap is recognized faster next time.

## Trust Calibration

The agent is good at engineering. It is not infallible.

- Trust it on architecture, file structure, library choices, refactoring, debugging methodology.
- Distrust it on "this looks fine" without verification, on rushed deploys without a backup, and on requests that feel small but produce sprawling changesets.
- Override it on product taste, money, and what the user actually needs. You see the user; the agent reads code.

A healthy relationship looks like: the agent makes most engineering calls without asking, you make all product calls, and either of you can stop the other when something is off.

## What This Document Is Not

- Not a course. You can read it once and skim it later.
- Not a contract. The agents are not bound by it; they are bound by `AI_WORKING_RULES.md`.
- Not exhaustive. If you hit a situation that is not covered, the right move is usually to ask the agent for the safer option and the explanation, then choose.

## Where To Go Next

- If you want to see the rules the agent operates under: `AI_WORKING_RULES.md`.
- If you want to see how the agents collaborate: `WORKFLOW.md`.
- If something broke and you want a debug protocol: `PLAYBOOK_DEBUG.md`.
- If a deploy is coming up: `PLAYBOOK_DEPLOY.md`.
- If you want to set up a new project: `PROJECT_TEMPLATE.md` and `HOW_TO_USE.md`.
