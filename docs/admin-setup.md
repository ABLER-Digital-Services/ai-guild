# 管理者セットアップ

このドキュメントは、リポジトリ作成直後に GitHub 側で設定する内容をまとめたものです。

## 現時点の既定方針

ユーザー確認待ちの項目はありますが、現時点では次を既定方針として扱います。

- main への直接 push は禁止
- Pull Request 経由でのみ変更する
- 人間レビューは最低 1 件必要
- AI レビュー初版は GitHub 標準寄りで導入する
- 貢献可視化は all-contributors を含む一覧ベースで始める

## GitHub で設定すること

### 1. Branch protection

- 対象ブランチは main
- Require a pull request before merging を有効化
- Require approvals を有効化
- Dismiss stale pull request approvals を有効化
- Require status checks to pass before merging を有効化
- Allow force pushes は無効
- Allow deletions は無効

### 2. CODEOWNERS

現在の CODEOWNERS は @jun-shiromizu を既定オーナーとして設定します。

初期の考え方:

- 当面は個人オーナー 1 名で開始する
- docs と workflows は必要に応じて別オーナーを重ねる

### 3. Pull Request review

- Copilot や GitHub の標準レビュー機能を使う場合は有効化を確認する
- 初期段階では GitHub 標準寄りの構成を優先する
- 専用 AI レビューを後から足す場合だけ、必要なシークレットと権限を整理する

### 4. Contributors 可視化

- all-contributors GitHub App は導入済み
- 使えない場合は CLI または手動更新で contributors セクションを維持する

### 5. Repository settings

- Discussions を使うかは後で判断
- Projects は必要になってから有効化
- Wiki は使わず docs に寄せる

## 今後この後にやること

- AI レビューのワークフロー追加
- contributors 追加運用の初回確認

## GitHub 上で次に実施すること

この環境からは GitHub への外向きアクセスが proxy 認証で失敗しているため、以下の操作は GitHub Web UI で実施してください。

### 1. all-contributors の初回確認

1. ai-guild の issue を 1 件作成する
2. issue コメントで次を投稿する
3. `@all-contributors please add @jun-shiromizu for doc, ideas`
4. Bot が contributors 追加用の Pull Request を作成することを確認する
5. 生成された Pull Request をレビューしてマージする

確認ポイント:

- README の Contributors セクションに反映されること
- `.all-contributorsrc` に contributor 情報が追加されること
- Bot コメントと Pull Request 生成が正常に行われること

### 2. Branch protection の有効化

1. GitHub で `ABLER-Digital-Services/ai-guild` を開く
2. Settings > Branches を開く
3. `main` に対する branch protection rule を追加する

推奨設定:

- Require a pull request before merging: On
- Require approvals: 1
- Dismiss stale pull request approvals when new commits are pushed: On
- Require review from Code Owners: On
- Require status checks to pass before merging: On
- Required status checks: `PR Governance / validate-pr`
- Require branches to be up to date before merging: On
- Restrict who can push to matching branches: 必要に応じて設定
- Allow force pushes: Off
- Allow deletions: Off

### 3. GitHub 標準寄り AI レビューの確認

1. Pull Request 作成時に GitHub 標準レビュー導線が使えることを確認する
2. CODEOWNERS により @jun-shiromizu がレビュー対象に入ることを確認する
3. `PR Governance` が必須チェックとしてブロックすることを確認する

## 補足

もし `PR Governance / validate-pr` が required status checks に表示されない場合は、先に一度 Pull Request を流して workflow を実行し、チェック名が GitHub に認識された後で required に設定してください。