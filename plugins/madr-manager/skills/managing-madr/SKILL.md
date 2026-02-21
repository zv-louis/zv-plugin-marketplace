---
name: madr-manager
description: MADR（Markdown Architectural Decision Records）を作成・一覧・管理するスキル。Structured MADR v4.0.0 フォーマットに従い、ADR ファイルの新規作成、既存 ADR の確認・ステータス更新、一覧表示を行う。「ADR を書いて」「アーキテクチャ決定を記録して」「MADR を追加して」などの指示に反応する。
allowed-tools: Read, Write, Edit, Glob, Bash(ls *), Bash(mkdir -p *)
---

# MADR Manager Skill

## Overview

Support creating and managing ADR (Architectural Decision Records) files following the **Structured MADR v4.0.0** format.

Before any action, read `references/structured-madr-spec.md` to understand the full spec.

## Operations

### 1. Create a new ADR

**Trigger:** User asks to create/add/write an ADR or record an architectural decision.

**Steps:**

1. Determine the ADR storage directory:
   - Default: `docs/decisions/` relative to the user's working directory
   - Ask the user if a different location is preferred (only if the default doesn't exist and no preference was stated)

2. Determine the next sequence number:
   - List existing files matching `NNNN-*.md` in the target directory
   - Use the next available 4-digit number (e.g., `0001`, `0002`, ...)
   - If no files exist, start from `0001`

3. Gather required information via conversation:

   | Field | Required | Notes |
   |---|---|---|
   | Title | Yes | Short phrase describing problem + solution. Pattern: `Use [X] for [Y]` |
   | Context and Problem Statement | Yes | Background and why this decision is needed |
   | Considered Options | Yes | All options actually evaluated (list, ≥2 items) |
   | Decision Outcome (chosen option + reason) | Yes | Which option was chosen and why |
   | Status | Yes | Default: `accepted`. Options: `proposed`, `accepted`, `rejected`, `deprecated`, `superseded by ADR-XXXX` |
   | Date | Yes | Default: today's date (YYYY-MM-DD) |
   | Decision Makers | Optional | Who made the decision |
   | Consulted | Optional | Who was consulted (two-way communication) |
   | Informed | Optional | Who is informed (one-way communication) |
   | Decision Drivers | Optional | Constraints and quality requirements |
   | Consequences | Optional (recommended) | Good/Bad/Neutral impacts of the chosen option |
   | Confirmation | Optional (recommended) | How to verify the decision is implemented correctly |
   | Pros and Cons of the Options | Optional | Detailed comparison per option |
   | More Information | Optional | Links, related ADRs, review dates |

   Gathering guidelines:
   - Ask for title and problem statement first
   - Then ask for considered options and the chosen outcome
   - Offer to fill in optional sections (Consequences, Confirmation, Pros and Cons) — suggest including them as they improve the record quality
   - Use `AskUserQuestion` to present choices efficiently
   - If the user doesn't specify a date, use today's date without asking

4. Generate the filename: `NNNN-title-with-dashes.md`
   - Convert the title to lowercase, replace spaces with hyphens, remove special characters
   - Example: "Use PostgreSQL for relational data" → `0001-use-postgresql-for-relational-data.md`

5. Create the directory if it doesn't exist (`mkdir -p docs/decisions`)

6. Write the ADR file following the template structure below

7. Show the created file path and content summary to the user

### 2. List existing ADRs

**Trigger:** User asks to list, show, or view existing ADRs.

**Steps:**

1. Find ADR files in `docs/decisions/` (or user-specified directory)
2. Read the YAML front matter (status, date) and H1 title from each file
3. Display a table:

   ```
   | # | File | Title | Status | Date |
   |---|------|-------|--------|------|
   | 1 | 0001-use-postgresql.md | Use PostgreSQL for relational data | accepted | 2025-01-15 |
   ```

### 3. Update ADR status

**Trigger:** User asks to update, change status, deprecate, supersede, or reject an existing ADR.

**Steps:**

1. Identify the target ADR file (by number or name)
2. Show the current status
3. Ask for the new status if not specified
4. Update the `status` field in the YAML front matter
5. If superseding, also update `More Information` to reference the superseding ADR

### 4. Show ADR details

**Trigger:** User asks to show, read, or view a specific ADR.

**Steps:**

1. Identify the target ADR file
2. Read and display the full content

## ADR File Template

```markdown
---
status: "{proposed | rejected | accepted | deprecated | superseded by ADR-XXXX}"
date: {YYYY-MM-DD}
decision-makers: {names, or omit if not specified}
consulted: {names, or omit if not specified}
informed: {names, or omit if not specified}
---

# {Short title: describes both problem and solution}

## Context and Problem Statement

{Background and why this decision is needed. Use question form to invite discussion.}

## Decision Drivers

* {Driver 1}
* {Driver 2}

## Considered Options

* {Option 1 — chosen option first by convention}
* {Option 2}
* {Option 3}

## Decision Outcome

Chosen option: "{chosen option}", because {reason referencing Decision Drivers or Pros/Cons}.

### Consequences

* Good, because {positive impact}
* Bad, because {negative impact}
* Neutral, because {neutral impact}

### Confirmation

{How to verify the decision is implemented correctly. Automation (CI checks, ArchUnit) strongly recommended.}

## Pros and Cons of the Options

### {Option 1}

{Optional: description, example, or URL}

* Good, because {argument A}
* Neutral, because {argument B}
* Bad, because {argument C}

### {Option 2}

* Good, because {argument A}
* Bad, because {argument B}

## More Information

{Supplemental info, related ADR links, external resources, review schedule.}
```

### Template rules

- **YAML Front Matter:** Include only if at least one field has a value. Omit entire block otherwise.
- **Optional fields:** Omit sections that have no content rather than leaving them empty.
- **Considered Options order:** Put the chosen option first (project-wide convention).
- **Pros and Cons subsections:** Must match the order and names used in Considered Options.
- **Never delete ADRs:** Even rejected or deprecated ones must be kept as historical records.

## Resources

### references/

- **structured-madr-spec.md**: Full Structured MADR v4.0.0 specification including template variants, section details, best practices, and complete examples. Always read this before creating or editing ADRs.
