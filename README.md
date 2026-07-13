# Geometry Rush 🎮

A self-contained Geometry Dash-style arcade runner — cube + ship modes, portals,
unlockable colors, coins, stars, and a Demon level with its own soundtrack.
Built as an installable **PWA** that works offline.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole game (HTML + CSS + JS inline) |
| `manifest.webmanifest` | PWA metadata (name, icons, colors) |
| `sw.js` | Service worker — offline caching + installability |
| `icons/icon-192.png`, `icons/icon-512.png` | App icons |
| `.nojekyll` | Tells GitHub Pages to serve files as-is |

## Run locally

A PWA needs `http(s)` — service workers don't run from `file://`. Serve the folder:

```bash
# from inside the geometrydash folder
python -m http.server 8000
```

Then open <http://localhost:8000>. (Opening `index.html` directly still plays the
game, but the service worker / install prompt won't activate.)

## Deploy to GitHub Pages

1. Create a repo (e.g. `geometry-rush`) and push this folder's contents to it:
   ```bash
   git init
   git add .
   git commit -m "Geometry Rush PWA"
   git branch -M main
   git remote add origin https://github.com/<your-user>/geometry-rush.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Build and deployment**
   - **Source:** *Deploy from a branch*
   - **Branch:** `main`, folder `/ (root)` → **Save**
3. Wait ~1 minute. Your game is live at:
   ```
   https://<your-user>.github.io/geometry-rush/
   ```

All paths in this project are **relative**, so it works whether it's hosted at a
domain root or in a `/repo-name/` subpath.

## Installing the app

Open the Pages URL in Chrome/Edge (desktop or Android) and use the **Install**
icon in the address bar, or Android's "Add to Home screen". On iOS Safari use
**Share → Add to Home Screen**. Once installed it launches fullscreen and runs offline.

## Updating after changes

Browsers cache the app via the service worker. After editing `index.html` (or any
asset), bump the version in `sw.js`:

```js
const CACHE_VERSION = 'geo-rush-v2';   // was v1
```

Commit & push — clients pick up the new version on their next visit.
