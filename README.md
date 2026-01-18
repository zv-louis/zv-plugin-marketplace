# ZV Plugin Marketplace

[日本語](README_ja.md) | English

Claude Code Plugin Marketplace

## Overview

This repository is a marketplace for distributing Claude Code plugins.
It contains information for installing plugins defined in each repository.

## Layout

```txt
./
├── .claude-plugin/
│   └── marketplace.json        # Marketplace catalog
├── README_ja.md
└── zv-marketplace.code-workspace
```

## Usage

### Adding the Marketplace

Add this marketplace to Claude Code.
Run the following command in the Claude Code console.

```bash
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

After adding the marketplace, you can view the plugins available in the marketplace.

```bash
/plugin marketplace list
```

### Installing Plugins

Select and install plugins from the marketplace.

Example of installing the zv-louis/sync-agent-config plugin

```bash
/plugin install sync-agent-config@zv-plugin-marketplace
```

## Plugins

- [sync-agent-config](https://github.com/zv-louis/sync-agent-config)
  A skill set for synchronizing Agent Skill/MCP settings across multiple agent tools.

## License

MIT
