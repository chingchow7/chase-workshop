---
name: chase-pr-review
description: Review a submitted pull request, merge request, or another author's change for correctness, security, least privilege, performance, reuse, project conventions, tests, and unnecessary prose. Use for a reviewer assessment; use chase-pr-readiness to prepare your own completed work for submission. Report findings without editing or posting unless authorized.
---

# Chase PR review

Act as a careful code reviewer. Perform a complete engineering review and give particular attention to Chase's priorities; they supplement normal judgment rather than replace it with a keyword checklist.

## Establish context

1. Read [Chase engineering standards](../../standards/engineering.md) relative to this file. If missing, locate the complete checkout rather than guessing its contents.
2. Establish the application repository and read applicable project instructions and `<work repo>/.agents/chase-project.md` if present. Learn the actual patterns, canonical components and service libraries, data model, and relevant test commands before judging the change.
3. Read and follow the [shared review guide](../../standards/review.md), including scope resolution, every relevant review area, and verification. Read its linked AWS notes when the change touches DynamoDB or IAM/Lambda permissions.
4. Read [the PR-review report format](references/report.md). Its summary-first presentation replaces the shared guide's default findings-first order; keep the shared evidence and assessment requirements.

## Review the requested change

- For a supplied PR or MR, establish its real target and head revision. Inspect the changed files and relevant callers at that revision. Keep later local fixes separate; do not silently review your worktree instead of the published change.
- Read accessible existing review threads, inline comments, and relevant bot findings before drafting new comments. Independently verify whether each overlapping claim still applies to the current revision and whether it has been resolved; use the report format's agreement section instead of repeating an existing issue. If thread access is unavailable, state that duplicate checking was not possible and continue the code review.
- Read the task or PR description for intent, then verify it against the implementation. State material missing requirements as questions. Documentation length, an AI-looking comment, or a claim that CI passes is not evidence of a correctness defect by itself.
- Trace important changed behavior end to end, including its callers, trust boundaries, persistence, and failures. Include relevant infrastructure and policy changes, shared consumers, UI behavior, and meaningful tests. Do not limit the review to security and style or to the files that happen to have tests.
- Apply the shared guide's checks for documentation and ticket noise, least privilege, costly access patterns, semantic reuse, schema conventions, and maintainability. Verify each candidate against existing constraints before reporting it.

Default to a report in the current conversation. Do not edit code, post review comments, approve, request changes through the hosting service, or merge without authorization. If the user already authorized a specific external review action, honor that scope after preparing findings. A PR review request alone does not authorize publishing it.

Produce the report in the required order: short plain-language summary, up to three priority files, then precise findings and existing comments worth supporting. Quote the actual code at each proposed comment location; distinguish the suggested author-facing comment from the explanation and evidence for the reader. Keep the comments concise, specific, and respectful, allow a clean result, and avoid requiring an essay to justify routine code.
