<p align="center">
  <img src="docs/assets/icon.png" width="128" height="128" alt="Sparrow">
</p>

<h1 align="center">Sparrow</h1>

<p align="center">
  A terminal designed for AI agents.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-1.6.3--beta-blue" alt="Version 1.6.3-beta">
  <img src="https://img.shields.io/badge/platform-macOS%20(Apple%20Silicon)-lightgrey" alt="macOS Apple Silicon">
  <img src="https://img.shields.io/badge/status-beta-orange" alt="Beta">
</p>

<p align="center">
  <a href="#install">Install</a> &middot;
  <a href="#features">Features</a> &middot;
  <a href="#mcp-server">MCP Server</a> &middot;
  <a href="#plugins">Plugins</a> &middot;
  <a href="#keyboard-shortcuts">Shortcuts</a>
</p>

---

> **Beta Release** — Some features are still under active development. Please report any issues you encounter.

**What makes Sparrow different?** Most terminals don't have a full git workflow (staging, shelving, cherry pick), a file explorer with inline diffs, clipboard history with snippets, or an MCP server that lets AI agents drive your terminal. Sparrow has all of these built in.

## Install

### Homebrew (recommended)

```bash
brew install sagarmk/sparrow/sparrow-terminal
```

### Manual download

1. [**Download sparrow-1.6.3-beta-arm64.dmg**](https://github.com/sagarmk/sparrow-terminal/releases/latest/download/sparrow-1.6.3-beta-arm64.dmg)
2. Open the `.dmg` and drag **Sparrow** to your Applications folder
3. Launch Sparrow from your Applications folder

This build is **signed and notarized by Apple** — it opens instantly with no Gatekeeper warnings and no `xattr` workarounds needed.

> Requires **macOS 12** (Monterey) or later. Apple Silicon (arm64) only.

---

## Features

### AI Agent Control via MCP

Let Claude Code, Gemini CLI, or any MCP-compatible agent control your terminal — create panes, run commands, capture output, and take screenshots.

https://github.com/user-attachments/assets/sparrow-mcp-demo.mov

### File Explorer & Diff

Browse your project, create files and folders, review inline diffs, and revert unwanted changes — all without leaving the terminal.

<p align="center">
  <img src="docs/assets/sparrow file explorer and updated file diff.png" width="800" alt="File explorer with inline diff view">
</p>

### Git Graph — Shelve, Stage, Cherry Pick

Full git graph with staging, shelving working changes, cherry picking hunks from any commit, and inline commit.

<p align="center">
  <img src="docs/assets/sparrow git shelve and cherry pick working changes.png" width="800" alt="Git graph with shelving and cherry pick">
</p>

### Tab Groups & Clipboard

Color-coded tab groups for terminals and file tabs. Clipboard history with pinning. Reusable command snippets with parameters.

<p align="center">
  <img src="docs/assets/sparrow tab grouping and clipboard.png" width="800" alt="Tab groups, clipboard history, and command snippets">
</p>

### Voice Input

Speak commands instead of typing — hold `Cmd+Shift+Space` or the mic button in the title bar. Native macOS speech recognition runs on-device with no cloud APIs. A live transcript appears as you speak, and the text is written to the terminal at your cursor when you release.

### Everything Else

| Feature | |
|---|---|
| **Split Panes** | Vertical and horizontal splits — work in multiple terminals side by side |
| **Tabs** | Dynamic titles that reflect the running process and working directory |
| **Session Restore** | Tabs, panes, and working directories are saved and restored on relaunch |
| **Broadcast Input** | Type once, send to every pane — great for multi-server commands |
| **GIF Recording** | Record terminal sessions as animated GIFs with one click |
| **5 Themes** | Dracula (default), Nord, Monokai, Dark, and Light |
| **Notifications** | Desktop alerts when a long-running command finishes |
| **Quick Select** | Regex-based selection of URLs, paths, IPs, and hashes from terminal output |
| **Deep Linking** | `sparrow://open?path=/your/dir` opens a terminal at that directory |
| **Finder Integration** | Drag a folder to the dock icon or use `open -a Sparrow /path` |
| **SSH Profiles** | Saved connections with host, user, port, identity file, and jump host |
| **Command Palette** | `Cmd+Shift+R` — fuzzy search with sub-completions and `/pane`, `/branch`, `/worktree` flags |

---

## MCP Server

The **Sparrow MCP Server** lets AI coding agents (Claude Code, Gemini CLI, etc.) interact with your terminal — no separate install needed, it ships inside the app.

### Add to Claude Code

Edit `~/.claude/settings.json`:

```json
{
  "mcpServers": {
    "sparrow": {
      "command": "node",
      "args": ["/Applications/sparrow.app/Contents/Resources/mcp-server/dist/index.js"],
      "env": { "SPARROW_PANE_ID": "" }
    }
  }
}
```

### Add to Gemini CLI

Edit `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "sparrow": {
      "command": "node",
      "args": ["/Applications/sparrow.app/Contents/Resources/mcp-server/dist/index.js"],
      "env": { "SPARROW_PANE_ID": "" }
    }
  }
}
```

> `SPARROW_PANE_ID` is set automatically when launching agents from within Sparrow.

### Tools

| Tool | Description |
|------|-------------|
| `sparrow_create_pane` | Open a new terminal pane with an optional command |
| `sparrow_close_pane` | Close a terminal pane |
| `sparrow_rename_pane` | Rename a pane's tab label |
| `sparrow_write_to_pane` | Type text or send signals (Ctrl-C, kill) to a pane |
| `sparrow_run_command` | Run a command and capture its output (ANSI-stripped) |
| `sparrow_screenshot` | Capture a PNG screenshot of a pane |
| `sparrow_notify` | Send a desktop notification |
| `sparrow_clipboard` | Read or write the system clipboard |

### Resources

| URI | Description |
|-----|-------------|
| `sparrow://context` | Your current pane ID and Sparrow environment |
| `sparrow://panes` | All open panes — IDs, names, working directories |
| `sparrow://panes/{id}/output` | Recent terminal output from a pane (last 200 lines) |

### Token Stats Hooks

Track token usage from Claude Code and Gemini CLI directly in your terminal tab headers. Hook scripts are bundled at `/Applications/sparrow.app/Contents/Resources/mcp-server/hooks/`.

---

## Plugins

Sparrow supports sidebar plugins — custom panels that run alongside your terminal. See [`plugins/`](plugins/) for templates, examples, and the full SparrowBridge API reference.

```bash
# Quick start — copy the template
cp -r plugins/plugin-template ~/.sparrow/plugins/my-plugin
# Restart Sparrow — your plugin appears in the sidebar
```

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd+T` | New terminal |
| `Cmd+W` | Close pane |
| `Cmd+D` | Search selected text |
| `Cmd+Shift+D` | Split pane |
| `Cmd+F` | Search in terminal |
| `Cmd+,` | Settings |
| `Cmd+B` | File browser |
| `Cmd+G` | Git panel |
| `Cmd+Shift+V` | Clipboard history |
| `Cmd+Shift+R` | Command palette |
| `Cmd+Shift+B` | Broadcast input |
| `Cmd+Shift+H` | Quick select |
| `Cmd+Shift+Space` | Voice input (hold to speak) |
| `Esc` | Close overlay |

## Repository Structure

```
docs/           Website (GitHub Pages, served from /docs)
homebrew/       Homebrew cask formula (brew install sagarmk/sparrow/sparrow-terminal)
plugins/        Plugin templates, examples, and SparrowBridge API docs
LICENSE         Proprietary license
```

## Requirements

- macOS 12 (Monterey) or later
- Apple Silicon (arm64)

## License

Sparrow is proprietary software by Spriggan AI Inc. Free to download and use — not for modification or redistribution. See [LICENSE](LICENSE) for full terms.
