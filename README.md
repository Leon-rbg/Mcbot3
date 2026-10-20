# Mineflayer Civilization — Starter Kit

A multi-bot Mineflayer starter for a Minecraft Java server, with roles, team status, movement commands and optional Ollama-based planning.

## Reality check

This is a working starter framework, not an all-capable autonomous civilization. It currently supports connecting multiple bots, basic role assignment, following/coming/stopping, team status and optional AI planning constrained to those supported actions. Autonomous mining, farming, chest logistics, crafting, combat and building need dedicated task implementations and testing.

Mineflayer's project currently lists Minecraft 26.1 among supported versions. Do not assume that 26.1.2 or 26.2 works; check the exact server version and current dependency support first.

## Requirements

- Node.js 20+
- A Minecraft Java server that permits bots
- For `MC_AUTH=offline`, the server itself must be configured for offline mode. This does not bypass authentication on online-mode servers.
- Optional: an Ollama server with a model already downloaded

## Setup

1. Copy `.env.example` to `.env`.
2. Edit `MC_HOST`, `MC_PORT`, `MC_VERSION`, `BOT_NAMES` and `CONTROLLER_NAMES`.
3. Install packages:
   ```bash
   npm install
   ```
4. Check syntax:
   ```bash
   npm run check
   ```
5. Start:
   ```bash
   npm start
   ```

## In-game commands

Commands are accepted only from names listed in `CONTROLLER_NAMES`.

- `!status` — report bot roles and connection state
- `!team` — show the team status
- `!come` — move the bot near you
- `!follow` — follow you
- `!stop` — stop movement
- `!task <request>` — ask the optional AI planner to interpret a request; only a small allowlist of actions can be executed

The controller must be visible to the bot for `!come` and `!follow`.

## Optional Ollama

Set `OLLAMA_URL` to an accessible Ollama endpoint, for example `http://127.0.0.1:11434` if Ollama runs on the same machine. Set `OLLAMA_MODEL` to a model that has been downloaded there. The bot host must be able to reach the endpoint. A cloud host and a separate local Ollama instance are not automatically connected.

Ollama on the same free cloud instance may be too resource-heavy. Never expose an unauthenticated Ollama port publicly. If your endpoint is remote, protect it and use a private network or secure tunnel.

## Hosting limits

- GitHub Codespaces is for development/testing, not reliable 24/7 hosting. Free personal accounts have a monthly included compute quota.
- Render Free web services can spin down after inactivity and are not appropriate for a persistent Minecraft TCP bot.
- A genuinely always-on host usually requires a paid server or a suitable computer left running. Free offers can change and are not guaranteed.
- Never commit `.env` or account credentials to GitHub.

## Troubleshooting

- `ECONNREFUSED`: check host/port and whether the server is online.
- `Unsupported protocol version`: check exact Mineflayer and Minecraft version compatibility; do not lie about the server version.
- `Kicked`: check server rules, allowlist, authentication mode and whether bots are allowed.
- Bot names must be unique and the server may enforce account authentication or rate limits.
