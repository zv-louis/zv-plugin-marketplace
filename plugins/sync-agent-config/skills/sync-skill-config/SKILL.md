---
name: sync-skill-config
description: Synchronize skill configurations across different Agent tools. Use when you want to copy, apply, or sync skills between multiple Agent environments like Claude Code, Codex, Gemini CLI, VS Code, Cursor, and Antigravity. Supports both user-scope (global) and project-scope settings, with options for full synchronization or selective skill synchronization.
allowed-tools: Read, Write, Bash, Glob, WebSearch, WebFetch, AskUserQuestion
---

# Skill Configuration Synchronization Skill

## Overview

This skill provides procedures for synchronizing skill configurations across different Agent tool environments.

## What This Skill Does

1. Read skill configurations registered in the source Agent tool
2. Apply the skill configurations to the target Agent tool
3. Support both full synchronization and selective skill synchronization
4. Handle both user-scope (global) and project-scope configurations

## Configuration Scopes

Skill settings can exist at different scopes depending on the Agent tool:

| Agent Tool  | User Scope (Global)                    | Project Scope                          |
| ----------- | -------------------------------------- | -------------------------------------- |
| Claude Code | `~/.claude/settings.json`              | `.claude/settings.json` (in project)   |
| Codex CLI   | `~/.codex/config.json`                 | `.codex/config.json` (in project)      |
| Gemini CLI  | `~/.gemini/settings.json`              | `.gemini/settings.json` (in project)   |
| VS Code     | User `settings.json`                   | `.vscode/settings.json` (in project)   |
| Cursor      | User `settings.json`                   | `.cursor/settings.json` (in project)   |
| Antigravity | `~/.gemini/antigravity/settings.json`  | ❌ Not Supported                       |

When synchronizing settings, consider:

- **User Scope (Global)**: Applied to all projects for the user
- **Project Scope**: Applied only to the specific project directory

## Operation Modes

### Synchronization Modes

#### Full Synchronization

Synchronize all skills from the source to the target Agent tool.

#### Selective Synchronization

Synchronize only specified skills from the source to the target Agent tool. Users can specify:

- A single skill name
- Multiple skill names
- Skills matching a pattern (if supported)

### Deletion Mode

#### Selective Deletion

Delete specified skills from the target Agent tool's configuration. Users can specify:

- A single skill name to delete
- Multiple skill names to delete

This is useful when:

- You want to remove unused or deprecated skills from an environment
- You want to clean up skill configurations that are no longer needed
- You want to remove specific skills without affecting others

**Important**: This operation does not require a source Agent tool - it operates directly on the target configuration.

## Procedures

### 1. Check Operating System Environment

Before starting the synchronization process, verify the current operating system environment using the Bash tool or by checking environment variables. This is important because:

