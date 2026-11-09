# ZV Plugin Marketplace

[English](README.md) | 日本語

Claude Code Plugin Marketplace

## 概要

このリポジトリは Claude Code プラグインを配布するためのマーケットプレイスです.  
各リポジトリで定義されているプラグインをインストールするための情報を配置しています.  

## レイアウト

```txt
./
├── .claude-plugin/
│   └── marketplace.json        # マーケットプレイスカタログ
├── LICENSE
├── README.md
├── README_ja.md
└── zv-marketplace.code-workspace
```

## 使い方

### マーケットプレイスの追加

Claude Code のコンソールで以下のコマンドを実行して、このマーケットプレイスを追加します.  

```bash
/plugin marketplace add {このリポジトリのURL}
# もしくは
/plugin marketplace add zv-louis/zv-plugin-marketplace
```

マーケットプレイスを追加すると、提供されているプラグインを確認できます.  

```bash
/plugin
```

### プラグインのインストール

マーケットプレイスからプラグインをインストールします.  

```bash
/plugin install {プラグイン名}@zv-plugins
```

## プラグイン

各プラグインは、それぞれの GitHub リポジトリを参照しています.  

- [madr-manager](https://github.com/zv-louis/madr-manager)
  Structured MADR v4.0.0 フォーマットに従って ADR ファイルを対話的に作成・一覧表示・管理するツール.
- [mktotp-mcp](https://github.com/zv-louis/mktotp)
  TOTP(時間ベースのワンタイムパスワード)のシークレットを対話的に作成・一覧表示・管理し、ワンタイムパスワードを生成するツール.
- [updsts-mcp](https://github.com/zv-louis/updsts)
  既存の AWS プロファイルを使って AWS STS 認証情報を取得・更新するツール.
- [exam-exp-gen](https://github.com/zv-louis/exam-exp-gen)
  試験問題(PDF・画像・テキスト)を読み込み、解説を markdown / ODT / DOCX で生成するツール.

## ライセンス

MIT
