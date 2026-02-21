# Structured MADR 仕様書

> MADR = **M**arkdown **A**rchitectural **D**ecision **R**ecords (v4.0.0)

---

## 概要

**MADR** は、アーキテクチャ上の設計決定を Markdown で記録するための軽量フォーマット。「decisions that matter（重要な決定）」をもじった名称（発音: [ˈmæɾɚ]）。

**Structured MADR** とは、MADR が提供する複数テンプレート変種の中でも、**全セクション（必須 + オプション）を含むフルテンプレート**（`adr-template.md`）を指す。

### テンプレート変種一覧

| ファイル名 | セクション | ガイダンス文 |
|---|---|---|
| `adr-template.md` | 全セクション（必須 + オプション）| あり |
| `adr-template-minimal.md` | 必須セクションのみ | あり |
| `adr-template-bare.md` | 全セクション | なし |
| `adr-template-bare-minimal.md` | 必須セクションのみ | なし |

---

## ファイル命名規則・配置

```
docs/decisions/
├── 0001-use-postgresql.md
├── 0002-use-graphql-api.md
└── 0003-...
```

- パターン: `NNNN-title-with-dashes.md`（4桁連番）
- 配置場所: `docs/decisions/`（コードと同じリポジトリに格納）
- 大規模プロジェクトではサブディレクトリで領域ごとに管理可

---

## ステータス値とライフサイクル

```
proposed --> accepted --> deprecated --> (歴史的記録として保持)
         --> rejected --> (歴史的記録として保持)
accepted --> superseded by ADR-XXXX --> (歴史的記録として保持)
```

| ステータス | 意味 |
|---|---|
| `proposed` | 議論中、未確定 |
| `accepted` | 合意済み、有効 |
| `rejected` | 評価の結果、不採用 |
| `deprecated` | かつて有効だったが、現在は非推奨 |
| `superseded by ADR-XXXX` | 別の ADR に置き換えられた |

> **注意:** ADR は削除しない。却下・廃止されたものも歴史的記録として保持する。

---

## テンプレート全体構造

```markdown
---
status: "{proposed | rejected | accepted | deprecated | superseded by ADR-XXXX}"
date: {YYYY-MM-DD}
decision-makers: {意思決定に関与した全員}
consulted: {意見を求めた人（双方向コミュニケーション）}
informed: {進捗を共有する人（一方向コミュニケーション）}
---

# {短いタイトル：問題と解決策を表す}

## Context and Problem Statement

{問題の背景と、なぜこの決定が必要なのかを記述}

## Decision Drivers

* {決定要因 1}
* {決定要因 2}

## Considered Options

* {選択肢 1}
* {選択肢 2}
* {選択肢 3}

## Decision Outcome

Chosen option: "{選択した選択肢}", because {理由}.

### Consequences

* Good, because {良い影響}
* Bad, because {悪い影響}

### Confirmation

{実装・準拠の確認方法}

## Pros and Cons of the Options

### {選択肢 1}

{説明・例・参照リンク（任意）}

* Good, because {引数 A}
* Neutral, because {引数 B}
* Bad, because {引数 C}

### {選択肢 2}

* Good, because {引数 A}
* Bad, because {引数 B}

## More Information

{補足情報・関連 ADR リンク・外部リソース・見直し時期など}
```

---

## 各セクション詳細

### YAML Front Matter（オプション）

```yaml
---
status: "proposed"
date: 2025-01-15
decision-makers: Alice, Bob
consulted: Charlie (アーキテクト)
informed: チーム全員
---
```

- **目的:** 機械可読なメタデータ。RACI モデルに対応
  - `decision-makers` → Responsible / Accountable
  - `consulted` → Consulted（双方向）
  - `informed` → Informed（一方向）
- **省略可:** 不要なら Front Matter ブロック全体を削除

---

### H1: タイトル（必須）

```markdown
# Use PostgreSQL for relational data storage
```

- 問題と解決策の両方を表す簡潔なフレーズ
- 推奨パターン: `Use [Solution] for [Problem]` / `Do not use [X] for [Y]`

---

### H2: Context and Problem Statement（必須）

```markdown
## Context and Problem Statement

Which database should we use for storing relational data?
We need a solution that supports ACID transactions and complex queries.
```

