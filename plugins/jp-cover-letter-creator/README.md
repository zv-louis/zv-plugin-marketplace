# jp-cover-letter-creator

English | [日本語](README_ja.md)

A Claude Code plugin for interactively creating Japanese business cover letters (送付状 / 案内状 / 添え状).

<!-- TOC tocDepth:2..3 chapterDepth:2..6 -->

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Template Specification](#template-specification)
- [License](#license)

<!-- /TOC -->

## Overview

This plugin guides users through an interactive dialogue to gather the necessary information and generates a cover letter as a docx file based on a predefined template specification.

**Workflow:**

1. Load the template specification
2. Gather required information from the user (date, recipient, sender, subject, body, itemized content, etc.)
3. Draft the document in Markdown format for user approval
4. Generate the docx file

## Project Structure

```txt
.
├── .claude-plugin/
│   └── plugin.json              # Plugin manifest
├── skills/
│   └── creating-jp-cover-letter/
│       ├── SKILL.md             # Skill definition
│       └── references/
│           └── cover_letter_template_spec.md  # Document template specification
├── LICENSE
├── README.md
└── README_ja.md
```

## Prerequisites

| Tool              | Purpose                                      |
|-------------------|----------------------------------------------|
| **Node.js / npm** | Document generation via the docx skill       |
| **uv**            | Python script execution environment          |
| **docx skill**    | Docx file generation (`document-skills:docx`)|

## Installation

Install jp-cover-letter-creator from the marketplace.

```bash
# Install the plugin
/plugin install jp-cover-letter-creator@zv-plugins
```

Install the dependent skill.
Install document-skills from Anthropic's official marketplace.

```bash
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills
```

## Usage

Invoke the plugin in Claude Code:

```txt
送付状を作成して
```

After providing the required information (recipient, sender, subject, body, etc.) through the interactive dialogue, a docx file conforming to the template specification will be generated.

## Template Specification

The generated document follows these specifications:

- **Paper**: A4 portrait, margins: top 35mm / bottom 30mm / left 25mm / right 25mm
- **Fonts**: Body: MS PMincho, Title: HGPGothicM, Western: Arial
- **Layout**: Date, sender, and closing phrase are right-aligned; title and "記" are center-aligned; body text is justified

See [cover_letter_template_spec.md](skills/creating-jp-cover-letter/references/cover_letter_template_spec.md) for details.

## License

[MIT](LICENSE)
