# Gemini CLI - Skill Configuration Information

## Configuration File Locations

Gemini CLI uses configuration files for skill (extension) settings.

### User Scope (Global)

- **User Settings**: `~/.gemini/settings.json`

### Project Scope

- **Project Settings**: `.gemini/settings.json` (in project directory)

## Settings Priority

Settings are applied in order of specificity:
Project → User Global

More specific settings override broader settings.

## File Format

JSON format

## Configuration Example

```json
{
  "extensions": [
    {
      "name": "my-extension",
      "path": "/path/to/extension",
      "enabled": true
    },
    {
      "name": "remote-extension",
      "url": "https://example.com/extension-package",
      "enabled": true
    }
  ]
}
```

## Configuration Items

- `extensions`: Array of extension (skill) configurations
  - `name`: Unique identifier for the extension
  - `path`: Local path to extension directory (for local extensions)
  - `url`: URL to remote extension package (for remote extensions)
  - `enabled`: Boolean indicating if the extension is enabled (optional, defaults to true)

## Extension Identifier Formats

1. **Local Path**: Absolute path to an extension directory
   - Example: `/home/user/my-extensions/custom-ext`

2. **URL**: Remote extension package URL
   - Example: `https://github.com/user/extension-repo`

## Important Notes

- Extensions in Gemini CLI are similar to skills in other Agent tools
- Each extension is an object with name and path/url properties
- The `enabled` field can be used to disable an extension without removing it
- Project-level settings override user-level settings

## Format Conversion Notes

When converting from Claude Code format:

| Claude Code                     | Gemini CLI                                  |
| ------------------------------- | ------------------------------------------- |
| `skills.allowed` array          | `extensions` array with objects             |
| `skills.disabled` array         | Set `enabled: false` in extension object    |
| Path string                     | `{ "name": "...", "path": "..." }`          |
| URL string                      | `{ "name": "...", "url": "..." }`           |

## References

- [Gemini CLI Documentation](https://github.com/google-gemini/gemini-cli)
- [Gemini CLI Extensions Guide](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions.md)
