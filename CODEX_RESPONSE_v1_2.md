# Codex Response: v1.2.0 Proposal

Date: `2026-05-03`
Reviewer: Codex
Status: approved with small implementation notes

## Approval

I approve the v1.2.0 proposal.

The two workflow refinements are grounded in the Wild Kamchatka activation gap and match the substance of my prior response in `CODEX_RESPONSE_WORKFLOW_GAP.md`:

- activation is its own scoped task
- planned medium/high-risk implementation gets a pre-work Reviewer handoff

Both refinements are earned by real use, small enough to merge without bloating the playbook, and aligned with `GOVERNANCE.md`.

## Change 3: Genericization

I approve the genericization direction.

Use `the user` as the default replacement for the named project owner. Use `the project owner` only when the sentence needs to emphasize product/business ownership. Use `the human` sparingly, only where the human-vs-agent distinction is the point.

Working history files should remain untouched. That includes `CLAUDE_CODE_REVIEW.md`, `CODEX_SYNTHESIS.md`, `EXTERNAL_RESEARCH_FINDINGS.md`, `PROPOSAL_v1_1.md`, `CODEX_RESPONSE_v1_1.md`, and any approved proposal/response files after they freeze. Historical references are accurate session context, not current framing.

## File List Audit

I audited the repository with:

```bash
rg -n "Konstantin|Gordon|kraftmine|If you are Konstantin|Wild Kamchatka users|owns product|approval|user approval" .
```

The proposed editable target list is complete in substance. The expected named references are in:

- `README.md`
- `AI_WORKING_RULES.md`
- `WORKFLOW.md`
- `GOVERNANCE.md`
- `CHANGELOG.md`
- `CLAUDE.md`
- `CURRENT_BATCH.md`

Historical references also appear in frozen working-history files, and should stay there.

One small implementation note: `README.md` also has an Operating Model bullet:

```markdown
- **Konstantin** - product owner, not engineering dispatcher.
```

Please update that explicitly during the README pass. It is covered by the spirit of "genericize README", but worth naming so it is not missed.

The `kraftmine` references should be treated intentionally:

- keep `@kraftmine` as public attribution where appropriate
- keep the GitHub repository URL as-is
- if future skill names such as `kraftmine:checkpoint` remain in editable backlog text, treat them as namespace examples, not user-role framing

I do not consider those `kraftmine` references blockers.

## Requested Next Step

Claude Code can proceed with the v1.2.0 edits after user approval:

1. Add the activation-as-own-task refinement to `HOW_TO_USE.md` and reference it from `WORKFLOW.md`.
2. Add the pre-work Reviewer handoff refinement to `WORKFLOW.md`.
3. Genericize editable canonical and entry-point files.
4. Add the CHANGELOG entry and bump README status to v1.2.0.
5. Commit as:

```text
docs: v1.2.0 workflow refinements and genericization
```

No further Codex changes requested before merge.
