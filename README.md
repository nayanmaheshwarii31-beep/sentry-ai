# SENTRY AI — Delhi Urban Intelligence Platform

A single-page Apple-inspired dashboard covering all 13 Delhi NCT districts, 110+ localities,
69 metro stations, 300 roads, hotspots, analytics, an AI assistant, and an Urban Intelligence
Feed — all driven by deterministic, structured prediction data (no random generators).

## Open in VS Code

1. Unzip this folder and open it in VS Code (`File → Open Folder…`).
2. Install the recommended extension when prompted — **Live Server** (`ritwickdey.LiveServer`).
   VS Code should auto-suggest it; if not, install it from the Extensions panel.
3. Right-click `index.html` → **"Open with Live Server"** (or click "Go Live" in the
   bottom-right status bar).
4. The app opens at `http://127.0.0.1:5500`.

You can also just double-click `index.html` to open it directly in a browser — everything
works without a server, since there's no build step.

## About the "Claude AI" features

The AI Assistant and the Urban Intelligence Feed call `https://api.anthropic.com/v1/messages`
directly from the browser. That endpoint requires a server-side API key and CORS isn't open
to arbitrary websites, so when you run this locally those calls will fail — by design, the
code catches that and **automatically falls back to the built-in deterministic responses**
(`generateFallbackReply`, `getFallbackNews`), so nothing breaks. You'll just see the
rule-based answers instead of live Claude-generated text.

To make the AI features actually call Claude, you'd need to proxy the request through your
own backend that holds the API key (never put an API key in client-side JS).

## Project structure

```
.
├── index.html        # the entire app — HTML, CSS, and JS in one file
└── .vscode/
    ├── extensions.json   # recommends Live Server
    └── settings.json     # Live Server default port/config
```

## Editing tips

- All app logic lives in the single `<script>` block at the bottom of `index.html`.
- Data layers (`DISTRICTS`, `LOCALITIES`, `METRO_STATIONS`, `ROADS`, `HOTSPOTS_DATA`,
  `SEARCH_INDEX`, etc.) are plain JS objects/arrays near the top of the script — edit
  these directly to add or adjust coverage.
- No npm install or build step is required.
