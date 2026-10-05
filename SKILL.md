---
name: local-issues
description: ローカル環境にissue.mdと統括するROADMAP.mdを配置。何がしたくて、今どこで、何が終わっているのかを管理する。何らかの問題や機能追加、並びにその相談時などに実行する。
---

# local-issues

- `docs\local-issues\`に、ローカルのissue.mdを入れる。`docs\local-issues\`内には`not-started\`,`wip\`,`done\`を置き、状態に応じて置く場所を決める。
- issue.mdは、`issue-{num}-{やること}.md`の形で書く。
- 中身は、概要、やることが最低限ほしい。また、修正か機能追加で最低限分ける。TODO方式でのリストもissue.md内に入れる。ユーザー指定のYAMLフロントマターなどもあれば使用する。
- issue毎にブランチを切る。基本はデフォルトブランチ -> issueブランチ -> デフォルトブランチにマージ -> 次のissueブランチ、という形で、毎度デフォルトブランチにマージをするサイクル。ただし、issueブランチ内で確実に動くことが確定している&&ユーザーの許可を以て始めてマージされる。マージされて初めて`done\`に移動し、許可なく移動することやデフォルトブランチへのマージは許されない。

## ROADMAP
- issuesを統括するドキュメントであり、issue.md作成や更新時などに更新する必要がある。(issue.mdだけいじってROADMAP.mdを更新しないのはNG)
- フォーマットに関しては[roadmap_format.md](./references/roadmap_format.md)に準拠する。
- `docs\local-issues\ROADMAP.md`に置く。
- もし必要であれば外部公開用のROADMAP.mdをリポジトリ直下に設置。ただしこれはlocal-issues内のROADMAP.mdとは別で扱い、外部用に整形したものを置く。外部用のROADMAP.mdは、local-issues内のROADMAP.mdを元に整形すること。（ユーザーに必要かどうかの質問をし、必要であれば作成する）

## sub-issues
- local-issuesにおいて、作業中更にissueが発生した時に実行。大元のissue番号に小数点をつける。(e.g. `issue-3.1-`)
- 大元のissue.mdにサブissueを追記し、ブランチを分ける。(サブissue.mdは作らない。)
- サブissuesも1つずつ解決し、1つずつ大元のブランチにマージ。すべてのサブissueブランチがlocal-issueブランチにマージされるようにする。