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
| `webarcade package` | Package app for distribution |

## License

MIT
