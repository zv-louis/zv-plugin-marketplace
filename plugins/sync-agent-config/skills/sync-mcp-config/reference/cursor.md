# Cursor - MCP Configuration Information

## Overview

Cursor is an AI-powered code editor built on VS Code. It supports MCP (Model Context Protocol) servers for extending AI capabilities. Cursor uses a similar configuration structure to VS Code but with Cursor-specific paths.

## Configuration File Locations

Cursor uses the **mcp.json** file to configure MCP servers.

### Global Settings (User-Level)

- **Windows**: `%APPDATA%\Cursor\User\mcp.json`
- **macOS**: `~/Library/Application Support/Cursor/User/mcp.json`
- **Linux**: `~/.config/Cursor/User/mcp.json`

### Project-Level Settings (Workspace)

- **All OS**: `.cursor/mcp.json` (in project directory)

Cursor supports project-level MCP configuration. When a `.cursor/mcp.json` file exists in the project directory, workspace settings take priority over user settings. This allows teams to share MCP configurations through version control.

## How to Access Configuration Files

### Via Cursor Settings

1. Open Cursor Settings with `Ctrl+,` (Windows/Linux) or `Cmd+,` (macOS)
2. Navigate to the MCP section
3. Click on "Edit in mcp.json" or similar option

### Via Command Palette

1. Open Command Palette with `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS)
2. Search for MCP-related commands

## File Format

JSON format

## Basic Structure

```json
{
  "mcpServers": {
    "server-name": {
      "command": "command",
      "args": [],
      "env": {}
    }
  }
}
```

## Configuration Examples

### Basic stdio Server

```json
{
  "mcpServers": {
    "memory": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-memory"
      ]
    },
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/path/to/directory"
      ]
    }
  }
}
```

### Configuration with Environment Variables

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```

### Python-based MCP Server

```json
{
  "mcpServers": {
    "custom-server": {
      "command": "python",
      "args": ["/path/to/server.py"],
      "env": {
        "API_KEY": "your-api-key"
      }
    }
  }
}
```

### SSE Server (Remote)

```json
{
  "mcpServers": {
    "remote-server": {
      "url": "https://example.com/mcp/sse",
      "env": {
        "API_KEY": "your-api-key"
      }
    }
  }
}
```

## Configuration Items

### stdio Server (Local Execution)

- `command`: Command to execute (required) e.g., `"npx"`, `"python"`, `"node"`
- `args`: Array of command-line arguments (optional)
- `env`: Object of environment variables (optional)

### SSE Server (Remote)

- `url`: Server URL (required)
- `env`: Object for environment variables including authentication (optional)

## Format Conversion Notes

When converting from VS Code format:

| VS Code                         | Cursor                                  |
| ------------------------------- | --------------------------------------- |
| `servers`                       | `mcpServers`                            |
| `type: "stdio"`                 | (implicit, no type field needed)        |
| `.vscode/mcp.json`              | `.cursor/mcp.json`                      |
| User `mcp.json` path            | Cursor User `mcp.json` path             |

When converting from Claude Code format:

| Claude Code                     | Cursor                                  |
| ------------------------------- | --------------------------------------- |
| `mcpServers`                    | `mcpServers` (same structure)           |
| `~/.claude.json`                | `%APPDATA%\Cursor\User\mcp.json`        |
| `.mcp.json`                     | `.cursor/mcp.json`                      |

## Important Notes

### Compatibility with VS Code

- Cursor is based on VS Code, so many configurations are similar
- However, configuration file paths are Cursor-specific
- Some VS Code MCP features may not be available in Cursor

### Security

- MCP servers can execute arbitrary code, so **only add servers from trusted sources**
- Store sensitive information (API keys, tokens) securely
- Consider using environment variables from secure sources

### Settings Priority

Workspace settings (`.cursor/mcp.json`) take priority over user settings.

## References

- [Cursor Documentation](https://cursor.sh/docs)
- [Cursor MCP Configuration](https://docs.cursor.com/context/model-context-protocol)
- [Configure MCP Servers on VSCode, Cursor & Claude Desktop](https://spknowledge.com/2025/06/06/configure-mcp-servers-on-vscode-cursor-claude-desktop/)
