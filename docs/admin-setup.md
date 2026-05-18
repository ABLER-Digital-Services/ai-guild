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

- all-contributors GitHub App を対象リポジトリにインストールする
- 使えない場合は CLI または手動更新で contributors セクションを維持する

### 5. Repository settings

- Discussions を使うかは後で判断
- Projects は必要になってから有効化
- Wiki は使わず docs に寄せる

## 今後この後にやること

- AI レビューのワークフロー追加
- all-contributors GitHub App の導入確認