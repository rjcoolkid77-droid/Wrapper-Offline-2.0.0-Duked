# Base44 Dev Environment

## What this app is
Wrapper Online — a GoAnimate Legacy Video Maker remake in plain Node.js.
No framework (raw `http.createServer`), no database (file-based storage in `_SAVED`, `_CACHÉ`, `_THEMES`, `_PREMADE`, `_EXAMPLES`).

## How it runs
- Entry point: `main.js` → requires `server.js` which creates an HTTP server.
- Port: set via `PORT` env var (defaults to `SERVER_PORT=80` from `env.json`). Compose sets `PORT=3000`.
- Dependencies: `npm install` (one dep, `node-zip`, is a GitHub repo so the image must have git — `node:22` full image includes it).
- Live reload: `node --watch main.js` restarts on source changes; call `reload_preview` to refresh the iframe (no HMR — plain HTML).

## Verifying it works
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → 302 (redirects to `/pages/html/list.html`)
- The list page at `/pages/html/list.html` is the main UI.
- Flash content (SWF) loads from an external asset server configured in `config.json` (`SWF_URL`, `STORE_URL`, `CLIENT_URL`); without that server the HTML still serves but Flash won't render.

## No external secrets needed
The app boots without any credentials. TTS features call free/demo APIs at runtime.
