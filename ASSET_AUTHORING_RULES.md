# 資産投稿ルール

このドキュメントは、ai-guild に資産を追加・更新するときの共通ルールと、カテゴリごとの投稿ルールの正本です。

レビュー基準そのものは [.docs/asset-review-standards.md](.docs/asset-review-standards.md) を参照してください。この文書は、投稿者が「どこに」「どんな形で」置くべきかを整理するためのものです。

## 使い分け

- 投稿ルールの全体像を知りたい: [CONTRIBUTING.md](CONTRIBUTING.md)
- 共通ルールとカテゴリ別ルールを確認したい: この文書
- レビューアが何を見るかを確認したい: [.docs/asset-review-standards.md](.docs/asset-review-standards.md)

## 共通ルール

### 1. 置き場所

- 資産は既存のトップレベル分類に置く
- 新しいトップレベル分類は勝手に増やさない
- リポジトリ全体の階層構造の説明は [README.md](README.md) に置く
- 投稿・レビューの流れは [CONTRIBUTING.md](CONTRIBUTING.md) に置く
- 管理者向けの運用ルールは `.docs/` に置く

### 2. 最低限そろえること

- 何のための資産か
- どの AI エージェントや利用者を対象にするか
- 前提条件と制約
- 実行時の注意点や失敗時の扱い
- 既存資産との違い

### 3. 禁止事項

- 顧客情報、秘密情報、内部トークンを含めない
- 危険な権限委譲や曖昧な自動実行を書かない
- 社内標準と矛盾する運用を既定値として提案しない
- 既存資産と実質的に同じ内容を重複追加しない

### 4. 命名の考え方

- フォルダ名やファイル名は、役割が推測できる短い名前にする
- 英数字とハイフンを基本にし、意味の曖昧な省略を避ける
- 既存カテゴリの命名パターンがある場合はそれに合わせる
- Rulesets が参照する workflow 名や check 名は安定させる

## カテゴリ別ルール

### instructions

- AI エージェントに適用する指示資産を置く
- 対象エージェント、適用範囲、前提条件を明記する
- path-specific instructions では `applyTo` を意図どおりに絞る
- 禁止事項やレビュー観点は、曖昧な表現ではなく運用可能な粒度で書く

### agents

- 特定目的のエージェント定義を置く
- 責務、利用ツール、権限境界を明記する
- 目的が広すぎる万能エージェントは避ける
- 危険な権限や自動実行を要求する場合は、必要性と制約を明示する

### skills

- 再利用可能な手順や知識パッケージを置く
- Agent Skills の公式仕様に合わせ、skill ルートには `SKILL.md` を必ず置く
- `SKILL.md` は YAML frontmatter と Markdown 本文で構成する
- `name` と `description` を必ず書く
- `name` は skill ディレクトリ名と一致させる
- `description` は何をする skill かと、いつ使うかが分かる説明にする
- `scripts/` を含む場合は危険なコマンドや秘密情報の混入を避ける

#### Agent Skills 公式仕様に基づく記述ルール

##### ディレクトリ構成

- skill は 1 ディレクトリ単位で管理する
- skill ルートには `SKILL.md` を必ず置く
- `scripts/` は実行コード、`references/` は追加文書、`assets/` は静的リソースに使う
- 詳細資料は `references/` などに分離し、`SKILL.md` は中核手順に絞る

##### frontmatter

- `SKILL.md` の先頭は YAML frontmatter にする
- 必須項目は `name` と `description`
- `name` は 1-64 文字、英小文字、数字、ハイフンのみを使う
- `name` は先頭・末尾をハイフンにしない
- `name` では連続ハイフンを使わない
- `description` は 1-1024 文字で空文字にしない
- `description` は「何をする skill か」と「いつ使うか」を両方書く
- `description` には、利用者がプロンプトで言いそうなキーワードや状況を含める
- 必要な場合だけ `license`、`compatibility`、`metadata`、`allowed-tools` を使う

##### 本文の書き方

- 本文は agent が実行時にそのまま読んで使う手順書として書く
- まず手順、前提条件、入出力、期待成果が分かる構成にする
- agent が元から知っている一般論より、このリポジトリ固有の制約や判断基準を優先して書く
- 曖昧な宣言より、再利用できる手順やチェックリストを書く
- 長くなりすぎる場合は `SKILL.md` を 500 行以内を目安に保ち、詳細は `references/` に逃がす
- 追加ファイルへの参照は skill ルートからの相対パスで書き、深い参照連鎖は避ける

##### description の書き方

- `description` は skill 発見の主な手がかりになるため、短すぎる要約にしない
- 「何を内部で実装しているか」より、「利用者が何を達成したいときに使うか」を優先して書く
- 「どんなときに使うか」を、日本語または対象利用者が使う言語で明示する
- 過度に広い説明は避け、近い別 skill と競合しない境界を保つ
- 迷ったら、発動してほしい例と発動してほしくない例を想定して過不足を見直す

#### skill 命名プレフィックス案

以下は、このリポジトリで主にシステム開発系 skill を集約することを前提にしたドラフト提案です。現時点では推奨ルールであり、既存 skill の一括改名までは求めません。

##### 基本形

- 推奨形式は `<phase>-<topic>` または `<phase>-<domain>-<topic>`
- 機能・非機能の区別が発見性に効く場合のみ `<phase>-<concern>-<domain>-<topic>` を使う
- プレフィックスを増やしすぎると 64 文字制約や可読性を損ねるため、原則 2-3 区分までにする

##### 工程プレフィックス案

- `req`: 要件定義
- `des`: 設計
- `cod`: コーディング
- `ut`: 単体テスト
- `it`: 結合テスト
- `st`: システムテスト

##### 観点プレフィックス案

- `fn`: 機能
- `nf`: 非機能

##### ドメインプレフィックス案

- `app`: アプリケーション
- `inf`: インフラ
- `ops`: 運用
- `mig`: 移行
- `pm`: プロジェクト管理

##### 命名例

- `req-pm-scope-alignment`
- `des-app-api-contract-review`
- `cod-app-react-form-implementation`
- `ut-app-service-unit-test`
- `it-inf-ci-pipeline-check`
- `st-nf-performance-regression`
- `des-mig-data-cutover-plan`

##### 運用上の補足

- skill 名は人間向けの分類ラベルではなく、agent の発見性も意識して topic 部分を具体的にする
- プレフィックスが曖昧な場合は、工程より topic の具体性を優先する
- 複数工程にまたがる skill は、主たる利用局面を 1 つ選ぶ
- 命名案を採用する場合は、テンプレート、validator、既存 skill 命名との差分整理を別途行う

### hooks

- 補助処理やフック資産を置く
- 実行タイミング、副作用、失敗時の影響、必要権限を明記する
- 自動実行される場合は、利用者が止める方法や回避方法が分かるようにする

### workflows

- GitHub Actions や自動化資産を置く
- トリガー、必要権限、失敗時の扱いを明記する
- workflow 名、job 名、required check 名は安定させる
- 人間向けログや自動生成メッセージは既定として日本語にする

### cookbook

- すぐ使えるレシピやサンプルを置く
- コピペ利用した際の前提条件と注意点を明記する
- サンプルは誤誘導や危険な既定値にならないようにする

## ルール変更の扱い

- 共通ルールやカテゴリ別ルールを変える場合は、この文書を正本として更新する
- レビュー観点が変わる場合は、必要に応じて [.docs/asset-review-standards.md](.docs/asset-review-standards.md) も更新する
- Copilot review や validator が依存する場合は、`.github/instructions/` や `.github/workflows/` も合わせて更新する