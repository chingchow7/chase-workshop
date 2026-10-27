---
name: chase-pr-readiness
description: Review completed changes for pull-request readiness against Chase engineering standards, including correctness, reuse, scope, comments, contracts, and meaningful test coverage. Use before opening or updating a PR or when asked to review a branch, commit, diff, or PR. Report findings before editing.
---

# Chase PR readiness

Review the actual change and enough surrounding code to judge its consequences. Default to report-only: do not edit application files, stage, commit, or publish findings. A request to review does not authorize fixes. When the user explicitly requests fixes, identify findings first, apply the authorized changes, and recheck the affected behavior.

## Establish scope

1. Read [Chase engineering standards](../../standards/engineering.md) relative to this file. If missing, locate the complete checkout rather than claiming to have applied it.
2. Establish the work repository and read applicable project instructions plus `<work repo>/.agents/chase-project.md` if present.
3. Follow [scope resolution](references/scope.md) to identify the requested target, comparison base, and relevant local changes. Never assume the target branch is `main`. State the reviewed scope and resolved revisions.
4. Read the diff, affected implementations, relevant callers, contracts, and tests. Include changed behavior that lacks tests; reviewing only modified test files is insufficient.

## Review in focused passes

Apply the shared standards through these lenses. Work sequentially by default; these are review passes, not requirements for separate agents or installed reviewer skills.

| Pass | Questions that matter |
| --- | --- |
| Behavior and failures | Does the change satisfy the requested outcome? What concrete inputs, states, or failures expose a regression? Are errors truthful and actionable? |
| Boundaries and contracts | Are callers, authorization, persisted data, public names, configuration, and side effects still compatible? Consider concurrency or partial updates when relevant. |
| Reuse and structure | Does suitable functionality already exist? Does the design reduce complexity or distribute it across more layers? Are new abstractions and dependencies justified? |
| Types and names | Does the change use existing domain contracts and preserve useful guarantees? Do new names misstate behavior, units, or representation? |
| Test quality and coverage | Would a plausible broken implementation pass? Do assertions execute, inspect the relevant contract, and exercise the subject rather than its replacement? Is important changed behavior missing coverage? |
| Comments and scope | Are added or affected comments necessary and accurate? Are unrelated edits, stale explanations, session narration, or avoidable churn present? |

For each candidate finding, reread the location and check the relevant callers and constraints. Report defects introduced by the change or existing behavior the change makes newly problematic. An old issue merely nearby is not a PR finding. For an explicitly requested file snapshot, review issues present in the named files without claiming they were introduced by a diff.

Distinguish confirmed impact from unanswered questions. Give a concrete trigger and consequence for correctness findings; for maintainability findings, identify the actual duplicated responsibility, ambiguity, or unnecessary moving parts. Aesthetic preference alone is insufficient. Check that a proposed remedy fits existing contracts and would actually simplify the code.

## Verification and restraint

- Run relevant non-destructive checks when practical and allowed. Report-only review may run tests, but avoid commands that rewrite sources, snapshots, or fixtures or affect shared services without authorization.
- Treat CI results as evidence only when their revision and scope are known. Do not infer a passing pipeline from configuration files or from a claim about another revision.
- When practical, demonstrate a weak test with a concrete missed regression. If deliberately breaking the implementation would help, use an isolated copy and existing execution permissions; do not mutate the user's worktree during review.
- Identify skipped applicable passes and unavailable verification. Distinguish checks that do not apply from checks that were not performed. A prose-only change does not need application tests simply to fill a checklist.
- Consolidate duplicate findings and reconcile contradictory remedies. Preserve user decisions from earlier rounds; revisit one only with materially new evidence. Review other changes normally.
- Do not manufacture findings, demand arbitrary file sizes or assertion styles, or propose speculative refactors. Avoid repeated review loops without new changes or evidence.

## Report

Lead with actionable findings, ordered by consequence. For each, give a verified `path:line`, a short title, the trigger and consequence, and a focused remedy. Label it **Blocking** when a demonstrated defect or violated requirement should prevent merging; label other worthwhile improvements **Suggestion**. Keep unresolved questions separate from findings and explain what would settle them.

Finish with the reviewed scope, verification performed or unavailable, and one assessment:

- **Changes needed:** blocking findings remain.
- **No blocking findings:** review completed without a blocking issue; this is not a claim that every possible defect was excluded.
- **Review incomplete:** missing scope, requirements, access, or evidence prevents a meaningful assessment. Identify the gap, even if some findings are already known.

Mention limitations alongside the assessment. A missing critical verification can make the review incomplete; a non-applicable check does not. Keep optional suggestions separate, and say plainly when there are no findings. If requested, draft a PR description using observed changes and verification without claiming unperformed checks.