- Configuration file paths may differ between operating systems (Windows, macOS, Linux)
- File path separators are different (Windows uses `\`, Unix-like systems use `/`)
- Default installation locations vary by OS

Use appropriate methods to determine:

- Operating system type (Windows, macOS, Linux, etc.)
- User home directory path
- Relevant environment-specific paths

### 2. Confirm Operation Parameters with User

Before proceeding, confirm with the user using the AskUserQuestion tool:

1. **Operation Type**: Synchronization or Deletion
2. **Source Agent Tool** (for synchronization only): Which Agent tool to read skills from
3. **Target Agent Tool**: Which Agent tool to apply changes to
4. **Scope**: User scope (global), project scope, or both
5. **Mode**: Full synchronization, selective synchronization, or selective deletion
6. **Skill Selection** (if selective): Which specific skills to synchronize or delete

For selective synchronization, present the list of available skills from the source and confirm which skills to synchronize.
For selective deletion, present the list of existing skills in the target and confirm which skills to delete.

### 3. Verify Skill Configuration File Specifications

Since skill configuration methods may vary depending on the Agent tool, first verify and understand the specifications of the skill configuration files for both the source and target Agent tools.

Refer to the md documents in the following directory for specifications:

- [Skill Configuration Method Reference](./reference/)

Available references:

- [Claude Code](./reference/claude_code.md)
- [Codex CLI](./reference/codex_cli.md)
- [Gemini CLI](./reference/gemini_cli.md)
- [VS Code](./reference/vscode.md)
- [Cursor](./reference/cursor.md)
- [Antigravity](./reference/antigravity.md)

**If reference documentation is not available for the target Agent tool:**

- Use WebSearch and WebFetch tools to search the web for the configuration file specifications
- Look for official documentation, README files, or configuration examples
- Verify the file format (JSON, YAML, TOML, etc.) and required structure
- Identify the correct configuration file path and naming convention
- Understand how skills should be defined in that specific tool's format

### 4. Check Available Skills in Source

Read the configuration file containing the skill settings of the source Agent tool and check available skills.
The configuration includes the following information:

- Skill name
- Skill path or URL
- Skill description (if available)
- Skill-specific settings (if any)
- Enabled/disabled status

For selective synchronization, present the list of available skills to the user and confirm which skills to synchronize.

### 5. Apply Changes to Target Agent Tool Configuration File

Read the target Agent tool's skill configuration file and apply the changes based on the operation mode.

#### For Synchronization Operations

- For full synchronization: Apply all skills from the source.
- For selective synchronization: Apply only the specified skills.
- If the same skill is already registered, compare the contents and let the user decide if an update is needed.
- Preserve existing skills in the target that are not being synchronized.
- Handle format differences between source and target Agent tools.

#### For Deletion Operations

- For selective deletion: Remove only the specified skills from the target configuration.
- Before deleting, confirm with the user which skills will be removed.
- Preserve all skills that are not specified for deletion.

#### Common Guidelines

- Write correctly according to the target configuration file format.
- Create backups as necessary before making changes.

### 6. Validate Settings

After making changes, validate that the configuration file has no issues.

- Check file format integrity (JSON syntax validation, etc.)
- Verify that required fields are present
- Confirm skill paths or URLs are valid (if verifiable)

## Special Cases / Exceptional Cases / Errors

In the following cases, notify the user and stop processing:

- There are no skills registered in the source configuration file (for synchronization).
- The source configuration file does not exist (for synchronization).
- The target configuration file is not writable.
- The configuration file format is invalid.
- The requested skill for selective sync does not exist in the source.
- The requested skill for selective deletion does not exist in the target.
- There are no skills registered in the target configuration file (for deletion).

In the following cases, use tools as necessary to handle the situation:

- The target configuration file does not exist.
  Create a new target configuration file. (use Bash tool if necessary)

- The skill settings are incompatible between the source and target Agent tools.
  Since configuration file formats and element names may differ, verify the specifications of both source and target, and rewrite the format so that the skill settings content remains the same.
  If there are unclear points, perform web searches to verify specifications. (use WebSearch WebFetch tool if necessary)

## Prohibited Actions

The following actions are prohibited when managing skill settings:

- Modifying settings other than skills
- Leaking authentication information or sensitive data
- Applying invalid skill settings
- Overwriting existing skills without user confirmation
- Deleting skills without user confirmation
- Deleting skills that are not specified for deletion

## When to Use This Skill

- When users want to synchronize skill configurations across multiple Agent environments
- When setting up skills in a new environment based on an existing setup
- When sharing project-specific skill configurations with team members
- When migrating skill configurations to a different Agent tool
- When users want to remove specific skills from an Agent environment
- When cleaning up unused or deprecated skill configurations

## Examples

**Example 1**: "I want to apply Claude Code's skills to Codex"

- Read Claude Code's skill configuration file (user scope)
- Apply the same settings to Codex's skill configuration file

**Example 2**: "Sync only the 'pdf' and 'docx' skills from Claude Code to Codex"

- Read Claude Code's skill configuration file
- Extract only the 'pdf' and 'docx' skill configurations
- Apply those specific skills to Codex's skill configuration file

**Example 3**: "Sync project-level skills from Claude Code to Codex for this project"

- Read the project's `.claude/settings.json` file
- Apply the skills to the project's `.codex/config.json` file

**Example 4**: "Delete the 'pdf' skill from Claude Code" (Selective Deletion)

- Read Claude Code's skill configuration file
- Confirm the 'pdf' skill exists
- Remove the 'pdf' skill from the configuration
- Preserve all other skills

**Example 5**: "Remove the 'docx' and 'xlsx' skills from Codex's global settings"

- Read Codex's global skill configuration file
- Confirm both 'docx' and 'xlsx' skills exist
- Remove those specific skills from the configuration
- Preserve all other skills

**Example 6**: "Clean up unused skills from VS Code"

- Read VS Code's skill configuration file
- List all available skills to the user
- Ask user which skills to delete
- Remove the specified skills from the configuration

## Best Practices

- Always confirm the operation type (sync/delete), scope (user/project), and mode with the user before proceeding
- Back up configuration files before any changes
- Refer to documentation when configuration file specifications are unclear
- Perform web searches if reference documentation is not available
- For selective synchronization, show the user the available skills before asking which to sync
- For selective deletion, show the user the existing skills before asking which to delete
- When skills exist in both source and target, show the differences and ask user preference
- Preserve existing skills in the target that are not part of the operation
- Always require explicit user confirmation before deleting any skills
