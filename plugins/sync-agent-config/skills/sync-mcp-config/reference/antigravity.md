# Antigravity - MCP Configuration Information

## Configuration File Locations

### Global Settings

- **Windows**: `C:\Users\<USER_NAME>\.gemini\antigravity\mcp_config.json`
- **Other OS**: `~/.gemini/antigravity/mcp_config.json` (estimated)

### Project-Level Settings

Antigravity does **NOT** currently support project-level MCP configuration. All MCP server settings are stored globally at the user level.

Per-workspace MCP configuration is a [requested feature](https://discuss.ai.google.dev/t/support-for-per-workspace-mcp-config-on-antigravity/111952) that may be added in future updates.

## How to Access Configuration File

1. Select "Manage MCP Servers" at the top of the MCP Store
2. Click "View raw config" in the main tab to edit `mcp_config.json`

Or

1. Open the agent pane on the right side of the workspace
2. Click the ellipsis (…)
3. Select "MCP Servers" from the dropdown

## File Format

JSON format

## Configuration Example

```json
{
  "mcpServers": {
    "firebase-mcp-server": {
      "command": "npx",
      "args": [
        "-y",
        "firebase-tools@latest",
        "mcp"
      ]
    },
    "custom-server": {
      "command": "node",
      "args": [
        "/path/to/server.js"
      ],
      "env": {
        "API_KEY": "your-api-key",
        "DEBUG": "true"
      }
    }
  }
}
```

## Configuration Items

- `mcpServers`: Object containing MCP server configurations
  - `<server-name>`: Unique identifier for each server
    - `command`: Command to execute
    - `args`: Array of command-line arguments
    - `env` (optional): Environment variables for the server

## References

- [Antigravity Editor: MCP Integration](https://antigravity.google/docs/mcp)
- [How to connect MCP servers with Google Antigravity](https://composio.dev/blog/howto-mcp-antigravity)
- [Google Antigravity: How to add custom MCP server](https://medium.com/google-developer-experts/google-antigravity-custom-mcp-server-integration-to-improve-vibe-coding-f92ddbc1c22d)
- [Quickstart (AntiGravity) - Augment](https://docs.augmentcode.com/context-services/mcp/quickstart-anti-gravity)
