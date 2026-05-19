# AI レビュー方針

ai-guild の AI 自動レビュー初版は、GitHub Rulesets と Copilot code review を軸に始めます。

## この方針の意味

ここでいう GitHub 標準寄りとは、GitHub 上で完結する既存機能と通常の Pull Request チェックを中心に運用することです。

対象例:

- GitHub Copilot code review
- Pull Request テンプレート
- CODEOWNERS
- Rulesets
- GitHub Actions による軽量な妥当性チェック

## 初版で目指すこと

- 導入と運用を重くしない
- シークレット管理を増やしすぎない
- 人間レビューの前段で明らかな抜け漏れを減らす
- Pull Request 作成直後に自動で初回レビュー信号を出す
- どの観点が不足するかを実運用で把握する

## 初版でやるレビュー

- Pull Request テンプレート必須項目の確認
- 許可されたディレクトリ構成の確認
- Copilot code review の自動実行
- `.github/instructions/*.instructions.md` によるレビュー観点の補強
- skills 向けの独立 validator を required check として実行
- CODEOWNERS と人間レビューの前提整備
- Rulesets による main 保護

## 初版でまだやらないこと

- 外部 LLM API を呼ぶ専用レビュー
- ファイル種別ごとの高度な意味解析
- 独自スコアリングや自動採点
- 複数エージェントによる並列レビューの本格運用

## 後から追加する判断基準

次のどれかが明確になったら、Actions ベースの専用レビュー追加を検討します。

- instructions や agents の危険性チェックが標準機能では足りない
- skills や .docs の重複判定をもっと自動化したい
- メタデータ検証をカテゴリ別に強化したい
- PR 数が増え、人手レビュー前の仕分けが必要になった

## 段階的な拡張イメージ

1. GitHub 標準寄りの運用で開始
2. Rulesets と PR ガードを有効化
3. Copilot code review を自動実行
4. メタデータ検証を追加
5. 必要になったカテゴリだけ専用レビューを追加