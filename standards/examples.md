# Calibration examples

Read these when a standards decision is unclear. They illustrate judgment rather than prescribe a language, framework, or line limit.

## Comments

Remove narration:

```ts
// Loop through the users and save each user.
for (const user of users) await saveUser(user);
```

Keep context the code cannot express:

```ts
// The vendor rejects batches larger than 100 records.
const batchSize = 100;
```

Keep an explanation of an otherwise surprising rule, provided it is accurate:

```ts
// Customer billing closes at midnight in the account's timezone.
const billingDate = toAccountDate(event.timestamp, account.timezone);
```

A subtle synchronization invariant or algorithm may need several sentences. Preserve the necessary explanation; do not compress it until it becomes misleading. Renaming a constant cannot always communicate why a value or constraint exists.

Remove session narration such as `// Updated this to match your request`. A useful explanation should make sense to someone who never saw the agent conversation.

A suppression, doctest, coverage directive, or documentation annotation may affect tools. Investigate before treating its removal as cosmetic.

## Reuse

If `getVisibleProjects(user)` already applies tenant and permission rules, do not add another query with a slightly different copy of those rules. Inspect its behavior and reuse or extend the canonical implementation.

Two short formatting functions for different external protocols may deserve separate implementations even if their current bodies match. Combine them only when their semantics and expected changes align.

## Tests

A service test that stubs a repository and asserts the returned entity can catch a wrong lookup or dropped result. Do not reject it merely because the expected value came from a fixture. Ask which plausible defects it detects and which important ones it misses.

An assertion on `response.status` alone is weak when the requirement also defines an error code and field errors. Conversely, a subset assertion on a large response can be appropriate when unrelated metadata is intentionally outside the contract.

For a bug involving duplicate submissions, test the observable duplicate-prevention behavior. Counting calls to a private helper is insufficient if the public flow can still create two records.

## Review findings

Actionable:

> Blocking - `src/orders.ts:84`: Retrying after a timeout can submit the same order twice because the retry generates a new idempotency key. Reuse the key for the logical operation and cover the timeout/retry case.
>
> Evidence: Traced - the timeout handler resubmits through the key-generating entry point; this path was not executed. Remedy: Behavior-affecting - repeat attempts must share one key, changing duplicate-submission behavior; check the retry caller and payment adapter's key contract.

Actionable maintainability suggestion:

> Suggestion - `src/project-search.ts:32`: This adds a second implementation of tenant filtering already owned by `visibleProjectsQuery`. Reuse it here so permission changes do not need coordinated edits in two places.
>
> Evidence: Traced - the new query repeats the canonical query's tenant predicate. Remedy: impact unverified until the helper's visibility defaults and callers are checked; matching one predicate alone does not prove equivalent behavior.

Insufficient:

> This function is too long. Split it up.

Explain the specific responsibilities or coupling that cause a problem and how the remedy reduces them. A personal line-count preference is not enough.
