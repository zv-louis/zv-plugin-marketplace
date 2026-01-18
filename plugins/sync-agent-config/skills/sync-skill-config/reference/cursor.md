# Cursor - Skill Configuration Information

## Overview

Cursor is an AI-powered code editor built on VS Code. It supports AI agent skills through its built-in AI features and extensions. Cursor uses a similar settings structure to VS Code but with Cursor-specific configurations.

## Configuration File Locations

### User Scope (Global)

- **Windows**: `%APPDATA%\Cursor\User\settings.json`
- **macOS**: `~/Library/Application Support/Cursor/User/settings.json`
- **Linux**: `~/.config/Cursor/User/settings.json`

### Project Scope

- **Workspace Settings**: `.cursor/settings.json` (in project directory)
- **VS Code Compatible**: `.vscode/settings.json` (also recognized)

## Settings Priority

Settings are applied in order of specificity:
Workspace (.cursor) → Workspace (.vscode) → User Global → Default

More specific settings override broader settings.

## File Format

JSON format (JSONC - JSON with Comments supported)

## Configuration Example

```json
{
  "cursor.skills": {
    "allowed": [
      "/path/to/local/skill",
      "https://example.com/skill-package"
    ],
    "disabled": []
  },
  "cursor.rules": {
    "enabled": true,
    "paths": [
      ".cursorrules",
      ".cursor/rules"
    ]
  }
}
```

## Configuration Items

- `cursor.skills`: Object containing skill configurations
  - `allowed`: Array of allowed skill identifiers
  - `disabled`: Array of disabled skill identifiers

- `cursor.rules`: Cursor Rules configuration (related to AI behavior)
  - `enabled`: Boolean to enable/disable rules
  - `paths`: Array of paths to rules files

## Skill Identifier Formats

1. **Local Path**: Absolute path to a skill directory
   - Example: `/home/user/my-skills/custom-skill`
   - Example: `C:\Users\user\my-skills\custom-skill` (Windows)

2. **URL**: Remote skill package URL
   - Example: `https://github.com/user/skill-repo`

## Cursor Rules

Cursor also supports `.cursorrules` files for defining AI behavior rules at the project level. These are similar to skills but focused on behavior customization:

- **Project Rules**: `.cursorrules` (in project root)
- **Directory Rules**: `.cursor/rules/` (in project directory)

## Important Notes

- Cursor inherits VS Code's settings system but uses its own configuration directory
- Both `.cursor/` and `.vscode/` directories are recognized for workspace settings
- Cursor-specific settings use the `cursor.` prefix
- The `.cursorrules` file is Cursor-specific and not compatible with VS Code

## Format Conversion Notes

When converting from Claude Code format:

| Claude Code                     | Cursor                                  |
| ------------------------------- | --------------------------------------- |
| `~/.claude/settings.json`       | `%APPDATA%\Cursor\User\settings.json`   |
| `.claude/settings.json`         | `.cursor/settings.json`                 |
| `skills.allowed`                | `cursor.skills.allowed`                 |
| `skills.disabled`               | `cursor.skills.disabled`                |

When converting from VS Code format:

| VS Code                         | Cursor                                  |
| ------------------------------- | --------------------------------------- |
| `%APPDATA%\Code\User\...`       | `%APPDATA%\Cursor\User\...`             |
| `.vscode/settings.json`         | `.cursor/settings.json` (preferred)     |
| `claude-code.skills.*`          | `cursor.skills.*`                       |

## References

- [Cursor Documentation](https://cursor.sh/docs)
- [Cursor Rules Documentation](https://cursor.sh/docs/rules)
- [Cursor Settings Guide](https://cursor.sh/docs/settings)
