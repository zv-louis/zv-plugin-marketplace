---
name: creating-jp-cover-letter
description: 日本語ビジネス送付状（案内状・添え状）を作成するスキル。ユーザから必要項目をヒアリングし、テンプレート仕様に基づいた文書案を作成・承認後、docx ファイルとして出力する。送付状、案内状、添え状、カバーレターの作成時に使用する。
allowed-tools: Bash(node --version), Bash(npm --version), Bash(uv --version), Bash(mktemp *), Bash(uv venv *), Bash(uv pip install *), Bash(npm install *), Bash(npx *), Bash(*/jp-cover-letter-*/.venv/Scripts/python* *), Bash(*/jp-cover-letter-*/.venv/bin/python* *), Bash(rm -rf */jp-cover-letter-*)
---

# Japanese Cover Letter Skill

**IMPORTANT: All user-facing communication (questions, messages, document drafts, error messages) MUST be in Japanese.**

## Overview

Interactively create Japanese business cover letters (送付状 / 案内状 / 添え状).
Follows the template spec (`references/cover_letter_template_spec.md`) through a workflow of: hearing requirements -> drafting -> approval -> docx output.

## Prerequisites

### 1. Node.js / npm

This skill uses Node.js via the docx skill. At workflow start, verify `node` and `npm` are available (`node --version` and `npm --version`).

If unavailable, **abort the workflow** and show the user this message:

> Node.js / npm が見つかりません。docx ファイルの生成に必要です。
>
> 以下のいずれかの方法でインストールしてください:
>
> - **公式サイト**: https://nodejs.org/ から LTS 版をダウンロード・インストール
> - **winget** (Windows): `winget install OpenJS.NodeJS.LTS`
> - **brew** (macOS/Linux): `brew install node`
>
> インストール後、ターミナルを再起動してから再度このスキルを実行してください。

### 2. uv (Python runtime)

This skill uses `uv` for Python script execution. At workflow start, verify `uv` is available (`uv --version`).

If unavailable, **abort the workflow** and show the user this message:

> uv が見つかりません。Python スクリプトの実行環境として必要です。
>
> 以下のいずれかの方法でインストールしてください:
>
> - **Windows** (PowerShell): `irm https://astral.sh/uv/install.ps1 | iex`
> - **macOS/Linux**: `curl -LsSf https://astral.sh/uv/install.sh | sh`
> - **pip**: `pip install uv`
>
> インストール後、ターミナルを再起動してから再度このスキルを実行してください。

### 3. docx skill

This skill requires the **docx skill** (`document-skills:docx`) for file generation.

At workflow start, verify that `docx` (`document-skills:docx` or `example-skills:docx`) is in the available skills list.

If unavailable, **abort the workflow** and show the user this message:

> docx スキルが見つかりません。docx ファイルの生成には docx スキルが必要です。
>
> 以下のコマンドで **document-skills** プラグインをインストールしてください:
>
> ```
> claude skills add anthropic-agent-skills/document-skills
> ```
>
> インストール後、再度このスキルを実行してください。

## Workflow

### Step 1: Load template spec

Read `references/cover_letter_template_spec.md` to understand the document layout, fonts, and styles.

### Step 2: Gather required information from user

Collect the following items from the user via AskUserQuestion or conversation. Continue until all items are filled.

#### Required fields

| # | Field | Description | Example |
|---|-------|-------------|---------|
| 1 | Date | Document date (YYYY年M月D日) | 2024年11月24日 |
| 2 | Recipient dept | Organization/department name | 〇〇株式会社 総務部 総務ユニット |
| 3 | Recipient name | Individual name with title, or 各位 | 部長 田中太郎 様 / 保護者 各位 |
| 4 | Sender dept | Sender's organization/department | 〇〇株式会社 〇〇部 〇〇課 |
| 5 | Sender name | Sender's name (no honorific) | 田中 太郎 |
| 6 | Title | Document subject line | 借用開発機材送付の件 |
| 7 | Body summary | Purpose/background of the letter | 会議の開催案内、機材送付の連絡 等 |
| 8 | Detail items | Content for the 記 section | 日時、場所、持ち物、送付物リスト 等 |

#### Additional checks

- **Same organization?** If sender and recipient share an organization, omit the org name.
- **Internal vs external**: Determines greeting formality.
  - Internal: simple greeting (e.g. お疲れ様です。)
  - External: seasonal greeting with formal tone
- **Closing word**: Default to 敬具 unless specified otherwise.
- **Detail format**: Propose bullet list, numbered list, or item table based on content.

#### Hearing guidelines

- If the user does not specify a date, ask whether to use today's date.
- If any field is unclear, show examples and re-confirm.
- Group questions contextually rather than asking all at once.

### Step 3: Draft and approval

Create a Markdown draft with the following layout and present it to the user:

```markdown
                                        YYYY年M月D日

宛先部署名
宛先名

                                差出人所属部署名
                                    差出人名

            文書タイトル（下線付き）

　挨拶文
　要件文
                                        結語

                    －記－

要件内容（箇条書き・番号付きリスト等）

                                        以上
```

- Present the draft and ask the user for corrections.
- Apply any requested changes and seek approval again.
- Repeat until approved.

### Step 4: Generate docx

After approval, invoke the **docx skill** to create the docx file.

Follow `references/cover_letter_template_spec.md` strictly:

- **Page**: A4 portrait, margins top 35mm / bottom 30mm / left 25mm / right 25mm
- **Fonts**: body MS P明朝, title HGPゴシックM, latin Arial
- **Font sizes**: date 10.5pt, recipient dept 14pt, recipient name 12pt, sender 10.5pt, title 14pt (underlined), body 11pt, list items 10.5pt
- **Alignment**: date/sender/closing right-aligned, title/記 centered, body justified
- **Closing style**: Closing (right-aligned)
- **記 style**: Note Heading (centered)
- **Numbered list**: (1), (2), (3)... format

## Mandatory rules

- **Temp files**: Always create a temp directory under the OS temporary directory using `mktemp -d -t jp-cover-letter-XXXXXX`. The `jp-cover-letter-` prefix is mandatory — the `allowed-tools` permissions are scoped to this prefix.
- **Python runtime**: Use `uv` to create a venv inside the temp directory and run all Python scripts through it. If `uv` is unavailable, prompt the user to install it.
- **Cleanup**: After completion, delete the temp directory entirely with `rm -rf <temp-dir>`. Leave only the final docx output at the user-specified location or the working directory.

### Constraint inheritance for child skills

When invoking child skills (e.g. docx skill), **all mandatory rules above remain in effect**.

Key points:

- **Python execution in child skills**: Even if the child skill instructs `python script.py` or `pip install`, use the venv created by this skill via `uv`.
  - `pip install package` -> `uv pip install package --python .venv/Scripts/python.exe` (or OS-appropriate path)
  - `python script.py` -> `.venv/Scripts/python.exe script.py` (or OS-appropriate path)
- **Temp file rules also apply** to child skills. Any intermediate files they generate must go in the temp directory and be cleaned up.

## Resources

### references/

- **cover_letter_template_spec.md**: Document template spec covering page setup, fonts, styles, and layout patterns. Adhere to this spec when generating docx output.
