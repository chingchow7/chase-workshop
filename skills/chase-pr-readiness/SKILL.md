---
name: chase-pr-readiness
description: Check your own completed change before opening or updating a pull request, including review findings, verification gaps, and submission readiness. Use for a pre-submission check of local work; use chase-pr-review for a reviewer assessment of a submitted PR or another author's change.
---

# Chase PR readiness

Check the author's completed work before submission. Apply the same engineering review bar as `chase-pr-review`, then identify anything needed to make the change ready for review.

## Establish scope

1. Read [Chase engineering standards](../../standards/engineering.md) relative to this file. If missing, locate the complete checkout rather than claiming to have applied it.
2. Establish the work repository and read applicable project instructions plus `<work repo>/.agents/chase-project.md` if present.
3. Read and follow the [shared review guide](../../standards/review.md), including its scope reference, review areas, verification rules, and evidence-based report. Report-only is the default; fixes and external actions require user authorization, including authorization already supplied.

## Submission checks

- Unless the user requests a specific revision or layer, assess the final local change: committed branch changes plus relevant staged, unstaged, and untracked work. Identify anything that is still local rather than in an existing PR.
- Apply every relevant review area in the shared guide. Security, performance, reuse, documentation quality, and project conventions matter before submission as well as during independent review.
- Confirm that the change satisfies the task and that intended files, contract updates, and meaningful test coverage are included. Separate implementation defects from missing verification or incomplete submission context.
- When asked, draft a concise PR description grounded in the actual change, its purpose, and observed verification. Identify required configuration or rollout steps when the change needs them; do not invent a rollout process for an ordinary edit.

Finish with the shared guide's findings and assessment, then a short list of remaining submission work if any. Do not create, update, approve, merge, or publish a PR merely because this skill ran.
