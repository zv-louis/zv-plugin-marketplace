# madr-manager

English | [日本語](README_ja.md)

A Claude Code plugin for interactively creating and managing MADR (Markdown Architectural Decision Records) following the Structured MADR v4.0.0 format.

## Overview

This plugin helps you record architectural decisions as ADR files through a guided conversation. It supports creating new ADRs, listing existing ones, updating statuses, and viewing ADR details.

**Supported operations:**

- **Create** a new ADR with interactive Q&A
- **List** all existing ADRs in the project
- **Update** the status of an existing ADR (accept, reject, deprecate, supersede)
- **View** the full content of a specific ADR

## Project Structure

```
plugins/madr-manager/
├── .claude-plugin/
│   └── plugin.json                  # Plugin manifest
├── skills/
│   └── madr-manager/
│       ├── SKILL.md                 # Skill definition and workflow
│       └── references/
│           └── structured-madr-spec.md  # Structured MADR v4.0.0 specification
├── LICENSE
├── README.md
└── README_ja.md
```

## Installation

```bash
claude skills add <this-plugin-path>
```

## Usage

Once installed, trigger the skill by asking Claude Code to manage ADRs:

```
# Create a new ADR
ADR を作成して
アーキテクチャ上の決定を記録したい

# List existing ADRs
既存の ADR を一覧表示して

# Update ADR status
ADR-0002 を deprecated に更新して

# View an ADR
ADR-0001 を表示して
```

The skill stores ADR files in `docs/decisions/` by default, following the naming convention `NNNN-title-with-dashes.md`.

## MADR Format

ADR files follow the [Structured MADR v4.0.0](https://adr.github.io/madr/) format:

```markdown
---
status: "accepted"
date: 2025-01-15
decision-makers: Alice, Bob
---

# Use PostgreSQL for relational data storage

## Context and Problem Statement
...

## Considered Options
* PostgreSQL
* MySQL

## Decision Outcome
Chosen option: "PostgreSQL", because ...
```

See `skills/madr-manager/references/structured-madr-spec.md` for the full specification.

## License

MIT
