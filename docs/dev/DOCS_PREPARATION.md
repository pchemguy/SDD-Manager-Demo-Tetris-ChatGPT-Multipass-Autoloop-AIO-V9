# Main documentation preparation record

## Current control

- Mode: autodoc/autoloop, selected by the user request of 24 October 2026.
- Delivery mode: strict by default; no flexible integration permission supplied. Preserve every established earlier phase/task range.
- Current scope: pass 3, Conditional ghost visibility; cursor DOCS-007.
- Authority: initialization and document preparation authorized; first PROJECT and presented interaction choices accepted by the user’s “Approve” response. Later PROJECT approvals are waived, and subsequent document checkpoints are preapproved by the requested mode. Newly discovered material choices after that approval are delegated with visible rationale.
- Stop: after pass 6 DOCS-008; DOCS-009, whole-package QC, documentation integration, implementation and implementation activation remain outside this range.
- Tracking: root AGENTS.md enables documentation and implementation tracking by default. Complete preparation projection verified before target writes: native milestone 1, sdd-docs-main, and DOCS-001–009 issues 1–9, exact template briefs and associations read back. Milestone and all issues initially open.
- Publication: push and exact readback after each owned commit. Reporting: Explicit bootstrap, then Standard; Minimal and Explicit available.

## Scope sequence

1. **Playable classic baseline:** Falling tetrominoes, movement, rotation, gravity, line clearing, scoring, game over and restart. Keep the product minimal and coherent.
2. **Gameplay enhancements:** Hold, ghost, 7-bag, wall kicks, hard drop and default full-gravity-interval lock delay, including after hard drop.
3. **Conditional ghost visibility:** Hide projected ghosts in the upper half; show in the lower half, with a proposed whole-piece boundary rule below.
4. **Penetrator mode:** Bonus-gated hotkey activation lasting until lock; traverse occupied cells without destruction; final placement fully inside and non-overlapping. Hard drop finds the lowest valid landing and visible ghost agrees. Four-line clears award one bonus, capped at three. Active pieces entirely white, regular pieces non-white; side panel displays one symbol per bonus and updates on earn/spend.
5. **Session-only configuration:** Six side-panel settings: ghost hidden/dynamic/always; hard drop on/off; next preview on/off; hard-drop locking follows general/immediate; general locking failed-down/full interval; Hold on/off. Add next preview. No reload persistence.
6. **Configuration persistence:** All six settings resolve independently valid explicit URL value, then valid cookie, then default. On player changes save cookie and update corresponding URL parameter. Save valid explicit URL values to cookies even when equal to defaults. Omitted parameters retain cookie values. Restore on reload/reopen.

## Per-pass decisions

The recommendations below originated with the agent during initial exploration and were accepted by the user’s “Approve” response to published proposal c7424e990408d5c6fd168240121ed94fe092d925 and its presented interaction choices. The supplied requirements in Scope sequence remain authoritative.

