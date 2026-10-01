<!-- BEGIN CODEX PR REVIEW RULES v1 -->
# Code Review Rules

These instructions apply only to native Codex pull-request reviews. They do not mandate pull requests or approvals, authorize edits, or change repository authoring workflows.

- Report only actual material defects introduced by this PR. Give a changed file:line, a reachable trigger, expected versus actual behavior, and a reproducer or decisive source-path proof. Unvalidated or speculative concerns, missing newly requested tests, style, naming, and unrelated existing debt are advisory.
- Existing required executable acceptance checks retain their current role; actual failures are not waived. An unavailable interpreter or check is an honest unvalidated coverage gap, never PASS and never an automatic code-fix request.
- Review is read-only: do not edit, invoke a fix agent, or start an automatic fix/re-review loop.
- Follow-ups resolve original unresolved findings and evidence-backed serious regressions caused by fixes. No new nits; do not reopen a closed finding without new evidence.
- Use current supported contracts and documented safe exceptions. Do not revive retired CodeRabbit or mutation-testing requirements.

## Repository-specific checks

- Runtime behavior — for packages/react, react-reconciler, react-dom and scheduler changes, flag demonstrated regressions in the changed public behavior, hook/state/effect ordering, hydration/rendering or renderer compatibility under the affected release channel and feature flags. Use the repository's yarn test wrapper and a targeted existing test/reproducer; __DEV__-only diagnostics, experimental APIs, controlled scheduler mocks and deliberate hot-path dispatcher behavior are valid.
- Compiler semantics and Rust port — for compiler changes, flag demonstrated semantic output changes, misordered passes or error-handling changes that violate the active TypeScript/Rust contract. Negative/error.todo fixtures, graceful unsupported-feature bailouts and required Rust ownership/arena deviations are deliberate. A CONVENTION/FIDELITY label alone is advisory: cite the corresponding source and explain the observable correctness consequence before blocking. Do not require statement-for-statement structure or naming cleanup.
- Fork and CI scope — review the actual PR diff and affected packages at its head SHA; unchanged upstream debt and a mirror sync are not an invitation to impose the personal harness across this monorepo. Preserve the separate runtime/compiler CI paths and documented supported test configurations. Formatting belongs to existing mechanical checks; missing a newly invented test suite or not running unrelated release/publish/devtools workflows is not a model-review blocker.

## Relevant existing checks

Use current CI results and only affected existing checks when authorized and available in a disposable test environment. These examples do not require all commands on every PR. Missing prerequisites remain unvalidated; do not use live providers, deploy/provision resources, or run mutating snapshot/replay builders as a review.

- `yarn test ReactHooks --env=development --runInBand` — Example focused existing runtime suite through scripts/jest/jest-cli.js; choose actual changed test and supported affected release channel, then production when behavior is relevant.
- `yarn test ReactHooks --env=production --runInBand` — Affected production path for the same focused runtime suite; development-only assertions need not be duplicated as production expectations.
- `cd compiler && yarn snap -p <affected-fixture-pattern>` — Existing compiler fixture CLI from compiler/CLAUDE.md; build prerequisites and the actual pattern must be resolved from the checkout.
- `cd compiler && yarn workspace babel-plugin-react-compiler lint` — Existing path-scoped compiler lint job.

<!-- END CODEX PR REVIEW RULES v1 -->
