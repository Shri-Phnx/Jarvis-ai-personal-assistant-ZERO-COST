# Clean installation (zero cost, Kokoro voice)

Based on [adewaskar/jarvis](https://github.com/adewaskar/jarvis) (MIT). No API
keys and no paid services. You only need a Claude Code login.

## Easiest: let Claude Code do it

1. Install [Node.js 20+](https://nodejs.org) and
   [Claude Code](https://docs.claude.com/en/docs/claude-code), then run
   `claude auth login` once.
2. Clone this repo and open it in Claude Code.
3. Say: **"Set up and run Jarvis."** Claude follows `CLAUDE.md` step by step,
   including the Kokoro voice.

## Manual

```bash
git clone https://github.com/Shri-Phnx/Jarvis-ai-personal-assistant-ZERO-COST.git
cd Jarvis-ai-personal-assistant-ZERO-COST
npm install
npm run setup
```

Create a file named `.env.local` in the project folder containing:

```
VITE_TTS_ENGINE=kokoro
```

Start it:

```bash
npm start
```

Open the `Local:` address it prints (usually http://localhost:5173) in Chrome or
Edge, click **INITIALISE**, allow the microphone, and say **"Hey Jarvis"**.

## Windows notes

- PowerShell may say *"running scripts is disabled"*. Use `npm.cmd` instead of
  `npm` (e.g. `npm.cmd start`). No need to change your execution policy.
- *"EADDRINUSE: address already in use"* means Jarvis (or something else) is
  already running on that port. Close the other copy, or see step 5 in
  `CLAUDE.md` to move to another port.
- Keep only one Jarvis tab open — Chrome gives the microphone to one tab.

## Voice

- Kokoro downloads a ~85 MB voice model the first time, then runs offline.
  It is noticeably slower to respond than the built-in voice.
- Too slow? Set `VITE_TTS_ENGINE=system` in `.env.local` and restart.
- Press **V** in the app to cycle voices, **D** for diagnostics.
