# External Research Findings

Date: `2026-05-03`
Researcher: Claude Code
Purpose: Survey existing AI agent playbooks/rules/conventions to identify ideas worth integrating into our playbook before we lock it in.

## Sources surveyed

1. **Anthropic Claude Code Best Practices** — official documentation
2. **HumanLayer — Writing a good CLAUDE.md** — by the team behind 12-factor agents
3. **AGENTS.md specification** — open standard, 20,000+ repos adopted
4. **12-factor agents** (humanlayer/12-factor-agents) — production-grade agent principles
5. **smartwhale8/claude-playbook** — production-ready scaffolding template
6. **awesome-claude-code** (hesreallyhim) — curated list of skills, hooks, agents
7. **Anthropic — Building Effective Agents** — orchestrator-workers pattern reference

## TL;DR

Lots of generic playbooks exist. **None covers exactly what we need**, but **several contain ideas we should adopt** before locking our playbook in. Specifically: CLAUDE.md size discipline, AGENTS.md adoption, hooks as a deterministic layer, native `@` import for progressive disclosure, and the official Writer/Reviewer pattern that validates Konstantin's framing.

Konstantin's intuition that **Claude orchestrator + Codex builder** is the right split is **directly validated** by Anthropic's "Building Effective Agents" — this is literally the orchestrator-workers pattern as documented officially. We are not inventing the wheel here.

## Top 10 actionable additions for our playbook

### 1. CLAUDE.md must be short — drastically shorter than I was planning

**Source: Anthropic official + HumanLayer**

Anthropic guidance: "Keep it short and human-readable." HumanLayer: "Target under 300 lines, ideally under 60 lines for the root file."

Reasoning: Claude's system prompt has roughly 50 instructions baseline; frontier models follow ~150-200 with reasonable consistency. Bloated CLAUDE.md → important rules get lost.

**Action**: When we write `CLAUDE_MD_GLOBAL.md`, target under **80 lines**. Use progressive disclosure (point 5 below) for everything else.

### 2. Adopt AGENTS.md as the per-project agent context file

**Source: AGENTS.md specification**

20,000+ repos use this convention. AGENTS.md is the machine-readable counterpart to README.md, containing setup commands, testing, code style, build, security, PR guidelines.

