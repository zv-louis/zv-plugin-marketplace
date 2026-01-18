# Claude Code - Skill Configuration Information

## Configuration File Locations

Claude Code uses hierarchical configuration files for skill settings.

### User Scope (Global)

- **User Settings**: `~/.claude/settings.json`
- **User Local Settings**: `~/.claude/settings.local.json`

### Project Scope

- **Project Settings**: `.claude/settings.json` (in project directory)
- **Project Local Settings**: `.claude/settings.local.json` (in project directory)

## Settings Priority

Settings are applied in order of specificity:
Project Local → Project → User Local → User Global

More specific settings override broader settings.

## File Format

JSON format

## Configuration Example

```json
{
  "skills": {
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

## Configuration Items

- `skills`: Object containing skill configurations
  - `allowed`: Array of allowed skill identifiers
    - Local path to skill directory
    - URL to remote skill package
    - Qualified skill name (e.g., `example-skills:pdf`)
  - `disabled`: Array of disabled skill identifiers (optional)

## Skill Identifier Formats

1. **Local Path**: Absolute or relative path to a skill directory
   - Example: `/home/user/my-skills/custom-skill`
   - Example: `./skills/my-skill`

2. **URL**: Remote skill package URL
   - Example: `https://github.com/user/skill-repo`

3. **Qualified Name**: Package name with skill name
   - Format: `<package-name>:<skill-name>`
   - Example: `example-skills:pdf`
   - Example: `document-skills:xlsx`

## Important Notes

- Skills must be explicitly allowed in the configuration to be used
- The `disabled` array takes precedence over `allowed`
- Project-level settings can override user-level settings
- Both `.json` files in `.claude/` directory are checked

## References

- [Claude Code Skills Documentation](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Claude Code Settings Documentation](https://docs.anthropic.com/en/docs/claude-code/settings)
