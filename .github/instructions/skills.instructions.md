---
applyTo: "skills/**,.github/skills/**"
excludeAgent: "cloud-agent"
---

このリポジトリの Copilot code review で `skills/**` または `.github/skills/**` をレビューするときは、次を優先してください。

- `SKILL.md` の `name` が skill ディレクトリ名と一致しているか
- `name` が英小文字、数字、ハイフンのみで 1-64 文字に収まるか
- `description` が 10-1024 文字で、何をする skill かと、いつ使うかの両方を説明しているか
- 本文が冗長すぎず、入出力、適用条件、期待成果が読み取れるか
- 既存 skill と重複していないか

`scripts/` をレビューするときは、次を重点確認してください。

- 秘密情報やトークンのハードコード
- `curl | sh`、`wget | sh`、`Invoke-Expression`、`iex` などの危険な実行パターン
- `sudo` や `-Verb RunAs` などの権限昇格
- 無差別削除や環境破壊につながるコマンド
- 外部通信、環境変更、依存追加の必要性説明

`skills/**` では、形式逸脱、発見性を落とす description、危険な script、既存資産との重複を優先して指摘してください。