# Visual Studio Code - MCP Configuration Information

## Configuration File Locations

VS Code uses the **mcp.json** file to configure MCP servers.

### Global Settings (User-Level)

- **Windows**: `C:\Users\<username>\AppData\Roaming\Code\User\mcp.json`
- **macOS**: `/Users/<username>/Library/Application Support/Code/User/mcp.json`
- **Linux**: `~/.config/Code/User/mcp.json`

### Project-Level Settings (Workspace)

- **All OS**: `.vscode/mcp.json` (in project directory)

VS Code supports project-level MCP configuration. When a `.vscode/mcp.json` file exists in the project directory, workspace settings take priority over user settings. This allows teams to share MCP configurations through version control.

### Remote Settings

Configuration file for remote connections (Remote SSH, Containers, WSL, etc.)

## How to Access Configuration Files

### Via Command Palette

1. Open Command Palette with `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS)
2. Execute one of the following:
   - **`MCP: Open User Configuration`** - Open user settings
   - **`MCP: Open Workspace Folder Configuration`** - Open workspace settings
   - **`MCP: Add Server`** - Add a server (choose from NPM, PyPI, Docker)

## File Format

JSON format

## Basic Structure

```json
{
  "servers": {},
  "inputs": []
}
```

- **`servers`**: Define MCP servers and their configurations
- **`inputs`**: Placeholders for sensitive information like API keys

## Configuration Examples

### Basic stdio Server

```json
{
  "servers": {
    "memory": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-memory"
      ]
    },
    "filesystem": {
      "type": "stdio",
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
  "servers": {
    "github": {
      "type": "stdio",
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

### Configuration with Environment File

```json
{
  "servers": {
    "custom-server": {
      "type": "stdio",
      "command": "python",
      "args": ["/path/to/server.py"],
      "envFile": "/path/to/.env"
    }
  }
}
```

### Managing Sensitive Information with Input Variables

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "github-token",
      "description": "GitHub Personal Access Token",
      "password": true
    }
  ],
  "servers": {
    "github": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_TOKEN": "${input:github-token}"
      }
    }
  }
}
```

### HTTP/SSE Server (Remote)

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "api-key",
      "description": "API Key for remote server",
      "password": true
    }
  ],
  "servers": {
    "remote-server": {
      "type": "http",
      "url": "https://example.com/mcp",
      "headers": {
        "Authorization": "Bearer ${input:api-key}"
      }
    }
  }
}
```

### Azure MCP Server Configuration Example

```json
{
  "servers": {
    "Azure MCP Server": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@azure/mcp@latest",
        "server",
        "start"
      ]
    }
  }
}
```

## Configuration Items

### stdio Server (Local Execution)

- `type`: `"stdio"` (required)
- `command`: Command to execute (required) e.g., `"npx"`, `"python"`, `"node"`
- `args`: Array of command-line arguments (optional)
- `env`: Object of environment variables (optional)
- `envFile`: Path to environment variable file (optional)

### HTTP/SSE Server (Remote)

- `type`: `"http"` or `"sse"` (required)
- `url`: Server URL (required)
- `headers`: Object for authentication headers, etc. (optional)

### Input Variables (inputs)

- `type`: Input type (e.g., `"promptString"`)
- `id`: Unique identifier for the input variable
- `description`: Description displayed to the user
- `password`: If `true`, input is hidden and stored securely

## Important Notes

### Security

- MCP servers can execute arbitrary code, so **only add servers from trusted sources**
- Manage sensitive information (API keys, tokens, etc.) using input variables; do not hardcode them
- VS Code encrypts and securely stores input variable values

### Auto-Restart

- Enabling the `chat.mcp.autostart` setting will automatically restart MCP servers when settings change (experimental feature)

### Settings Priority

Workspace settings take priority over user settings.

## New Features in 2025

- **Input Variables**: Securely encrypt and store sensitive information
- **Environment File Support**: Reference `.env` files
- **Streamable HTTP**: Support for the latest MCP specification transport
- **Auto-Restart**: Automatic detection and restart on configuration changes

## References

- [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)
- [How to Set Up and Use VSCode MCP Server](https://medium.com/towards-agi/how-to-set-up-and-use-vscode-mcp-server-352c1e6f42e9)
- [Beyond the tools, adding MCP in VS Code](https://code.visualstudio.com/blogs/2025/05/12/agent-mode-meets-mcp)
- [MCP developer guide | Visual Studio Code Extension API](https://code.visualstudio.com/api/extension-guides/ai/mcp)
- [Setting Up Local MCP Servers in Visual Studio Code](https://medium.com/@johnnyorellana32/setting-up-local-mcp-servers-in-visual-studio-code-4f69220c9013)
- [Configure MCP Servers on VSCode, Cursor & Claude Desktop](https://spknowledge.com/2025/06/06/configure-mcp-servers-on-vscode-cursor-claude-desktop/)
