# Browser Tetris

## Purpose and users

Provide desktop keyboard players with a responsive, understandable browser Tetris game. Players position falling tetrominoes, clear rows, earn points and restart after game over.

## Goals and constraints

Use TypeScript, a Canvas board and native HTML controls, delivered statically over HTTP(S) without a backend. Keep game rules deterministic under injected time and randomness. Follow the root browser policy: isolated Chromium primary and compatible managed Firefox secondary; headless interaction and screenshots are sufficient. Preserve a usable game throughout incremental delivery.

## Principal scope

The classic game has a 10×20 visible board, seven tetromino shapes, movement, clockwise rotation, soft drop, fixed-speed gravity, collision-safe locking, row clearing, scoring, game over and restart. Hiding the page suspends simulation time.

Hold, a landing ghost, 7-bag generation, SRS clockwise wall kicks and hard drop support modern play. Grounded pieces normally receive one full gravity interval before locking; grounded adjustments do not reset that delay.

The ghost is shown only when its entire projected footprint is in the lower half of the board. A footprint straddling the midline is hidden.

Bonus-gated penetrator activation lets the current piece pass through settled cells without destroying them. The final placement must be fully inside the board and non-overlapping; hard drop and ghost share the lowest valid landing. Hold is unavailable while penetration is active. Four-line clears grant one bonus, capped at three. Active penetrators are entirely white; regular pieces are not white. One side-panel symbol represents each available bonus.

Six side-panel settings control ghost visibility, hard drop, next preview, hard-drop locking, general locking and Hold. Feature toggles apply immediately; locking-policy selections affect the next spawned piece. Disabling Hold preserves its stored piece. Restart retains selected settings.

Each setting independently resolves a valid explicit URL value, then a valid cookie, then its default. Player changes update both cookie and URL. Valid explicit URL values are saved even when equal to defaults; omitted parameters preserve cookies. Invalid values fall through independently without overwriting valid saved choices. Persistence failures leave gameplay operational and display a concise warning.

## Non-goals and intended outcome

No accounts, multiplayer, online leaderboard, backend, touch controls, audio or level progression is required. Success is a complete responsive game with clear status, predictable rules and verified interactions across its enabled capabilities. The documents define intended behavior; they do not claim a delivered implementation.
