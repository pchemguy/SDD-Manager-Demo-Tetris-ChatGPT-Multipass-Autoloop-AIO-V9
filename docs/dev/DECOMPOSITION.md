# Component decomposition

[ARCHITECTURE](ARCHITECTURE.md) owns block relationships. Components below refine those blocks without prescribing physical placement; `layout.md` owns that allocation.

## Responsibilities and verification seams

| Component | Responsibility and limits | Provisional boundary | Verification seam |
| --- | --- | --- | --- |
| Geometry | Tetromino cells, orientations, bounds and legal placement; no score or DOM | cells(type, orientation), canPlace(board, piece) | Pure cell/boundary tests |
| Board rules | Commit legal pieces, find full rows, compact them; no timing | commitAndClear(board, piece) | Simultaneous clears and invariant tests |
| Piece source | Provide ordinary random shape draws through injected RNG; no engine lifecycle | next() | Controlled draw tests |
| Engine | Active/settled state, score, running/game-over lifecycle, spawn and movement | dispatch(state, command), advance(state, elapsed) | Seeded action and elapsed-time sequences |
| Session controller | One dispatch queue and simulation clock; owns restart orchestration | start(), dispatch(), suspend(), resume(), dispose() | Fake clock and listener lifecycle tests |
| Canvas view | Paint board and active cells from snapshot; no state mutation | render(snapshot) | Browser screenshot/geometry checks |
| Browser input/status | Map focused keyboard/events and HTML restart/status | controller commands, render status | Real key/focus/visibility interactions |

## Collaboration and ownership

Composition creates the random source, engine, controller and views once. Keyboard events submit commands; animation callbacks submit simulation deltas. The controller serializes both and publishes a snapshot only after the engine transaction finishes. Geometry returns cells; board rules return a new board/clear result; the engine owns progression and scoring. Browser adapters may fail independently of the pure core.

Restart resets engine-owned gameplay state and clock anchors; it does not install a second listener set. Hidden-page suspension is a controller concern. Game over stops gameplay transitions but permits restart. Input fields and native controls retain their keyboard behavior. Rendering is a one-way read of state, so tests can exercise rules without screenshots and browser tests can assess actual presentation and focus.
