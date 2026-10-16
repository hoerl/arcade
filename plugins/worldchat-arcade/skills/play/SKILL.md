---
name: play
description: Launch an actual Arcade catalog game inline when the user mentions @arcade (including a bare mention), asks Arcade to play, or names an Arcade game. Choose a game when none is specified. Never invent a substitute game. Do not use for requests to develop or edit Arcade.
---

# Arcade

An Arcade mention is a request to launch a game, not a request for a game-selection conversation. Use the connected Arcade tools to open its real inline card.

## Invocation contract

Do not answer a play request before calling the launch tool. A plugin mention is already authorization to open its game; never ask for confirmation. In this host, `arcade.catalog` and `arcade.play` may be exposed as `mcp__worldchat__arcade_catalog` and `mcp__worldchat__arcade_play`. The registered connection may instead expose these under the Arcade MCP app namespace. Use the actual exposed names belonging to Arcade’s connected app. If necessary discover them through the host tool registry.

Examples:
- `@arcade` or `@arcade start a game`: read the catalog, choose a supported game, call the play tool.
- `@arcade rally`: read the catalog, call the play tool with `{"gameId":"rally"}`. Rally is paddle arcade, never racing.
- `yes` after a mistaken racing description: correct it by launching the real catalog game, without another question.

A successful launch must come from the tool's inline UI resource. Text such as “ready to race,” a generated game, or instructions to tap the plugin do not fulfill the request.

## Choose and launch

1. Call `arcade.catalog` to get the currently available games. The live catalog is authoritative; do not use remembered prototypes or infer rules from a game's name.
2. If the user names an available game, use its exact catalog ID. If no game is specified, choose Rally when present, otherwise the first listed game supported by `arcade.play`. Do not ask which game they want or whether to launch it. If a requested game is unavailable, briefly say so and choose an available catalog game instead.
3. Call `arcade.play` with that `gameId` once to render the game inline in this conversation. For Rally, `arcade.open` is an equivalent launch if `arcade.play` is unavailable. A catalog listing or a prose reply alone does not open a game.
4. Let the player interact with the card. Omit accompanying prose or use one short factual sentence. Do not send the user to a browser, side panel, plugin picker, or another chat to start playing.

Rally is **Classic paddle arcade**: two paddles and a ball. It is not a racing game. Describe any game only using its catalog entry and actual tool results.

## No substitutes

Never invent a game, rules, scores, opponents, or a running match. Never generate HTML, a canvas, an artifact, a visualization, or a text adventure as a replacement for the Arcade tool's UI. This applies even if the user says “yes,” “start,” or “go” after an earlier mistaken description: correct the misunderstanding and launch the catalog game.

If tools are not initially exposed, use the host's available tool-discovery capability to find Arcade's catalog and launch tools. If they remain unavailable, the catalog is empty, a call errors, or the selected game cannot be launched, state that Arcade could not open. Do not claim success or build a substitute. Stop the launch attempt rather than repeatedly retrying.

## Player controls and unrelated work

The card offers a labelled bot, World ID verification, and real human matchmaking. Do not claim a human partner is ready or the player is verified unless the service confirms it. World ID connection starts when the player chooses it in the card and may expand into the host panel for a QR code; never collect credentials or simulate verification.

Play does not require, delay, or stop with agent work. Do not call `arcade.offer` or `arcade.activity` to unlock play. Continue unrelated work normally. Requests to list games should return the live catalog without launching; requests to build or modify Arcade are development tasks, not play requests.
