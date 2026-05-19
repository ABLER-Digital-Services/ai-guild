# Contributors 可視化方針

ai-guild の貢献可視化は、まずは all-contributors 方式の軽量運用から始めます。

## 目的

- コード以外の貢献も見えるようにする
- ランキングではなく、貢献の種類を残す
- 運用コストを増やしすぎない

## 初期方針

- 重み付きスコアやランキングは導入しない
- README の contributors セクションで可視化する
- 必要なら docs 側に運用ルールを補足する

## all-contributors を採用する理由

- 一覧表示が軽い
- コード以外の貢献も記録できる
- awesome-copilot 系の運用と相性がよい

## 運用候補

### 1. Bot 運用

- Pull Request や issue コメントから追加できる
- GitHub App の導入可否確認が必要
- 組織のネットワーク制約で使えない場合がある

### 2. CLI 運用

- 管理者が必要なタイミングで更新する
- 外部 GitHub App に依存しない
- 通常の Pull Request フローにそのまま載せられる

## 今のおすすめ

- `.all-contributorsrc` と README の置き場を維持する
- contributors 追加は CLI を既定運用にする
- Bot は使える場合のみ補助的に使う

## 現在の導入状態

- `.all-contributorsrc` は作成済み
- README の contributors セクションは all-contributors 仕様に合わせて配置済み
- CLI 利用コマンドは CONTRIBUTING.md に記載済み
- all-contributors GitHub App はインストール済み

## 使い始め方

- 管理者が contributors 追加用のブランチを作成します
- `npx all-contributors-cli add <username> <contributions>` を実行します
- 例: `npx all-contributors-cli add jun-shiromizu doc,ideas`
- 変更差分を Pull Request に載せて通常どおりレビューします
- Bot が利用しにくい環境では CLI を継続運用します

## GitHub Actions での手動実行

- GitHub Actions の `Contributors Update` を `workflow_dispatch` で起動できます
- 入力は `username` と `contributions` の 2 つです
- workflow は `all-contributors-cli` を実行し、差分があれば contributor 追加用 PR を自動作成します
- 差分がなければ PR は作られません