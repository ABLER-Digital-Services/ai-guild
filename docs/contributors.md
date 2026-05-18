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

### 2. CLI 運用

- 管理者が必要なタイミングで更新する
- Bot が使えない場合の代替になる

## 今のおすすめ

- まずは `.all-contributorsrc` と README の置き場だけ用意する
- Bot が導入可能なら Bot を使う
- 難しければ、最初は手動または CLI で十分

## 現在の導入状態

- `.all-contributorsrc` は作成済み
- README の contributors セクションは bot 仕様に合わせて配置済み
- Bot 利用コマンドは CONTRIBUTING.md に記載済み

## まだ手元で完了できないこと

- GitHub App として all-contributors Bot を対象リポジトリにインストールすること

この作業は GitHub 側の権限が必要です。導入する場合は、all-contributors の GitHub App を組織または対象リポジトリにインストールしてください。

導入後は、issue または Pull Request コメントから contributors を追加できます。