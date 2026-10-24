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

## Phase 2 — Modern gameplay

- [ ] Phase 2 — Modern gameplay
    - [ ] Milestone 2.1 — Piece generation and manipulation
        - [ ] T-008 — Implement seven-bag generation and peeking
            Scope: src/core/source.ts and source tests. Contract: E-01 in SPEC. Depends on: prior phase review, integration/publication/release and eligible phase tracking.
            Evidence: Permutation/refill/seed determinism and non-consuming peek. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-009 — Implement ordered SRS rotation candidates
            Scope: src/core/geometry.ts, engine rotation and tests. Contract: E-01 in SPEC. Depends on: T-008.
            Evidence: All clockwise transitions, I/JLSTZ/O differences, floor/wall late kicks and all-candidate rejection. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-010 — Integrate once-per-piece Hold
            Scope: src/core/engine.ts, Hold view and interaction tests. Contract: E-02 in SPEC. Depends on: T-009.
            Evidence: Empty/swap/blocked spawn, queue consumption, repeated C and lock-reset allowance. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/2/2.1.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 2.2 — Landing preview and delayed locking
        - [ ] T-011 — Implement shared landing, ghost and hard drop
            Scope: src/core/landing.ts, engine drop, view and focused tests. Contract: E-02 in SPEC. Depends on: T-010.
            Evidence: Obstacle-limited landing, zero-distance drop and visible projection/drop equality. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-012 — Implement grounding deadline semantics
            Scope: src/core/engine.ts and deterministic time tests. Contract: E-03 in SPEC. Depends on: T-011.
            Evidence: Grounded no-reset, airborne cancel/reground, drop behavior and timestamp precedence. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-013 — Verify enhanced browser interactions and delivery
            Scope: browser tests, keyboard/status view and README. Contract: E-01–E-03, Q-01 in SPEC. Depends on: T-012.
            Evidence: Hold/drop/ghost interactions, hidden/resume deadlines, two-browser screenshots and classic regression. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/2/2.2.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 2.3 — Phase review
        - [ ] T-014 — Review, test and report phase 2
            Scope: whole phase code and integration, applicable SPEC contracts and PLAN exits. Depends on: all phase delivery milestones completed/closed; last delivery task T-013.
            Evidence: separate code review and required tests, repaired blockers, docs/dev/reports/phases/2/PHASE-REPORT.md and refreshed HANDOFF; verify target merge and publication before release 0.2.0. Prepare version/notes and publish matching GitHub release only after authorized implementation is verified and integrated. Required browser failures remain blockers.

## Phase 3 — Dynamic ghost visibility

- [ ] Phase 3 — Dynamic ghost visibility
    - [ ] Milestone 3.1 — Midline-aware ghost
        - [ ] T-015 — Implement whole-footprint visibility predicate
            Scope: src/view/ghost.ts and predicate tests. Contract: G-01 in SPEC. Depends on: prior phase review, integration/publication/release and eligible phase tracking.
            Evidence: Upper, straddling, min-row 9 and min-row 10 cases. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-016 — Integrate and verify dynamic ghost rendering
            Scope: Canvas view, browser tests and README. Contract: G-01, E-02 in SPEC. Depends on: T-015.
            Evidence: Move/rotate/spawn and board-change transitions; show/hide return paths; identical hard-drop landings in both browsers. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/3/3.1.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 3.2 — Phase review
        - [ ] T-017 — Review, test and report phase 3
            Scope: whole phase code and integration, applicable SPEC contracts and PLAN exits. Depends on: all phase delivery milestones completed/closed; last delivery task T-016.
            Evidence: separate code review and required tests, repaired blockers, docs/dev/reports/phases/3/PHASE-REPORT.md and refreshed HANDOFF; verify target merge and publication before release 0.3.0. Prepare version/notes and publish matching GitHub release only after authorized implementation is verified and integrated. Required browser failures remain blockers.

## Phase 4 — Penetrator gameplay

