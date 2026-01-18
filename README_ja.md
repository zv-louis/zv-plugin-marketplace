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
├── README_ja.md
└── zv-marketplace.code-workspace
```

## 使い方

### マーケットプレイスの追加

Claude Code にこのマーケットプレイスを追加します.  
Claude Code のコンソールで以下のコマンドを実行します.  

```bash
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

マーケットプレイス追加後、マーケットプレイスで提供されているプラグインを確認できるようになります.  

```bash
/plugin marketplace list
```

### プラグインのインストール

マーケットプレイスからプラグインを選択してインストールします.  

zv-louis/sync-agent-config プラグインをインストールする例  

```bash
/plugin install sync-agent-config@zv-plugin-marketplace
```

## Plugins

- [sync-agent-config](https://github.com/zv-louis/sync-agent-config)  
  複数のエージェントツール間でAgentのSkill/MCP設定を同期するためのスキルセット.

## ライセンス

MIT
