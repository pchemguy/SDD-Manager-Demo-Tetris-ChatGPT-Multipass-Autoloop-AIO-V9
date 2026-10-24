# Repository layout

Proposed source placement for [DECOMPOSITION](DECOMPOSITION.md) and [PLAN](PLAN.md); paths below do not claim implementation exists. Paths in grouped rows are relative to the repository root.

## Physical ownership

| Paths | Ownership |
| --- | --- |
| index.html, src/main.ts | Static shell and composition; no rules |
| src/core/types.ts, geometry.ts | State/value types and fixed shape/orientation definitions |
| src/core/board.ts, source.ts, engine.ts | Board operations, random source, authoritative state transitions |
| src/session/controller.ts | Serialized action dispatch and simulation-time lifecycle |
| src/view/board.ts, status.ts; src/browser/input.ts | Canvas/HTML rendering and focused keyboard/visibility events |
| src/styles.css | Desktop board/panel layout and visible focus |
| tests/core/, tests/session/ | Deterministic rules/time tests without DOM |
| tests/browser/; playwright.config.ts | Actual static application keyboard/focus/screenshot checks for isolated Chromium/Firefox |
| package.json, lockfile, tsconfig.json, vite.config.ts | Pinned TypeScript/static build/test tooling; no backend |
| README.md; docs/dev/reports/phases/ | Validated setup/play instructions; implementation milestone/phase evidence |
| src/core/landing.ts; tests/core/landing.test.ts | Shared projection/drop landing; source/geometry/engine files own 7-bag, SRS, Hold and lock state |
| src/view/ghost.ts; tests/view/ghost.test.ts | Pure ghost visibility predicate; board view consumes result |
| src/config/settings.ts; src/view/settings.ts, preview.ts | Settings state/defaults and native controls/next preview; engine captures policy at spawn |
| tests/config/; tests/browser/configuration.spec.ts | Defaults/live changes and policy-combination acceptance |

## Boundaries and generated artifacts

Core imports only core values/helpers; session depends on core; views/adapters depend on snapshots/controller; main composes them. Tests mirror responsibility boundaries without requiring one test file per implementation file. Keep exact filenames adaptable within their owner when implementation establishes a better local name; do not move ownership across blocks silently.

Use an absolute project-owned PLAYWRIGHT_BROWSERS_PATH for installation and every test process. Place browser binaries, profiles, reports, screenshots, dist and dependency caches in identified ignored/generated locations; never commit binaries or credentials. Keep *.tkn excluded and untracked. Only owned temporary artifacts may be cleaned. Declare validated commands and actual supported versions in README and root AGENTS during implementation, without inventing passing commands during preparation.

Milestone reports use docs/dev/reports/phases/<phase>/<milestone>.md; phase reports use PHASE-REPORT.md in that phase directory. The final phase review includes docs/dev/reports/IMPLEMENTATION-REPORT.md and aggregated eligible TODOs only when the complete authorized task list finishes. Preparation records remain in docs/dev; root policies and the bundled plugin retain their existing ownership.
