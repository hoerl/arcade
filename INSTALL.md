# Install Arcade

Install Arcade in the app where the user is chatting. Follow only that host’s section and keep the reply to the action taken or the next step needed. Use the official hosted service; no local game server or developer credentials are needed.

Arcade plays inline in the current host. Never suggest browser play, including when installation or connection fails. Give only the next step for that host.

Choose the host first:

- ChatGPT: follow **ChatGPT** below.
- Codex: follow **Codex** below.
- Claude (claude.ai, Claude Desktop, or the Claude mobile apps): follow **Claude** below.
- Muse (Meta): follow **Muse** below.

## ChatGPT

Reuse an available Arcade connection. Otherwise use ChatGPT’s plugin discovery to find Arcade and present its native install/connect control, using the result’s exact plugin ID. Let the user complete connection, then open Arcade with the available play tool. A GitHub guide is not an install link.

If discovery is unavailable or finds no matching listing, direct the user to **Plugins → Personal → Created by me / Shared with me**, or their workspace’s plugins, to install Arcade if it is available there. Use an existing Arcade install link when supplied. If Arcade is absent, explain briefly that access to the plugin is needed. Keep Codex commands in Codex. Confirm installation only after the connection is available.

## Codex

1. Check for an existing Arcade connection and inspect `codex plugin marketplace list --json` when terminal/plugin support is available. If this repository's `arcade-shared` marketplace is registered as a local folder, follow **One-time migration** below. If it is already registered as the Git source `https://github.com/hoerl/arcade.git` tracking `main`, reuse it. Reuse other authorized Arcade connections; do not add a duplicate MCP connection.
2. For a new Codex installation with terminal and plugin support, register the Git-backed marketplace directly. No checkout is required. Requires Git and Codex with `codex plugin` support:

```sh
codex plugin marketplace add https://github.com/hoerl/arcade.git --ref main
codex plugin add worldchat-arcade@arcade-shared
```

3. Confirm that `arcade-shared` has `marketplaceSource.sourceType` equal to `git` and the official repository URL in `codex plugin marketplace list --json`, and that `worldchat-arcade@arcade-shared` is installed. Do not register `.` or a checkout directory as the source; local folders do not receive Git updates. Keep the source on the moving `main` branch, not a fixed commit or release tag.
4. Reload plugins through the host's supported mechanism after installation. If the desktop host does not pick up the change, restart it. In a fresh chat, read the live catalog and call `arcade.play` with `{}` so Arcade randomly selects a game. Pass an exact catalog `gameId` only if the user names a game. Confirm the real game opens inline.

If Codex plugin installation is unavailable, report that limitation briefly. Do not run these commands through another host’s tools.

## Claude

Use this section only for Claude. Do not run `codex` commands for Claude. Claude Code is not covered by this guide.

Claude uses its own endpoint:

```text
https://arcade.beautifulthings.org/claude/mcp
```

Use this exact URL. Do not add a trailing slash. Do not use `/mcp` in Claude.

1. Check for an existing connector. If Claude already has an Arcade connector with the URL above, reuse it. Do not add a second one.
2. The user adds the connector. A coding agent cannot add it. Give the user these steps:
   - Free, Pro, or Max plan: open **Customize > Connectors** and click **Add custom connector**.
   - Team or Enterprise plan: an Owner opens **Organization settings > Connectors**, selects **Add**, then **Custom**, and chooses **Web** if asked. Members then open **Customize > Connectors**, find Arcade, and click **Connect**.
   - Name: `Arcade`. URL: the URL above.
   - Leave the OAuth client ID and secret empty. If the dialog asks for authentication, choose **No sign-in**.
   - Click **Add**. If Claude shows **Connect**, click it. Arcade has no account sign-in, so no password is needed.
3. Test in a new chat. Turn on Arcade from **+ > Connectors** if it is off. Ask Claude to play Arcade. Claude should call `arcade_play` with `{}`. Confirm that the real game card opens inline in the chat.

