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

## 本リポジトリ独自仕様

- skill の命名統一のためにプレフィックス案も提案しています。
  - 工程プレフィックス案: `req`(要件定義), `des`(設計), `cod`(コーディング), `ut`(単体テスト), `it`(結合テスト), `st`(システムテスト)
  - 観点プレフィックス案: `fn`(機能), `nf`(非機能)
  - ドメインプレフィックス案: `app`(業務アプリ), `inf`(インフラ), `ops`(運用), `mig`(移行), `pm`(プロ管)
  - 例: `des-app-api-contract-review`, `ut-app-service-unit-test`, `st-nf-performance-regression`

- skill をプロジェクトを横断して共有できるようにするため、「リポジトリのディレクトリ構成」に特別なルールを設けず、どんなディレクトリ構成であっても使えるようなスキルにして下さい。
  - ディレクトリ情報が必要な場合は外部から取得できる前提でスキルを作ってください。
