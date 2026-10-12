# CLAUDE.md — set this project up for the user

Claude Code reads this file automatically when it opens this repo. If the user
asks to "set up", "install" or "run" Jarvis, follow these steps in order. Go one
step at a time, say what happened after each, and stop if a step fails twice.

This is a browser voice assistant (Vite/React "face" + Node "bridge" that runs
Claude Code headless). It needs NO API keys. Voice = Kokoro (free, runs in the
browser). Do not ask for ElevenLabs or any other key.

## Ground rules

- Ask before installing anything system-wide (Node.js, Git, Claude Code).
- Never delete files. Never commit or push anything.
- Never read or edit `~/.claude.json`. Do not add MCP servers or connectors.
- Read-only mode only: never run `npm run bridge:writes`.
- Never print keys or tokens; mask them as `<YOUR_KEY_HERE>`.

## Steps

1. **Prerequisites** — check, don't install:
   - `node --version` → must be 20 or newer
   - `claude --version` and `claude auth status` → must be logged in.
     If not logged in, ask the user to run `claude auth login` themselves.
2. **Install dependencies:** `npm install`
   (Windows PowerShell blocks `npm.ps1`; use `npm.cmd install` there.)
3. **Preflight check:** `npm run setup` — report its result in plain words.
4. **Kokoro voice:** if `.env.local` does not exist, create it with exactly:
   ```
   VITE_TTS_ENGINE=kokoro
   ```
   If it exists, make sure that line is present and leave the rest alone.
   Keep the default voice (`bm_george`) unless the user asks otherwise.
5. **Port check:** the bridge uses port 8787 and the page uses 5173. If 8787 is
   already in use, pick a free port (e.g. 8788) and set all three:
   - start with `JARVIS_BRIDGE_PORT=8788`
   - add `VITE_BRIDGE_URL=ws://localhost:8788` to `.env.local`
   - in `index.html`, change every `localhost:8787` / `127.0.0.1:8787` in the
     Content-Security-Policy to the new port.
6. **Start:** `npm start` (Windows: `npm.cmd start`). Report the `Local:` URL it
   prints. Tell the user to keep that terminal open — closing it stops Jarvis.
7. **Hand over to the user** (Claude cannot do this part):
   - Open the URL in a real Chrome or Edge window (not an editor preview pane).
   - Close any other Jarvis tab — Chrome lets only one tab use the microphone.
   - Click INITIALISE, allow the microphone, say "Hey Jarvis".
   - First Kokoro use downloads ~85 MB once; replies start slowly until it loads.
8. **If the voice lags or fails:** change `.env.local` to
   `VITE_TTS_ENGINE=system` and restart. That uses the browser's built-in voice.
