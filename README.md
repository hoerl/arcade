# Arcade

**Play games together.**

Multiplayer games inside ChatGPT and Claude. Connect your World ID and play with real people, on either app. Warm up against a bot while waiting for a human.

## Install

Paste this into your coding agent:

```text
Read https://raw.githubusercontent.com/hoerl/arcade/main/INSTALL.md and install Arcade.
```

The guide installs the hosted MCP plugin from a Git-backed marketplace. Codex Desktop checks for package updates at app-server startup, so users do not need to rerun install commands for each release. Existing local-checkout installs need the guide's one-time migration. Public ChatGPT installation is coming soon.

In Claude, add a custom connector with this URL (the install guide has the steps):

```text
https://arcade.beautifulthings.org/claude/mcp
```

Rematch alerts are opt-in and require MCP Events in a supported ChatGPT Work chat or dot; installation alone does not enable notifications. Claude has no rematch alerts.

## Play

Mention **@Arcade** in a supported chat, ask Claude to play Arcade, or [play in your browser](https://arcade.beautifulthings.org/?game=rally). Select **Tap to Start** and verify with World ID when required. Practice against the bot while Arcade looks for another human. No separate World ID plugin needed.

**Rally** — Classic paddle arcade.

Licensed under [MIT](LICENSE.md).

[hello@beautifulthings.org](mailto:hello@beautifulthings.org)
