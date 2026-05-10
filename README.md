# kiro-recall

<p align="center">
  <img src="logo.svg" width="120" alt="kiro-recall logo" />
</p>

> Your knowledge. Your machine. Every session. Automatically.

A Kiro Power that forces your personal knowledge vault into every session before you type a single word. Wraps [@bitbonsai/mcpvault](https://github.com/bitbonsai/mcpvault) to inject relevant notes as ambient context, and captures new knowledge mid-session via `/recall`.

## What it does

Open a workspace in Kiro. Type your first prompt. Before it reaches the model, kiro-recall fires a hook, reads your personal knowledge vault from disk, and injects the relevant notes as context. You do nothing. It just happens.

No cloud calls to read your own notes. No data leaving your machine. Your vault is plain markdown files on your disk — readable by any text editor, not locked into any service.

## Install

1. Open Kiro → Powers panel → **Add power from GitHub**
2. Enter: `mikeartee/kiro-recall-power`
3. Open `mcp.json` and replace `YOUR_VAULT_PATH_HERE` with your vault path
   - Windows: `C:\\Users\\yourname\\vault`
   - macOS/Linux: `/Users/yourname/vault`
4. Restart Kiro or reconnect the MCP server from the MCP Server view
5. Run the **Vault Scaffold** hook once to create your folder structure
6. Your next session start hook fires automatically — vault context loads before your first prompt

**To make hooks fire in every workspace (recommended):** Copy the hook files from `.kiro/hooks/` to your user-level hooks directory:
- Windows: `C:\Users\{you}\.kiro\hooks\`
- macOS/Linux: `~/.kiro/hooks/`

Also add `mcpvault` to your user-level MCP config (`~/.kiro/settings/mcp.json`) using the server definition in `mcp.json`.

## What you get

| Hook | Trigger | What it does |
|------|---------|--------------|
| Session Start | Every first prompt | Reads vault, injects context before your first message |
| `/recall` | User triggered | Writes a structured note to `00-inbox/` |
| Vault Scaffold | User triggered | Creates the standard folder structure in a new vault |
| `/promote` | User triggered | Reformats an inbox note as a Zettelkasten permanent note |

## Vault structure (auto-scaffolded)

```
vault/
├── 00-inbox/          # Zero-friction capture — /recall writes here
├── 01-projects/       # Active project notes
├── 02-job-search/     # Applications and CV work
├── 03-learning/       # Course and certification notes
├── 04-knowledge/      # Permanent reference topics
├── 05-community/      # Community work
├── 06-permanent/      # Refined atomic Zettelkasten notes — loaded every session
└── 07-templates/      # Note templates
```

## Prerequisites

- Node.js 18+ (required to run the MCP server via npx)
- A folder to use as your vault (scaffolded automatically on first run)
- Obsidian is optional — only needed for visual graph browsing

## Why not just use steering files?

Steering files are passive. Kiro reads them if it feels like it. kiro-recall uses hooks — they fire whether Kiro wants to or not. Your context loads before the first prompt, every time.

## Source

Development repo: [github.com/mikeartee/kiro-recall](https://github.com/mikeartee/kiro-recall)

## Author

Mike Rewiri-Thorsen  
AWS Community Builder, AI Engineering, Class of 2026  
https://github.com/mikeartee
