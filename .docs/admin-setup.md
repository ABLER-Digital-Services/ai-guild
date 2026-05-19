# 管理者セットアップ

このドキュメントは、リポジトリ作成直後に GitHub 側で設定する内容をまとめたものです。

## 現時点の既定方針

ユーザー確認待ちの項目はありますが、現時点では次を既定方針として扱います。

- main への直接 push は禁止
- Pull Request 経由でのみ変更する
- 人間レビューは最低 1 件必要
- main は GitHub Rulesets で保護する
- Copilot code review は Pull Request ごとに自動実行する
- 貢献可視化は all-contributors を含む一覧ベースで始める

## GitHub で設定すること

### 1. Rulesets

- branch protection rule ではなく branch ruleset を使う
- 対象ブランチは main
- Enforcement status は Active にする
- Pull Request 必須、承認必須、必須チェック必須を有効化する
- force push と deletion は許可しない

### 2. CODEOWNERS

現在の CODEOWNERS は @jun-shiromizu を既定オーナーとして設定します。

初期の考え方:

- 当面は個人オーナー 1 名で開始する
- .docs と workflows は必要に応じて別オーナーを重ねる

### 3. Pull Request review

- GitHub Copilot code review を有効化する
- Pull Request 作成時の自動レビューを有効化する
- `.github/copilot-instructions.md` と `.github/instructions/*.instructions.md` をレビュー時にも使う
- 専用 AI レビュー workflow は現時点では追加しない

### 4. Contributors 可視化

- all-contributors の記録形式を採用する
- 初期運用は CLI で実施する
- GitHub App は使える場合のみ補助的に使う

### 5. Repository settings

- Discussions を使うかは後で判断
- Projects は必要になってから有効化
- Wiki は使わず .docs に寄せる

## 今後この後にやること

- Ruleset の本番反映
- Copilot 自動レビューの有効化確認
- contributors 追加運用の初回実行

## GitHub 上で次に実施すること

この環境からは GitHub への外向きアクセスが proxy 認証で失敗しているため、以下の操作は GitHub Web UI またはローカル端末で実施してください。

### 1. all-contributors の初回実行

1. contributors 追加用の作業ブランチを作成する、または GitHub Actions の `Contributors Update` を開く
2. ローカルで次を実行する、または workflow_dispatch の入力に同じ値を入れる
3. `npx all-contributors-cli add jun-shiromizu doc,ideas`
4. `README.md` と `.all-contributorsrc` の差分、または workflow が作成した Pull Request を確認する
5. ローカル実行時は変更を commit して Pull Request を作成する
6. レビューしてマージする

確認ポイント:

- README の Contributors セクションに反映されること
- `.all-contributorsrc` に contributor 情報が追加されること
- 通常の Pull Request フローで安全に反映できること

### 2. Rulesets の有効化

1. GitHub で `ABLER-Digital-Services/ai-guild` を開く
2. Settings > Rules > Rulesets を開く
3. `New ruleset` から branch ruleset を作成する
4. 対象ブランチパターンに `main` を指定する

推奨設定:

- Enforcement status: Active
- Require a pull request before merging: On
- Required approvals: 1
- Dismiss stale pull request approvals when new commits are pushed: On
- Require review from Code Owners: On
- Require status checks to pass before merging: On
- Required status checks: `PR Governance / validate-pr (pull_request)`
- Required status checks: `Skill Validation / validate-skills (pull_request)`
- Require branches to be up to date before merging: On
- Block force pushes: On
- Block deletions: On
- Restrict updates: 必要に応じて設定

補足:

- `Skill Validation / validate-skills (pull_request)` は全 Pull Request で実行し、skills に変更がない場合は no-op で成功終了する前提で required check に含める

### 3. Copilot code review の有効化

1. GitHub で Settings > Copilot > Code review を開く
2. Pull Request の自動レビューを有効化する
3. `Use custom instructions when reviewing pull requests` を有効化する
4. テスト用 Pull Request を 1 件作成し、Copilot が自動で review comment を付けることを確認する

確認ポイント:

- CODEOWNERS により @jun-shiromizu がレビュー対象に入ること
- `PR Governance / validate-pr (pull_request)` が required status check としてブロックすること
- `Skill Validation / validate-skills (pull_request)` が skill 変更時に検証を行い、非 skill PR では成功終了すること
- Copilot review comment が自動で付与されること
- `.github/copilot-instructions.md` の日本語方針がレビュー文面にも反映されること

## 補足

もし `PR Governance / validate-pr (pull_request)` または `Skill Validation / validate-skills (pull_request)` が required status checks に表示されない場合は、先に一度 Pull Request を流して workflow を実行し、チェック名が GitHub に認識された後で required に設定してください。

Copilot code review は required approval には数えられず、マージ可否を直接ブロックしません。このリポジトリでは Copilot review を早期検知の自動信号、人間レビューを最終判断として扱います。

all-contributors GitHub App は組織のネットワーク制約や外部 App 制約で無反応になることがあるため、このリポジトリでは CLI を既定運用とします。