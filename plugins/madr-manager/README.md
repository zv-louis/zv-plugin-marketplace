# madr-manager

English | [日本語](README_ja.md)

A Claude Code plugin for interactively creating and managing MADR (Markdown Architectural Decision Records) following the Structured MADR v4.0.0 format.

## Overview

This plugin helps you record architectural decisions as ADR files through a guided conversation.
It supports creating new ADRs from meeting notes or conversations, listing existing ones, updating statuses, viewing ADR details, generating an index file, and tracing decision history.

**Supported operations:**

- **Create**: Create a new ADR interactively
- **List**: List all existing ADRs in the project
- **Update**: Change the status of an existing ADR (accept / reject / deprecated / superseded)
- **View**: Display the full content of a specific ADR
- **Generate index**: Generate an index file (index.md) summarizing all ADRs in the project
- **Summarize history**: Trace and display the discussion and reasoning behind a decision

## Project Structure

```txt
plugins/madr-manager/
├── .claude-plugin/
│   └── plugin.json                  # Plugin manifest
├── skills/
│   └── managing-madr/
│       ├── SKILL.md                 # Skill definition and workflow
│       └── references/
│           ├── spec/
│           │   ├── adr-template.md      # ADR template
│           │   ├── index-template.md    # Index template
│           │   └── structured-madr-spec.md  # Structured MADR v4.0.0 specification
│           └── workflow/
│               ├── create-adr.md        # Create ADR workflow
│               ├── generate-index.md    # Generate index workflow
│               ├── list-adrs.md         # List ADRs workflow
│               ├── show-adr.md          # Show ADR workflow
│               ├── summarize-adr-history.md  # Summarize ADR history workflow
│               └── update-adr-status.md # Update ADR status workflow
├── LICENSE
├── README.md
└── README_ja.md
```

## Installation

Install madr-manager from the marketplace.

```bash
# Install the plugin
/plugin install madr-manager@zv-plugins
```

## Usage

Once installed, trigger the skill by asking Claude Code to manage ADRs:

```markdown
# Create a new ADR
Create an ADR from {meeting notes, etc.}
I want to record an architectural decision
I want to document the reason for adopting PostgreSQL in an ADR

# List existing ADRs
List existing ADRs

# Update ADR status
Update ADR-0002 to deprecated
ADR-0003 has been superseded by ADR-0005

# View an ADR
Show ADR-0001

# Summarize decision history
Tell me about the discussion and reasoning behind the current state of X
```

ADR files follow the naming convention `NNNN-title-with-dashes.md`.
By default, they are stored in `{ProjectRoot}/docs/decisions/`.
You can also specify a custom file or directory as the storage location.
In that case, it is recommended to specify the default ADR storage location in system files such as CLAUDE.md or AGENT.md.

## MADR Format

ADR files follow the [Structured MADR v4.0.0](https://adr.github.io/madr/) format.

## License

MIT
