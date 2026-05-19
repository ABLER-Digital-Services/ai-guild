# ai-guild

[![All Contributors](https://img.shields.io/badge/all_contributors-managed-ee8449.svg?style=flat-square)](#contributors)

社内向けの AI エージェント活用ナレッジとカスタマイズ資産を集約するリポジトリです。

本リポジトリは、委託先を含む当社関与案件での利用を前提とした社内利用専用資産です。閲覧、複製、改変、社内再配布は許可しますが、社外提供、公開転載、再販売は禁止します。

GitHub Copilot、Codex、Claude Code などを含む AI エージェント全般を対象にします。

目指す姿は、awesome-copilot を参考にした会社版の AI エージェント資産リポジトリです。ただし運用は完全なオープンコミュニティ型ではなく、次の前提を置きます。

- Team メンバーのみが直接編集できる
- それ以外の利用者は閲覧を基本とする
- 利用者は Fork して使える
- 投稿や改善提案は Pull Request 経由で受け付ける
- Pull Request には AI 自動レビューを必須でかける
- 貢献の量と質が見える状態をつくる

## このリポジトリの目的と位置づけ

このリポジトリは、AI エージェントを安全かつ再利用しやすい形で使うための社内標準の置き場です。

- 利用者にとっては、すぐ使える知見と手順の集約先です
- 投稿者にとっては、レビュー付きで資産を改善・共有する場です
- 管理者やレビューアにとっては、運用ルールと品質ゲートを保つ対象です

## 最初に読む場所

### 知見を使いたい人向け

- リポジトリ全体の概要: [README.md](README.md)
- 利用ルールと前提: [CONTRIBUTING.md](CONTRIBUTING.md)
- 問い合わせ先と Issue の使い分け: [SUPPORT.md](SUPPORT.md)

### 知見を投稿したい人向け

- 投稿ルール全体: [CONTRIBUTING.md](CONTRIBUTING.md)
- 共通ルールとカテゴリ別ルール: [ASSET_AUTHORING_RULES.md](ASSET_AUTHORING_RULES.md)
- 各資産のレビュー基準: [.docs/asset-review-standards.md](.docs/asset-review-standards.md)
- 管理者レビューで見られる観点: [.docs/ai-review.md](.docs/ai-review.md)

### リポジトリ管理者・レビューア向け

- GitHub 設定と Rulesets: [.docs/admin-setup.md](.docs/admin-setup.md)
- AI レビューの考え方: [.docs/ai-review.md](.docs/ai-review.md)
- 中長期の方針: [.docs/plan.md](.docs/plan.md)
- 未決定の論点: [.docs/decisions.md](.docs/decisions.md)

## 何を置くか

awesome-copilot を参考にしつつ、特定ツールに閉じない形で資産の種類を明確に分けます。

- instructions: 開発規約やレビュー観点などの指示資産
- agents: 特定業務向けのエージェント定義
- skills: 再利用可能な手順や専門知識
- hooks: 実行時の自動チェックや補助処理
- workflows: GitHub Actions で動く AI ワークフロー
- cookbook: 実運用で使えるレシピ集
- .docs: 内部向けの運用ガイド、設計方針、管理ルール

社内版として重要なのは、単に資産を並べることではなく、公開品質を保つための審査導線を最初から埋め込むことです。

## リポジトリ構成

- instructions: 指示資産の置き場
- agents: エージェント定義の置き場
- skills: 再利用可能な手順資産の置き場
- hooks: 補助処理やフックの置き場
- workflows: GitHub Actions や自動化資産の置き場
- cookbook: レシピやサンプルの置き場
- .docs: 内部向け運用文書の置き場

## 投稿とレビューの流れ

知見を追加・改善するときの基本導線は次のとおりです。

1. Issue で相談するか、直接 Pull Request を作るかを決める
2. Fork または作業ブランチで変更を作る
3. Pull Request に背景、影響範囲、リスク、検証内容を書く
4. 自動チェックと Copilot review の指摘を確認する
5. 必要に応じて修正し、人間レビューを経てマージする

詳しい使い分けや各資産のルールは [CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。

共通ルールやカテゴリ別の投稿ルールの正本は [ASSET_AUTHORING_RULES.md](ASSET_AUTHORING_RULES.md) にあります。

## Issue と問い合わせ

- 資産追加や改善提案、運用上の質問は [SUPPORT.md](SUPPORT.md) を参照
- セキュリティ上の問題は [SECURITY.md](SECURITY.md) を参照

## 運用原則

### 1. 読めるが、簡単には壊せない

社内の利用促進を優先しつつ、品質担保のためにメインブランチは保護します。

- 直接 push は Team メンバーでも原則禁止
- 変更は Pull Request 経由に統一
- レビュー承認と自動チェック通過を必須化
- 所有領域ごとにレビュー責任者を決める

### 2. AI は補助ではなくゲートの一部

AI レビューは参考コメントではなく、マージ判断に必要な信号として扱います。

- 命名や書式だけでなく、再利用性、セキュリティ、誤誘導、保守性を確認する
- instructions や agents では、危険な指示や曖昧な権限委譲を重点確認する
- .docs 変更でも、リンク切れ、重複、分類ミス、既存資産との競合を確認する
- AI コメントに対して未対応のままマージできない状態を目指す

### 3. 貢献を可視化して、再利用を増やす

コミット数だけではなく、使われた価値が見える指標を持ちます。

- 誰が何を追加したか
- どの資産が何回参照、利用、Fork されたか
- どの Pull Request が採用されたか
- どのカテゴリに貢献が集中しているか

## Contributors

貢献者の可視化は、まずは all-contributors 方式の軽量運用から始めます。

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/jun-shiromizu"><img src="https://avatars.githubusercontent.com/u/211425548?v=4?s=100" width="100px;" alt="白水淳"/><br /><sub><b>白水淳</b></sub></a><br /><a href="https://github.com/ABLER-Digital-Services/ai-guild/commits?author=jun-shiromizu" title="Documentation">📖</a> <a href="#ideas-jun-shiromizu" title="Ideas, Planning, & Feedback">🤔</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

このリポジトリは all-contributors の考え方を取り入れ、コード以外の貢献も可視化していきます。

## Governance

詳しくは次を参照してください。

- [CONTRIBUTING.md](CONTRIBUTING.md)
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
- [SECURITY.md](SECURITY.md)
- [SUPPORT.md](SUPPORT.md)

