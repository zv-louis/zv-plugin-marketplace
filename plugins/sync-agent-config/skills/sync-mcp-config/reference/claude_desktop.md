# Claude Desktop - MCP Configuration Information

## Configuration File Locations

Different locations depending on OS:

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

## File Format

JSON format

## Configuration Example

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/username/Desktop",
        "/Users/username/Downloads"
      ]
    },
    "custom-server": {
      "command": "python",
      "args": [
        "/path/to/server.py"
      ],
      "env": {
        "API_KEY": "your-api-key"
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
    - `env` (optional): Environment variables

## Project-Level Configuration

Claude Desktop does **NOT** support project-level MCP configuration. All MCP server settings are stored globally at the user level.

If you need project-specific MCP configurations, consider using Claude Code or VS Code which support workspace-level settings.

## Important Notes

After updating the `claude_desktop_config.json` settings, you must **restart Claude Desktop**.

## References

- [Getting Started with Local MCP Servers on Claude Desktop](https://support.claude.com/en/articles/10949351-getting-started-with-local-mcp-servers-on-claude-desktop)
- [Connect to local MCP servers - Model Context Protocol](https://modelcontextprotocol.io/docs/develop/connect-local-servers)
- [How to Setup Claude Code MCP Servers](https://claudelog.com/faqs/how-to-setup-claude-code-mcp-servers/)
- [How to Set Up Your First MCP Server with Claude Desktop](https://www.mcplist.ai/blog/setup-mcp-server-claude-desktop/)
