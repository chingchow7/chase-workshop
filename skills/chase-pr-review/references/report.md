# PR-review report format

Use this order for `chase-pr-review`. Keep the shared review guide's scope, evidence, impact, and final-assessment requirements. This reference controls presentation so the report is useful to someone placing comments manually.

## 1. Quick summary

Write two or three plain-language sentences, at most ten words each. Explain what the change does without assuming implementation knowledge. Briefly mention material risk or missing context when established. Prefer familiar words over acronyms and implementation details. Do not claim a clean review when evidence is missing.

## 2. Most important files

List the top two or three changed files, or fewer if fewer deserve attention. Give each path and a description of at most five words. Rank by changed behavior and risk, rather than file length or position in the diff.

Handlers, service logic, and shared behavior often deserve attention before routine wiring or boilerplate. Security-sensitive IAM/CDK, schema migrations, or infrastructure can be the highest-risk files; do not discount them because they are infrastructure. This is a reading-priority list, not a limit on which files the review examines.

## 3. Review report

Put consequential issues before optional suggestions. Separate new comments from existing comments to support. For each proposed new comment, provide:

1. **Priority and title:** `Blocking` or `Suggestion`, with a short, specific title.
2. **Where to comment:** exact repository-relative file path and verified one-based line, or the smallest useful line range. Identify the old or new diff side and the reviewed head revision. Prefer a changed line where the issue occurs. For a deletion, quote and identify the old-side code. If no valid inline anchor exists, say it needs a general PR/file comment; never invent an anchor.
3. **Code at that location:** a verbatim fenced snippet from the reviewed revision containing the cited line. Include only enough surrounding code to recognize it. Do not substitute proposed replacement code for the current code, or quote a later local fix as the published PR. For a documentation issue, quote the relevant text. If a snippet cannot be verified, identify the gap instead of offering a supposedly exact inline comment.
4. **Suggested comment:** ready-to-post text for the author, normally one or two short sentences. State the concrete problem and useful next action. Keep it precise, accurate, and free of speculation or rhetorical questions. Do not include the report's internal analysis in this comment.
5. **Why this matters:** a short plain-language explanation to the report's reader, separate from the suggested comment. Explain the failure or maintenance cost without repeating a long technical analysis.
6. **Evidence and remedy impact:** label the evidence `Observed`, `Traced`, or `Mixed`. Give the actual command/action and result when observed, or the concrete input/state and relevant path when traced. Include useful references or results when available. Label the proposed remedy's behavior impact as required by the shared guide, including affected consumers when relevant. Never imply execution, a measured performance result, or an exploit was observed when it was only inferred.

Anchor each snippet and line to the same revision. Recheck after any update before claiming the comment still lands correctly. Use a verified diff/file link when available; a precise path, line, and quoted code are still required. Keep extra context proportional to the issue.

### Existing comments to support

When an existing human or bot comment already identifies the same issue, do not draft another new comment for it. Compare the underlying claim and remedy, not merely matching words or line numbers.

For an existing issue worth highlighting, give:

- Its priority, author/bot, and verified thread link or identifier.
- A short description of the issue and its current code location/snippet when available.
- Whether you agree, partly agree, or disagree, with a concise reason and the evidence independently checked.
- A recommended action such as "Support this comment; resolve before merging." Recommending a plus-one is not authorization to add a reaction or reply.

Do not endorse a claim because CodeRabbit or another reviewer made it. Check current code, later fixes, and thread resolution. Omit stale or already-fixed claims from the outstanding-issue list; mention a resolved high-impact issue only when its verification matters. Add a separate finding only for a materially distinct issue or missing consequence, and link the related thread.

If existing comments could not be read, say duplicate checking was unavailable. Do not claim there are no prior comments. If no new findings exist but important existing comments remain valid, say "No new comments; existing issues remain" rather than calling the change clear.

### Close

End with the reviewed target/head/base and included local layers, checks performed or unavailable, and the shared assessment: `Changes needed`, `No blocking findings`, or `Review incomplete`. Include verified outstanding issues from existing comments in that assessment. Say plainly when there are no findings; do not fill the report with cosmetic comments.

The summary is always first. Additional technical evidence belongs with its finding or in the short verification close, not in an opening essay.
