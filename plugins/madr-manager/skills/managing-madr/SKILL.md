---
name: managing-madr
description: MADR（Markdown Architectural Decision Records）を作成・一覧・管理するスキル。Structured MADR v4.0.0 フォーマットに従い、ADR ファイルの新規作成、既存 ADR の確認・ステータス更新、一覧表示を行う。「ADR を書いて」「アーキテクチャ決定を記録して」「MADR を追加して」などの指示に反応する。
allowed-tools: Read, Write, Edit, Glob, Bash(ls *), Bash(mkdir -p *)
---

# MADR Manager Skill

## File Reading Policy

**Read reference files only when they are actually needed — never preload all references at startup.**

- Load a reference file immediately before executing the corresponding operation.
- Do not read reference files speculatively or "just in case."
- `references/spec/structured-madr-spec.md` is the authoritative MADR spec; read it only when you need to understand format details (e.g., during ADR creation or status update).

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
