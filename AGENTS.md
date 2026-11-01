# AGENTS.md

このファイルは、本リポジトリで作業するエージェント向けの基本情報をまとめたものです。

## プロジェクト概要

zv-marketplace は、Claude Code のプラグインを配布するためのマーケットプレイスです。マーケットプレイス名は `zv-plugins` です。

- プラグインの実体は持たず、各プラグインの GitHub リポジトリを参照するカタログ（`marketplace.json`）だけを管理します。
- 本リポジトリは GitHub の `zv-louis/zv-plugin-marketplace` にあります。
- ライセンスは MIT です。

## 登録しているプラグイン

| プラグイン名 | リポジトリ |
| --- | --- |
| `madr-manager` | `zv-louis/madr-manager` |
| `mktotp-mcp` | `zv-louis/mktotp` |
| `updsts-mcp` | `zv-louis/updsts` |

プラグイン名は、各リポジトリの `.claude-plugin/plugin.json` の `name` と同じです。リポジトリ名とは一致しないものがあります。

## ディレクトリ構成

```txt
.
├── .claude-plugin/
│   └── marketplace.json         # マーケットプレイスのカタログ
├── .claude/
│   └── CLAUDE.md                # AGENTS.md を読み込むだけのファイル
├── AGENTS.md                    # 本ファイル
├── README.md                    # 英語版 README
├── README_ja.md                 # 日本語版 README
├── LICENSE
└── zv-marketplace.code-workspace
```

## marketplace.json の書き方

プラグインのエントリは、次の形で書きます。

```json
{
  "name": "madr-manager",
  "description": "プラグインの説明",
  "source": {
    "source": "github",
    "repo": "zv-louis/madr-manager"
  }
}
```

- **`source` には GitHub のリポジトリを指定する。** 相対パスは使わず、`plugins/` のようなローカルのディレクトリにプラグインを置かない。そのため、`metadata.pluginRoot` は設定していない。
- **`version`、`author`、`license` は書かない。** 外部ソースのプラグインでは、各リポジトリの `plugin.json` の内容が使われる。marketplace.json にも書くと、バージョンを上げるたびに二重に更新することになる。
- **`description` だけは書く。** プラグインの一覧には marketplace.json の内容が表示され、インストール前は `plugin.json` を取得しないため。説明文を変えたら、marketplace.json も更新する。
- **`name` は `plugin.json` の `name` に合わせる。** インストールのコマンドは `/plugin install {name}@zv-plugins` になる。

### プラグインを追加する手順

1. 追加するリポジトリで、`.claude-plugin/plugin.json` がコミットされ、GitHub に push されていることを確認する。
2. marketplace.json の `plugins` に、上の形でエントリを追加する。
3. README.md と README_ja.md の「Plugins」「プラグイン」の一覧に、同じプラグインを追加する。
4. `claude plugin validate .` で marketplace.json を検証する。

## README の方針

- README.md（英語）と README_ja.md（日本語）は、同じ内容を保つ。片方を直したら、もう片方にも反映する。
- プラグインの一覧は、marketplace.json に登録している内容と一致させる。

## IDE のプラグイン検証

VSCode 拡張のプラグイン検証は、有効な属性（たとえばスキルファイルの `allowed-tools`）に警告を出すことがあります。
こうした警告に対応する前に、プラグインの仕様や、このリポジトリの他のスキルファイルと照らして、本当に無効かどうかを確認してください。
IDE の警告だけを根拠に、属性を削除したり変更したりしないでください。

## コミットメッセージ

`feat:`、`mod:`、`wip:` のように、先頭に変更の種類を付けます。
