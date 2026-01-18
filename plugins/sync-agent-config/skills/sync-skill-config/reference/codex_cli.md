# Codex CLI - Skill Configuration Information

## Configuration File Locations

Codex CLI uses configuration files for skill settings.

### User Scope (Global)

- **User Settings**: `~/.codex/config.json`

### Project Scope

- **Project Settings**: `.codex/config.json` (in project directory)

## Settings Priority

Settings are applied in order of specificity:
Project → User Global

More specific settings override broader settings.

## File Format

JSON format

## Configuration Example

```json
{
  "skills": [
    "/path/to/local/skill",
    "https://example.com/skill-package"
  ]
}
```

## Configuration Items

- `skills`: Array of skill identifiers
  - Local path to skill directory
  - URL to remote skill package

## Skill Identifier Formats

1. **Local Path**: Absolute or relative path to a skill directory
   - Example: `/home/user/my-skills/custom-skill`

2. **URL**: Remote skill package URL
   - Example: `https://github.com/user/skill-repo`

## Important Notes

- Codex CLI skill configuration is simpler than Claude Code
- Skills are specified as a flat array of paths or URLs
- No explicit disabled list - remove from array to disable
- Project-level settings override user-level settings

## Format Conversion Notes

When converting from Claude Code format:

| Claude Code                     | Codex CLI                        |
| ------------------------------- | -------------------------------- |
| `skills.allowed` array          | `skills` array                   |
| `skills.disabled` array         | Remove from `skills` array       |
| Qualified names (`pkg:skill`)   | May need full path/URL           |

## References

- [Codex CLI Documentation](https://github.com/openai/codex)
- [Codex CLI Configuration Guide](https://github.com/openai/codex/blob/main/docs/configuration.md)
