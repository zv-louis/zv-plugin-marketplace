# ZV Plugin Marketplace

English | [日本語](README_ja.md)

Claude Code Plugin Marketplace

## Overview

This repository is a marketplace for distributing Claude Code plugins.  
It contains information for installing plugins defined in each repository.  

## Layout

```txt
./
├── .claude-plugin/
│   └── marketplace.json        # Marketplace catalog
├── plugins/
│   ├── jp-cover-letter-creator/
│   ├── madr-manager/
│   └── sync-agent-config/
├── LICENSE
├── README.md
├── README_ja.md
└── zv-marketplace.code-workspace
```

## Usage

### Adding the Marketplace

Add this marketplace to Claude Code.  
Run the following command in the Claude Code console.  

```bash
/plugin marketplace add {URL of this repository}
# or
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

After adding the marketplace, you can view the plugins available in the marketplace.  

```bash
/plugin marketplace list
```

### Installing Plugins

Install plugins from the marketplace.

```bash
/plugin install {plugin-name}@zv-plugins
```

## Plugins

- [jp-cover-letter-creator](plugins/jp-cover-letter-creator)
  Interactive Japanese business cover letter creator with markdown preview and Word document (docx) export.
- [madr-manager](plugins/madr-manager)
  Interactive MADR (Markdown Architectural Decision Records) manager. Helps create, list, and manage ADR files following the Structured MADR v4.0.0 format.
- [sync-agent-config](plugins/sync-agent-config)
  A skill set for synchronizing Agent configurations (MCP servers, skills) across different Agent tools.

## License

MIT
