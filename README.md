# Chase Workshop

Three development workflows for focused implementation, evidence-based bug fixes, and careful pull-request review.

The skills apply shared engineering standards while working with the project's own architecture, tooling, and CI. They are Markdown instructions for a coding agent; they do not enforce behavior or guarantee a clean PR.

## Choose a skill

| Skill | Use it for | Expected result |
| --- | --- | --- |
| [chase-task](skills/chase-task/SKILL.md) | A feature, development task, or planned refactor. | A focused implementation with appropriate verification and an honest completion report. |
| [chase-bug](skills/chase-bug/SKILL.md) | Incorrect behavior, a regression, or a failing test. | An evidence-based diagnosis, a coherent fix, and regression verification where practical. |
| [chase-pr-readiness](skills/chase-pr-readiness/SKILL.md) | Completed changes before opening or updating a PR. | A scoped review with actionable findings, verification limits, and a readiness assessment. Report-only unless fixes are explicitly requested. |

All three read [Chase engineering standards](standards/engineering.md). Standards apply during implementation as well as review: necessary comments, semantic reuse, appropriate complexity, compatible contracts, truthful errors, and tests that can catch broken behavior.

## Use the local checkout directly

Keep this repository accessible to the agent alongside the application repository. For the initial checkout at `F:/github/chase-workshop`, use these explicit prompts. Replace bracketed task details and the review target with actual values.

**Task**

```text
Read F:/github/chase-workshop/skills/chase-task/SKILL.md and its referenced
standards. Apply that workflow to the current application repository to
implement: [task and acceptance criteria]. Continue through implementation
and relevant verification.
```

**Bug**

```text
Read F:/github/chase-workshop/skills/chase-bug/SKILL.md and its referenced
standards. Apply that workflow to the current application repository to
investigate and fix: [expected behavior, actual behavior, and reproduction
details]. Distinguish confirmed causes from hypotheses.
```

**PR readiness**

```text
Read F:/github/chase-workshop/skills/chase-pr-readiness/SKILL.md and its
referenced standards. Review the current application branch against
[actual target branch], including relevant local changes. Report actionable
findings before editing, and state what you could not verify.
```

If the agent cannot access an external folder, add the checkout to the workspace or use the native-discovery layout below. A public GitHub URL alone does not ensure the agent has read the current instructions and their references.

### Shorter prompts in Cursor

Optionally copy [templates/chase-workshop.mdc](templates/chase-workshop.mdc) into the application repository's `.cursor/rules/chase-workshop.mdc`. Adjust the checkout path for other machines. The rule tells the agent where explicitly requested skills live; it does not duplicate the standards.

Then use:

```text
Use chase-task to implement [feature].
Use chase-bug to investigate and fix [problem].
Use chase-pr-readiness to review this branch against [target branch].
```

Do not overwrite existing project guidance. The locator rule itself is always attached; the full workflows are read when requested. Follow-up instructions can authorize fixes or further work without repeating the setup.

For a less biased PR review, prefer a fresh chat when another chat implemented the change. Supply the task requirements, actual target branch, and relevant constraints so the reviewer can assess the code independently. This is a recommendation, not a prerequisite for review.

### Optional native discovery

Cursor supports project skills under `.cursor/skills/` and discovers nested `SKILL.md` files. To use that discovery, preserve the complete bundle under a category directory:

```text
your-project/
  .cursor/skills/chase-workshop/
    skills/
      chase-task/SKILL.md
      chase-bug/SKILL.md
      chase-pr-readiness/SKILL.md
      chase-pr-readiness/references/scope.md
    standards/
      engineering.md
      examples.md
    LICENSE
    THIRD_PARTY_NOTICES.md
```

Keep the `skills/` and `standards/` relationship intact: copying only an individual skill breaks its shared reference. Include both license notices when distributing the bundle. Type `/` in Cursor chat and select the discovered skill to invoke it explicitly. Use one setup consistently so the agent does not see competing copies. [Cursor skills documentation](https://cursor.com/docs/skills)

Native discovery also allows Cursor to select a skill automatically when it judges the description relevant. Explicit invocation is the recommended way to select the intended workflow reliably; it is not an explicit-only restriction. For named commands, choose `/chase-task`, `/chase-bug`, or `/chase-pr-readiness`. If you want to prevent automatic selection, add `disable-model-invocation: true` to each installed skill's YAML frontmatter. That setting controls Cursor's native discovery, not whether an agent can read the file when instructed directly. [Cursor invocation controls](https://cursor.com/docs/skills#disabling-automatic-invocation)

This repository does not depend on Claude Code plugins, hooks, subagents, or a skill-manager CLI. Other agents can read the files directly; their native discovery conventions may differ.

## Project-specific context

Each skill reads the application repository's existing instructions and optional `.agents/chase-project.md`. Use [the template](templates/chase-project.md) for local architecture, canonical helpers, vocabulary, exact test commands, environment requirements, and intentional exceptions. Keep this file in the application repository, outside the installed skills bundle, so skill updates do not replace local conventions.

For projects with repeatable app or integration checks, the template includes a compact verification recipe: launch, readiness, scenario, evidence, and cleanup. Fill in only the parts the project needs, using existing tooling.

No project overlay is required. Do not create one merely to run a skill.

## Keep the standards calibrated

- Edit shared standards once rather than introducing three versions of the same preference.
- Read [calibration examples](standards/examples.md) when judging comments, duplication, test quality, or review noise.
- Make updates deliberately. If reproducible behavior matters, record the Chase Workshop commit used for the work. A local clone does not automatically update when GitHub changes.
- Add or refine a rule in response to an observed failure, with a concrete example. Avoid collecting speculative prohibitions.
- Check all skill frontmatter and relative references after structural changes. The workflows should remain usable from both the source checkout and the documented installed layout.

PR readiness is a final audit, not a replacement for CI or a claim that all defects have been excluded. It does not automatically fix findings, post comments, create a PR, commit, or push. Existing user authorization still applies.

## Reference and attribution

[Mountain Time](https://github.com/DanielAWood/mountain-time) by Dan Wood informed the review standards, especially change scope, structural simplification, naming, type precision, error contracts, and test quality. Chase Workshop adapts those ideas into three workflows. It does not require Mountain Time to be installed.

The comment policy preserves necessary explanations and evaluates usefulness rather than treating uncertain comments as automatic deletions. Tests are judged by the behavior they protect; full-object equality, extractions, and mutation checks are tools rather than universal requirements.

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for the reference revision and upstream license notice.

## License

Chase Workshop is available under the [MIT License](LICENSE). Preserve the Mountain Time attribution and MIT notice in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) when redistributing adapted material.
