# Resolve the review scope

Run commands in the application repository, not the Chase Workshop checkout. Inspect `git status --short --branch`, the current branch, and remotes before choosing comparisons. Preserve existing work.

## Choose the target

| Request | Comparison |
| --- | --- |
| Existing PR | Use its actual target and head revisions from available metadata. Verify that a local checkout matches the requested revision before attributing local checks to it. |
| Branch versus a named target | Resolve both refs and compute their merge base. Review the branch tip against that base, excluding unrelated target-branch changes. |
| Single commit | Compare it with its first parent. For a root commit, use Git's root-commit diff support. For a merge commit, state the selected parent or clarify if the intended comparison is ambiguous. |
| Explicit range or staged/unstaged diff | Honor the requested endpoints or layer. Explain whether the range represents endpoint differences or changes since a merge base. |
| Explicit path snapshot | Review the current files as a snapshot. Do not claim findings were introduced by a change when no base exists. |
| No target supplied | Determine the work branch's intended target from PR metadata, explicit project configuration, or trustworthy branch context. The upstream may be the same feature branch on a remote, so it is not automatically a review target. If still ambiguous, ask for the target while inspecting local changes independently. |

The remote default branch is evidence, not proof of the feature's intended target. If a required ref is missing, fetch it when network access is authorized; otherwise report the missing comparison rather than substituting a guessed base. State when using locally cached remote refs without refreshing them.

## Inspect the relevant layers

For a normal branch-readiness review, inspect committed branch changes and separately identify staged, unstaged, and relevant untracked files. For example, after resolving real refs:

```text
git merge-base <target-ref> <head-ref>
git diff --stat <merge-base> <head-ref>
git diff <merge-base> <head-ref>
git diff --cached
git diff
git ls-files --others --exclude-standard
```

These commands inspect different layers; do not concatenate their patches and assume they describe the final file. Read the final worktree contents to reconcile overlapping edits. Do not report an issue already corrected locally as a defect in the final local change. If the published PR still contains it, distinguish that remote state from the local fix.

For an explicitly committed or published target, keep findings tied to that target. Mention later local fixes separately; do not silently replace the requested revision with the worktree. Local checks on a modified tree are evidence about that tree, not proof about a clean remote revision.

Inspect both old and new paths for renames and deletions, and confirm current line numbers before reporting. Identify generated artifacts, submodules, binary changes, or inaccessible files that the review cannot assess. An empty branch diff with local changes is not an empty review; a genuinely empty scope should be reported as such.

Record enough scope to reproduce the review: target branch or revision, resolved head and base, and which local layers or paths were included. Once those are clear, continue the review without repeatedly asking for confirmation.
