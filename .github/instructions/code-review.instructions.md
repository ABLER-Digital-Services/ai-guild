---
applyTo: "**"
excludeAgent: "cloud-agent"
---

このリポジトリの Copilot code review では、コメントは日本語で書いてください。

指摘は、実害のある不整合、運用リスク、リンク切れ、設定漏れ、レビュー観点の欠落に絞ってください。単なる好みのスタイル指摘は避けてください。

Pull Request では、`.github/PULL_REQUEST_TEMPLATE.md` の必須見出しが埋まっている前提で、本文と実際の差分が一致しているかを確認してください。

`README.md`、`CONTRIBUTING.md`、`.docs` 配下をレビューするときは、利用者向け説明と内部運用ルールの矛盾、古いパス参照、リンク切れ、手順の更新漏れを優先して確認してください。

`instructions`、`agents`、`skills`、`hooks`、`workflows` をレビューするときは、危険な権限委譲、秘密情報の混入、外部サービス依存の説明不足、既存資産との重複を優先して確認してください。

workflow をレビューするときは、固定 IP runner の必要性、人間向け文面の日本語化、権限スコープの過不足、repository 構成ルールとの整合を確認してください。

このリポジトリでは Copilot review は早期検知の自動信号であり、最終判断は人間レビューと required checks が担います。曖昧な懸念は広く列挙せず、再現可能で差分に結びつく指摘だけを残してください。


## コメントのメタ情報

各レビューコメントの冒頭には、次のいずれか 1 つを明示する。

- `[must]` 修正必須。この問題が残ると Approve できない。
- `[ask]` 回答必須。実装意図や根拠の確認が必要。
- `[imo]` 修正任意。別案や表現の提案。
- `[nits]` 修正任意。軽微な指摘。
- `[next]` 今回の修正は不要だが、今後の改善案。
- `[memo]` コード理解の補足メモ。
- `[good]` 良い点のフィードバック。

可能な限り、各コメントの先頭には対応する画像バッジ Markdown を明示的に出力する。画像バッジの直後に、同じ種別のテキストタグも必ず併記する。

- `must`: `![must-badge](https://img.shields.io/badge/review-must-red.svg) [must]`
- `ask`: `![ask-badge](https://img.shields.io/badge/review-ask-yellowgreen.svg) [ask]`
- `imo`: `![imo-badge](https://img.shields.io/badge/review-imo-orange.svg) [imo]`
- `nits`: `![nits-badge](https://img.shields.io/badge/review-nits-green.svg) [nits]`
- `next`: `![next-badge](https://img.shields.io/badge/review-next-blueviolet.svg) [next]`
- `memo`: `![memo-badge](https://img.shields.io/badge/review-memo-lightgrey.svg) [memo]`
- `good`: `![good-badge](https://img.shields.io/badge/review-good-brightgreen.svg) [good]`

各コメントは、原則として次の形式で始める。

`![must-badge](https://img.shields.io/badge/review-must-red.svg) [must] 問題点の要約`

画像バッジを使える場合は省略しない。Markdown 画像が表示されない環境でも意味が残るよう、テキストタグは必ず残す。

## 出し分けのルール

- `must` は明確な不具合、仕様逸脱、重大な保守性低下、セキュリティ問題、テスト不足に限定する。
- `ask` は、意図が不明な実装・根拠不足の仕様変更・外部根拠が必要な判断に使う。
- `imo` と `next` は、必須ではない改善提案に使う。
- `good` は本当に価値のある設計・実装・テストの工夫があるときだけ使う。
- `nits` を大量に並べて重要指摘を埋もれさせない。