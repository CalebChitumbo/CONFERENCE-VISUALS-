---
name: verify
description: Build/launch/drive recipe for verifying changes to the conference display app (index.html) end-to-end in headless Chromium.
---

# Verifying this app

Single-file vanilla-JS app, no build step. Surface = browser GUI with TWO
windows: control panel (`index.html`) and projector display (`index.html#display`).

## Launch

```bash
python3 -m http.server 8931 &          # serve repo root (BroadcastChannel needs http, not file://)
```

Drive with Playwright + the pre-installed browser (do NOT `playwright install`):

```js
const browser = await chromium.launch({ executablePath: '/opt/pw-browsers/chromium' });
```

## Flows worth driving

- Control boots with 6 sample people; `#btnOpenDisplay` must open a popup
  **synchronously on click** (the Window Management `getScreenDetails()` await
  must come *after* `window.open`, or the popup gets blocked).
- Push each scene tab → display follows via BroadcastChannel within ~1s.
- Rapid ArrowRight spotlight stepping → `.scene-slot .scene` count must stay ≤ 2
  (scene-stacking regression check).
- Blackout toggle must fade `.blackout.on` **without** rebuilding the scene node.
- Countdown quick-set buttons live-apply when countdown is on screen; targets are
  LOCAL `datetime-local` strings (never `toISOString`).
- Forced test URL: `#display?scene=grid|spotlight|countdown|title`.
- Import a hostile JSON (non-object people, duplicate ids, `javascript:` photos,
  markup in names) via `#importFile` — must sanitize, render literally, no script exec.
  Accept the `confirm()` dialog via `page.once('dialog', d => d.accept())`.

## Gotchas

- Logo 404s (`logos/*.png`) are by design — the `onerror` swaps in a text fallback;
  filter those out of console-error assertions.
- State lives in `localStorage['rpo8.display.state.v1']` (+ a `.stamp` key for
  cheap cross-window polling); read it in `page.evaluate` to assert persistence.
- App functions (`state`, `persist()`, `renderAll()`, `uid()`) are globals —
  usable from `page.evaluate` to seed bulk data (e.g. 32-person grid overflow check).