**Action**: Per-project, create both:
- `CLAUDE.md` — short project-specific context for Claude
- `AGENTS.md` — agent-readable, includes commands. Codex reads this natively (see OpenAI's docs).

This means **one source of truth read by both Claude Code and Codex** without us maintaining two parallel files.

### 3. Use Claude Code's native `@` import for progressive disclosure

**Source: Anthropic official**

`CLAUDE.md` supports `@path/to/file` syntax to import other markdown. So instead of one giant file, do:

```markdown
# CLAUDE.md (60 lines)
See @AGENTS.md for project commands and structure.

# Hard rules
- File >1500 LoC = STOP, propose extraction
- Commit at meaningful boundaries

# Specialized contexts (loaded on demand)
- Git workflow: @docs/git-workflow.md
- Deploy: @docs/deploy.md
- Personal overrides: @~/.claude/my-overrides.md
```

**Action**: Restructure planned `CLAUDE_MD_GLOBAL.md` to use `@` imports for specialized topics, keeping the root file small.

### 4. Add a hooks layer for deterministic checks

**Source: Anthropic official + smartwhale8**

Anthropic: "Unlike CLAUDE.md instructions which are advisory, hooks are deterministic and guarantee the action happens."

Examples from smartwhale8 playbook:
- `lint-on-edit.sh` — runs ESLint after every file edit (PostToolUse)
- `block-migration-writes.sh` — refuses writes to migrations folder

**Action**: Add to playbook a section on hooks. Most relevant for our context:
- `lint-on-edit` — auto-run lint after edits, surface regressions immediately
- `tests-on-domain-change` — auto-run domain tests when `src/domain/` is touched
- `git-status-on-session-start` — temperature reading as a hook, not a manual ritual

This is a layer we're missing. Adding it codifies operational discipline rather than relying on me to remember.

### 5. Use the layered memory hierarchy properly

**Source: Anthropic official**

Anthropic supports five locations for CLAUDE.md, each with specific purpose:
- `~/.claude/CLAUDE.md` — applies to all sessions (cross-project rules)
- `./CLAUDE.md` — project root, git-tracked, team-shared
- `./CLAUDE.local.md` — gitignored, personal project notes
- Parent directories — monorepo support
- Child directories — loaded on demand

We currently use only `~/.claude/CLAUDE.md` and we don't have project-level CLAUDE.md anywhere. This is a missed lever.

**Action**: Per project, commit a `CLAUDE.md` to git. Add `CLAUDE.local.md` to `.gitignore` for personal preferences (e.g., "Konstantin prefers Russian explanations"). Already partially done by our `.planning/coordination/` convention but should be formalized.

### 6. Embrace "Writer/Reviewer with parallel sessions" — it's the official pattern

**Source: Anthropic official ("parallel sessions" → "Writer/Reviewer pattern")**

Anthropic explicitly recommends:

> Session A (Writer): "Implement a rate limiter."
> Session B (Reviewer, fresh context): "Review the rate limiter. Look for edge cases."

This is **literally what we are doing** with Codex implementing and Claude Code reviewing on Wild Kamchatka. Konstantin's intuition was right. We should formalize this in `WORKFLOW.md` as the **default pattern for medium/high risk work**, not an exception.

### 7. "Verification is the single highest-leverage thing"

**Source: Anthropic official**

Direct quote: "Include tests, screenshots, or expected outputs so Claude can check itself. This is the single highest-leverage thing you can do."

We do this in `PLAYBOOK_DEPLOY.md` (tests + build + smoke) but it should be elevated to **Rule 1** of `AI_WORKING_RULES.md`, not just step in deploy playbook.

**Action**: Promote verification discipline to the top rule. "Every meaningful change must have a verification path before it's considered done."

### 8. Common failure patterns — match exactly to WK lessons

**Source: Anthropic official**

Anthropic enumerates these failure patterns:

| Pattern | Match in WK? |
|---|---|
| The kitchen sink session | Yes — `App.jsx` became kitchen-sink at the file level |
| Correcting over and over | Yes — owner proof bug got fixed three times before the right framing |
| Over-specified CLAUDE.md | Not yet, but we'd hit this if we wrote 500-line CLAUDE.md |
| Trust-then-verify gap | Yes — initial Phase 0.5 build had test count discrepancy I caught |
| Infinite exploration | Yes — pre-Codex audit, we read App.jsx many times in different sessions |

**Action**: `LESSONS_FROM_WK.md` should mention these by name. They are not WK-specific — they are universal AI failure patterns. Naming them makes them recognizable.

### 9. From 12-factor: Factor 10 — small focused agents

**Source: 12-factor agents**

> "Designing narrowly-scoped agents rather than monolithic ones."

Translates to our context: when we eventually build skills (`kraftmine:bootstrap`, `kraftmine:checkpoint`), each does ONE thing. Don't bundle.

**Action**: Add to playbook: any skill we create has a single trigger and a single outcome. Mega-skills are forbidden. This prevents Superpowers-style trigger creep.

### 10. "Let Claude interview you" — built-in Claude Code mechanism

**Source: Anthropic official**

For larger features, Claude can use the `AskUserQuestion` tool to interview the user before writing a spec. This is essentially Superpowers' discovery mechanism, but built into Claude Code natively.

> "I want to build [brief description]. Interview me in detail using AskUserQuestion. Ask about technical implementation, UI/UX, edge cases, concerns, and tradeoffs. Don't ask obvious questions, dig into the hard parts. Keep interviewing until we've covered everything, then write a complete spec to SPEC.md."

**Action**: Add to `WORKFLOW.md` as the "starting a new feature" pattern. We don't need Superpowers for this — Claude Code already supports it.

## What we already have right

Our playbook draft already includes (and external research validates):

- **Risk-based scaling** — matches the implicit Anthropic approach (skip planning for trivial fixes)
- **Push-back when warranted** — matches HumanLayer's emphasis on owning context and pushing back on flawed approaches
- **Deploy ritual with backup** — matches every production-oriented playbook surveyed
- **Konstantin owns product, AI owns engineering risk** — clean separation that no surveyed source contradicts
- **Don't accumulate skills/plugins for their own sake** — matches HumanLayer's "ruthlessly prune" guidance
- **Lessons from concrete project experience** — uniquely ours; no surveyed source has WK-specific examples

## What we should reject from external sources

Not everything in surveyed sources is worth adopting:

- **Most of 12-factor agents** is about building agent code (we use agents, we don't build them). Only Factors 7, 8, 10 are operationally relevant.
- **smartwhale8 playbook's 14 rule categories** are too many. We should not split into 14 files. Their split is for a backend-heavy production system; ours is operational.
- **Superpowers full methodology** is too heavyweight. We already declined this.
- **Some AGENTS.md examples are over-engineered** with monorepo complexity we don't have. Use AGENTS.md but keep it short.

## Specific recommendations per playbook artifact

### `AI_WORKING_RULES.md`

- Promote verification to Rule 1 (Anthropic: highest-leverage thing)
- Keep under 14 rules total
- Add Rule 13 (git hygiene), 14 (file-size hard ceiling), 15 (day 0 folder structure), 16 (ADR triggers) as I proposed in `CLAUDE_CODE_REVIEW.md`
- Add Rule 17: "Hooks beat CLAUDE.md instructions for actions that must happen every time" — references hooks layer

### `LESSONS_FROM_WK.md`

- Add Lesson 8: git neglect (per my prior review)
- Add Lesson 9: mutable globals (per my prior review)
- Add Lesson 10: i18n half-state (per my prior review)
- Add Lesson 11: name common failure patterns from Anthropic (kitchen sink, trust-then-verify, etc.) and link them to WK examples

### `WORKFLOW.md`

- Formalize **Writer/Reviewer pattern** as the default for medium/high risk
- Add **"Let Claude interview you"** as the starting pattern for larger features
- Add **`/clear` between unrelated tasks** as standard hygiene
- Add **subagents for investigation** to preserve main context
- Mention `claude --continue` and `--resume` for cross-session work

### `PROJECT_TEMPLATE.md`

- Add `CLAUDE.md` (short) and `AGENTS.md` (commands) as required day 0 files
- Reference the layered memory hierarchy
- Add a `hooks/` recommendation: at minimum `lint-on-edit` if applicable

### New artifact: `HOOKS_GUIDE.md`

- Currently we have nothing on hooks
- Should cover: when to use hooks vs CLAUDE.md vs skill, how to write one (Anthropic supports prompts like *"write a hook that runs ESLint after every file edit"*), how to install in `.claude/settings.json`
- Examples specific to our setup: lint-on-edit, tests-on-domain-change, git-status-on-session-start

## Recommended next moves

In priority order:

1. **Apply CLAUDE.md size discipline** (max 80 lines) when writing `CLAUDE_MD_GLOBAL.md` — biggest correction to my earlier plan.
2. **Adopt AGENTS.md** as the project-level commands/standards file. One file, both Claude Code and Codex read it.
3. **Add hooks layer** to the playbook. New artifact `HOOKS_GUIDE.md` with 3-5 concrete hook examples.
4. **Formalize Writer/Reviewer** in `WORKFLOW.md`. Konstantin's intuition is officially blessed by Anthropic; let's not bury it.
5. **Use `@` imports** in `CLAUDE.md` for progressive disclosure — native, no plugin needed.
6. **Update `LESSONS_FROM_WK.md`** with named failure patterns from Anthropic linked to WK examples.
7. **Add "Let Claude interview you"** to `WORKFLOW.md` as the new-feature-discovery pattern. Replaces our consideration of Superpowers for that specific moment.

After these seven moves, the playbook is:
- Smaller (CLAUDE.md under 80 lines, with `@` imports)
- More practical (hooks as deterministic layer)
- Standard-aligned (AGENTS.md, Writer/Reviewer pattern)
- Honest about lessons (named failure patterns)
- Avoids reinventing what Claude Code already supports

## Sources

- [Best Practices for Claude Code](https://code.claude.com/docs/en/best-practices) — Anthropic official
- [Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) — HumanLayer
- [AGENTS.md specification](https://agents.md/) — open standard
- [How to write a great agents.md](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/) — GitHub blog
- [12-factor agents](https://github.com/humanlayer/12-factor-agents) — humanlayer
- [smartwhale8/claude-playbook](https://github.com/smartwhale8/claude-playbook) — production-ready scaffolding template
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) — curated list
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Anthropic research (orchestrator-workers pattern)
