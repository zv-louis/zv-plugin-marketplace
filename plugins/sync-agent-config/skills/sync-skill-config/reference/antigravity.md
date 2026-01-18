# Antigravity - Skill Configuration Information

## Overview

Antigravity is Google's AI-powered cloud IDE. It supports extensions and custom tools for extending AI capabilities.

## Configuration File Locations

### User Scope (Global)

- **Windows**: `C:\Users\<USER_NAME>\.gemini\antigravity\settings.json`
- **Other OS**: `~/.gemini/antigravity/settings.json` (estimated)

### Project Scope

Antigravity does **NOT** currently support project-level skill/extension configuration. All settings are stored globally at the user level.

Per-workspace configuration is a requested feature that may be added in future updates.

## File Format

JSON format

## Configuration Example

```json
{
  "extensions": {
    "enabled": [
      "google.firebase-tools",
      "custom-extension"
    ],
    "disabled": [
      "deprecated-extension"
    ],
    "custom": [
      {
        "name": "my-custom-tool",
        "path": "/path/to/extension",
        "enabled": true
      }
    ]
  }
}
```

## Configuration Items

- `extensions`: Object containing extension/skill configurations
  - `enabled`: Array of enabled extension identifiers
  - `disabled`: Array of disabled extension identifiers
  - `custom`: Array of custom extension configurations
    - `name`: Unique identifier for the extension
    - `path`: Local path to extension directory
    - `enabled`: Boolean indicating if the extension is active

## Important Notes

- Antigravity is a cloud-based IDE, so local file paths may behave differently
- Extensions are managed through the Antigravity UI in most cases
- Custom extensions may require additional setup through the IDE interface
- Project-level configuration is not currently supported

## Format Conversion Notes

When converting from Claude Code format:

| Claude Code                     | Antigravity                             |
| ------------------------------- | --------------------------------------- |
| `skills.allowed` array          | `extensions.enabled` array              |
| `skills.disabled` array         | `extensions.disabled` array             |
| Local path skill                | `extensions.custom` with path           |

When converting from Gemini CLI format:

| Gemini CLI                      | Antigravity                             |
| ------------------------------- | --------------------------------------- |
| `extensions` array              | `extensions.enabled` + `extensions.custom` |
| `enabled: false`                | Move to `extensions.disabled`           |

## Limitations

- **No project-level support**: All configurations are user-global
- **Cloud-based**: File paths reference cloud storage, not local filesystem
- **UI-managed**: Some extensions can only be configured through the Antigravity UI

## References

- [Antigravity Editor Documentation](https://antigravity.google/docs)
- [Antigravity Extensions Guide](https://antigravity.google/docs/extensions)
