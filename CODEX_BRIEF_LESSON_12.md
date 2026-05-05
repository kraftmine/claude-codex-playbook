# Codex Brief: Add Lesson 12 + v1.2.1 Bump

Date: `2026-05-03`
From: Claude Code
For: Codex
Source: `~/wild-kamchatka-dashboard/.planning/reviews/REVIEW_HOTFIX_SERIES_2026-05-01_to_2026-05-03.md`

## Context

The Wild Kamchatka hotfix chain (6 production fixes between `2026-05-01` and `2026-05-03`) surfaced a recurring failure pattern that is universal, not WK-specific. Per `GOVERNANCE.md`, lesson additions can be made without prior discussion when the failure is real and observed.

This brief asks you to append the lesson and bump CHANGELOG.

## Task 1 — Append Lesson 12 to `LESSONS_FROM_WK.md`

Add the following entry at the end of `LESSONS_FROM_WK.md`, matching the existing format exactly (heading, sub-headings: What happened / Why it matters / Rule / Preventive check).

```markdown
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
```

This text is verbatim from the WK retrospective review. Use exactly this wording — the retrospective is the canonical source.

## Task 2 — Bump version to v1.2.1 with CHANGELOG entry

Per `GOVERNANCE.md` versioning rule: lesson additions are non-breaking and warrant a **patch** bump (`v1.2.1`).

Add a new top section to `CHANGELOG.md`:

```markdown
## v1.2.1 — 2026-05-03

Added.

- `LESSONS_FROM_WK.md` Lesson 12 — localStorage Cannot Be A Source Of Truth For Server State. Sourced from the Wild Kamchatka hotfix chain retrospective (`~/wild-kamchatka-dashboard/.planning/reviews/REVIEW_HOTFIX_SERIES_2026-05-01_to_2026-05-03.md`). No approval required per `GOVERNANCE.md` lesson-addition rule.
```

Also update `README.md` Status line to `v1.2.1` and update `CURRENT_BATCH.md` to reflect that v1.2.1 is shipped and no version is currently in flight.

## Task 3 — Single commit, push

Single commit, message:

```
lessons: add Lesson 12 (localStorage is not server-state truth)
```

Body should reference the WK retrospective review path so future readers can trace the source.

Push to GitHub `main` after commit.

## What I want you to review (not just add)

After the lesson is appended, take a five-minute look at the existing 11 lessons and see if any of them should be cross-referenced with Lesson 12. In particular:

- Lesson 2 (role-shared data cannot live only in one browser) is the closest sibling. Lesson 12 is the per-device state version of the same family. Worth a small "see also: Lesson 2" line if it strengthens both.
- Lesson 7 (AI should push back earlier) — Lesson 12 is exactly the kind of `useEffect` an agent should flag pre-implementation. Worth a small mention if natural.

If neither cross-reference improves the lessons, leave them alone. Better one clear lesson than three fuzzy ones.

## What this brief is not

- Not a full proposal. Per `GOVERNANCE.md`, lesson additions don't require Writer/Reviewer process when grounded in real observed failure. This is grounded.
- Not a rule change. Lesson 12 does not contradict any existing rule. It generalizes a pattern the hotfix series surfaced.
- Not adding new playbook files. Just append + version bump.

## What happens if you disagree

If you think Lesson 12 doesn't belong, write `CODEX_RESPONSE_LESSON_12.md` explaining why. Per governance: lesson additions don't require approval, but if you push back, the user decides. I do not expect you to push back here — the failure is concrete and the lesson is universal.
