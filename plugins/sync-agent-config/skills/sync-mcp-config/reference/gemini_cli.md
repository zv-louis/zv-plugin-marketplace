# Gemini CLI - MCP Configuration Information

## Configuration File Locations

### Global Settings

- **All OS**: `~/.gemini/settings.json`

### Project-Level Settings

- **Project Directory**: `.gemini/settings.json` (in project directory)
- **Firebase Studio Interactive Chat**: `.idx/mcp.json`

Gemini CLI supports project-level MCP configuration. When a `.gemini/settings.json` file exists in the project directory, it takes precedence over the global settings.

## File Format

JSON format

## Configuration Example

```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-git"
      ]
    },
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    },
    "remote-server": {
      "httpUrl": "https://example.com/mcp",
      "headers": {
        "Authorization": "Bearer token"
      }
    }
  }
}
```

## Configuration Items

- `mcpServers`: Object containing MCP server configurations
  - `<server-name>`: Unique identifier for each server
    - `command`: Command to execute local server
    - `args`: Array of command-line arguments
    - `httpUrl`: URL of remote MCP server
    - `url`: Alternative remote server URL
    - `env` (optional): Environment variables
    - `headers` (optional): HTTP request headers

## Important Notes

- At least one of `command`, `url`, or `httpUrl` must be specified
- Priority when multiple are specified: `httpUrl` > `url` > `command`

## References

- [MCP servers with the Gemini CLI](https://geminicli.com/docs/tools/mcp-server/)
- [Gemini CLI settings.json with MCP Config](https://audrey.feldroy.com/articles/2025-07-27-Gemini-CLI-Settings-With-MCP)
- [Gemini CLI Tutorial Series — Part 5 : GitHub MCP Server](https://medium.com/google-cloud/gemini-cli-tutorial-series-part-5-github-mcp-server-b557ae449e6e)
- [Gemini CLI configuration](https://geminicli.com/docs/get-started/configuration/)
