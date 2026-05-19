# Contributing

ai-guild は、社内向けの AI エージェント活用ナレッジとカスタマイズ資産を扱うリポジトリです。

対象は GitHub Copilot に限らず、Codex、Claude Code、そのほかの AI エージェントを含みます。

## 基本方針

- このリポジトリは社外公開前提ではなく、委託先を含む当社関与案件での社内利用を前提に運用します
- メインブランチへの直接 push は行いません
- 変更は Pull Request 経由で受け付けます
- Team メンバー以外は Fork からの提案を基本とします
- すべての Pull Request に自動チェックと AI レビューをかける前提で運用します

## この文書の対象

この文書は、知見を投稿したい人向けのガイドです。次をまとめています。

- どの資産をどこに置くか
- GitHub Issues と Pull Request をどう使い分けるか
- 投稿からレビュー対応までの流れ
- 資産カテゴリごとの最低限のルール

共通ルールとカテゴリ別ルールの正本は [ASSET_AUTHORING_RULES.md](ASSET_AUTHORING_RULES.md) を参照してください。

## 受け付ける内容

次のような変更を歓迎します。

- instructions の追加、改善、廃止提案
- agents や skills の追加、改善
- hooks や workflows の整備
- cookbook や .docs の改善
- 分類、メタデータ、索引の改善

## Issue と Pull Request の使い分け

### Issue を使うケース

- まだ方針が固まっていない提案
- どのカテゴリに置くべきか迷っている相談
- 既存資産の改善案や運用上の質問
- 先にレビュー観点や関係者の合意を取りたい変更

### Pull Request を使うケース

- 置き場所と変更内容が明確で、そのまま提案できる変更
- 軽微な修正、リンク修正、説明改善
- 既存ルールに沿って追加できる資産

### 判断に迷うとき

- まず相談したいなら Issue
- すぐに差分を見せられるなら Pull Request
- 問い合わせ先は [SUPPORT.md](SUPPORT.md) を参照

## 投稿前に確認すること

- 既存資産と重複していないか
- どの AI エージェントを対象にしているか明確か
- 実行前提や制約が書かれているか
- 社内標準と矛盾していないか
- 危険な権限委譲や曖昧な指示がないか

## 資産カテゴリごとの最低限のルール

以下は投稿時に最低限意識する要約です。詳細な正本は [ASSET_AUTHORING_RULES.md](ASSET_AUTHORING_RULES.md) にあります。

### 共通ルール

- 既存のトップレベル分類を優先し、新しい分類は勝手に増やさない
- 何のための資産か、対象エージェント、前提条件、制約を分かるようにする
- 既存資産との重複や競合がないか確認する

### instructions

- 指示対象と適用範囲を明確にする
- 危険な権限委譲や曖昧な禁止事項を書かない

### agents

- 責務、利用ツール、権限境界を明記する
- 目的が広すぎる定義は避ける

### skills

- `SKILL.md` の `name` と `description` を必ず書く
- `name` は skill ディレクトリ名と一致させる
- `description` は何をする skill かと、いつ使うかが分かる説明にする
- `scripts/` を含む場合は危険なコマンドや秘密情報の混入を避ける

### hooks

- 実行タイミング、失敗時の影響、必要権限を明記する

### workflows

- トリガー、必要権限、失敗時の扱いを明記する
- Rulesets が参照する check 名や workflow 名は安定させる

### cookbook

- 実運用での使いどころと前提条件を明確にする
- サンプルが誤誘導にならないようにする

### .docs

- 利用者向け説明ではなく、内部向け運用ルールとして整理する

詳細な投稿ルールは [ASSET_AUTHORING_RULES.md](ASSET_AUTHORING_RULES.md)、レビュー基準は [.docs/asset-review-standards.md](.docs/asset-review-standards.md) を参照してください。

## Pull Request の流れ

1. Issue で相談するか、直接 Pull Request にするかを決める
2. Fork または作業ブランチを作成して変更をまとめる
3. 変更対象のカテゴリに合う場所へ資産を追加・修正する
4. Pull Request テンプレートに沿って背景、影響範囲、リスク、検証内容を書く
5. 自動チェックと Copilot review の結果を確認する
6. 指摘に対応し、必要なら説明を補足する
7. 人間レビューの承認後にマージする

## 貢献者の追加

このリポジトリでは all-contributors を使って、コード以外の貢献も記録します。

既定運用では、管理者が CLI で contributor 情報を追加します。

`npx all-contributors-cli add <username> <contributions>`

例:

`npx all-contributors-cli add jun-shiromizu doc,ideas`

このコマンドで `.all-contributorsrc` と `README.md` が更新されます。変更は通常の Pull Request と同じようにレビューして main に取り込みます。

使える contribution type は all-contributors の定義に従います。必要に応じて管理者が `npx all-contributors-cli generate` で一覧を再生成できます。GitHub App の Bot は使える環境でのみ補助的に扱います。

## レビューで見る観点

- 配置場所が妥当か
- 必須メタデータや構造がそろっているか
- 説明が十分で、誤読しにくいか
- 安全性と再利用性に問題がないか
- 既存資産との競合や重複がないか
- Issue / Pull Request の使い分けが妥当か

## マージの前提

次を満たさない Pull Request は、原則としてマージしません。

- 変更意図が説明されている
- AI レビューの指摘に対応済み、または理由付きで扱いが明確になっている
- 必要な人間レビューを通過している
- リポジトリの分類ルールと命名ルールに従っている

## 未確定の運用項目

次は運用開始までに確定させます。

- ブランチ保護の厳格度
- contributors 追加をどこまで定期運用に寄せるか

詳細な検討事項は .docs/decisions.md を参照してください。