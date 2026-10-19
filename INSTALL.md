# Install Arcade

Instructions for a coding agent. Use the official hosted service; no local game server or developer credentials are needed.

1. Check for an existing Arcade connection. If `arcade.catalog` and `arcade.play` are available, reuse it; do not add a duplicate connection. For an existing installation from this repository, follow **Update** below so the bundled instructions are current.
2. In Codex with terminal access and plugin support, run the commands below. Reuse an existing checkout when possible; preserve local changes. Requires Git and Codex with `codex plugin` support. After installation, reload plugins through the host's supported mechanism. If the desktop host does not pick up the change, restart it. Test in a fresh chat.
3. Read the live catalog, choose Rally when present (otherwise an available game), and call `arcade.play` with its exact ID. Confirm the real game opens inline.

```sh
git clone https://github.com/hoerl/arcade.git
cd arcade
codex plugin marketplace add .
codex plugin add worldchat-arcade@arcade-shared
```

If terminal/plugin installation is unavailable, do not attempt these commands through an unrelated tool. In ChatGPT, reuse an existing authorized Arcade connection if available. Otherwise explain that public ChatGPT installation is pending and offer [browser play](https://arcade.beautifulthings.org/?game=rally). This GitHub guide does not grant access to a private ChatGPT app.

## Rules

- The bundled connection uses `https://arcade.beautifulthings.org/mcp`.
- Do not install a second MCP or World ID plugin, start a local server, request secrets, or use sandbox World ID.
- Players verify inside Arcade when they choose **Play a Human**. Let the user complete verification. **Destroy a Bot** does not require World ID.
- If no game is specified, choose from the live catalog. Never generate a substitute game or claim that installation alone proves it launched.
- Test an Arcade mention in a fresh chat when possible. Report any missing host support, access, or unverified behavior plainly.
- Preserve the copyright and [MIT license](LICENSE.md) notices.

## Update

Server-side fixes apply on the next MCP request. Bundled skills are installed files and need a package update. In the existing public installer checkout, run:

```sh
git pull --ff-only
codex plugin marketplace add .
codex plugin add worldchat-arcade@arcade-shared
```

Preserve local changes. If the pull cannot fast-forward or conflicts with local work, stop and resolve that without resetting, cleaning, or overwriting files. Reload plugins through the host's supported mechanism (restart the desktop host if needed), then use a fresh chat and open a new game card. Version 0.3.6 includes the gameplay-only notification instructions.

## Multiplayer invitations

Playing a game does not enable background notifications. Rematch alerts are opt-in and require a host that supports MCP Events, currently a supported ChatGPT Work chat or dot. Ordinary chats and hosts without MCP Events can still play games; do not claim alerts are enabled there. Let Arcade's card and native host controls handle setup and authentication; keep gameplay chat focused on games and opponents.
