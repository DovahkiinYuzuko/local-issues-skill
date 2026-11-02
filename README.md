# local-issues-skill

ローカル環境でのIssue管理とDAG依存関係解析、進捗ダッシュボード運用を行うAIエージェント向けスキル / Agent skill for local issue management, DAG dependency resolution, and task dashboard generation.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square&logo=opensourceinitiative&logoColor=white)](./LICENSE.MIT)
![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

[日本語](#日本語) | [English](#english)

## 日本語

### 概要
`local-issues-skill` は、外部の課題管理サービスを使用せず、ローカルリポジトリ内で完結してタスク（Issue）と依存関係（DAG）を管理するためのエージェントスキルです。
Python標準ライブラリ（外部依存なし）によるスクリプトを備えており、Issueのメタデータから決定論的に `DASHBOARD.md` およびデジタル庁デザインシステム（DADS）に準拠した静的HTMLダッシュボード（`dashboard.html`）を自動生成します。

### インストール

スキルとしてのインストール：
```bash
npx skills add https://github.com/DovahkiinYuzuko/local-issues-skill
```

ターミナルから `issue` コマンドとして使用する場合（任意）：
本スキルのディレクトリに移動し、編集可能モードでインストールします。
```bash
cd path/to/local-issues-skill
pip install -e .
```

### 主な特徴
- **ディレクトリベースの状態管理**: `docs/local-issues/` 配下の `not-started/`、`wip/`、`done/` ディレクトリ間でファイルを移動させることで、進捗状態を直接管理できます。`not-started/` と `done/` はカテゴリタイプ（`feat/`, `fix/`, `refactor/` など）で分類可能です。
- **DAG依存関係解析**: フロントマターに `depends_on: [issue-1]` を記述することで、前提タスクの依存関係をトポロジカルソートで自動解決します。依存が解消された「着手可能」なタスクを、後続タスクを多く解放する順に自動整列します。
- **循環参照の自動検知**: 依存関係にループが発生した場合、即座にエラーとして検出し、診断情報を出力します。
- **Gitブランチと連動した安全設計**: 各Issueごとにブランチを切り、動作検証およびユーザーの承認を経てからのみマージおよび `done/` への移動を許可するワークフローを強制します。
- **統括ダッシュボードの自動生成**: 全体の進捗を可視化する `DASHBOARD.md` と、デジタル庁デザインシステム（DADS）完全準拠の単一静的HTMLダッシュボード（`dashboard.html`）を外部ライブラリなしで出力します。
- **多言語対応**: デフォルトの英語（`en`）に加え、`--lang ja` または設定ファイルにより日本語表示に切り替え可能です。

### 使い方
1. AIエージェントに本スキルを読み込ませます。
2. 機能追加や不具合修正の相談を行うと、エージェントが `docs/local-issues/not-started/<カテゴリタイプ>/issue-{num}-{やること}.md` を作成し、具体的なTODOリストを記述します。
3. 着手時にファイルを `wip/` に移動し、対応するGitブランチで実装を進めます。
4. 検証完了およびユーザーの承認後、ブランチをマージしてファイルを `done/<カテゴリタイプ>/` に移動します。
5. 付属のスクリプト（またはインストールした `issue` コマンド）を実行することで、ファイル移動やブランチ作成、ダッシュボードの更新を機械的に補助できます。

### LICENSE
[MIT](./LICENSE.MIT)

## English

### Overview
`local-issues-skill` is an agent skill designed for managing tasks (issues) and DAG dependencies locally within a repository without external issue-tracking services.
Equipped with a Python standard-library script (zero external dependencies), it deterministically parses issue metadata and generates `DASHBOARD.md` and a static HTML dashboard (`dashboard.html`) compliant with Japan's Digital Agency Design System (DADS).

### Install

Install as an agent skill:
```bash
npx skills add https://github.com/DovahkiinYuzuko/local-issues-skill
```

To use directly from the terminal via the `issue` command (Optional):
Navigate to the directory of this skill and install it in editable mode:
```bash
cd path/to/local-issues-skill
pip install -e .
```

### Key Features
- **Directory-Based Status Tracking**: Tracks progress by moving files between `not-started/`, `wip/`, and `done/` under `docs/local-issues/`. The `not-started/` and `done/` directories can be organized by category types (e.g., `feat/`, `fix/`, `refactor/`).
- **DAG Dependency Analysis**: Declare `depends_on: [issue-1]` in the frontmatter to automatically resolve prerequisite tasks via topological sorting. Identifies "Ready to Start" tasks and orders them by downstream unblock impact.
- **Cycle Detection**: Automatically detects circular dependency loops and outputs diagnostic error paths.
- **Git Branch Lifecycle Safety**: Enforces a workflow where each issue has a dedicated branch, and merging to the default branch and moving to `done/` strictly requires operational verification and user approval.
- **Master Dashboard Generation**: Generates a master `DASHBOARD.md` and a standalone, zero-dependency static HTML dashboard (`dashboard.html`) fully compliant with the Digital Agency Design System (DADS).
- **Multi-tier Localization**: Defaults to English (`en`), with instant Japanese switching via `--lang ja` or configuration.

### Usage
1. Load this skill into the AI agent.
2. When discussing feature requests or bug fixes, the agent scaffolds `docs/local-issues/not-started/<category>/issue-{num}-{task}.md` and writes concrete TODO items.
3. Move the file to `wip/` upon starting work and implement changes within the corresponding Git branch.
4. After verification and user approval, merge the branch and move the issue file to `done/<category>/`.
5. The included script (or the installed `issue` command) can be executed to assist with file movements, branch creations, and dashboard synchronizations.

### LICENSE
[MIT](./LICENSE.MIT)
