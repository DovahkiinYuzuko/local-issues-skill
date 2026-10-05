# local-issues-skill

ローカル環境でのIssue管理とロードマップ運用を行うAIエージェント向けスキル / Agent skill for managing local issues and roadmaps in development environments

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square&logo=opensourceinitiative&logoColor=white)](./LICENSE.MIT)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

[日本語](#日本語) | [English](#english)

## 日本語

### 概要
`local-issues-skill` は、AIエージェントとの協調開発において、タスクや進捗状況をローカルリポジトリ内で完結して管理するためのエージェントスキルです。外部の課題管理サービスを使用せず、MarkdownファイルとGitブランチのライフサイクルによって安全かつ見通しの良い開発フローを提供します。

### インストール

```bash
npx skills add https://github.com/DovahkiinYuzuko/local-issues-skill
```

### 主な特徴
- **ディレクトリベースのステータス管理**: `docs/local-issues/` 配下の `not-started/`、`wip/`、`done/` ディレクトリ間でファイルを移動させることで、ファイルツリーから即座に進捗状態を把握できます。
- **Gitブランチと連動した安全設計**: 各Issueごとにブランチを切り、動作検証およびユーザーの承認を経てからのみマージおよび `done/` への移動を許可するワークフローを強制します。
- **統括ロードマップとの同期**: 全体の進捗を可視化する `ROADMAP.md` を内部管理用として保持し、必要に応じて外部公開用のロードマップへ集約・出力させることも可能です。
- **サブIssue対応**: 作業中に発生した派生タスクは、大元のIssueファイル内への追記と小数点付きブランチ（例: `issue-3.1-`）によって管理コストを抑えながら追跡できます。

> [!NOTE]
> 現在内部用の`ROADMAP.md`のみ細かいフォーマットを指定していますが、`issue.md`や外部用の`ROADMAP.md`のフォーマット指定などはあまりしていません。環境に合わせて改造することをおすすめします。

### ディレクトリ構造
```text
docs/
└── local-issues/
    ├── ROADMAP.md
    ├── not-started/
    │   └── issue-{num}-{task}.md
    ├── wip/
    └── done/
```

### 使い方
1. AIエージェントに本スキルを読み込ませます。
2. 機能追加や不具合修正の相談を行うと、エージェントが `docs/local-issues/not-started/issue-{num}-{やること}.md` を作成し、`ROADMAP.md` を更新します。
3. 着手時にファイルを `wip/` に移動し、対応するGitブランチで実装を進めます。
4. 検証完了およびユーザーの承認後、ブランチをマージしてファイルを `done/` に移動します。

### LICENSE
[MIT](./LICENSE.MIT)

---

## English

### Overview
`local-issues-skill` is an agent skill designed for AI-assisted development to manage tasks and progress locally within a repository. Without relying on external issue-tracking services, it provides a safe and transparent development workflow using Markdown files and Git branch lifecycles.

### Install

```bash
npx skills add https://github.com/DovahkiinYuzuko/local-issues-skill
```

### Key Features
- **Directory-Based Status Tracking**: By moving files between the `not-started/`, `wip/`, and `done/` directories under `docs/local-issues/`, progress can be instantly identified via the file tree.
- **Git Branch Lifecycle Safety**: Creates a dedicated branch for each issue, enforcing a workflow where merging to the default branch and moving to `done/` strictly requires operational verification and user approval.
- **Master Roadmap Synchronization**: Maintains an internal `ROADMAP.md` to track overall progress, with the option to format and export a public-facing roadmap at the repository root.
- **Sub-Issue Support**: Additional tasks arising during implementation are tracked by appending to the parent issue file and creating decimal-numbered branches (e.g., `issue-3.1-`), minimizing management overhead.

> [!NOTE]
> Currently, a detailed format is only specified for the internal `ROADMAP.md`, while strict templates are not enforced for `issue.md` or the public-facing `ROADMAP.md`. We recommend customizing them to best fit your development environment.

### Directory Structure
```text
docs/
└── local-issues/
    ├── ROADMAP.md
    ├── not-started/
    │   └── issue-{num}-{task}.md
    ├── wip/
    └── done/
```

### Usage
1. Load this skill into the AI agent.
2. When discussing feature requests or bug fixes, the agent creates `docs/local-issues/not-started/issue-{num}-{task}.md` and updates `ROADMAP.md`.
3. Move the file to `wip/` upon starting work and implement changes within the corresponding Git branch.
4. After verification and user approval, merge the branch and move the issue file to `done/`.

### LICENSE
[MIT](./LICENSE.MIT)