| Origin / decision | Proposed resolution and rationale | Basis | Applicability / status |
| --- | --- | --- | --- |
| Pass 1 / platform | Desktop keyboard browser game; TypeScript, Canvas board and native HTML status/controls; static delivery without backend. DOM board remains a viable alternative; Canvas offers direct rendering with a separately testable engine. Avoid a framework without a concrete need. | Agent recommendation from seed and browser policy | All scopes; accepted |
| Pass 1 / baseline | 10×20 visible board, seven tetromino types; basic clockwise rotation rejects collisions without wall kicks; simple random draws, immediate lock on failed downward movement, fixed gravity interval and line-clear scoring. No level system required. | Agent recommendation preserving minimal baseline | Pass 1; accepted; enhanced randomization and locking replace these in pass 2 |
| Pass 1 / delivery and versions | First playable release 0.1.0; increment minor version for each later delivered capability phase, patches for compatible repairs. No product release or tag for documentation alone. Publish corresponding notes and release only after an authorized implementation phase verifies and integrates. | User release requirement plus agent version recommendation | All delivery phases; accepted |
| Pass 2 / delay | Capture one current gravity interval at grounding. Grounded moves/rotations do not reset the deadline. Becoming airborne cancels it; later grounding starts a fresh interval. Manual downward attempts do not shorten interval locking. Hard drop preserves an existing grounded deadline or begins one at landing. | Agent recommendation avoids indefinite grounded resets and honors one full interval | Passes 2–6; accepted |
| Pass 2 / Hold | Once per falling piece, reset on lock; empty Hold draws a new piece; swaps use normal spawn and blocked spawn ends game. | Agent recommendation | Passes 2–6; accepted |
| Pass 3 / midline | Show only when every projected ghost cell lies in lower-half rows 10–19. Any cell in rows 0–9 hides the whole ghost; a straddling piece is hidden. | Agent recommendation supplies an unambiguous whole-piece boundary | Passes 3–6; accepted |
| Pass 4 / Hold and activation | Disable Hold for an activated penetrator. Spend one available bonus once per piece; repeated activation is a no-op. Restart clears bonuses. | Agent recommendation; activation-until-lock requirement | Passes 4–6; accepted |
| Pass 4 / valid landing | Find greatest board row at or below current origin yielding a fully contained, non-overlapping placement, scanning through occupied intermediate positions. Reject movement/rotation that would leave no valid downward landing. Stop gravity at that terminal landing; transient overlap never locks, clears cells or ends the game. Activation preserves an existing lock deadline if still grounded; becoming airborne cancels it. | Agent recommendation prevents trapped overlap and preserves lock safety | Passes 4–6; accepted |
| Pass 5 / defaults | Dynamic ghost, hard drop enabled, next preview enabled, hard drop follows general policy, full-interval general locking, Hold enabled. | Agent recommendation preserves prior gameplay | Passes 5–6; accepted |
| Pass 5 / live changes | Visibility, preview and hard-drop/Hold enable switches apply immediately; disabling Hold retains its stored piece. Locking-policy changes apply at the next spawned piece; active piece retains captured policies and deadline. Restart retains settings and resets gameplay. Hiding the page suspends simulation rather than accumulating gravity/lock time. | Agent recommendation avoids retroactive locking and accidental background losses | Configuration scopes; background suspension applies to baseline |
| Pass 6 / invalid sources | Validate each source independently. An invalid URL value falls back to a valid cookie, then default, and does not overwrite that cookie. Invalid cookies fall back to default. Empty values invalid; for duplicate parameters use the last occurrence and validate it. Preserve unrelated query parameters and fragment. | Agent recommendation maintains independent precedence | Pass 6; accepted |
| Pass 6 / persistence failure | Settings remain effective in memory if cookie or history updates fail; show a concise non-blocking persistence warning. Cookie is host-only, path /, SameSite=Lax, with Secure on HTTPS; no personal data. Serve over HTTP(S). | Agent recommendation preserves playable behavior under browser restrictions | Pass 6; accepted |

## Cross-scope decisions

| Concern | Applicable decision | Reconsideration condition |
| --- | --- | --- |
| Baseline isolation | Pass 1 baseline excludes future enhancements and settings; retain future scope here until its turn. | Explicit user scope amendment |
| Ghost/penetration/midline | Pass 3 whole-piece boundary evaluates the same landing calculator used by hard drop; pass 4 changes its penetration policy. | Changed board size or landing rule |
| Grounding/activation/live policy | Pass 2 delay, pass 4 valid landing and pass 5 policy capture cooperate; overlap is never a legal lock state. | Contradictory acceptance scenario or user change |
| Hold/penetrator/configuration | Pass 4 active penetrator always disables Hold, regardless of enabled setting; retained Hold slot survives disabling. | User change to activation lifetime |
| Persistence | Pass 5 is memory only; pass 6 introduces independent source validation and round-trip updates. | New setting or storage requirement |
| Verification | Follow root BROWSER_DEV_POLICY.md: isolated Chromium primary, managed Firefox secondary; no browser installation for document-only work. | Accepted test matrix amendment or actual facility blocker |

