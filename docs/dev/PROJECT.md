# Browser Tetris

## Purpose and users

Provide desktop keyboard players with a responsive, understandable browser Tetris game. Players position falling tetrominoes, clear rows, earn points and restart after game over.

## Goals and constraints

Use TypeScript, a Canvas board and native HTML controls, delivered statically over HTTP(S) without a backend. Keep game rules deterministic under injected time and randomness. Follow the root browser policy: isolated Chromium primary and compatible managed Firefox secondary; headless interaction and screenshots are sufficient. Preserve a usable game throughout incremental delivery.

## Principal scope

The classic game has a 10×20 visible board, seven tetromino shapes, movement, clockwise rotation, soft drop, fixed-speed gravity, collision-safe locking, row clearing, scoring, game over and restart. Hiding the page suspends simulation time.

Hold, a landing ghost, 7-bag generation, SRS clockwise wall kicks and hard drop support modern play. Grounded pieces normally receive one full gravity interval before locking; grounded adjustments do not reset that delay.

## Non-goals and intended outcome

No accounts, multiplayer, online leaderboard, backend, touch controls, audio or level progression is required. Success is a complete responsive game with clear status, predictable rules and verified interactions across its enabled capabilities. The documents define intended behavior; they do not claim a delivered implementation.
