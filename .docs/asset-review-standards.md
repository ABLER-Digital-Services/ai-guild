# 資産レビュー基準

このドキュメントは、agents、skills、hooks、instructions、workflows などの資産をレビューするときの基準のうち、まず agents と skills に適用する初版ルールをまとめたものです。

投稿時の共通ルール、カテゴリ別ルール、命名や置き場所の正本は [../ASSET_AUTHORING_RULES.md](../ASSET_AUTHORING_RULES.md) を参照してください。

## 基本方針

- 形式チェックは GitHub Actions で機械的に弾く
- 内容チェックは Copilot code review で早期検知する
- 最終判断は人間レビューで行う
- 厳密な schema が固まっていないカテゴリは、まずレビュー観点を先に定義し、機械チェックは最小限から始める

## agents のレビュー基準

agents 配下の資産は、少なくとも次を明記することを求めます。

- 何のためのエージェントか
- どの AI エージェントや実行環境を対象にするか
- 使うツールと権限境界
- 前提条件と制約
- 想定利用者

レビューでは次を重点確認します。

- 役割が広すぎず、責務が説明に見合っているか
- 危険な権限委譲や過剰な自動実行を含まないか
- 外部サービス依存や必要権限が明示されているか
- 既存 agent と重複しないか
- 説明不足のまま強い権限を要求していないか

## skills のレビュー基準

skills 配下の資産は、`.github/skills/make-skill-template/SKILL.md` の制約を初版ルールとして準用します。

### SKILL.md frontmatter

- `name` は必須
- `description` は必須
- `name` は 1-64 文字
- `name` は英小文字、数字、ハイフンのみを使う
- `name` は skill ディレクトリ名と一致させる
- `description` は 10-1024 文字
- `description` は何をする skill かと、いつ使うかの両方を説明する

### SKILL.md 本文

- 本文は 500 行以内を目安にする
- 入出力、適用条件、期待成果が分かること
- 追加リソースがある場合は、scripts、references、assets、templates の役割が読み取れること

### scripts のセキュリティ基準

skills 配下の `scripts/` は、少なくとも次を満たすことを求めます。

- 秘密情報やトークンをハードコードしない
- 権限昇格を前提にしない
- 外部から取得したスクリプトをそのまま pipe で実行しない
- ルート削除や無差別削除のような破壊的コマンドを含めない
- 利用者の環境を広く変更する処理は、必要性と影響を説明する

初版の自動チェックでは、次のような明確な危険パターンを禁止対象にします。

- `rm -rf /`
- `curl ... | sh`
- `wget ... | sh`
- `sudo ` や `-Verb RunAs` による権限昇格
- `Invoke-Expression` や `iex`
- 明確な秘密情報形式の埋め込み

## 初版の自動チェック範囲

初版 workflow では skills を対象に、次を検査します。

- `SKILL.md` の frontmatter 必須項目
- `name` とディレクトリ名の一致
- `name` と `description` の文字数
- `description` の記述ぶり
- `SKILL.md` の行数上限
- `scripts/` 配下の明確な危険パターン

この workflow は `Skill Validation / validate-skills (pull_request)` という独立 check として運用し、Rulesets の required status checks に加えます。

- workflow 自体は全 Pull Request で実行する
- skills に変更がない場合は no-op で成功終了する
- `PR Governance` には混ぜず、カテゴリ固有の検証として独立させる

agents はまだ厳密な定義ファイル形式を固定していないため、初版では Copilot review の観点定義を先に入れ、機械チェックは後から追加します。