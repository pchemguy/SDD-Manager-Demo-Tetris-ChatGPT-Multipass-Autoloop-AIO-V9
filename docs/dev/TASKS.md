# Implementation tasks

Unchecked tasks are planned work, not implementation evidence. [PLAN](PLAN.md) owns phase/milestone outcomes; [SPEC](SPEC.md) owns acceptance and [layout](layout.md) owns physical placement. Execute only an authorized range after accepted preparation integration and eligible phase tracking. Each task closes with its verified result, relevant tests/docs/evidence and initial checkbox in one commit; push/read back before advancing, then reconcile its issue.

All delivery milestones below have fewer than four implementation tasks, so their final implementation task owns milestone code review/testing/repairs/report and HANDOFF. Special phase review milestones each retain exactly one separate task. Review tasks count in requested ranges. The final phase review in the complete accepted list also writes the final implementation report and aggregates eligible non-critical TODOs; no review task may declare blocked SPEC/PLAN acceptance complete. Partial phase ranges push and pause without integration.

## Phase 1 — Classic playable game

- [ ] Phase 1 — Classic playable game
    - [ ] Milestone 1.1 — Rule-complete game core
        - [ ] T-001 — Establish typed geometry and board placement
            Scope: src/core/geometry.ts, board.ts and focused tests. Contract: B-01, B-04, B-06 in SPEC. Depends on: none; accepted preparation integrated/published and phase tracking verified.
            Evidence: Empty/edge placements, all shapes, simultaneous clears and compaction. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-002 — Implement classic engine transitions
            Scope: src/core/engine.ts, source.ts and engine tests. Contract: B-02–B-05 in SPEC. Depends on: T-001.
            Evidence: Seeded draws, rejected rotation, movement, score and blocked-spawn/restart state. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-003 — Implement deterministic gravity and lifecycle timing
            Scope: src/session/controller.ts and clock/engine integration tests. Contract: B-03–B-05 in SPEC. Depends on: T-002.
            Evidence: 999/1000 ms, failed-down lock, hidden/resume and long-frame equivalence. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/1/1.1.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 1.2 — Playable browser delivery
        - [ ] T-004 — Provision isolated browser verification and static shell
            Scope: package/tooling configuration, index.html and browser smoke tests. Contract: Q-01 in SPEC. Depends on: T-003.
            Evidence: Pin runner/dependencies; diagnose Chromium and Firefox separately under root policy; launch actual static shell. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-005 — Integrate Canvas, status and keyboard gameplay
            Scope: src/view, src/browser/input.ts, main.ts and browser tests. Contract: B-01–B-04, Q-01 in SPEC. Depends on: T-004.
            Evidence: Real play, native status, game over, restart, focus and screenshot review in both browsers. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-006 — Complete baseline usability and reproducible delivery
            Scope: styles, README and baseline integration/browser checks. Contract: B-01–B-05, Q-01 in SPEC. Depends on: T-005.
            Evidence: Build/type/unit/browser checks; desktop layout, hidden-page clock and restart listener regression; document validated commands. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/1/1.2.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 1.3 — Phase review
        - [ ] T-007 — Review, test and report phase 1
            Scope: whole phase code and integration, applicable SPEC contracts and PLAN exits. Depends on: all phase delivery milestones completed/closed; last delivery task T-006.
            Evidence: separate code review and required tests, repaired blockers, docs/dev/reports/phases/1/PHASE-REPORT.md and refreshed HANDOFF; verify target merge and publication before release 0.1.0. Prepare version/notes and publish matching GitHub release only after authorized implementation is verified and integrated. Required browser failures remain blockers.
