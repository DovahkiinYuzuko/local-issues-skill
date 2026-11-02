---
name: local-issues
description: ローカル環境にissue.mdと統括するDASHBOARD.md(旧ROADMAP.md)を配置。何がしたくて、今どこで、何が終わっているのかを管理する。何らかの問題や機能追加、並びにその相談時などに実行する。
---

# local-issues

- `docs\local-issues\`に、ローカルのissue.mdを入れる。`docs\local-issues\`内には`not-started\`,`wip\`,`done\`を置き、状態に応じて置く場所を決める。なお、`not-started\`と`done\`の中はカテゴリタイプ（`feat\`, `fix\`, `refactor\`等）で分けて整理してよい。
- issue.mdは、`issue-{num}-{やること}.md`の形で書く。
- 中身は、概要、やることが最低限ほしい。また、修正か機能追加で最低限分ける。TODO方式でのリストもissue.md内に入れる。
  - **重要**: AIは相談内容やコードベースの分析を踏まえ、具体的な修正対象ファイルや作業手順を反映した**中身のあるTODOリストを必ず記述すること**（ダミーのTODOのまま放置することは厳禁）。
  - 先頭にはYAMLフロントマター（`type`（カテゴリタイプ）, `description`, 必要に応じて前提タスクの `depends_on: [issue-X]`）を記載する。
- issue毎にブランチを切る。基本はデフォルトブランチ -> issueブランチ -> デフォルトブランチにマージ -> 次のissueブランチ、という形で、毎度デフォルトブランチにマージをするサイクル。ただし、issueブランチ内で確実に動くことが確定している&&ユーザーの許可を以て始めてマージされる。マージされて初めて`done\`に移動し、許可なく移動することやデフォルトブランチへのマージは許されない。
- ブランチ名は、`issue-{num}-{やること}`の形で作る。サブissueが発生した場合は、`issue-{num}.{subnum}-{やること}`の形で作る。

## DASHBOARD (旧ROADMAP)
- issuesを統括するドキュメントであり、issue.md作成や更新時などに更新する必要がある。(issue.mdだけいじってDASHBOARDを更新しないのはNG)
- `docs\local-issues\DASHBOARD.md` および閲覧用の `dashboard.html`（デジタル庁デザインシステム準拠）に反映する。
- これらは手動編集ではなく、付属のスクリプト（`python <skill>/scripts/issue_hub.py sync`）を実行して自動同期・再生成する。
- もし必要であれば外部公開用のROADMAP.mdをリポジトリ直下に設置。ただしこれはlocal-issues内のDASHBOARDとは別で扱い、外部用に整形したものを置く。外部用のROADMAP.mdは、DASHBOARD.mdを元に整形すること。（ユーザーに必要かどうかの質問をし、必要であれば作成する）

## sub-issues
- local-issuesにおいて、作業中更にissueが発生した時に実行。大元のissue番号に小数点をつける。(e.g. `issue-3.1-`)
- 大元のissue.mdにサブissueを追記し、ブランチを分ける。(サブissue.mdは作らない。)
- サブissuesも1つずつ解決し、1つずつ大元のブランチにマージ。すべてのサブissueブランチがlocal-issueブランチにマージされるようにする。

## 補助スクリプトの利用
手動でのファイル移動やダッシュボード更新を補助するため、付属のスクリプトを利用できる。
- 利用可能な言語一覧: `python <skill>/scripts/issue_hub.py --lang-list`
- 新規作成: `python <skill>/scripts/issue_hub.py new "<タイトル>" --type feat --desc "概要"` （作成後、AIは必ずissue.mdを開いて具体的なTODOを書き込むこと）
- 着手・移動: `python <skill>/scripts/issue_hub.py start <番号>` （wipへの移動とブランチ作成）
- 完了・移動: `python <skill>/scripts/issue_hub.py done <番号>` （ユーザー承認後にdoneへ移動）
- 同期・再生成: `python <skill>/scripts/issue_hub.py sync` （DASHBOARD.mdとHTMLの更新。`--lang ja`で日本語出力可能）
