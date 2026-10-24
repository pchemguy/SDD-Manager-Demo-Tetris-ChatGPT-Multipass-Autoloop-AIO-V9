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

## Q-01 — Quality, delivery and verification

The application runs without backend calls and exposes understandable score, lines and game status through native HTML. Board and controls remain usable without overlap at desktop viewport sizes; keyboard focus is visible. Rendering and event hookup must not create multiple animation loops after restart. Core tests control time/randomness and test transitions without DOM. Browser checks exercise real inputs, focus, screenshots and restart in isolated Chromium primary and compatible managed Firefox secondary under BROWSER_DEV_POLICY.md. Required browser failures are reported separately and block affected acceptance; a passing unit suite does not waive them.

Build/type checks and reproducible static serving instructions are part of delivery. Runtime dependency versions and browser binaries are pinned/identified during authorized implementation; document preparation does not install them. No performance claim or tested compatibility is asserted by this specification.
