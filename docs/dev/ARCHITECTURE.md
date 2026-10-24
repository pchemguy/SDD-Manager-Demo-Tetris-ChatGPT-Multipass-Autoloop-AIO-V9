# Architecture

[PROJECT](PROJECT.md) defines the intended product. This design uses a small functional game core and thin browser adapters; [DECOMPOSITION](DECOMPOSITION.md) assigns component responsibilities, and [SPEC](SPEC.md) owns exact contracts.

## Blocks and dependency direction

| Block | Owns | Depends on |
| --- | --- | --- |
| Game core | Board, active piece, legal transitions, score, lifecycle | Value types and injected randomness only |
| Session controller | Serial input dispatch, monotonic simulation clock, restart, snapshots | Game core |
| Browser presentation | Canvas rendering, HTML status, keyboard and visibility events | Read-only snapshots and controller commands |
| Application composition | Construction, event hookup, teardown | Concrete adapters and controller |

Events flow from browser adapters through the controller into the core, followed by a snapshot render. Core modules import no DOM, Canvas, browser storage or wall-clock globals. Presentation cannot mutate engine state. There is one authoritative settled board and one active piece; rendering never contributes collision data.

## State, timing and lifecycle

The controller normalizes animation time into simulation time, dispatching one ordered action stream. A hidden document suspends the simulation clock and clears held-key state. Resume establishes a new wall-clock anchor without catching up hidden time. Restart resets gameplay and timing through the same controller; no duplicate event subscriptions or animation loops are created.

The engine exposes transition functions over explicit state and immutable/read-only snapshots. State transition ownership is centralized because locking, clearing rows and spawning must be atomic. Geometry and placement predicates are pure helpers. Randomness is supplied at construction so deterministic tests can drive exact sequences without browser instrumentation.

## Tradeoffs and invariants

Canvas provides direct board rendering; native HTML keeps controls focusable and labels readable. A DOM board is viable but offers no required benefit for the bounded board. A UI framework and entity-component architecture add unnecessary machinery. This functional design uses small cohesive modules rather than inheritance or a plugin framework.

Only a legal, fully contained, non-overlapping placement can be committed to the settled board. One transition owns lock, clear, score and spawn; a renderer or input callback cannot partially perform it. Snapshots own presentation data, not browser resources. Application teardown cancels owned animation/events and leaves unrelated browser state alone.

## Enhanced game rules

The piece source owns a shuffled seven-piece bag. Rotation geometry owns SRS orientation and ordered kick candidates. The engine owns Hold eligibility and grounded lock state. A single landing service computes the normal first reachable downward landing for both ghost and hard drop; callers never maintain separate collision logic. The controller supplies elapsed simulation time, while the engine owns deadline creation/cancellation. This separates game policy from frame scheduling.
