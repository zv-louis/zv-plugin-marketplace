---
name: managing-madr
description: Skill for creating, listing, and managing MADR (Markdown Architectural Decision Records) following the Structured MADR v4.0.0 format. Handles creating new ADR files, reviewing and updating the status of existing ADRs, and listing all ADRs. Triggered by instructions such as "write an ADR", "record an architectural decision", or "add a MADR".
allowed-tools: Read, Write, Edit, Glob, Bash(ls *), Bash(mkdir -p *)
---

# MADR Manager Skill

## File Reading Policy

**Never read the same file twice. Before loading any reference file, check which files have already been read in this conversation and skip if already loaded.**

| Category | Pre-loading | Rule |
|---|---|---|
| `references/workflow/` | Prohibited | Load immediately before executing the corresponding operation |
| `references/spec/` | Allowed | Load when needed (pre-loading is acceptable) |

## Operations

Identify which operation the user is requesting, then read the corresponding reference file and follow its instructions.

### 1. Create a new ADR

**Trigger:** User asks to create / add / write an ADR, or to record an architectural decision.

→ Read `references/workflow/create-adr.md` and follow the workflow defined there.

### 2. List existing ADRs

**Trigger:** User asks to list, show, or view existing ADRs.

→ Read `references/workflow/list-adrs.md` and follow the workflow defined there.

### 3. Update ADR status

**Trigger:** User asks to update, change status, deprecate, supersede, or reject an existing ADR.

→ Read `references/workflow/update-adr-status.md` and follow the workflow defined there.

### 4. Show ADR details

**Trigger:** User asks to show, read, or view a specific ADR.

→ Read `references/workflow/show-adr.md` and follow the workflow defined there.

## Resources

| File | When to read |
|---|---|
| `references/workflow/create-adr.md` | When creating a new ADR |
| `references/workflow/list-adrs.md` | When listing existing ADRs |
| `references/workflow/update-adr-status.md` | When updating ADR status |
| `references/workflow/show-adr.md` | When showing a specific ADR |
| `references/spec/adr-template.md` | When writing an ADR file (referenced from create-adr.md) |
| `references/spec/structured-madr-spec.md` | When you need authoritative MADR format details |
