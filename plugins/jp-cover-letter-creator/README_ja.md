# jp-cover-letter-creator

[English](README.md) | 日本語

日本語ビジネス送付状（案内状・添え状）を対話的に作成する Claude Code プラグインです。

<!-- TOC tocDepth:2..3 chapterDepth:2..6 -->

- [概要](#概要)
- [プロジェクト構成](#プロジェクト構成)
- [前提条件](#前提条件)
- [インストール](#インストール)
- [使い方](#使い方)
- [テンプレート仕様](#テンプレート仕様)
- [ライセンス](#ライセンス)

<!-- /TOC -->

## 概要

ユーザとの対話を通じて必要項目をヒアリングし、テンプレート仕様に基づいた送付状を docx ファイルとして出力します。

**ワークフロー:**  

1. テンプレート仕様の読み込み
2. ユーザへの必要項目ヒアリング（日付、宛先、差出人、件名、本文、記書き内容 等）
3. Markdown 形式での文書案作成・承認
4. docx ファイルの生成

## プロジェクト構成

```txt
.
├── .claude-plugin/
│   └── plugin.json              # プラグインマニフェスト
├── skills/
│   └── creating-jp-cover-letter/
│       ├── SKILL.md             # スキル定義
│       └── references/
│           └── cover_letter_template_spec.md  # 文書テンプレート仕様
├── LICENSE
├── README.md
└── README_ja.md
```

## 前提条件

| ツール               | 用途                                   |
|-------------------|----------------------------------------|
| **Node.js / npm** | docx スキル経由での文書生成                 |
| **uv**            | Python スクリプトの実行環境                  |
| **docx スキル**      | docx ファイルの生成（`document-skills:docx`） |

## インストール

マーケットプレイスからjp-cover-letter-creatorをインストールします.

```bash
# プラグインのインストール
/plugin install jp-cover-letter-creator@zv-plugins
```

依存スキルをインストールします.  
anthropic公式のマーケットプレイスから document-skills をインストールしてください.  

```bash
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills
```

## 使い方

Claude Code で以下のように呼び出します:

```txt
送付状を作成して
```

対話形式で必要な情報（宛先、差出人、件名、本文など）を入力すると、テンプレート仕様に準拠した docx ファイルが生成されます。

## テンプレート仕様

生成される文書は以下の仕様に準拠します:

- **用紙**: A4 縦、余白 上35mm/下30mm/左25mm/右25mm
- **フォント**: 本文 MS P明朝、タイトル HGPゴシックM、欧文 Arial
- **レイアウト**: 日付・差出人・結語は右揃え、タイトル・記は中央揃え、本文は両端揃え

詳細は [cover_letter_template_spec.md](skills/creating-jp-cover-letter/references/cover_letter_template_spec.md) を参照してください。

## ライセンス

MIT
