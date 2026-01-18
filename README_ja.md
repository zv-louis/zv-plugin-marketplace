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
│   ├── sync-agent-config/
│   └── jp-cover-letter-creator/
├── README_ja.md
└── zv-marketplace.code-workspace
```

## 使い方

### マーケットプレイスの追加

Claude Code にこのマーケットプレイスを追加します.  
Claude Code のコンソールで以下のコマンドを実行します.  

```bash
# zv-louis/zv-plugin-marketplace をマーケットプレイスに追加する例
/plugin marketplace add zv-louis/zv-plugin-marketplace
# もしくは
/plugin marketplace add {このリポジトリのURL}
```

マーケットプレイス追加後、マーケットプレイスで提供されているプラグインを確認できるようになります.  

```bash
/plugin marketplace list
```

### プラグインのインストール

マーケットプレイスからプラグインを選択してインストールします.  

zv-louis/sync-agent-config プラグインをインストールする例  

```bash
/plugin install sync-agent-config@zv-plugins
```

## Plugins

- [sync-agent-config](plugins/sync-agent-config)  
  複数のエージェントツール間でAgentの設定を同期するためのスキルセット.  
- [jp-cover-letter-creator](plugins/jp-cover-letter-creator)  
  マークダウンプレビューとWord文書(docx)エクスポート機能を備えた、日本語ビジネス送付状の対話型作成ツール.  

## ライセンス

MIT
