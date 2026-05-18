# Contributing

ai-guild は、社内向けの AI エージェント活用ナレッジとカスタマイズ資産を扱うリポジトリです。

対象は GitHub Copilot に限らず、Codex、Claude Code、そのほかの AI エージェントを含みます。

## 基本方針

- メインブランチへの直接 push は行いません
- 変更は Pull Request 経由で受け付けます
- Team メンバー以外は Fork からの提案を基本とします
- すべての Pull Request に自動チェックと AI レビューをかける前提で運用します

## 受け付ける内容

次のような変更を歓迎します。

- instructions の追加、改善、廃止提案
- agents や skills の追加、改善
- hooks や workflows の整備
- cookbook や docs の改善
- 分類、メタデータ、索引の改善

## 投稿前に確認すること

- 既存資産と重複していないか
- どの AI エージェントを対象にしているか明確か
- 実行前提や制約が書かれているか
- 社内標準と矛盾していないか
- 危険な権限委譲や曖昧な指示がないか

## Pull Request の流れ

1. ブランチを作成して変更をまとめる
2. Pull Request テンプレートに沿って背景と影響範囲を書く
3. 自動チェックと AI レビューの結果を確認する
4. 必要に応じて修正する
5. 人間レビューの承認後にマージする

## 貢献者の追加

このリポジトリでは all-contributors を使って、コード以外の貢献も記録します。

Bot が有効な場合は、issue または Pull Request のコメントで次のように依頼できます。

`@all-contributors please add @<username> for <contributions>`

例:

`@all-contributors please add @jun-shiromizu for doc, ideas`

使える contribution type は all-contributors の定義に従います。Bot が使えない場合は、管理者が CLI または手動で反映します。

## レビューで見る観点

- 配置場所が妥当か
- 必須メタデータや構造がそろっているか
- 説明が十分で、誤読しにくいか
- 安全性と再利用性に問題がないか
- 既存資産との競合や重複がないか

## マージの前提

次を満たさない Pull Request は、原則としてマージしません。

- 変更意図が説明されている
- AI レビューの指摘に対応済み、または理由付きで扱いが明確になっている
- 必要な人間レビューを通過している
- リポジトリの分類ルールと命名ルールに従っている

## 未確定の運用項目

次は運用開始までに確定させます。

- ブランチ保護の厳格度
- all-contributors Bot の GitHub App 導入可否

詳細な検討事項は docs/decisions.md を参照してください。