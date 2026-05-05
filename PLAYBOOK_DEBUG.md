# Playbook: Debug

Use when something is broken and the cause is not obvious.

The goal is to find the root cause, not the next plausible patch. Patches without root cause produce repeat breakage and the same bug fixed in three places.

## When To Use

- A test or build that was passing now fails.
- A user reports broken behavior that the agent cannot immediately explain.
- The same symptom returned after a previous "fix."
- An error message appears in production logs and the trigger is unclear.
- The agent is about to attempt a fix without knowing why the bug exists.

Skip this for typo fixes and obvious one-line errors.

## Steps

### 1. Reproduce

Before reading any code, reproduce the failure deterministically.

- What input or action triggers it?
- Does it happen every time or only sometimes?
- Does it happen on a fresh state, or only after specific prior actions?

If you cannot reproduce, you cannot fix. Stop and find the trigger first.

### 2. Read the error carefully

The error message and stack trace are usually telling you exactly where to look.

- Read the full error, not just the headline.
- Note the file and line number.
- Note any preceding warnings or related logs.

If the error is a generic message ("something went wrong") that hides the real one, instrument the code to surface the real error first.

### 3. Inspect recent changes

What changed recently in or near the failing code?

```bash
git log -10 --oneline
git diff HEAD~1 -- <suspect_file>
```

Recent changes are the most likely cause of a new failure.

### 4. Form one hypothesis at a time

Pick one specific cause and test it.

- "I think the bug is X because of evidence Y."
- The hypothesis must be falsifiable — there must be a check that proves it wrong.

Do **not** make multiple changes hoping one will fix it. If two of them are wrong and one is right, you cannot tell which.

### 5. Make the smallest fix at the root cause

Once the hypothesis is confirmed:

- Fix the underlying cause, not the symptom.
- The fix should be small and focused on one thing.
- If the fix is large or touches multiple files, you may not have the root cause yet — re-check.

### 6. Verify the original symptom is gone

Run the exact reproduction steps from step 1 again.

- The original failure must no longer occur.
- Adjacent flows must still work (no regression).
- If the bug had a test, the test must now pass. If it did not, consider adding one (`AI_WORKING_RULES.md` Rule 11).

## Output To User

Keep the report short:

- **What was broken** — one sentence.
- **Root cause** — one sentence, no jargon.
- **The fix** — what changed, in one or two lines.
- **What was verified** — exactly which check was run and what it returned.
- **Whether anyone needs to manually test** — usually nobody, but say it explicitly.

## Anti-Patterns

These look like debugging but are not:

- **Stab-and-pray** — making changes hoping one fixes it. Wastes time and pollutes git history.
- **Symptom suppression** — wrapping the failing call in `try/catch` so the error stops appearing. The bug is still there.
- **Premature refactor** — using the bug as an excuse to restructure unrelated code. Increases risk and obscures the actual fix.
- **Patching one fork** — fixing the bug in one role's code path while the same bug lives in another role's code path (see `LESSONS_FROM_WK.md` Lesson 13).
- **"Looks fine to me"** — declaring the bug fixed without re-running the reproduction.

If the agent finds itself doing any of these, stop and restart from step 1.

## When To Escalate

If after one focused debug pass the bug is still not understood:

- Hand the problem to the other agent (Claude Code ↔ Codex) with the reproduction steps, the rejected hypotheses, and what is known.
- Do not keep flailing in the same context.

A second agent reading the same code with fresh context often spots the cause in minutes.
