# Chase engineering standards

Apply these standards while implementing and reviewing a change. They guide engineering judgment; formatting, linting, and CI remain the project's responsibility.

Follow the user's task and applicable project instructions. Use documented architecture and nearby code as evidence of conventions, rather than copying a nearby defect. Resolve routine choices independently. Ask when an unresolved decision materially changes requirements, compatibility, data handling, or scope.

## Focus and reuse

- Search relevant modules, callers, shared utilities, types, and tests before adding functionality. Reuse an implementation when its behavior and ownership fit; similar names or syntax alone do not establish a match.
- Keep the change focused. Avoid unrelated cleanup, formatting churn, dependency upgrades, and generated-file edits outside the project's generation workflow.
- Choose the simplest coherent solution to the current requirement. Avoid speculative configuration, fallback paths, extension points, and wrappers that add no useful boundary.
- Prefer removing unnecessary concepts over moving the same complexity across more files. Judge an extraction by what callers must understand and what future changes become easier, rather than by line count.
- Preserve legitimate isolation and dependency injection. A single implementation or a test seam is not automatically a defect. Do not force unrelated behaviors into a shared abstraction to eliminate superficial duplication.

## Comments and names

- Comments must be accurate, precise, and necessary. Prefer the shortest explanation that preserves the needed context; there is no fixed line limit.
- Explain a business or customer requirement, external constraint, subtle algorithm, safety invariant, or non-obvious consequence when the code cannot communicate it adequately.
- Remove obvious narration, repeated names or types, editing-session commentary, commented-out code, and decorative banners that provide no useful navigation.
- Correct or remove comments made stale by the change. Preserve legal notices, tool directives, and necessary public API documentation. Investigate suppressions before removing them; comments and docstrings can affect tooling or runtime behavior.
- Prefer clearer names or control flow when they eliminate the need for an explanation without distorting the design. A necessary explanation is not, by itself, proof of defective code.
- State the constraint itself. A ticket link may supplement that explanation but should not replace it. Review untouched comments only when the change makes them inaccurate or necessary to understand the new behavior.
- Use the project's vocabulary. Flag naming that conceals units, representation, lifecycle, or behavior; accept short, unambiguous locals. Public names, serialized fields, and configuration keys are contracts, so renaming them requires compatibility analysis.

## Contracts, types, and failures

- Inspect affected callers and consumers when changing a contract, including error payloads, persisted data, defaults, configuration, and deployment assumptions.
- Reuse the project's established domain types and schemas. Avoid parallel declarations, unsafe casts, and weaker types that discard useful guarantees. Do not introduce a new type framework merely to satisfy this preference.
- Validate untrusted input at the appropriate boundary. Preserve checks that enforce real invariants; remove a guard only after confirming the runtime and type-checker consequences under the project's actual configuration.
- When a proposed remedy depends on compiler behavior, check the proposed construct with the project's actual checker and configuration, including relevant flags. If unavailable, label its type compatibility unverified. A successful compile does not establish unchanged runtime or error behavior; check those separately.
- Follow established error conventions. Do not swallow failures, fabricate success, or disguise invalid state with unjustified defaults. Recovery and retries need defined semantics, bounded behavior, and consideration of repeated side effects.
- Give authorized callers enough safe information to act on an error. Where the contract supports it, report multiple actionable validation failures together. Preserve intentional fail-fast behavior and do not leak private data or internals to make an error more complete.
- When relevant, inspect authorization and ownership, resource cleanup, cancellation, concurrency, and partial updates. Tie checks to the affected behavior; avoid a generic hardening campaign.

## Verification

- Read project guidance, test configuration, scripts, and relevant tests. Recent changes can clarify conventions, but choose unit, integration, or end-to-end coverage based on the behavior and failure boundary.
- Add or update meaningful coverage for changed behavior. For a bug, prefer a regression test that fails before the fix and passes after it when practical. Do not add token tests for a trivial prose or formatting change.
- Ask what plausible incorrect implementation each test would reject. Assertions must depend on the subject's behavior and actually execute, including asynchronous assertions. Derive expectations from the requirement or an independent example rather than calling the same production logic for both sides.
- Mock appropriate boundaries without replacing the behavior being tested. Mock-return and collaborator-call assertions can verify real wiring; identify a concrete missed regression before calling them useless.
- Assert the contract that matters. Use full-object assertions when the entire stable shape is the contract; intentional subsets are valid for open or unrelated fields. Avoid coupling tests to private steps when the public behavior can be exercised reliably.
- For user-visible flows and integrations, exercise the running application or interface when practical. Passing CI or a unit test alone does not establish that the flow works. State any unavailable environment or credentials.
- Run the relevant project checks. Separate pre-existing or environmental failures from regressions using evidence. Do not weaken tests or disable checks to make a change pass.
- Distinguish implemented behavior, observed results, and assumptions. Report commands and outcomes accurately, including checks not run. When an applicable verification step is skipped, name the concrete obstacle or proportionality reason and any alternative evidence. Missing verification is a limitation, not a passing result.

For calibration on comments, tests, and review findings, read [examples.md](examples.md) when a decision is unclear.