- 意思決定が必要になった背景と問題を記述
- 疑問文形式で書くと議論を促しやすい
- イシュートラッカーへのリンクを含めてもよい

---

### H2: Decision Drivers（オプション）

```markdown
## Decision Drivers

* ACID トランザクションが必要
* チームが SQL に精通している
* オープンソースであること
* 水平スケーリングは当面不要
```

- 意思決定を左右する力・制約・品質要件を列挙
- 後続の Pros/Cons 評価の基準となる

---

### H2: Considered Options（必須）

```markdown
## Considered Options

* PostgreSQL
* MySQL
* MongoDB
```

- 実際に検討した全選択肢を列挙
- 採用した選択肢を最初に書く慣習を推奨（プロジェクト全体で統一）
- 抽象レベルを揃える（技術選択とデザインパターンを混在させない）

---

### H2: Decision Outcome（必須）

```markdown
## Decision Outcome

Chosen option: "PostgreSQL", because it satisfies our ACID requirements and the team already has deep expertise with it (see "Pros and Cons" below).
```

- 決定内容を明確に宣言
- Decision Drivers への参照、または Pros/Cons への参照で理由を示す
- **意図的に Pros/Cons より前に配置**：読者がスクロールせずに決定を把握できる

---

### H3: Consequences（オプション、Decision Outcome のサブセクション）

```markdown
### Consequences

* Good, because 複雑なクエリが書きやすい
* Good, because チームの学習コストが低い
* Bad, because 水平スケーリングが困難
* Neutral, because マネージドサービス（RDS 等）が必要
```

- 採用した選択肢がもたらす影響を記録
- `Good, because` / `Bad, because` / `Neutral, because` の形式を統一
- **良い影響だけでなく悪い影響も必ず記録する**

---

### H3: Confirmation（オプション、Decision Outcome のサブセクション）

```markdown
### Confirmation

* `package.json` の dependencies に `pg` のみが含まれていることを確認
* コードレビューで ORM が PostgreSQL 専用機能のみ使用しているか確認
* ArchUnit / 静的解析ツールで依存関係を自動チェック
```

- 決定が実装で遵守されているかを確認する方法
- v4.0.0 で「Validation」から「Confirmation」に改名
- 自動化（フィットネス関数、CI チェック）が強く推奨される
- オプション扱いだが、**多くの ADR で使用されるため実質的に推奨**

---

### H2: Pros and Cons of the Options（オプション）

```markdown
## Pros and Cons of the Options

### PostgreSQL

https://www.postgresql.org/

* Good, because ACID 完全準拠
* Good, because 豊富な拡張機能
* Good, because チームの知識が豊富
* Neutral, because 垂直スケーリングのみ
* Bad, because 水平スケーリングが困難

### MySQL

* Good, because 広く普及している
* Good, because 水平スケーリングオプションあり
* Bad, because ACID 準拠が PostgreSQL ほど厳密でない
* Bad, because チームの経験が少ない

### MongoDB

* Good, because スキーマレスで柔軟
* Bad, because ACID トランザクションが複雑
* Bad, because リレーショナルデータに不向き
```

- **Structured MADR の核心部分**：比較検討プロセスを完全に可視化
- 各選択肢に H3 サブセクションを作成（Considered Options の順番と一致させる）
- 各引数は `Good,` / `Neutral,` / `Bad,` + `because` で記述
- 選択肢ごとにオプションで説明文・例・URL を先頭に追加できる

---

### H2: More Information（オプション）

```markdown
## More Information

* [PostgreSQL vs MySQL 比較記事](https://example.com/comparison)
* ADR-0005 に関連（データモデル設計）
* 6 ヶ月後（2025 年 7 月）に水平スケーリング要件を再評価する
* チーム全員が Slack #arch-decisions で合意済み
```

- 補足情報・証拠・外部リンクを格納
- 関連 ADR へのクロスリファレンス
- 決定の見直し時期・条件
- チームの合意プロセスの記録

---

## 必須 vs オプション セクション早見表

