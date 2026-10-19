# Install Arcade

Instructions for a coding agent. Use the official hosted service; no local game server or developer credentials are needed.

1. Check for an existing Arcade connection and inspect `codex plugin marketplace list --json` when terminal/plugin support is available. If this repository's `arcade-shared` marketplace is registered as a local folder, follow **One-time migration** below. If it is already registered as the Git source `https://github.com/hoerl/arcade.git` tracking `main`, reuse it. Reuse other authorized Arcade connections; do not add a duplicate MCP connection.
2. For a new Codex installation with terminal and plugin support, register the Git-backed marketplace directly. No checkout is required. Requires Git and Codex with `codex plugin` support:

```sh
codex plugin marketplace add https://github.com/hoerl/arcade.git --ref main
codex plugin add worldchat-arcade@arcade-shared
```

3. Confirm that `arcade-shared` has `marketplaceSource.sourceType` equal to `git` and the official repository URL in `codex plugin marketplace list --json`, and that `worldchat-arcade@arcade-shared` is installed. Do not register `.` or a checkout directory as the source; local folders do not receive Git updates. Keep the source on the moving `main` branch, not a fixed commit or release tag.
4. Reload plugins through the host's supported mechanism after installation. If the desktop host does not pick up the change, restart it. In a fresh chat, read the live catalog, choose Rally when present (otherwise an available game), and call `arcade.play` with its exact ID. Confirm the real game opens inline.

If terminal/plugin installation is unavailable, do not attempt these commands through an unrelated tool. In ChatGPT, reuse an existing authorized Arcade connection if available. Otherwise explain that public ChatGPT installation is pending and offer [browser play](https://arcade.beautifulthings.org/?game=rally). This GitHub guide does not grant access to a private ChatGPT app.

## Rules

- The bundled connection uses `https://arcade.beautifulthings.org/mcp`.
- Do not install a second MCP or World ID plugin, start a local server, request secrets, or use sandbox World ID.
- Players verify inside Arcade when they choose **Play a Human**. Let the user complete verification. **Destroy a Bot** does not require World ID.
- If no game is specified, choose from the live catalog. Never generate a substitute game or claim that installation alone proves it launched.
- Test an Arcade mention in a fresh chat when possible. Report any missing host support, access, or unverified behavior plainly.
- Preserve the copyright and [MIT license](LICENSE.md) notices.

## Automatic updates

Codex Desktop checks configured Git marketplaces when its app server starts and refreshes installed plugin files. Future releases from `main` can therefore arrive without another install command or a manual `git pull`. Updates follow the host's refresh lifecycle; this is not a promise of immediate background updates while the app stays open. Restart the desktop host and use a fresh chat if it has been running since before a release. Hosts that do not run automatic marketplace refresh cannot be made automatic by this guide alone.

Server-side fixes apply on the next MCP request independently of package updates. The host manages the downloaded package; do not edit its cache or add a separate updater, startup hook, or scheduled job.

## One-time migration

Older versions of this guide registered a local checkout. An existing local registration cannot switch itself to GitHub remotely. Run this migration once, only when `arcade-shared` is still registered as a local source:

```sh
codex plugin marketplace remove arcade-shared
codex plugin marketplace add https://github.com/hoerl/arcade.git --ref main
codex plugin add worldchat-arcade@arcade-shared
```

Remove only this marketplace registration; do not uninstall Arcade, delete the old checkout, overwrite local changes, disconnect the player's account, or remove another marketplace. Keep the same `worldchat-arcade@arcade-shared` identity. If the source is managed by an administrator or the commands fail, preserve that configuration and report the failure rather than editing host files by hand. Verify the Git source as above, then reload the host and use a fresh chat. No per-release migration is needed afterward.

## Multiplayer invitations

Playing a game does not enable background notifications. Rematch alerts are opt-in and require a host that supports MCP Events, currently a supported ChatGPT Work chat or dot. Ordinary chats and hosts without MCP Events can still play games; do not claim alerts are enabled there. Let Arcade's card and native host controls handle setup and authentication; keep gameplay chat focused on games and opponents.
