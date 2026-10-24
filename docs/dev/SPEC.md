# Behavioral specification

[PROJECT](PROJECT.md), [ARCHITECTURE](ARCHITECTURE.md) and [DECOMPOSITION](DECOMPOSITION.md) govern intent and ownership. Requirements describe observable intended behavior; acceptance below is planned verification, not executed game tests.

## B-01 — Board, shapes and spawning

The visible board has columns 0–9 and rows 0–19, increasing downward. All seven tetrominoes have four occupied cells. Spawn orientation is 0 with the occupied bounding box centered horizontally and its top occupied row at row 0. Spawn failure because occupied cells overlap the board ends the game without modifying settled cells. Geometry uses fixed orientation tables, including the four SRS orientations when SRS is enabled. No active or settled occupied cell may lie outside the visible board after an accepted transition.

Acceptance: each shape spawns on an empty board, blocked spawn ends play, edge candidates are rejected, and a failed transition leaves board/state unchanged.


## B-06 — Coordinate geometry

Local cells are (x,y), right/down positive. Spawn cells are I: (0,1),(1,1),(2,1),(3,1); O: (0,0),(1,0),(0,1),(1,1); J: (0,0),(0,1),(1,1),(2,1); L: (2,0),(0,1),(1,1),(2,1); S: (1,0),(2,0),(0,1),(1,1); T: (1,0),(0,1),(1,1),(2,1); Z: (0,0),(1,0),(1,1),(2,1). For J/L/S/T/Z, produce each clockwise orientation by (x,y) -> (2-y,x). For I use (x,y) -> (3-y,x); O occupied cells never change. State order is 0,R,2,L,0. Preserve the local origin during rotation before kicks. Spawn origin x is floor((10-width)/2)-minLocalX and y is -minLocalY, using the spawn occupied bounding box. Negative origins are allowed only when all occupied cells remain inside the visible board. This fully-contained spawn/top-boundary rule is project-specific; no hidden spawn rows are required.

Acceptance: exact cells for each orientation, a four-rotation cycle, centered spawn and rejected out-of-board occupied cells are independently asserted.

## B-02 — Input and movement

ArrowLeft/ArrowRight move one column per keydown, ArrowDown attempts one row and ArrowUp rotates clockwise. Operating-system key repeat may repeat movement/soft drop; rotation is one action per non-repeated keydown. There is no custom DAS/ARR requirement. Prevent browser scrolling only for handled gameplay keys when the game owns focus. Native form controls keep their keyboard events; shortcuts do nothing in editable fields/selects/buttons. The visible Restart button supports pointer and keyboard activation. R restarts only when game focus owns that key.

Movement and rotation never overwrite settled cells. Ordinary pieces may occupy only legal non-overlapping positions. A failed sideways/rotation action leaves state unchanged and does not count as downward movement.

Acceptance: real keyboard movement, repeated versus non-repeated actions, focus isolation, wall collisions and controls are verified in isolated Chromium and Firefox.

## B-03 — Gravity and time

Gravity interval is fixed at 1000 ms. Soft drop never changes this interval or awards points. Simulation uses monotonic elapsed time, processes due events chronologically, and gives a due lock precedence over an action at the same simulation timestamp. Advance deterministic elapsed time through every due gravity/lock event; rendering may coalesce intermediate snapshots. When hidden or blurred, clear held inputs; hidden documents suspend both gravity and locking. Resume causes no hidden-time catch-up. Restart resets timers and anchors.

Acceptance: 999/1000 ms gravity boundaries, delayed-frame equivalence, simultaneous deadlines, hidden intervals and restart timing use an injected clock.

## B-04 — Lock, clear and score

Only fully contained non-overlapping active cells can lock. Lock commits four cells, clears all full rows simultaneously, compacts rows down, adds points and then spawns the next piece atomically. Clearing 1/2/3/4 rows awards 100/300/500/800 points; no-clear placement awards zero. Cleared-line count increases by the number removed. There is no level or speed progression. Game over freezes movement, rotation, gravity and score; Restart resets board, score, lines and active state.