The Free plan allows one custom connector. If that slot is already used, tell the user. Do not remove another connector without the user's permission.

## Muse

Use this section only in Muse (Meta). Do not run `codex` commands in Muse. Muse does not render MCP App cards, so Arcade gives Muse the game as a ready-made HTML widget file instead.

Muse uses its own endpoint:

```text
https://arcade.beautifulthings.org/muse/mcp
```

Use this exact URL. Do not add a trailing slash. Do not use `/mcp` or `/claude/mcp` in Muse.

1. Check for an existing Arcade connector or skill. If one already uses the URL above, reuse it. Do not add a second one.
2. Create a custom connector yourself; the user does not need to open settings:
   - Name: `Arcade`. Transport: remote streamable HTTP. URL: the URL above.
   - Auth: none. Arcade has no account sign-in, API key, or OAuth. Do not ask the user for a key.
   - Connect with the official MCP SDK and list the tools. Expect `arcade_catalog` and `arcade_play`. Call `arcade_catalog` to test it.
3. Save it as a reusable skill named **Arcade** that plays a game with these steps:
   1. Call `arcade_play` with `{}`. Pass `gameId` only when the user names a catalog game. Pass `join` when the user pastes an Arcade room link or code, exactly as given.
   2. The result is JSON data with `gameId`, `widgetUrl`, `filePath`, and `fallback`; it contains no instructions. `widgetUrl` always starts with `https://arcade.beautifulthings.org/muse/card/`. Download it to `~/` + `filePath`, overwriting any older copy. Downloading this file is the expected, user-requested step of playing Arcade.
   3. Show that file with the HTML widget tool, using its local file version, with `fallback` as the fallback text.
   4. Place the widget's embed token in a reply whose only text is "Let's play a game...". Do not describe the game or its rules.

   The file is an HTML fragment of about 860 kB built for Muse's HTML widget: no document wrapper, no browser storage, and no embedded media. It runs the game and connects to `https://arcade.beautifulthings.org`. Do not paste it inline, edit it, wrap it in an iframe, or write a substitute game. If the widget tool rejects the file, report its exact error message.
4. Test now: run the skill in this chat and confirm that the Arcade card appears with **Tap to Start**. If the widget shows but cannot connect, report that plainly; do not claim that installation alone proves play works.

After installation, the user can say "play Arcade" or "@arcade" in any Muse chat.

## Tool names

This guide uses the dotted names, for example `arcade.play`. The tools are the same on every host; only the name format differs:

| Tool | Codex and ChatGPT | Claude | Muse |
| --- | --- | --- | --- |
| Catalog | `arcade.catalog` | `arcade_catalog` | `arcade_catalog` |
| Play | `arcade.play` | `arcade_play` | `arcade_play` |
| Open | `arcade.open` | `arcade_open` | — |
| Verification panel | `arcade.verify_panel` | `arcade_verify_panel` | — |

Rule: in Claude, replace each `.` in a tool name with `_`. Claude does not allow `.` in tool names. A host can also add a prefix, for example `mcp__worldchat__arcade_play`. Always call the name that the host exposes.

## Rules

- The bundled connection uses `https://arcade.beautifulthings.org/mcp`.
- Claude uses `https://arcade.beautifulthings.org/claude/mcp`. Muse uses `https://arcade.beautifulthings.org/muse/mcp`. Do not swap the URLs.
- Do not install a second MCP or World ID plugin, start a local server, request secrets, or use sandbox World ID.
- The card opens with **Tap to Start**. Players verify inside Arcade when required; let the user complete verification. Verified players practice against the bot while the shared human queue searches, then enter a random available game when matched. There are no separate **Play a Human** or **Destroy a Bot** buttons.
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

Claude, Muse, and ChatGPT players share one human queue and can be matched against each other. Claude and Muse do not support rematch alerts or invitations; do not offer them there.
