# Codex CLI - MCP Configuration Information

## Configuration File Location

- **All OS**: `~/.codex/config.toml`

## How to Access Configuration File

**Via IDE Extension**:
1. Click the gear icon in the upper right of the extension
2. Select "Codex Settings" → "Open config.toml"

**Via CLI**:
- Edit `~/.codex/config.toml` directly with any text editor
- Or use the `codex mcp` command to manage MCP server settings

## File Format

TOML format

## Configuration Example

```toml
# Default model settings
default_model = "gpt-4"

# Approval policy
approval_policy = "auto"

# Sandbox settings
sandbox_enabled = true

# MCP server configuration
[mcp_servers.filesystem]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/directory"]

[mcp_servers.github]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-github"]

[mcp_servers.github.env]
GITHUB_TOKEN = "your-github-token"

[mcp_servers.custom-server]
command = "python"
args = ["/path/to/server.py"]

[mcp_servers.custom-server.env]
API_KEY = "your-api-key"
DEBUG = "true"
```

## Configuration Items

Each MCP server is configured as a `[mcp_servers.<server-name>]` table:

- `command`: Command to execute
- `args`: Array of command-line arguments
- `env`: Environment variables (defined as a subtable)

## Optional Features

### Rust MCP Client Implementation

To enable the Rust-based MCP client implementation, add the following to your configuration file if needed:

```toml
[features]
rmcp_client = true
```

## Project-Level Configuration

Codex CLI does **NOT** support project-level MCP configuration. All MCP server settings are stored globally in `~/.codex/config.toml`.

Unlike Claude Code or VS Code which support workspace-level configuration files, Codex uses a centralized global configuration approach. This means:

- MCP servers configured in `config.toml` are available across all projects
- Configuration cannot be version-controlled per project
- Each team member must manually set up their own MCP configuration

## Important Notes

- This configuration file is **shared** between the CLI and IDE extension
- MCP server settings are available in both Codex CLI and Codex IDE extension

## References

- [Codex MCP Configuration: TOML Setup Guide](https://vladimirsiedykh.com/blog/codex-mcp-config-toml-shared-configuration-cli-vscode-setup-2025)
- [Configuring Codex](https://developers.openai.com/codex/local-config/)
- [codex/docs/config.md](https://github.com/openai/codex/blob/main/docs/config.md)
- [The Ultimate Codex CLI MCP Guide](https://blog.wenhaofree.com/en/posts/technology/codex-mcp-comprehensive-guide/)
- [Model Context Protocol - OpenAI Developers](https://developers.openai.com/codex/mcp/)
