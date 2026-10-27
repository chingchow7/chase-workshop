---
name: chase-task
description: Implement a development task, feature, or planned refactor using Chase engineering standards, existing project patterns, and behavior-focused verification. Use for requested implementation work; use chase-bug for defect diagnosis and chase-pr-readiness for a review of completed changes.
---

# Chase task

Carry the requested task through implementation and relevant verification. A plan alone does not complete an implementation request.

## Load context

1. Read [Chase engineering standards](../../standards/engineering.md), resolving the path relative to this file. If it is missing, locate the complete Chase Workshop checkout; do not silently substitute remembered standards.
2. Establish the work repository separately from this skills repository. Read applicable agent instructions, project guidance, and `<work repo>/.agents/chase-project.md` if present. The optional project file supplies local conventions; it is not a prerequisite or a reason to generate configuration.
3. Inspect the working tree before editing. Preserve unrelated work and distinguish existing changes from your own.

## Implement

- Establish acceptance criteria from the request: the expected outcome, relevant failure cases, and compatibility constraints. State material assumptions briefly. Ask only about unresolved choices that change those outcomes; continue useful independent work while waiting.
- Inspect relevant code paths, callers, shared implementations, and tests. Search for existing behavior before introducing a helper, type, dependency, or service. Reuse only where semantics fit.
- Choose a focused implementation. For a substantial architectural choice, compare credible alternatives briefly; do not require a design ceremony for routine edits.
- Apply the shared standards as you write. Preserve established layer boundaries and domain terminology. Avoid unrelated cleanup and speculative abstractions.
- For a planned refactor, identify the observable behavior and contracts that must stay stable, including errors and side effects. Keep feature changes separate unless explicitly requested. Inspect affected references rather than using broad textual replacement for renames.
- Update documentation or configuration when the task changes the contract they describe. Keep comments necessary and concise.

## Verify and finish

- Choose tests and commands from the work repository's actual setup. Cover the changed behavior at its relevant boundary, with important failure cases. Follow the verification standards rather than adding tests solely because a file changed.
- Exercise the affected user flow or integration when practical. Report what was actually observed and any environment gaps.
- Inspect the final diff for mistakes, duplicated functionality, unnecessary comments, compatibility changes, and unrelated edits. This self-review does not require invoking another skill.
- Run further checks when new edits or failures warrant them. If progress depends on unavailable input or infrastructure, finish independent work and state exactly what remains unresolved.

Close with the outcome, relevant verification and results, and material limitations. Keep the report proportional to the task. Make clear whether a PR-readiness review has also been requested and performed; do not imply one happened merely because you self-reviewed.

This workflow does not itself authorize commits, pushes, PRs, deployment, or unrelated external actions. Follow any authorization already supplied by the user without asking for it again.