Acceptance: zero through four simultaneous clears, separated full rows, compaction, scoring, blocked-next-spawn and restart have exact state assertions.

## B-05 — Classic delivery rules

Choose each next shape independently using injected uniform random draws over the seven types; repeats are permitted. Rotation tests only the target orientation at its unchanged origin and rejects collisions without wall kicks. A failed downward attempt, from gravity or ArrowDown, immediately locks the current piece. First arriving on a supported row does not itself lock; the next failed downward attempt does.

Acceptance: controlled randomness may repeat a shape; a blocked rotation leaves origin/orientation unchanged; floor arrival and subsequent failed downward attempt are distinguished.

B-05 defines the classic delivery boundary. The modern gameplay delivery applies E-01 through E-03 in place of B-05 randomization, rotation and locking; all unaffected board, input, timing and scoring contracts remain applicable.

## E-01 — Seven-bag source and rotation

Generate each bag by Fisher–Yates shuffle over all seven types using injected uniform RNG. Consume each bag fully before the next; a fresh game starts a fresh bag. The next queue is deterministic for a fixed RNG stream. Use standard clockwise SRS orientation transitions and ordered JLSTZ and I kick tables, with vertical offsets translated into this downward-positive coordinate system. O rotates without changing its occupied cells. Reject when every candidate fails; never accept an out-of-board occupied cell. Use the ordered offsets below, expressed as (dx,dy) with positive y downward. Tests independently assert these normative offsets and exercise real collision scenarios; no counterclockwise or 180-degree input is required.

Acceptance: every consecutive source bag is a permutation, refill preserves the stream, O is stable, and wall/floor/stack cases exercise successful late kicks and complete rejection.


### Clockwise kick offsets

| Transition | JLSTZ ordered offsets | I ordered offsets |
| --- | --- | --- |
| 0 to R | (0,0), (-1,0), (-1,-1), (0,2), (-1,2) | (0,0), (-2,0), (1,0), (-2,1), (1,-2) |
| R to 2 | (0,0), (1,0), (1,1), (0,-2), (1,-2) | (0,0), (-1,0), (2,0), (-1,-2), (2,1) |
| 2 to L | (0,0), (1,0), (1,-1), (0,2), (1,2) | (0,0), (2,0), (-1,0), (2,-1), (-1,2) |
| L to 0 | (0,0), (-1,0), (-1,1), (0,-2), (-1,-2) | (0,0), (1,0), (-2,0), (1,2), (-2,-1) |

O uses only (0,0). Select the first candidate satisfying the active mode’s bounds/placement constraints. These clockwise SRS kick conventions operate under B-06’s fully-contained visible-board rule; full Tetris Guideline compliance is not a requirement.

## E-02 — Hold, ghost and hard drop

C holds the active shape once before its next lock; repeated keydown is ignored. Empty Hold stores it and draws from the queue; populated Hold swaps without consuming the queue. The replacement starts in spawn orientation/location; failure ends the game. Hold resets the active grounding state but does not restore the consumed Hold allowance. A lock restores allowance. Restart clears the slot.

Space hard-drops on non-repeated keydown to the ordinary lowest reachable legal landing: iterate downward until the first blocked candidate, then choose the preceding legal row. Do not cross intervening obstacles. A hard drop with zero distance is still a drop command subject to the selected locking policy. Hard drop awards no extra score. The ghost projects the same shape/orientation at exactly that landing and is visually distinct from active and settled cells. It never changes physics or board state. Rendering the active piece above the ghost avoids ambiguity when they coincide.

Acceptance: empty/populated/repeated Hold, blocked replacement spawn, matching ghost/drop positions, intervening obstacles and zero-distance drop are verified.

## E-03 — Grounding and lock delay

A piece is grounded when it is at its applicable terminal landing. On first grounding, start a 1000 ms simulation-time deadline. Grounded lateral moves and rotations preserve it if still grounded. Becoming airborne cancels it; later grounding starts a new full interval. A failed down attempt does not shorten interval locking. A hard drop starts a full interval at landing unless an existing grounded deadline remains applicable; it never resets such a deadline. At expiry, revalidate legal placement before locking; an illegal transient state cannot be committed. Hold/new spawn clears the old deadline.

