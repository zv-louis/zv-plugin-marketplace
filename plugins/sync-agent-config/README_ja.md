# sync-agent-config

[English](README.md) | 日本語

異なるAgentツール間でAgent設定（MCPサーバー、スキル）を同期するためのClaude Codeプラグインです。

## 概要

このプロジェクトは、Claude Code、VSCode、Claude Desktop、Codex、Cursor、Gemini CLI、Antigravityなど、異なるAgent環境間で設定を同期できるスキルを提供します。  
ソースAgentツールから構成を読み取り、ターゲットAgentツールに適用することで、複数の開発環境で一貫した設定を確保します。  

### 含まれるスキル

- **sync-mcp-config**: MCPサーバー設定を同期
- **sync-skill-config**: スキル設定を同期

## 機能

- **クロスプラットフォーム対応**:
  Windows、macOS、Linuxで動作します
- **マルチツール互換性**:
  以下を含む様々なAgentツールをサポート:
  - Claude Code
  - VSCode
  - Claude Desktop
  - Codex CLI
  - Cursor
  - Gemini CLI
  - Antigravity
- **安全な同期**:
  変更を適用する前にバックアップを作成し、構成を検証します
- **インテリジェントな処理**:
  異なるAgentツール間のフォーマットの違いを自動的に処理します
- **Web検索統合**:
  ドキュメントが利用できない場合、自動的に構成仕様を検索します

## インストール

### Claude Code へのインストール

GitHubリポジトリから直接Claude Codeにプラグインをインストールできます。

1. Claude Codeを起動します

2. 以下のコマンドを実行してプラグインのマーケットプレイスを追加します.

```bash
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

マーケットプレイスを追加したら、マーケットプレイスからプラグインをインストールします.  

```bash
/plugin install sync-agent-config@zv-plugins
```
  
3. インストールが完了すると、スキルが利用可能になります

## 使用方法

Agentにツール間で設定を同期するよう指示するだけです:

**MCP設定の同期例:**

- 「Claude CodeのMCP設定をCodexに適用したい」
- 「VSCodeからClaude DesktopにMCP構成を同期して」
- 「Claude DesktopからClaude CodeにMCPサーバー設定をコピーして」

**スキル設定の同期例:**

- 「Claude Codeのスキル設定をCursorに同期して」
- 「VSCodeからGemini CLIにスキル構成をコピーして」

スキルは以下を実行します:

1. オペレーティングシステム環境を確認
2. ソースAgentツールの構成を読み取り
3. 利用可能な設定をチェック
4. ターゲットAgentツールに設定を適用
5. 構成を検証

## 動作の仕組み

1. **OS環境チェック**:
  オペレーティングシステムを検出し、適切なパスを設定
2. **構成の検証**:
  ソースとターゲットの両方の構成フォーマットを読み取り理解
3. **サーバー検出**:
  ソース構成に登録されているすべてのMCPサーバーを識別
4. **フォーマット変換**:
  ターゲットツールのフォーマットに合わせて自動的に設定を変換
5. **安全な適用**:
  変更を加える前に既存の構成をバックアップ
6. **検証**:
  新しい構成が有効であることを確認

## 構成ファイルの場所

スキルは、オペレーティングシステムとAgentツールに基づいて構成ファイルのパスを自動的に検出します。  
サポートされている各Agentツールのリファレンスドキュメントは、各スキルの`reference/`ディレクトリにあります:  

- MCP設定: [`skills/sync-mcp-config/reference/`](skills/sync-mcp-config/reference/)
- スキル設定: [`skills/sync-skill-config/reference/`](skills/sync-skill-config/reference/)

## プラグインについて

### ファイルレイアウト

```txt
sync-agent-config/
├── .claude-plugin/
│   └── plugin.json          # プラグインマニフェスト
├── skills/
│   ├── sync-mcp-config/     # MCP設定同期スキル
│   │   ├── SKILL.md         # スキル定義
│   │   └── reference/       # 構成リファレンスドキュメント
│   │       ├── antigravity.md
│   │       ├── claude_code.md
│   │       ├── claude_desktop.md
│   │       ├── codex_cli.md
│   │       ├── cursor.md
│   │       ├── gemini_cli.md
│   │       └── vscode.md
│   └── sync-skill-config/   # スキル設定同期スキル
│       ├── SKILL.md         # スキル定義
│       └── reference/       # 構成リファレンスドキュメント
│           ├── antigravity.md
│           ├── claude_code.md
│           ├── codex_cli.md
│           ├── cursor.md
│           ├── gemini_cli.md
│           └── vscode.md
├── LICENSE
├── README.md
└── README_ja.md
```

## 誤動作に対するガードレール

- **バックアップ作成**:
  変更を加える前に既存の構成を自動的にバックアップ.
- **競合検出**:
  サーバーが既に登録されている場合を識別し、ユーザーの確認を求めます.
- **検証**:
  変更後に構成ファイルの整合性をチェック.
- **読み取り専用モード**:
  MCPサーバ以外の設定も含むファイルでは、MCPサーバー設定のみを変更し、他の構成には触れないようにしています.

## エラーハンドリング

スキルは様々なエラーシナリオを処理します:

- ソース構成ファイルの欠落
- 書き込み保護されたターゲットファイル
- 無効な構成フォーマット
- 異なるAgentツール間での互換性のない設定

## ライセンス

MITライセンスの下でライセンスされています.  
詳細は`LICENSE`ファイルを参照してください.
