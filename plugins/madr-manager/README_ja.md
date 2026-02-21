# madr-manager

[English](README.md) | 日本語

Structured MADR v4.0.0 フォーマットに従って MADR（Markdown Architectural Decision Records）を対話的に作成・管理する Claude Code プラグイン.

## 概要

このプラグインは、会話形式のガイドを通じて設計や運用面の意思決定を ADR(Architectual Decision Records) ファイルとして記録します。  
議事録や会話録から新規にADRを作成/追加したり、既存 ADR の一覧表示、ステータスの更新、内容や経緯の確認をサポートします。  


**サポートする操作:**

- **作成**: 対話形式で新規 ADR を作成・追加
- **一覧**: プロジェクト内の既存 ADR を一覧表示
- **更新**: 既存 ADR のステータスを変更（accept / reject / deprecated / superseded）
- **表示**: 特定の ADR の全内容を表示
- **ADR一覧ファイルの生成**: プロジェクト内の全 ADR をまとめた一覧ファイル(index.md)を生成
- **決定履歴の確認**: 意思決定に至るまでの議論や理由を追跡して表示

## プロジェクト構成

```txt
plugins/madr-manager/
├── .claude-plugin/
│   └── plugin.json                  # プラグインマニフェスト
├── skills/
│   └── managing-madr/
│       ├── SKILL.md                 # スキル定義とワークフロー
│       └── references/
│           ├── spec/
│           │   ├── adr-template.md      # ADR テンプレート
│           │   ├── index-template.md    # インデックステンプレート
│           │   └── structured-madr-spec.md  # Structured MADR v4.0.0 仕様書
│           └── workflow/
│               ├── create-adr.md        # ADR 作成ワークフロー
│               ├── generate-index.md    # インデックス生成ワークフロー
│               ├── list-adrs.md         # ADR 一覧ワークフロー
│               ├── show-adr.md          # ADR 表示ワークフロー
│               ├── summarize-adr-history.md  # 決定履歴確認ワークフロー
│               └── update-adr-status.md # ADR ステータス更新ワークフロー
├── LICENSE
├── README.md
└── README_ja.md
```

## インストール

マーケットプレイスから madr-manager をインストールします.  

```bash
# プラグインのインストール
/plugin install madr-manager@zv-plugins
```

## 使い方

インストール後、Claude Code に ADR 管理を依頼するだけで起動します:

```markdown
# 新規 ADR の作成
〇〇〇{議事録ファイルなど} から ADR をつくって

# 既存 ADR の一覧表示
既存の ADR を一覧表示して

# ADR ステータスの更新
ADR-0002 を deprecated に更新して
ADR-0003 は ADR-0005 に supersede されたのでステータスを更新して

# ADR の表示
ADR-0001 を表示して

# 決定履歴の確認
〇〇〇について、現在の状況はどうなっている？
ADR を参照して、いままでの議論や決定の経緯を教えてほしい.
```

ADR ファイルは`NNNN-title-with-dashes.md` の命名規則に従います.  
デフォルトでは `{ProjectRoot}/docs/decisions/` に保存されます.  
特定のファイルやディレクトリを保存先に指定して ADR を管理することも可能です.  
この場合は、CLAUDE.md や AGENT.md などのシステムファイルで ADRのデフォルト保存先を指定することを推奨します.  

## MADR フォーマット

ADR ファイルは [Structured MADR v4.0.0](https://adr.github.io/madr/) フォーマットに従って記録されます.  

## ライセンス

MIT
