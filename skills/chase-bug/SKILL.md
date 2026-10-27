---
name: chase-bug
description: Investigate and fix a reported defect using Chase engineering standards, evidence-based diagnosis, focused changes, and regression verification. Use for incorrect behavior and failing tests; use chase-task for planned features and refactors.
---

# Chase bug

Find the cause of the reported failure and fix the affected behavior. Distinguish observations, hypotheses, and confirmed causes throughout the investigation.

## Load context

1. Read [Chase engineering standards](../../standards/engineering.md), resolving the path relative to this file. If it is missing, locate the complete Chase Workshop checkout rather than guessing its contents.
2. Establish the work repository, read applicable agent and project guidance, and read `<work repo>/.agents/chase-project.md` if present. Keep application edits in the work repository.
3. Inspect existing changes before editing and preserve unrelated work.

## Investigate

- Establish expected versus actual behavior, the failing input or workflow, and relevant environment details. Use available logs, tests, issue context, and history before asking for information already present.
- Reproduce the failure with the smallest useful case when practical. If reproduction is unavailable, record the evidence and missing conditions; do not claim reproduction or a confirmed cause without support.
- Trace the failing path through callers, state changes, boundaries, and error handling. Check other callers that share the suspected behavior. Search for an existing correct implementation or regression test before adding one.
- Test the leading explanation against the evidence. Do not fix the first suspicious line merely because it looks unusual. Narrow an uncertain diagnosis before making broad changes.
- If the expected behavior is genuinely ambiguous, clarify the product contract. A failing test, current output, or old comment is evidence rather than unquestionable authority.

## Fix and verify

- Make the smallest coherent fix for the established cause. Preserve compatibility outside the intended correction. Avoid patches that hide the failure with an empty catch, fabricated default, arbitrary delay, or unbounded retry.
- Prefer a regression test that fails on the original implementation and passes with the fix. Capture the pre-fix failure before editing when practical. If it was not checked, say so; never report an inferred red/green result as observed.
- Include other affected callers or a related boundary case where the diagnosis shows they are at risk. Choose the appropriate test level using the project's setup, rather than automatically adding both unit and end-to-end tests.
- Verify the original failure path, relevant surrounding behavior, and applicable project checks. Exercise the real app or interface when practical. Do not weaken an assertion merely to match the broken behavior.
- Inspect the final diff for collateral changes, stale comments, duplicated logic, and unnecessary complexity. Finish independent work if infrastructure blocks part of the verification.

Close with the failure and cause, the fix, the verification actually performed, and any remaining uncertainty. Identify evidence-based causes separately from hypotheses when the investigation remains incomplete.

This workflow does not itself authorize commits, pushes, PRs, deployment, or unrelated external actions. Respect authorization already given.
