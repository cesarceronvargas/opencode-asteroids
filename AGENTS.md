# AGENTS.md

Vanilla JS + HTML5 Canvas clone of Asteroids. No build step, no dependencies, no framework, no `package.json`, no tests, no linter, no typecheck. The whole game is one file.

## Running

Open `index.html` directly in a browser, or:

```bash
npx serve .
```

Visit http://localhost:3000. No HMR — reload the page to see changes.

## Verification

No automated checks exist. After any change, open the game in a browser and confirm it boots and the changed behavior works. Do not invent `npm`/lint/test commands — there are none.

## Architecture

- `index.html` — page shell; loads `game.js` as a **classic `<script>`** (not a module). `game.js` relies on top-level script scope and a canvas with `id="canvas"`.
- `game.js` — all logic (~420 lines): input, entities, game state, main loop.
- Canvas is fixed 800x600 (`W`/`H` constants); the page is not responsive.

## Conventions to preserve

- Comments, HUD strings, and overlay text are in **Spanish** — match this.
- Entity motion is **delta-time based** (`dt` in seconds). The loop clamps `dt` to `0.05` to survive tab-switch stalls.
- World is **toroidal**: positions wrap via `wrap(v, max)`; any new entity motion must keep wrapping.
- Input has two layers: `keys[code]` (held state) and `pressed(code)` (single-frame, **consumed on read** — call it exactly once per frame in `update()`, or input is silently dropped).
- Game state machine: `'playing'` | `'dead'` | `'gameover'` (dispatched at the top of `update()`).
- Entity classes (`Ship`, `Asteroid`, `Bullet`, `Particle`, `PowerUp`) each expose `update(dt)`, `draw()`, and a `dead` flag used for array filtering each frame. Follow this contract when adding entities.
