# ZV Plugin Marketplace

[English](README.md) | 日本語

Claude Code Plugin Marketplace

## 概要

このリポジトリは Claude Code プラグインを配布するためのマーケットプレイスです.  
各リポジトリで定義されているpluginをインストールするための情報を配置しています.  

## レイアウト

```txt
./
├── .claude-plugin/
│   └── marketplace.json        # マーケットプレイスカタログ
├── plugins/
│   ├── jp-cover-letter-creator/
│   ├── madr-manager/
│   └── sync-agent-config/
├── LICENSE
├── README.md
├── README_ja.md
└── zv-marketplace.code-workspace
```

## 使い方

### マーケットプレイスの追加

Claude Code にこのマーケットプレイスを追加します.  
Claude Code のコンソールで以下のコマンドを実行します.  

```bash
/plugin marketplace add {このリポジトリのURL}
# もしくは
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

マーケットプレイス追加後、マーケットプレイスで提供されているプラグインを確認できるようになります.  

```bash
/plugin marketplace list
```

### プラグインのインストール

マーケットプレイスからプラグインをインストールします.  

```bash
/plugin install {プラグイン名}@zv-plugins
```

## Plugins

- [jp-cover-letter-creator](plugins/jp-cover-letter-creator)
  マークダウンプレビューとWord文書(docx)エクスポート機能を備えた、日本語ビジネス送付状の対話型作成ツール.
- [madr-manager](plugins/madr-manager)
  Structured MADR v4.0.0 フォーマットに従って ADR ファイルを対話的に作成・一覧表示・管理するツール.
- [sync-agent-config](plugins/sync-agent-config)
  複数のエージェントツール間でAgentの設定を同期するためのスキルセット.

## ライセンス

MIT