## Decisions and document evidence

| Task | Evidence / decision basis |
| --- | --- |
| DOCS-001 | Four existing root files preserved byte for byte against initial SHA-256 inventory; no root copies needed. Default provenance scaffold verified and integrated; task template copied from bundled package. Initialization commit 8f4be5bafa9fac43e3abfe4162af1e4c4e3997f1 published with exact matching remote readback and confirmed cleanup; issue 1 closed/completed and read back before PROJECT work. |
| DOCS-002 | First PROJECT/interaction approval: user Approve to proposal c7424e990408d5c6fd168240121ed94fe092d925; current-pass evidence below. |
| DOCS-003–008 | Current-pass accepted content identities and owner QC appear in the pass-qualified evidence below; checkpoints covered by scoped mode preapproval. |
| DOCS-009 | Outside current authorized stopping boundary; remains unchecked and issue 9 open. |

## Initialization and current reset

- Original retained roots: AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md, SKILL_DISCOVERY_PROTOCOL.md. Copied roots: none. All four present, so no mixed-initialization pause applies.
- Provenance: default enabled; two scaffold assets copied byte for byte, without transcripts. Base main 00d05adb658650f8f5bd2c096dcfd90b1a84e9fc; seed c3fcd9b7c917cc38bbdc34bf65281a119f05bede; explicit two-parent main merge 88474bff25c572f5ee8a3bb75f98d801c15d2b6f. Both published with exact matching remote readback and confirmed cleanup.
- Credential: conventional gh.tkn saved only after complete projection, with *.tkn ignored and path untracked. No credential is part of project documents.
- Current reset: pass 2 DOCS-008 completed/published; advance to predefined pass 3 under accepted autoloop authority. Preserve all documents/ranges, uncheck DOCS-002–009 and reopen same issues after reset publication before revisions.

## Pass 1 document evidence

- DOCS-003: ARCHITECTURE.md, SHA-256 887a62212cb7e705c1be19b702a9e9028b18bb0665d050f6d3f283a457f603d8; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-004: DECOMPOSITION.md, SHA-256 6702c186f56c6056cc2fd8a83b388218f372b6f5c45b839eac0298b377937333; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-005: SPEC.md, SHA-256 c4f4b4cddf5c5b02c9c8bddb7ef1653f04724efb8424b3a29885cd24bf88dcd9; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. SPEC-REVIEW-REPORT.md records current design/contract QC; no unresolved blockers.
- DOCS-006: PLAN.md, SHA-256 4fe758542ff43f1133b872ea0748bb13ef842d093a06b0b059fe804717cfa6ce; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. PLAN-REVIEW-REPORT.md records strategy QC and bounded milestone-count rationale.
- DOCS-007: layout.md, SHA-256 a957cb051dc7906aa025cab2041747ca0fbb0e440dfed3e9e32fc42ecd0f7c37; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. PLAN-REVIEW-REPORT.md records strategy/layout QC, count rationale and protected phases.
- DOCS-008: TASKS.md, SHA-256 806cc92eec0313b64302743357574f6b8b4a582de42d8d983138f105690dd4e9; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. TASKS-REVIEW-REPORT.md records derivation QC and protected prior task ranges. New task range: T-001–T-007.

## Pass 1 result

Current cumulative scope Playable classic baseline is covered through DOCS-008; per-document gates are recorded above. PLAN/TASKS phases 1–1 retained with new phase 1 and task range T-001–T-007. Earlier phase blocks remain byte-identical. No new product decision supersedes the accepted cross-scope decisions. Publish/close issue 8 before reset or final stop; DOCS-009 remains unchecked.

## Reset to pass 2

