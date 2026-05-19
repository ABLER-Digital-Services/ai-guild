# skills

このディレクトリには、再利用可能な手順や知識パッケージを配置します。

共通ルールやカテゴリ別の投稿ルールは [../ASSET_AUTHORING_RULES.md](../ASSET_AUTHORING_RULES.md) を参照してください。

## 公式仕様
Agent Skills の記述ルールは、公式仕様に合わせて次を満たしてください。

- skill ルートに `SKILL.md` を置く
- `SKILL.md` は YAML frontmatter と Markdown 本文で構成する
- `name` はディレクトリ名と一致させ、英小文字、数字、ハイフンのみを使う
- `description` は skill が何をするかと、いつ使うかを具体的に書く
- 詳細資料は `references/`、実行コードは `scripts/`、静的リソースは `assets/` に分ける

このリポジトリでは、システム開発系 skill の命名統一のためにプレフィックス案も提案しています。詳細は [../ASSET_AUTHORING_RULES.md](../ASSET_AUTHORING_RULES.md) の skills 章を参照してください。

- 工程プレフィックス案: `req`, `des`, `cod`, `ut`, `it`, `st`
- 観点プレフィックス案: `fn`, `nf`
- ドメインプレフィックス案: `app`, `inf`, `ops`, `mig`, `pm`
- 例: `des-app-api-contract-review`, `ut-app-service-unit-test`, `st-nf-performance-regression`

例:

- 特定フレームワークの実装手順
- 調査やレビューの定型手順
- 社内標準のまとめ

追加時は、入出力、適用条件、期待する成果を明記してください。