| セクション | 要否 | 備考 |
|---|---|---|
| YAML Front Matter | オプション | 不要なら省略可 |
| タイトル（H1） | **必須** | |
| Context and Problem Statement | **必須** | |
| Decision Drivers | オプション | 文脈から明らかなら省略可 |
| Considered Options | **必須** | |
| Decision Outcome | **必須** | |
| └ Consequences | オプション | 強く推奨 |
| └ Confirmation | オプション | 強く推奨（多数の ADR で使用） |
| Pros and Cons of the Options | オプション | Structured MADR の核心 |
| More Information | オプション | 補足・クロスリファレンス用 |

---

## ベストプラクティス

### 記述品質

- 問題を疑問文で書く（「どのフレームワークを使うべきか？」）
- 選択肢の抽象レベルを揃える
- 良い影響・悪い影響の両方を記録する
- `Neutral, because` を活用して完全な分析を示す
- 採用した選択肢を Considered Options の先頭に書く（プロジェクト内で統一）

### プロセス

- ADR は個人作業でなくチームで共同作成
- コードレビューと同様に ADR もレビューする
- プロジェクト開始時にテンプレート変種を統一する（後から変更はコスト大）
- **ADR は絶対に削除しない**（却下・廃止済みも歴史的記録として保持）
- 上書き時は `superseded by ADR-XXXX` で明示的にリンクする

### ツール

```bash
# npm 経由でインストール
npm install madr
mkdir -p docs/decisions
cp node_modules/madr/template/* docs/decisions/
```

- `markdownlint` + MADR 提供の設定でフォーマット統一
- ArchUnit 等の静的解析ツールで Confirmation を自動化

---

## 完全な記述例

```markdown
---
status: "accepted"
date: 2025-01-15
decision-makers: Alice, Bob
consulted: Charlie (シニアアーキテクト)
informed: 開発チーム全員
---

# Use Plain JUnit5 for Advanced Test Assertions

## Context and Problem Statement

テスト内で読みやすいアサーションをどう書くべきか？
特に複雑なテストケースで可読性を維持するにはどのライブラリが最適か？

## Decision Drivers

* コードベースに不慣れな開発者でも読めること
* 外部依存を最小限にすること
* 「一般常識」として知られていること（オンボーディングコストの削減）

## Considered Options

* Plain JUnit5
* Hamcrest
* AssertJ

## Decision Outcome

Chosen option: "Plain JUnit5", because comes out best (see "Pros and Cons of the Options" below).

### Consequences

* Good, because テストが読みやすくなる
* Good, because テストの記述が簡単
* Bad, because 複雑なアサーションは読みにくくなる場合がある

### Confirmation

* プロジェクトの依存関係に JUnit5 のみが含まれることを確認
* スプリントレビューで JUnit5 の使用感についてフィードバック収集
* 今後の決定再評価時期: 次回メジャーバージョンアップ時

## Pros and Cons of the Options

### Plain JUnit5

https://junit.org/junit5/docs/current/user-guide/

* Good, because Java エンジニアの「常識」として広く知られている
* Bad, because 複雑なアサーションは読みにくくなりやすい
* Bad, because Fluent API がない

### Hamcrest

https://github.com/hamcrest/JavaHamcrest

* Good, because 高度なマッチャー（`contains` 等）が使える
* Bad, because 完全な Fluent API ではない
* Bad, because 学習コストが高い

### AssertJ

https://joel-costigliola.github.io/assertj/

* Good, because Fluent API でチェーン記述できる
* Good, because 部分文字列テストなど柔軟な検証が可能
* Bad, because 一般的でないため、新規参加者の学習コストが高い
* Bad, because テストケースの書き方がバラつきやすい

## More Information

* [HamcrestとAssertJの比較（ドイツ語）](https://www.sigs-datacom.de/uploads/tx_dmjournals/philipp_JS_06_15_gRfN.pdf)
* ADR-0004（テスト戦略）と関連
```

---

## 参考リソース

- [MADR 公式サイト](https://adr.github.io/madr/)
- [GitHub リポジトリ (adr/madr)](https://github.com/adr/madr)
- [MADR テンプレート解説記事 (ozimmer.ch)](https://ozimmer.ch/practices/2022/11/22/MADRTemplatePrimer.html)
- [論文: Markdown Architectural Decision Records (CEUR-WS)](https://ceur-ws.org/Vol-2072/paper9.pdf)