Acceptance: arrival at time t cannot lock before t+1000; repeated grounded adjustments/drop do not postpone it; airborne cancellation and regrounding start a new deadline; hidden time does not consume it.

## G-01 — Whole-piece ghost boundary

Dynamic visibility shows the whole ghost if and only if every projected occupied cell has row >=10. Any projected cell in rows 0–9 hides the entire ghost; a shape spanning rows 9 and 10 is hidden. Recompute after every accepted movement/rotation/spawn, board change and activation affecting projection. Visibility cannot change the projected landing or hard-drop result.

Acceptance: footprints with minimum rows 9 and 10 distinguish the boundary, straddling hides, and transitions from lower to upper and back update without stale ghosts.

## P-01 — Activation, motion and legal landing

P on non-repeated keydown activates the current running piece only if at least one bonus exists and it is not already active. Spend exactly one bonus on success; otherwise leave state unchanged. Activation lasts until this piece locks or the game restarts/ends. Hold is disabled while active, even if its setting is enabled; attempted Hold cannot spend a bonus, change the slot or consume queue entries.

Penetrator translation and SRS candidates may cross/temporarily overlap occupied cells without changing them. They must keep occupied cells within board bounds and leave at least one legal non-overlapping placement at or below the proposed origin in that column/orientation. A candidate failing that future-landing predicate is rejected, including a kick candidate; test later kick candidates in order. A penetrator terminal landing is the greatest origin row at or below its current origin yielding a legal non-overlapping placement, scanning through occupied intermediate rows. Gravity/soft drop advances toward that terminal row and stops there; it must not step below it into an unresolvable overlap. Hard drop moves directly to it, and the ghost uses exactly the same projection. No landing may move the piece upward. Activation preserves a deadline only if still grounded; otherwise cancels it.

Acceptance: buried holes, separated legal gaps, a solid bottom row, overlapping transit, rejected no-landing adjustments, unchanged settled cells, Hold rejection and same ghost/drop terminal position are tested. Locking always revalidates containment/non-overlap.

## P-02 — Inventory and presentation

Start with zero bonuses. Exactly four rows cleared by one lock awards one bonus, whether the piece was ordinary or penetrating. Cap inventory at three; spending happens on activation before any later award. Restart resets inventory to zero. Render every occupied active penetrator cell white, with no colored fills; regular shapes use non-white colors. White borders are not required. A visible penetrator ghost uses white with a distinct outline/opacity. Show one lightning symbol per available bonus (zero means none) plus an accessible numeric label, updating immediately on earn/spend. Locked penetrator cells retain their shape’s regular non-white color because mode lifetime ends at lock.

Acceptance: 0/1/2/3 counts, capped awards, earn-after-spend, no award for fewer rows, restart and white active/non-white ordinary rendering are verified.

## C-01 — Six settings and defaults

Provide labeled native side-panel controls with these canonical values. Boolean controls use the canonical URL/cookie tokens on/off.

| Key | Allowed tokens | Default |
| --- | --- | --- |
| ghost | hide, dynamic, show | dynamic |
| hardDrop | on, off | on |
| next | on, off | on |
| hardDropLock | general, immediate | general |
| lock | failed-down, interval | interval |
| hold | on, off | on |

Show mode labels understandable without tokens. Next preview displays exactly one queued shape when enabled and consumes no queue entry. Disabled Hold hides/marks its control unavailable but retains its slot. Hard-drop-off ignores Space without invoking any locking action. Ghost hide suppresses projection rendering; show ignores midline; dynamic uses G-01. Disabling preview hides it without changing queue state. Native settings controls retain keyboard navigation without moving the piece.

Acceptance: all values/defaults, combinations including hidden ghost with enabled drop, hidden next with unchanged queue, disabled Hold with retained slot, and control focus are verified.

## C-02 — Live policies and restart

