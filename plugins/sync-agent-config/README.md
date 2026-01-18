# sync-agent-config

English | [日本語](README_ja.md)

A Claude Code plugin for synchronizing Agent configurations (MCP servers, skills) across different Agent tools.

## Overview

This project provides skills that enable you to synchronize configurations between different Agent environments such as Claude Code, VSCode, Claude Desktop, Codex, Cursor, Gemini CLI, and Antigravity.  
It reads the configuration from a source Agent tool and applies it to a target Agent tool, ensuring consistent settings across multiple development environments.  

### Included Skills

- **sync-mcp-config**: Synchronizes MCP server settings
- **sync-skill-config**: Synchronizes skill configurations

## Features

- **Cross-Platform Support**:
  Works on Windows, macOS, and Linux
- **Multi-Tool Compatibility**:
  Supports various Agent tools including:
  - Claude Code
  - VSCode
  - Claude Desktop
  - Codex CLI
  - Cursor
  - Gemini CLI
  - Antigravity
- **Safe Synchronization**:
  Creates backups and validates configurations before applying changes
- **Intelligent Handling**:
  Automatically handles format differences between different Agent tools
- **Web Search Integration**:
  Automatically searches for configuration specifications when documentation is not available

## Installation

### Installing to Claude Code

You can install the plugin directly from a GitHub repository to Claude Code.

1. Launch Claude Code

2. Run the following command to install the plugin:

Add this marketplace to Claude Code.  
Run the following command in the Claude Code console.  

```bash
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

Then, install the sync-agent-config plugin from the marketplace.  

```bash
/plugin install sync-agent-config@zv-plugins
```

3. Once installed, the skills will be available for use

## Usage

Simply tell your Agent to synchronize settings between tools:

**MCP configuration sync examples:**

- "I want to apply Claude Code's MCP settings to Codex"
- "Sync my MCP configuration from VSCode to Claude Desktop"
- "Copy MCP server settings from Claude Desktop to Claude Code"

**Skill configuration sync examples:**

- "Sync Claude Code's skill settings to Cursor"
- "Copy skill configuration from VSCode to Gemini CLI"

The skill will:

1. Verify your operating system environment
2. Read the source Agent tool's configuration
3. Check available settings
4. Apply the settings to the target Agent tool
5. Validate the configuration

## How It Works

1. **OS Environment Check**:
   Detects your operating system and sets appropriate paths
2. **Configuration Verification**:
   Reads and understands both source and target configuration formats
3. **Server Discovery**:
   Identifies all MCP servers registered in the source configuration
4. **Format Conversion**:
   Automatically converts settings to match the target tool's format
5. **Safe Application**:
   Backs up existing configurations before making changes
6. **Validation**:
   Ensures the new configuration is valid

## Configuration File Locations

The skill automatically detects configuration file paths based on your operating system and Agent tool.  
Reference documentation for each supported Agent tool is available in the `reference/` directory of each skill:

- MCP settings: [`skills/sync-mcp-config/reference/`](skills/sync-mcp-config/reference/)
- Skill settings: [`skills/sync-skill-config/reference/`](skills/sync-skill-config/reference/)

## About the Plugin

### File Layout

```txt
sync-agent-config/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/
│   ├── sync-mcp-config/     # MCP config sync skill
│   │   ├── SKILL.md         # Skill definition
│   │   └── reference/       # Configuration reference documentation
│   │       ├── antigravity.md
│   │       ├── claude_code.md
│   │       ├── claude_desktop.md
│   │       ├── codex_cli.md
│   │       ├── cursor.md
│   │       ├── gemini_cli.md
│   │       └── vscode.md
│   └── sync-skill-config/   # Skill config sync skill
│       ├── SKILL.md         # Skill definition
│       └── reference/       # Configuration reference documentation
│           ├── antigravity.md
│           ├── claude_code.md
│           ├── codex_cli.md
│           ├── cursor.md
│           ├── gemini_cli.md
│           └── vscode.md
├── LICENSE
├── README.md
└── README_ja.md
```

## Safety Features

- **Backup Creation**:
  Automatically backs up existing configurations before making changes
- **Conflict Detection**:
  Identifies when servers are already registered and asks for user confirmation
- **Validation**:
  Checks configuration file integrity after modifications
- **Read-Only Mode**:
  Only modifies MCP server settings, leaving other configurations untouched

## Error Handling

The skill handles various error scenarios:

- Missing source configuration files
- Write-protected target files
- Invalid configuration formats
- Incompatible settings between different Agent tools

## License

Licensed under the MIT License.  
See the `LICENSE` file for details.
