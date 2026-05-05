# Lessons From Wild Kamchatka

This document captures real mistakes from the Wild Kamchatka dashboard and turns them into reusable rules.

The tone is not blame. The point is to make future work easier.

## Lesson 1: Monoliths Make Every Change Riskier

What happened:

- `src/App.jsx` became too large and absorbed unrelated concerns.
- UI, business logic, permissions, persistence assumptions, and workflows became tangled.
- Simple bugfixes became scary because one file contained too much state.

Why it happened:

- Early speed was prioritized over structure.
- Agents followed feature requests locally instead of pushing back on architectural accumulation.

Rule:

- New reusable logic goes into `src/domain`, `src/hooks`, `src/ui`, or feature modules.
- Huge files may receive narrow hotfixes, but should not receive new subsystems.

Preventive check:

- Before substantial edits, inspect target file size and ask: "Am I adding logic that belongs somewhere else?"

## Lesson 2: Role-Shared Data Cannot Live Only In One Browser

What happened:

- Some settings were initially tempting to store in local browser state.
- But owner, Marina, and sellers need to see the same operational truth.

Why it matters:

- `localStorage` works for one browser, not for a multi-role operations system.

Rule:

- If multiple people/roles/devices must see it, use Supabase or another shared source.
- If local storage is used temporarily, name it as debt and schedule migration.

Preventive check:

- Ask: "Who else needs to see this data, and from where?"

See also: Lesson 12 — the creation-side variant (gating server-state writes on `localStorage` flags re-fires on every fresh device).

## Lesson 3: Hidden UI Is Often Experienced As Broken

What happened:

- Inventory tasks existed but were too hidden in Marina's flow.
- The user reasonably perceived this as "it does not display."

Why it happened:

- The system had the data, but not enough role-specific visibility and notification.

Rule:

- If a role has an action to perform, show a clear badge/banner in that role's main workflow.

Preventive check:

- Browser smoke should verify not only that data exists, but that the intended role can find the next action.

## Lesson 4: Deploys Need A Ritual, But A Short One

What happened:

- Fast iteration made it easy to blur local build, live deploy, manual smoke, and rollback state.

Rule:

- Every live deploy needs build, tests, smoke, backup, and live bundle verification.

Preventive check:

- Use `PLAYBOOK_DEPLOY.md`.

## Lesson 5: Business Rules Need Names

What happened:

- Percentages, salaries, permissions, and warehouse ownership rules appeared as inline assumptions.

Why it matters:

- Inline business rules are hard to audit and easy to contradict.

Rule:

- Money, permissions, role access, and inventory rules must have named helpers/constants and tests where practical.

Preventive check:

- Search for magic values when touching finance, payroll, stock, or permissions.

## Lesson 6: Manual User Testing Should Be Focused, Not Exhaustive

What happened:

- After every change, it felt like the user might need to recheck every screen.

Better approach:

- Agents should identify affected flows and run smoke tests.
- The user should only manually check the flows that changed or are high risk.

Rule:

- End reports must say exactly what the user should manually verify, if anything.

## Lesson 7: AI Should Push Back Earlier

What happened:

- Some issues were caused by agents accepting the next visible request without challenging structure.

Rule:

- If a request increases monolith size, duplicates logic, hides shared data locally, or weakens rollback safety, the agent must pause and recommend a safer path.

Preventive check:

- Before implementation, answer: "Does this make the next change easier or harder?"

## Lesson 8: Git Neglect Costs More Than It Saves

What happened:

- Wild Kamchatka had weeks of important work ahead of `HEAD`.
- Some recovery confidence depended on filesystem snapshots instead of clean commits and remote backup.

Why it matters:

- Without commits, every risky refactor becomes scarier.
- Without remote backup, a single device failure can erase progress.

Rule:

- Commit or checkpoint after meaningful boundaries, before risky operations, and after deploys.
- Push when a trusted remote exists and the project expects cloud backup.

Preventive check:

- Start substantial sessions with `git status --short`.
- If the tree has been dirty too long, propose a checkpoint before more work.

## Lesson 9: Mutable Globals Defeat Extraction Later

What happened:

- Shared runtime objects such as warehouses, products, and staff started as convenient module-level state.
- Later redesign/extraction work became harder because data flow was implicit.

Why it matters:

- Mutable globals make it unclear who owns data, who updates it, and which role sees the truth.
- They are fast early and expensive later.

Rule:

- Shared business data should live in an explicit data layer, context, database, or function arguments.
- If a global is temporary, name the debt and set a cleanup trigger.

Preventive check:

- Ask: "If another role/browser needs this value, where does it come from?"

## Lesson 10: Half-State i18n Is Dead Code

What happened:

- Translation infrastructure existed before the product had a full localization path.
- Some strings stayed hardcoded, so the system looked more internationalized than it really was.

Why it matters:

- Half-built infrastructure creates false confidence.
- Future agents may assume a feature is ready because the scaffolding exists.

Rule:

- Either commit to localization as a real product requirement or remove/park the unused abstraction.
- If localization is required later, track catalog translation, UI strings, role defaults, and testing as one feature.

Preventive check:

- Ask: "Can a real user complete this flow in the target language today?"

## Lesson 11: Name Common AI Failure Patterns

What happened:

- Wild Kamchatka hit several universal AI-collaboration failure modes:
- kitchen-sink session: too much accumulated in `App.jsx`
- trust-then-verify gap: assumptions looked done before build/test/smoke confirmed them
- correcting over and over: some bugs were patched locally before the real framing was found
- infinite exploration: repeated audits read similar context without producing a durable rule

Why it matters:

- Named patterns are easier to catch early.

Rule:

- When a session starts to repeat itself, stop and convert the lesson into a rule, test, ADR, or playbook.

Preventive check:

- Ask: "Are we learning something new, or circling the same failure pattern?"

## Lesson 12: localStorage Cannot Be A Source Of Truth For Server State

What happened:

- A `useEffect` checked `localStorage["wk_last_audit_date"]` to decide whether to auto-create three inventory audits.
- Fresh devices had no entry, so the effect ran on first login and created phantom audits.
- After 54 legacy audit rows were deleted from Supabase, the next user who logged in on a new phone re-created them.

Why it matters:

- `localStorage` is per-browser, per-device. Anything gated on `localStorage` will fire on every fresh device login, regardless of whether the corresponding server-side state already exists.
- This is a class of bug, not a one-off: any feature gated by browser-local memory will leak through onboarding flows, multi-device users, incognito sessions, and cleared caches.

Rule:

- Do not gate the creation of shared server state on `localStorage` checks.
- If a feature needs "do this once," derive that from the server state directly (does the row already exist?), or remove the auto-creation entirely and require an explicit user action.

Preventive check:

- When reviewing any `useEffect` that creates rows in Supabase or other shared storage, ask: "What happens on a fresh browser/device with empty localStorage? Will this run again? Will it duplicate state?"

See also: Lesson 2 — same family (browser-local state vs. shared truth), different angle (Lesson 2 is about *visibility* across roles, Lesson 12 is about *creation* of shared state being gated by per-device memory).
