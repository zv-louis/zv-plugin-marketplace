# madr-manager

[English](README.md) | 日本語

Structured MADR v4.0.0 フォーマットに従って MADR（Markdown Architectural Decision Records）を対話的に作成・管理する Claude Code プラグイン。

## 概要

このプラグインは、会話形式のガイドを通じてアーキテクチャ上の設計決定を ADR ファイルとして記録します。新規 ADR の作成、既存 ADR の一覧表示、ステータスの更新、内容の確認をサポートします。

**サポートする操作:**

- **作成**: 対話形式で新規 ADR を作成
- **一覧**: プロジェクト内の既存 ADR を一覧表示
- **更新**: 既存 ADR のステータスを変更（accept / reject / deprecated / superseded）
- **表示**: 特定の ADR の全内容を表示

## プロジェクト構成

```
plugins/madr-manager/
├── .claude-plugin/
│   └── plugin.json                  # プラグインマニフェスト
├── skills/
│   └── madr-manager/
│       ├── SKILL.md                 # スキル定義とワークフロー
│       └── references/
│           └── structured-madr-spec.md  # Structured MADR v4.0.0 仕様書
├── LICENSE
├── README.md
└── README_ja.md
```

## インストール

```bash
claude skills add <このプラグインのパス>
```

## 使い方

インストール後、Claude Code に ADR 管理を依頼するだけで起動します:

```
# 新規 ADR の作成
ADR を作成して
アーキテクチャ上の決定を記録したい
PostgreSQL の採用理由を ADR に残したい

# 既存 ADR の一覧表示
既存の ADR を一覧表示して

# ADR ステータスの更新
ADR-0002 を deprecated に更新して
ADR-0003 は ADR-0005 に supersede された

# ADR の表示
ADR-0001 を表示して
```

ADR ファイルはデフォルトで `docs/decisions/` に保存され、`NNNN-title-with-dashes.md` の命名規則に従います。

## MADR フォーマット

ADR ファイルは [Structured MADR v4.0.0](https://adr.github.io/madr/) フォーマットに従います:

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

全仕様は `skills/madr-manager/references/structured-madr-spec.md` を参照してください。

## ライセンス

MIT
