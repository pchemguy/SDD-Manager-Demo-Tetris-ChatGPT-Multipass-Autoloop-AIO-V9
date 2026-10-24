# Delivery plan

## Delivery strategy

Deliver coherent playable capability increments over a verified static client baseline. [SPEC](SPEC.md) owns contracts; `TASKS.md` derives executable units and `layout.md` allocates physical ownership. Core tests control time/randomness; isolated Chromium and managed Firefox verify real UI and screenshots under the root browser policy.

Each milestone integrates its capability before dependent growth. Every delivery milestone requires code review, tests, blocker repair, a committed milestone report and HANDOFF. Each phase ends with a separate one-task review milestone. Future planned functionality does not block a completed earlier phase whose own contracts pass. For changed rules, verify the intended new contract and unaffected earlier behavior rather than asserting that superseded behavior still applies.

Runtime/browser provisioning is a bounded implementation task: use pinned dependencies, proactively diagnose official download/launch failures separately for each required browser, and report unmet facilities without using personal/global browsers. Browser failures do not justify declaring browser acceptance complete.

Versioning starts with 0.1.0 for the first playable release. Increment minor versions for delivered capability phases and patch versions for compatible repairs. Each authorized implementation phase must verify, integrate and publish before its release; documentation-only work creates no product tags/releases. Release notes describe delivered changes and actual validation limits. Release preparation belongs to the completed phase boundary, not a second product phase.

## Phase delivery boundaries

## Phase 1 — Classic playable game

Outcome: classic playable game as a usable integrated capability. Contract scope: B-01–B-06, Q-01. Target release: 0.1.0. This establishes the smallest playable classic product; modern gameplay and settings are excluded.

### Milestone 1.1 — Rule-complete game core

Legal board/shape transitions, gravity, clearing, scoring and lifecycle work under deterministic tests. Depends on the phase entry baseline. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: Legal board/shape transitions, gravity, clearing, scoring and lifecycle work under deterministic tests. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 1.2 — Playable browser delivery

Real keyboard play, visible state and restart run in the supported isolated browsers. Depends on the preceding delivery milestone. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: Real keyboard play, visible state and restart run in the supported isolated browsers. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 1.3 — Phase review

Exactly one phase code review/testing/report task, after all delivery milestones complete and close. Verify applicable contracts, cross-milestone interactions, required browser matrix and preserved prior behavior; fix blockers, retain phase report and HANDOFF, then close the review milestone. Explicitly integrate the verified phase, check the merged result and publish/read back. Prepare version 0.1.0 and release notes; only after authorized implementation completion/integration publish its matching tag and GitHub release. No phase/release is complete while required checks or publication remain blocked.

## Phase 2 — Modern gameplay

Outcome: modern gameplay as a usable integrated capability. Contract scope: E-01–E-03, preserved baseline outcomes, Q-01. Target release: 0.2.0. Depends on verified, published integration and release of phase 1. Retain prior player-visible capabilities except the explicitly scheduled rule changes in this phase.

### Milestone 2.1 — Piece generation and manipulation

7-bag, clockwise SRS and Hold integrate without breaking ordinary movement. Depends on the phase entry baseline. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: 7-bag, clockwise SRS and Hold integrate without breaking ordinary movement. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 2.2 — Landing preview and delayed locking

Ghost/drop agreement and full-interval locking produce adjustable landings. Depends on the preceding delivery milestone. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: Ghost/drop agreement and full-interval locking produce adjustable landings. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 2.3 — Phase review

Exactly one phase code review/testing/report task, after all delivery milestones complete and close. Verify applicable contracts, cross-milestone interactions, required browser matrix and preserved prior behavior; fix blockers, retain phase report and HANDOFF, then close the review milestone. Explicitly integrate the verified phase, check the merged result and publish/read back. Prepare version 0.2.0 and release notes; only after authorized implementation completion/integration publish its matching tag and GitHub release. No phase/release is complete while required checks or publication remain blocked.

## Phase 3 — Dynamic ghost visibility

Outcome: dynamic ghost visibility as a usable integrated capability. Contract scope: G-01, preserved modern gameplay. Target release: 0.3.0. Depends on verified, published integration and release of phase 2. Retain prior player-visible capabilities except the explicitly scheduled rule changes in this phase.

### Milestone 3.1 — Midline-aware ghost

Whole-footprint visibility changes without changing landing physics. Depends on the phase entry baseline. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: Whole-footprint visibility changes without changing landing physics. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 3.2 — Phase review

Exactly one phase code review/testing/report task, after all delivery milestones complete and close. Verify applicable contracts, cross-milestone interactions, required browser matrix and preserved prior behavior; fix blockers, retain phase report and HANDOFF, then close the review milestone. Explicitly integrate the verified phase, check the merged result and publish/read back. Prepare version 0.3.0 and release notes; only after authorized implementation completion/integration publish its matching tag and GitHub release. No phase/release is complete while required checks or publication remain blocked.

## Phase 4 — Penetrator gameplay

Outcome: penetrator gameplay as a usable integrated capability. Contract scope: P-01–P-02, ghost and locking interactions. Target release: 0.4.0. Depends on verified, published integration and release of phase 3. Retain prior player-visible capabilities except the explicitly scheduled rule changes in this phase.

### Milestone 4.1 — Safe penetration movement

Bonus activation and shared terminal-landing policy allow safe passage through occupied cells. Depends on the phase entry baseline. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: Bonus activation and shared terminal-landing policy allow safe passage through occupied cells. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 4.2 — Bonus feedback and complete mode

Four-line awards, bounded inventory and presentation complete the player-facing capability. Depends on the preceding delivery milestone. Exit: integrated contract checks and applicable regressions pass; review the whole milestone code, repair blockers, commit the milestone report and refresh HANDOFF. The final implementation task owns these obligations unless task-count thresholds require a standalone review.

Demonstration: Four-line awards, bounded inventory and presentation complete the player-facing capability. Inspect functional evidence and relevant usability/focus feedback before continuing; a consequential change may prompt continue/amend/simplify/stop direction without inventing an extra routine approval gate.

### Milestone 4.3 — Phase review

Exactly one phase code review/testing/report task, after all delivery milestones complete and close. Verify applicable contracts, cross-milestone interactions, required browser matrix and preserved prior behavior; fix blockers, retain phase report and HANDOFF, then close the review milestone. Explicitly integrate the verified phase, check the merged result and publish/read back. Prepare version 0.4.0 and release notes; only after authorized implementation completion/integration publish its matching tag and GitHub release. No phase/release is complete while required checks or publication remain blocked.