- [ ] Phase 4 — Penetrator gameplay
    - [ ] Milestone 4.1 — Safe penetration movement
        - [ ] T-018 — Implement penetrating landing and safe adjustments
            Scope: src/core/landing.ts, geometry/engine movement and tests. Contract: P-01 in SPEC. Depends on: prior phase review, integration/publication/release and eligible phase tracking.
            Evidence: Buried gaps, bottom obstruction, no-upward result and rejected adjustments with no future landing. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-019 — Integrate activation, Hold exclusion and locking
            Scope: src/core/engine.ts, input mapping and tests. Contract: P-01, E-03 in SPEC. Depends on: T-018.
            Evidence: Spend once, repeated P, overlapping transit, legal commit, deadline cancellation and Hold rejection. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-020 — Verify penetrating drop and ghost agreement
            Scope: core integration and browser scenarios. Contract: P-01, G-01 in SPEC. Depends on: T-019.
            Evidence: Lowest valid gap, drop through obstacles, midline visibility and ordinary-mode regression. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/4/4.1.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 4.2 — Bonus feedback and complete mode
        - [ ] T-021 — Implement atomic bonus awards and cap
            Scope: engine lock/clear state and tests. Contract: P-02 in SPEC. Depends on: T-020.
            Evidence: 0–3 bounds, four-line-only award, spend then award, restart resets. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-022 — Render white activation and accessible bonus count
            Scope: Canvas/status view, styles and screenshot tests. Contract: P-02 in SPEC. Depends on: T-021.
            Evidence: Entire active white, regular non-white, distinct ghost and symbol count matches inventory. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-023 — Verify full penetrator play and reproducible delivery
            Scope: browser scenarios and README. Contract: P-01–P-02, E-03, G-01, Q-01 in SPEC. Depends on: T-022.
            Evidence: Earn/activate/drop/lock/restart, Hold refusal, timing and two-browser regression with no cell destruction. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/4/4.2.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 4.3 — Phase review
        - [ ] T-024 — Review, test and report phase 4
            Scope: whole phase code and integration, applicable SPEC contracts and PLAN exits. Depends on: all phase delivery milestones completed/closed; last delivery task T-023.
            Evidence: separate code review and required tests, repaired blockers, docs/dev/reports/phases/4/PHASE-REPORT.md and refreshed HANDOFF; verify target merge and publication before release 0.4.0. Prepare version/notes and publish matching GitHub release only after authorized implementation is verified and integrated. Required browser failures remain blockers.

## Phase 5 — Session configuration

- [ ] Phase 5 — Session configuration
    - [ ] Milestone 5.1 — Live session settings
        - [ ] T-025 — Implement validated settings and spawn policy capture
            Scope: src/config/settings.ts, engine/controller and tests. Contract: C-01–C-02 in SPEC. Depends on: prior phase review, integration/publication/release and eligible phase tracking.
            Evidence: Defaults/token rejection, immediate switches, captured lock policies through spawn/Hold/restart. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-026 — Integrate native settings controls and next preview
            Scope: settings/preview view, styles and browser tests. Contract: C-01 in SPEC. Depends on: T-025.
            Evidence: All six controls, non-consuming preview, focus isolation and retained Hold slot. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-027 — Verify configuration combinations and session lifetime
            Scope: engine/browser scenarios and README. Contract: C-01–C-03 in SPEC. Depends on: T-026.
            Evidence: Policy cross-product including penetrators/zero drop; no persistence writes; restart retention and reload defaults in both browsers. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/5/5.1.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 5.2 — Phase review
        - [ ] T-028 — Review, test and report phase 5
            Scope: whole phase code and integration, applicable SPEC contracts and PLAN exits. Depends on: all phase delivery milestones completed/closed; last delivery task T-027.
            Evidence: separate code review and required tests, repaired blockers, docs/dev/reports/phases/5/PHASE-REPORT.md and refreshed HANDOFF; verify target merge and publication before release 0.5.0. Prepare version/notes and publish matching GitHub release only after authorized implementation is verified and integrated. Required browser failures remain blockers.

## Phase 6 — Persistent configuration

- [ ] Phase 6 — Persistent configuration
    - [ ] Milestone 6.1 — URL and cookie configuration
        - [ ] T-029 — Implement canonical codec and source resolution
            Scope: src/config/codec.ts and focused table-driven tests. Contract: S-01 in SPEC. Depends on: prior phase review, integration/publication/release and eligible phase tracking.
            Evidence: All six keys, mixed validity, explicit defaults, omissions, duplicates and malformed cookies. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-030 — Integrate startup and browser persistence adapter
            Scope: src/browser/persistence.ts, composition and adapter tests. Contract: S-01–S-02 in SPEC. Depends on: T-029.
            Evidence: Resolve before first spawn; independent cookie/history attempts; blocked reads/writes, silent rejection and warning. Include focused tests and relevant module/user documentation with this result.
        - [ ] T-031 — Verify persistence round-trips and complete delivery
            Scope: browser tests, README and failure scenarios. Contract: S-01–S-02, C-01–C-02, Q-01 in SPEC. Depends on: T-030.
            Evidence: All six settings across reload/reopen; defaults overriding cookies, omitted retention, unrelated URL/fragment and active gameplay regression in both browsers. Include focused tests and relevant module/user documentation with this result.
            Milestone exit: after all other milestone tasks, review whole-capability code, run required checks/regressions, repair blockers and commit docs/dev/reports/phases/6/6.1.md plus HANDOFF with this task’s implementation and initial checkbox. Record findings separately from eligible non-critical TODOs; verified issue/milestone closure precedes dependent phase review.
    - [ ] Milestone 6.2 — Phase review
        - [ ] T-032 — Review, test and report phase 6
            Scope: whole phase code and integration, applicable SPEC contracts and PLAN exits. Depends on: all phase delivery milestones completed/closed; last delivery task T-031.
            Evidence: separate code review and required tests, repaired blockers, docs/dev/reports/phases/6/PHASE-REPORT.md and refreshed HANDOFF; verify target merge and publication before release 0.6.0. Prepare version/notes and publish matching GitHub release only after authorized implementation is verified and integrated. Required browser failures remain blockers.
