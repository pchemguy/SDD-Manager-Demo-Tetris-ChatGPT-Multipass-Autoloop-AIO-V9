# Component decomposition

[ARCHITECTURE](ARCHITECTURE.md) owns block relationships. Components below refine those blocks without prescribing physical placement; [layout](layout.md) owns that allocation.

## Responsibilities and verification seams

| Component | Responsibility and limits | Provisional boundary | Verification seam |
| --- | --- | --- | --- |
| Geometry | Tetromino cells, orientations, bounds and legal placement; no score or DOM | cells(type, orientation), canPlace(board, piece) | Pure cell/boundary tests |
| Board rules | Commit legal pieces, find full rows, compact them; no timing | commitAndClear(board, piece) | Simultaneous clears and invariant tests |
| Piece source | Shuffled 7-bag and peekable queue; injected RNG, independent of Hold | next(), peek() | Bag permutations, refill and non-consuming peek |
| Engine | Active/settled state, score, running/game-over lifecycle, spawn and movement | dispatch(state, command), advance(state, elapsed) | Seeded action and elapsed-time sequences |
| Session controller | One dispatch queue and simulation clock; owns restart orchestration | start(), dispatch(), suspend(), resume(), dispose() | Fake clock and listener lifecycle tests |
| Canvas view | Paint board and active cells from snapshot; no state mutation | render(snapshot) | Browser screenshot/geometry checks |
| Browser input/status | Map focused keyboard/events and HTML restart/status | controller commands, render status | Real key/focus/visibility interactions |
| Landing/rotation | Ordinary landing and ordered SRS kick candidates; no mode lifetime | landing(board,piece,mode), rotate(board,piece) | Obstacles, walls/floor and orientation cases |
| Hold/lock state | Engine-owned Hold slot, per-piece eligibility and grounded deadline | Engine commands and snapshot fields | Swap/spawn failures and exact deadline boundaries |
| Ghost visibility | Whole-footprint midline predicate; never alters projection | visibleGhost(cells, policy) | All-upper, straddling and all-lower cases |
| Penetration rules | Engine-owned mode/inventory; landing-policy scan and safe adjustment validation | activate(), landing(...,penetrator) | Buried gaps, transient overlap, illegal terminal states and bonus cap |
| Settings model | Defaults and six validated selections; lock policy snapshot at spawn | get(), set(key,value), subscribe() | Live switches and next-piece policies |
| Settings/preview view | Labeled selects, non-consuming next preview and Hold availability | Settings notifications plus engine snapshot | Focus isolation and visible control/state agreement |
| Configuration codec | Canonical keys/tokens and per-source independent validation | parse(key,raw), serialize(key,value), resolve(sources) | Mixed validity, omissions, defaults and duplicates |
| Browser persistence | Cookie reads/writes and URL history replacement; memory fallback | load(), saveSetting(), warning result | Round-trip reload, blocked cookies and throwing history |

## Collaboration and ownership

Composition creates the random source, engine, controller and views once. Keyboard events submit commands; animation callbacks submit simulation deltas. The controller serializes both and publishes a snapshot only after the engine transaction finishes. Geometry returns cells; board rules return a new board/clear result; the engine owns progression and scoring. Browser adapters may fail independently of the pure core.

Restart resets engine-owned gameplay state and clock anchors; it does not install a second listener set. Hidden-page suspension is a controller concern. Game over stops gameplay transitions but permits restart. Input fields and native controls retain their keyboard behavior. Rendering is a one-way read of state, so tests can exercise rules without screenshots and browser tests can assess actual presentation and focus.

The engine owns held piece, Hold availability, active orientation and lock deadline. Landing projection is pure and shared by ghost/drop. A swap creates a new active spawn transaction, while Hold-use eligibility remains consumed until lock. Lock timing does not live in setTimeout callbacks.

Penetrator mode and bonus count belong only to the engine. Placement/landing helpers receive mode explicitly; they do not spend bonuses. Rendering reads mode rather than guessing from shape color. Lock/clear awards inventory before the next spawn and resets mode.

Settings own selections; each active piece owns its captured locking policies. A Hold replacement is a spawn for policy capture but does not restore Hold eligibility. The preview reads the next queue item without consumption.

Startup resolution finishes before first spawn. Codec tests use string inputs and no DOM. Adapter tests supply fake cookie/history ports; browser tests verify real reload behavior. A failed persistence write returns a warning without rolling back the in-memory selection.
