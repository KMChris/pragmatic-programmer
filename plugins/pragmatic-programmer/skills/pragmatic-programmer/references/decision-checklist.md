# Pragmatic decision checklist

Use only the sections relevant to the current task. Do not turn this checklist into a ceremony or a long user-facing report.

## Before editing

- What user outcome must change?
- What evidence will prove completion?
- What is the smallest end-to-end path that exposes the main risk?
- Which files are authoritative, generated, or owned by another tool?
- What pre-existing work must remain untouched?
- Which repository instructions apply to the files involved?
- Can the current behavior be reproduced or tested before the change?

## Design

### Easier to change

- Does the change localize likely future edits?
- Is the new interface smaller and clearer than the alternative?
- Can the decision be reversed without rewriting unrelated modules?
- Is configuration used for genuine environment or policy variation, rather than speculative flexibility?

### Knowledge and duplication

- Is a business rule represented in one authoritative place?
- Are duplicated literals, schemas, validation rules, or operational steps likely to drift?
- Are two similar blocks actually different knowledge with different reasons to change?
- Can generated artifacts be derived from one source instead of synchronized manually?

### Coupling and boundaries

- Are dependencies explicit and directed toward stable boundaries?
- Does a local change remain local?
- Is shared mutable state avoidable?
- Is call order an undocumented requirement?
- Can an external service, database, queue, clock, or filesystem be substituted in tests through an existing seam?
- Would composition express the relationship more accurately than inheritance?

### Contracts and failure

- What inputs are trusted, untrusted, optional, or invalid?
- Which invariants must hold before and after the operation?
- Does invalid internal state fail close to its source?
- Are errors useful to callers without leaking secrets or internals?
- Are resources closed on every success and failure path?
- Is retry behavior bounded, idempotent, and observable?

### Security and privacy

- Does the change minimize collected, stored, logged, and returned data?
- Are authorization checks performed at the correct boundary?
- Are secrets excluded from source, logs, tests, and error messages?
- Are file paths, commands, templates, queries, URLs, and serialized input handled safely?
- Does a new dependency or permission widen the attack surface?
- Is the default behavior safe when configuration is missing or malformed?

## Feature work

- Start with a thin vertical slice through real boundaries.
- Keep the first slice small enough to validate quickly.
- Use domain terms in APIs, data structures, UI copy, and tests.
- Cover the main success path, relevant failure paths, and boundary conditions.
- Avoid optional features not required for the current outcome.
- Update documentation and examples that users rely on.

## Bug fixing

- Reproduce the symptom or capture reliable evidence.
- Separate the root cause from the visible failure.
- Add a regression test before the fix when practical.
- Narrow the search with logs, assertions, data inspection, or binary isolation.
- Fix the cause at the correct boundary, not only the final symptom.
- Check adjacent paths that share the same rule.
- Remove temporary debugging code and sensitive output.

## Refactoring

- Protect current behavior with tests before structural edits.
- Make one small structural move at a time.
- Keep tests green between steps when feasible.
- Refactor because of duplication of knowledge, poor boundaries, outdated understanding, measured performance, or current usage evidence.
- Do not combine a broad redesign with unrelated feature behavior unless the task requires both.
- Stop when the code is easier to change for the present need.

## Concurrency and asynchronous work

- Identify which operations truly require ordering.
- Remove accidental temporal coupling.
- Prefer ownership and message passing over shared mutable state.
- Define idempotency, cancellation, timeout, retry, and shutdown behavior.
- Test races, duplicate delivery, partial failure, and reordered events where relevant.
- Do not claim a concurrency bug is fixed from one successful run. Use deterministic tests, stress runs, or instrumentation when available.

## Data and schema migrations

- Define forward and rollback paths before editing production schemas.
- Preserve compatibility during rolling deployment when required.
- Separate schema change, backfill, code switch, and cleanup when one-step deployment is unsafe.
- Make backfills restartable and observable.
- Avoid destructive operations without explicit approval and verified backup or recovery strategy.
- Test with representative data volume and edge cases when practical.

## Dependencies and tooling

- Prefer built-in or already adopted project capabilities.
- Confirm compatibility with runtime and lockfiles.
- Check maintenance, license, security posture, package size, and transitive cost when adding a dependency.
- Do not replace working tooling merely because another tool is fashionable.
- Automate a repeated manual process when the automation is reliable, documented, and proportionate.

## Documentation and user-visible text

- State behavior, constraints, examples, and failure modes that users need.
- Keep documentation with the code or source of truth that changes it.
- Explain why a non-obvious trade-off exists.
- Remove stale instructions made obsolete by the change.
- Use normal human phrasing and repository terminology.
- Avoid Unicode code point U+2014 in newly written prose and comments.

## Before committing

- Acceptance criteria are met or a limitation is explicit.
- Relevant tests and checks ran.
- The final diff contains only task changes.
- No debug output, secrets, dead code, or accidental formatting churn remains.
- Generated files match their source.
- Documentation and comments match behavior.
- Staged files and hunks are correct.
- Commit subject is short, English, imperative, and specific.
