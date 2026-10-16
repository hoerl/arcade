# Install Arcade

Instructions for a coding agent. Use the official hosted service; no local game server or developer credentials are needed.

1. Check for an existing Arcade connection. If `arcade.catalog` and `arcade.play` are available, reuse it and skip installation.
2. In Codex with terminal access and plugin support, run the commands below. Reuse an existing checkout when possible; preserve local changes. Requires Git and Codex with `codex plugin` support. Refresh the plugin through the host's supported mechanism after installation.
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

To update an existing checkout: pull without overwriting local changes, rerun `codex plugin add worldchat-arcade@arcade-shared`, and refresh the connection. Open a new game card.
