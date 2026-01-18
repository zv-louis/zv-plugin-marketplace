# VS Code - Skill Configuration Information

## Overview

VS Code supports AI agent skills through extensions like Claude Code extension, GitHub Copilot, and other AI assistants. Skill configurations are typically managed through VS Code's settings system.

## Configuration File Locations

### User Scope (Global)

- **Windows**: `%APPDATA%\Code\User\settings.json`
- **macOS**: `~/Library/Application Support/Code/User/settings.json`
- **Linux**: `~/.config/Code/User/settings.json`

### Project Scope

- **Workspace Settings**: `.vscode/settings.json` (in project directory)

## Settings Priority

Settings are applied in order of specificity:
Workspace → User Global → Default

More specific settings override broader settings.

## File Format

JSON format (JSONC - JSON with Comments supported)

## Configuration Example

For Claude Code extension in VS Code:

```json
{
  "claude-code.skills": {
    "allowed": [
      "/path/to/local/skill",
      "https://example.com/skill-package",
      "example-skills:pdf"
    ],
    "disabled": [
      "example-skills:docx"
    ]
  }
}
```

For GitHub Copilot extensions:

```json
{
  "github.copilot.chat.skills": [
    "/path/to/skill"
  ]
}
```

## Configuration Items

The configuration structure depends on the specific AI extension being used:

### Claude Code Extension

- `claude-code.skills`: Object containing skill configurations
  - `allowed`: Array of allowed skill identifiers
  - `disabled`: Array of disabled skill identifiers

### GitHub Copilot

- `github.copilot.chat.skills`: Array of skill paths or identifiers

## Skill Identifier Formats

1. **Local Path**: Absolute path to a skill directory
   - Example: `/home/user/my-skills/custom-skill`
   - Example: `C:\Users\user\my-skills\custom-skill` (Windows)

2. **URL**: Remote skill package URL
   - Example: `https://github.com/user/skill-repo`

3. **Qualified Name**: Package name with skill name (Claude Code extension)
   - Format: `<package-name>:<skill-name>`
   - Example: `example-skills:pdf`

## Important Notes

- VS Code settings can include comments (JSONC format)
- Settings are extension-specific - different AI extensions have different configuration keys
- The `.vscode/settings.json` file can be committed to version control for team sharing
- User settings apply across all workspaces

## Format Conversion Notes

When converting from Claude Code CLI format:

| Claude Code CLI                 | VS Code (Claude Extension)              |
| ------------------------------- | --------------------------------------- |
| `~/.claude/settings.json`       | `%APPDATA%\Code\User\settings.json`     |
| `.claude/settings.json`         | `.vscode/settings.json`                 |
| `skills.allowed`                | `claude-code.skills.allowed`            |
| `skills.disabled`               | `claude-code.skills.disabled`           |

## References

- [VS Code Settings Documentation](https://code.visualstudio.com/docs/getstarted/settings)
- [Claude Code VS Code Extension](https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