Prior pass completion: 7d4024ecc9e20bc62be2be9f7ce66930db3e13c6. Next scope: Gameplay enhancements. Accepted autoloop authority; retain earlier decisions and strict protected ranges. No Git reset/deletion. Same issues 2–9 require open-state readback after publication.

## Pass 2 document evidence

- DOCS-002: PROJECT.md, SHA-256 029de48e0785b78b46eb306c0b7c82146efbe93f88fd27564f8102041a2cb3ea; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-003: ARCHITECTURE.md, SHA-256 a4c0ea92f93dd07c2e9015e2d36c12885b0991adfd6ee7acec5bc55c95ed59ca; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-004: DECOMPOSITION.md, SHA-256 0707b5669ce4d7a48c8d3b529ffd36bf8aeaa1d464c9dd39104813e33368fd18; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-005: SPEC.md, SHA-256 1b4cd24aff53fff9563e3858d112fad38163f2843f1ab0f458f835eae2ed7fd6; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. SPEC-REVIEW-REPORT.md records current design/contract QC; no unresolved blockers.
- DOCS-006: PLAN.md, SHA-256 8d2bb49e86e48f8bc0bfc482ca73330e5cda96efdad0a077d93b3832987cb397; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. PLAN-REVIEW-REPORT.md records strategy QC, count rationale and protected phases.
- DOCS-007: layout.md, SHA-256 48bc59a4313ec49c7d5299d29f0026bcaac1058d3ccdaed22a9a5d99e0388391; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. PLAN-REVIEW-REPORT.md records strategy/layout QC, count rationale and protected phases.
- DOCS-008: TASKS.md, SHA-256 3c6d212f6df4a6f08d93061d4d134628028abaa3ba6b085a34c40e10b8874460; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. TASKS-REVIEW-REPORT.md records derivation QC and protected prior task ranges. New task range: T-008–T-014.

## Pass 2 result

Current cumulative scope Gameplay enhancements is covered through DOCS-008; per-document gates are recorded above. PLAN/TASKS phases 1–2 retained with new phase 2 and task range T-008–T-014. Earlier phase blocks remain byte-identical. No new product decision supersedes the accepted cross-scope decisions. Publish/close issue 8 before reset or final stop; DOCS-009 remains unchecked.

## Reset to pass 3

Prior pass completion: b3298b35a2af597ac507f497a8fea3e27f7dec4c. Next scope: Conditional ghost visibility. Accepted autoloop authority; retain earlier decisions and strict protected ranges. No Git reset/deletion. Same issues 2–9 require open-state readback after publication.

## Pass 3 document evidence

- DOCS-002: PROJECT.md, SHA-256 32a089f5781b37bc32722f518c1532d123583bacea0ab8462e3af91c0fab09e3; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-003: ARCHITECTURE.md, SHA-256 08094e319211a5993e9c79baea66ae90af046331223ecd47afd4ef706416a7fc; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-004: DECOMPOSITION.md, SHA-256 7050c9ddb63602bc4bf3e45a4e92540563a79e163f52fb1666b2dd3cfc1e08e6; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing.
- DOCS-005: SPEC.md, SHA-256 25e5eaa96608d2247cdd0f6f8c79b45d80fbb907b0044f6c50d5b14f7cb8a5da; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. SPEC-REVIEW-REPORT.md records current design/contract QC; no unresolved blockers.
- DOCS-006: PLAN.md, SHA-256 d7ece063f4799e4595fbc62dbf76d9e8bf398314b34bd909046b5d5dfdde48f8; Autodoc/autoloop scoped preapproval. Owner reviewed scope, dependencies, content boundaries and local Markdown links/spacing. PLAN-REVIEW-REPORT.md records strategy QC, count rationale and protected phases.

## Pending transitions

Publish/read back the owning completion commit, then close/read back its same DOCS issue before dependent work. No implementation activation or package QC is authorized.
