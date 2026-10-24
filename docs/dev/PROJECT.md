# Browser Tetris

## Purpose and users

Build a small browser game for desktop keyboard players who want a complete, understandable classic Tetris session. The player moves and rotates falling tetrominoes, fills rows, earns points, reaches game over and can immediately restart.

## Intended outcome

Deliver a playable game with clear board state, responsive controls, visible score and an unmistakable game-over state. Keep gameplay rules predictable and independently testable. A restart begins a clean game without reloading the page.

## Scope

- A board with seven standard tetromino shapes, one falling piece and settled cells.
- Keyboard movement left and right, clockwise rotation and soft drop, with automatic gravity.
- Collision handling that keeps settled pieces within the board and prevents overlapping placements.
- Piece locking, simultaneous full-row clearing, downward compaction and line-clear scoring.
- Visible score and cleared-line count, game over on blocked spawning, and a restart control.
- Suspension when the page is hidden, preventing background time from causing an unexpected loss.

## Proposed baseline choices

Use a 10-column by 20-row visible board, fixed gravity speed, independently random piece draws and simple rotation without wall kicks. Lock immediately when a downward attempt cannot move the piece. Award points for completed rows using a documented deterministic rule. Detailed geometry, controls, timing and scoring acceptance belong in the specification.

These are agent recommendations for approval with this brief; they were not additional requirements supplied by the user.

## Delivery constraints

The proposed implementation uses TypeScript, Canvas for the board and ordinary HTML for status and controls. It runs as a static client application over HTTP(S), with no backend dependency. Keep the game engine separate from rendering and browser input so deterministic rule tests do not need a browser.

Use the repository's browser development policy: isolated Chromium as the primary verification target and framework-compatible managed Firefox as the secondary target. Headless execution can cover gameplay interaction and screenshots. Browser setup is an implementation prerequisite, not a requirement for reviewing these documents.

## Non-goals

Online multiplayer, accounts, network leaderboards, mobile touch controls, audio, a level/speed progression system and visual effects are outside the proposed baseline. The game does not need external services or user data collection.

## Readiness and delegated detail

This brief defines intended behavior, not an existing implementation. Board presentation, exact score values, keyboard bindings and component interfaces remain for the specification and design owners within the agreed scope.
