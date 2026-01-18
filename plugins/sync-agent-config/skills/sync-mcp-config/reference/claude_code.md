# Claude Code - MCP Configuration Information

## Configuration File Locations

Claude Code uses multiple configuration files hierarchically.

- **Main Global Settings**: `~/.claude.json`
- **User Global Settings**: `~/.claude/settings.json`
- **User Local Settings**: `~/.claude/settings.local.json`
- **Project-Specific Settings**: `.claude/settings.local.json` (in project directory)
- **Project MCP Settings**: `.mcp.json` (in project directory)

## Important Notes

Only the following files are recognized as MCP server settings:
- The `.claude.json` file in the home directory (`~/.claude.json`)
- The local `.mcp.json` file in the project directory

**Note**: Settings in the `~/.claude/settings.json` file are NOT applied to MCP servers.

## Settings Priority

Settings are applied in order of specificity:
Project-specific → User Local → User Global → Main Global

More specific settings override broader settings.

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
        "/path/to/directory"
      ],
      "env": {
        "ENV_VAR": "value"
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

## References

- [Claude Code Settings Documentation](https://code.claude.com/docs/en/settings)
- [Configuring MCP Tools in Claude Code - The Better Way](https://scottspence.com/posts/configuring-mcp-tools-in-claude-code)
- [Add MCP Servers to Claude Code - Setup & Configuration Guide](https://mcpcat.io/guides/adding-an-mcp-server-to-claude-code/)
- [Where Are Claude Code Global Settings Files Located](https://claudelog.com/faqs/where-are-claude-code-global-settings/)
