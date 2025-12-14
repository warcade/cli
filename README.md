# webarcade-cli

CLI for [WebArcade](https://github.com/warcade/core) - Create and build native desktop app plugins.

## Installation

```bash
cargo install webarcade
```

## Quick Start

```bash
# Initialize a new project
webarcade init my-app
cd my-app

# Create a new plugin
webarcade new my-plugin

# Build the plugin
webarcade build my-plugin

# Run the app
webarcade run

# Package the app
webarcade package
```

## Commands

| Command | Description |
|---------|-------------|
| `webarcade init <name>` | Initialize a new WebArcade project |
| `webarcade new <plugin>` | Create a new plugin |
| `webarcade build <plugin>` | Build a plugin |
| `webarcade build --all` | Build all plugins |
| `webarcade list` | List available plugins |
| `webarcade run` | Build and run the app |
| `webarcade app` | Build production app with installer |
| `webarcade package` | Package app for distribution (interactive) |
| `webarcade install <user/repo>` | Install a plugin from GitHub |
| `webarcade update` | Update the CLI to latest version |

## Build Progress Display

When building plugins, the CLI shows a clean, professional progress display:

```
  ▶  Building Plugins
  ──────────────────────────────────────────────────

  ✓ hello-world      ● systemMonitor    ○ themes

  → systemMonitor: Compiling DLL...

  ━━━━━━━━━━━━━━━━━━────────────────────── 66% (2/3)
```

Features:
- Real-time status for each plugin (○ pending, ● building, ✓ complete, ✗ failed)
- Current build step displayed (Bundling frontend, Compiling DLL, etc.)
- Progress bar with percentage
- Clean summary on completion

## Updating the CLI

Check for updates and install the latest version:

```bash
webarcade update
```

This will:
- Show your current version
- Check crates.io for the latest version
- Prompt to install if an update is available

## Build Optimizations

The CLI includes smart build caching to speed up development:

### Incremental Plugin Builds

Plugins are only rebuilt when their source files change. The CLI tracks file hashes and skips unchanged plugins:

```bash
# Only rebuilds plugins that have changed
webarcade build --all

# Force rebuild all plugins (ignore cache)
webarcade build --all -f
```

### Build Flags

| Flag | Description |
|------|-------------|
| `-f, --force` | Force rebuild, ignoring cache |

### Package Flags

| Flag | Description |
|------|-------------|
| `--locked` | Embed plugins in binary (locked mode) |
| `--no-rebuild` | Only rebuild changed plugins (use cache) |
| `--skip-binary` | Skip frontend/binary rebuild (use existing) |
| `--skip-prompts` | Use current config without prompts |

### Common Workflows

```bash
# Full rebuild and package
webarcade package --locked

# Only 1 plugin changed, rebuild just that plugin
webarcade package --no-rebuild --locked

# Plugin changed, binary unchanged (unlocked mode only)
webarcade package --no-rebuild --skip-binary

# Quick repackage with no rebuilds
webarcade package --no-rebuild --skip-binary --skip-prompts
```

## Automatic Process Management

The CLI automatically terminates running app processes before building to prevent "file in use" errors. This happens automatically when you run:

- `webarcade build`
- `webarcade app`
- `webarcade package`

## Build Cache

Plugin build state is stored in `build/.build_cache.json`. The cache tracks:

- SHA-256 hash of all source files (`.rs`, `.jsx`, `.js`, `.ts`, `.tsx`, `.json`, `.toml`, `.css`, `.scss`)
- Build timestamp

Changes that trigger a rebuild:
- Any source file content change
- Adding/removing/renaming files
- Missing output file (`.dll`, `.js`)
- Using `--force` flag

Changes that don't trigger a rebuild:
- Lock file changes (`package-lock.json`, `Cargo.lock`)
- `node_modules/` or `target/` changes
- File timestamp changes without content changes

## License

MIT
