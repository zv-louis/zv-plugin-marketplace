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
├── LICENSE
├── README.md
├── README_ja.md
└── zv-marketplace.code-workspace
```

## Usage

### Adding the Marketplace

Run the following command in the Claude Code console to add this marketplace.  

```bash
/plugin marketplace add {URL of this repository}
# or
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

Once the marketplace is added, you can view its available plugins.  

```bash
/plugin
```

### Installing Plugins

Install plugins from the marketplace.

```bash
/plugin install {plugin-name}@zv-plugins
```

## Plugins

Each plugin is referenced from its own GitHub repository.  

- [madr-manager](https://github.com/zv-louis/madr-manager)
  Interactive MADR (Markdown Architectural Decision Records) manager. Helps create, list, and manage ADR files following the Structured MADR v4.0.0 format.
- [mktotp-mcp](https://github.com/zv-louis/mktotp)
  Interactive TOTP (Time-based One-Time Password) manager. Helps create, list, and manage TOTP secrets and generate one-time passwords.
- [updsts-mcp](https://github.com/zv-louis/updsts)
  Get and update AWS STS credential using existing AWS profile.

## License

MIT