Serialize setting changes as session actions. Visibility and hard-drop/Hold enablement apply immediately. Capture general and hard-drop locking selections at each active-piece spawn, including Hold replacement; changes do not alter that piece’s captured policy or deadline. Restart retains current selections, creates a fresh game and captures them on the first piece.

Under failed-down general locking, lock only on a failed gravity or soft-down attempt at terminal landing, not just on arrival. There is no interval timer under this policy. A penetrator at terminal landing counts as failed-down even if the next overlapping row geometrically fits bounds. Under interval locking apply E-03. Immediate hard-drop locking overrides either general policy only for an enabled successful hard-drop command, including zero-distance drops. Follow-general preserves the general policy, so failed-down hard drop arrives without synthesizing a failed downward attempt. Other input remains subject to active mode and Hold eligibility.

Acceptance: change both policies while grounded, observe unchanged active timing, then verify new policies after spawn/Hold/restart. Test general-policy × hard-drop-policy combinations for ordinary and penetrating pieces, zero-distance drops and disabled Space.

## S-01 — Independent startup resolution

Use the C-01 keys for query parameters and cookie names prefixed tetris_ (for example ghost and tetris_ghost). Tokens are exact case-sensitive strings after normal URL decoding. Empty/unknown/case-mismatched values are invalid. If a query key repeats, use its last occurrence and validate only that occurrence. Decode cookie values safely; malformed encoding is invalid. For duplicate same-name cookies use the first observed value to avoid non-deterministic merges; document the limitation that other paths may shadow app-owned cookies.

Resolve each setting independently: valid explicit URL token, else valid cookie, else default. Invalid URL values do not overwrite a valid cookie. Missing query parameters preserve cookie choices. Invalid cookies do not contaminate other settings. Apply the entire resolved settings snapshot before the first piece spawns, so initial lock-policy capture is correct. Save each valid explicit URL token to its corresponding cookie, including defaults, without writing cookies for omitted/invalid URL keys merely because resolution used a default. Startup must not add omitted parameters or normalize unrelated fields.

Acceptance: mixed sources across all six keys; valid explicit default overriding a non-default cookie; omitted keys retaining cookies; invalid URL with valid cookie; invalid cookie/default; duplicate and malformed inputs; first-spawn policy agreement.

## S-02 — Writes, URL and failure behavior

On each player setting change, validate and apply the selection in memory, write its cookie, and set exactly one corresponding query parameter using history.replaceState without navigation. Set collapses duplicates for that key. Preserve unrelated query parameters, their values, other settings’ parameters and the fragment; equivalent URL encoding may be normalized by URLSearchParams. Cookie and URL writes are attempted independently, so failure of either cannot skip the other.

Cookies contain only canonical setting tokens, use Path=/, SameSite=Lax, a 365-day Max-Age, no Domain, and Secure on HTTPS. Cookie-read/write or History API errors leave the selected in-memory value effective and display a non-blocking persistence warning. Detect silent cookie-write rejection by reading back the selected cookie; a URL write exception also warns. Read failures treat the affected source as unavailable and continue resolution. No persistent gameplay board, score, Hold slot or bonus inventory is stored. Reload/reopen restores configuration according to S-01, not prior gameplay.

Acceptance: all six setting round-trips across reload, explicit default write, independent write failures, blocked cookies, history exceptions, fragment/unrelated fields and retained omitted-cookie values are browser/adapter scenarios.

## Q-01 — Quality, delivery and verification

The application runs without backend calls and exposes understandable score, lines and game status through native HTML. Board and controls remain usable without overlap at desktop viewport sizes; keyboard focus is visible. Rendering and event hookup must not create multiple animation loops after restart. Core tests control time/randomness and test transitions without DOM. Browser checks exercise real inputs, focus, screenshots and restart in isolated Chromium primary and compatible managed Firefox secondary under BROWSER_DEV_POLICY.md. Required browser failures are reported separately and block affected acceptance; a passing unit suite does not waive them.

Build/type checks and reproducible static serving instructions are part of delivery. Runtime dependency versions and browser binaries are pinned/identified during authorized implementation; document preparation does not install them. No performance claim or tested compatibility is asserted by this specification.
