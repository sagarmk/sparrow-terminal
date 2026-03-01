# Sparrow Plugins

Sidebar plugins that run alongside your terminal. Each plugin is a folder in `~/.sparrow/plugins/` with at least two files: `plugin.json` and `panel.html`.

## Quick Start

```bash
# Copy the template to your plugins directory
cp -r plugin-template ~/.sparrow/plugins/my-plugin
# Restart Sparrow — your plugin appears in the sidebar
```

## Plugin Structure

```
~/.sparrow/plugins/
  my-plugin/
    plugin.json      # manifest (required)
    panel.html       # sidebar UI (required)
    main.js          # main-process code (optional)
```

## plugin.json

| Field | Required | Description |
|-------|----------|-------------|
| `name` | yes | Unique identifier (folder name) |
| `displayName` | yes | Label shown in the sidebar |
| `version` | yes | Semver version |
| `description` | no | Short description |
| `iconSvg` | no | Inline SVG for the sidebar icon |
| `defaultWidth` | no | Initial panel width in pixels (default: 300) |
| `minWidth` | no | Minimum resize width (default: 200) |
| `placement` | no | `"left"` or `"right"` (default: `"left"`) |
| `keybinding` | no | Keyboard shortcut to toggle the panel (e.g. `"Meta+Shift+p"`) |

## SparrowBridge API

The bridge is injected into `panel.html` automatically — no imports needed.

| Method | Returns | Description |
|--------|---------|-------------|
| `SparrowBridge.getCwd()` | `Promise<string>` | Working directory of the active pane |
| `SparrowBridge.onCwdChange(cb)` | `function` (unsubscribe) | Called when the active pane's cwd changes |
| `SparrowBridge.readFile(path)` | `Promise<string>` | Read a file from disk |
| `SparrowBridge.writeFile(path, content)` | `Promise<boolean>` | Write a file to disk |
| `SparrowBridge.git.getStatus(cwd)` | `Promise<object>` | Git status (branch, isDirty, isRepo) |
| `SparrowBridge.git.listBranches(cwd)` | `Promise<array>` | List git branches |
| `SparrowBridge.close()` | — | Close the plugin panel |
| `SparrowBridge.theme` | `object` | Current theme colors (`background`, `text`, `textMuted`, `border`, `accent`) |

## Examples

- **`plugin-template/`** — Minimal starter with theme colors, cwd tracking, and git status
- **`examples/mcp-guide/`** — MCP tools reference panel (the built-in guide plugin)
