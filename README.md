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
├── plugins/
│   ├── sync-agent-config/
│   └── jp-cover-letter-creator/
├── README_ja.md
└── zv-marketplace.code-workspace
```

## Usage

### Adding the Marketplace

Add this marketplace to Claude Code.  
Run the following command in the Claude Code console.  

```bash
# Example of adding zv-louis/zv-plugin-marketplace to the marketplace
/plugin marketplace add zv-louis/zv-plugin-marketplace
# or
/plugin marketplace add {URL of this repository}
```

After adding the marketplace, you can view the plugins available in the marketplace.  

```bash
/plugin marketplace list
```

### Installing Plugins

Select and install plugins from the marketplace.  

Example of installing the zv-louis/sync-agent-config plugin:  

```bash
/plugin install sync-agent-config@zv-plugins
```

## Plugins

- [sync-agent-config](plugins/sync-agent-config)  
  A skill set for synchronizing Agent configurations (MCP servers, skills) across different Agent tools.  
- [jp-cover-letter-creator](plugins/jp-cover-letter-creator)  
  Interactive Japanese business cover letter creator with markdown preview and Word document (docx) export.  

## License

MIT
