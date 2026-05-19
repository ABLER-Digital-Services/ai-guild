# ai-guild

[![All Contributors](https://img.shields.io/github/all-contributors/ABLER-Digital-Services/ai-guild?color=ee8449&style=flat-square)](#contributors)

社内向けの AI エージェント活用ナレッジとカスタマイズ資産を集約するリポジトリです。

GitHub Copilot、Codex、Claude Code などを含む AI エージェント全般を対象にします。

目指す姿は、awesome-copilot を参考にした会社版の AI エージェント資産リポジトリです。ただし運用は完全なオープンコミュニティ型ではなく、次の前提を置きます。

- Team メンバーのみが直接編集できる
- それ以外の利用者は閲覧を基本とする
- 利用者は Fork して使える
- 投稿や改善提案は Pull Request 経由で受け付ける
- Pull Request には AI 自動レビューを必須でかける
- 貢献の量と質が見える状態をつくる

## 何を置くか

awesome-copilot を参考にしつつ、特定ツールに閉じない形で資産の種類を明確に分けます。

- instructions: 開発規約やレビュー観点などの指示資産
- agents: 特定業務向けのエージェント定義
- skills: 再利用可能な手順や専門知識
- hooks: 実行時の自動チェックや補助処理
- workflows: GitHub Actions で動く AI ワークフロー
- cookbook: 実運用で使えるレシピ集
- docs: 利用ガイド、設計方針、運用ルール

社内版として重要なのは、単に資産を並べることではなく、公開品質を保つための審査導線を最初から埋め込むことです。

## 使い始める

- 利用ルールは CONTRIBUTING.md を参照
- 中長期の設計方針は docs/plan.md を参照
- 未決定の論点は docs/decisions.md を参照
- AI エージェント向けの作業指針は AGENTS.md を参照
- 運用上の問い合わせは SUPPORT.md を参照
- セキュリティ報告は SECURITY.md を参照

## リポジトリ構成

- instructions: 指示資産の置き場
- agents: エージェント定義の置き場
- skills: 再利用可能な手順資産の置き場
- hooks: 補助処理やフックの置き場
- workflows: GitHub Actions や自動化資産の置き場
- cookbook: レシピやサンプルの置き場
- docs: 運用文書の置き場

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
- docs 変更でも、リンク切れ、重複、分類ミス、既存資産との競合を確認する
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
<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

このリポジトリは all-contributors の考え方を取り入れ、コード以外の貢献も可視化していきます。

## Governance

詳しくは次を参照してください。

- CONTRIBUTING.md
- CODE_OF_CONDUCT.md
- SECURITY.md
- SUPPORT.md

