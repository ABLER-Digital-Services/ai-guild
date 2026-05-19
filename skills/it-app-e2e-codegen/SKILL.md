---
name: it-app-e2e-codegen
description: 'E2Eテスト仕様（YAML）からPlaywrightテストコード（.spec.ts）を生成する。Use when テストコードを生成する、specからコードを作る、YAMLからテストを実装する、テストを実装して、と依頼されたとき。'
---

# E2Eテストコード生成

YAML 仕様から、Playwright テストコードを生成する。

以下の `specs/`、`tests/`、`fixtures/` などの名称や配置は説明用の例です。実際のディレクトリ構成は対象リポジトリ側の E2E 規約に従ってください。

## When to Use This Skill

- specs に新しい YAML が追加されたとき
- 「テストコードを生成して」「spec から実装して」と依頼されたとき
- テスト仕様が変更され、コードを再生成する必要があるとき

## 入出力

仕様ディレクトリの構造を、テストコード側へ対応づける。

- **入力例**: `specs/<画面>/<アクション>.yaml`
- **出力例**: `tests/<画面>/<アクション>.spec.ts`

```
specs/login/login-success.yaml  →  tests/login/login-success.spec.ts
specs/login/login-error.yaml    →  tests/login/login-error.spec.ts
specs/inventory/add-to-cart.yaml → tests/inventory/add-to-cart.spec.ts
```

## コード生成ルール

### 1. セマンティックロケータを使う（必須）

DOM セレクタではなく、Playwright のセマンティックロケータを優先する。

**優先順位:**
1. `getByRole()` - ボタン、リンク、テキストボックス等
2. `getByLabel()` - フォーム入力フィールド
3. `getByPlaceholder()` - プレースホルダーテキスト
4. `getByText()` - 表示テキスト
5. `getByTestId()` - 上記で特定できない場合の最終手段

```typescript
// ✅ 良い例
await page.getByRole('button', { name: 'Login' }).click();
await page.getByPlaceholder('Username').fill('standard_user');

// ❌ 悪い例
await page.locator('#login-button').click();
await page.locator('input[data-test="username"]').fill('standard_user');
```

### 2. fixture を活用する

- YAML の `precondition` に対応する fixture を対象リポジトリ側の precondition カタログから特定する
- テストデータは対象リポジトリ側で定義された共有データモジュールから import する

**precondition → fixture のマッピング:**

コード生成時は必ず対象リポジトリ側の precondition カタログを参照し、precondition の key に対応する fixture 名を使う。

```yaml
# _preconditions.yaml の例
- key: "未ログイン状態"
  fixture: page
- key: "standard_userでログイン済み"
  fixture: loggedInPage
```

```typescript
// precondition: "未ログイン状態" → page（標準）
import { test, expect } from '@playwright/test';

// precondition: "standard_userでログイン済み" → loggedInPage
import { test, expect } from '../../fixtures/base';
test('...', async ({ loggedInPage: page }) => { ... });
```

- カタログに対応する precondition がない場合はコード生成を中断し、fixture の追加を促す
- テストデータの import 元は対象リポジトリ側の共有モジュールに合わせる

```typescript
import { PRODUCTS, CHECKOUT_INFO } from '../../fixtures/test-data';
```

### 3. 証跡を取得する

各テストの重要なステップで証跡を取得する。

```typescript
import { takeScreenshot } from '../helpers/evidence';

// アサーション前後でスクリーンショット
await takeScreenshot(page, 'checkout', 'before-confirm');
await page.getByRole('button', { name: 'Finish' }).click();
await takeScreenshot(page, 'checkout', 'after-confirm');
```

### 4. テスト構造のテンプレート

YAML 1ファイルから spec 1ファイルを生成する。テスト名には**シナリオID を必ず含める**（レポートから仕様へのトレーサビリティ確保）。

```typescript
import { test, expect } from '../../fixtures/base';
import { PRODUCTS } from '../../fixtures/test-data';
import { takeScreenshot } from '../../helpers/evidence';

test.describe('<feature> - <action>', () => {
  test('<シナリオID>: <シナリオ名>', async ({ loggedInPage: page }) => {
    // Arrange（前提条件の準備）

    // Act（操作の実行）

    // Assert（期待結果の検証）

    // Evidence（証跡取得）
    await takeScreenshot(page, '<scenario>', '<step>');
  });
});
```

**例:**
```typescript
test.describe('ログイン - ログイン成功', () => {
  test('LOGIN-001: 標準ユーザーでログインできる', async ({ page }) => { ... });
  test('LOGIN-002: パフォーマンス問題ユーザーでもログインできる', async ({ page }) => { ... });
});
```

**注意:** import パスの相対深度は、対象リポジトリ側のテストファイル配置に応じて調整する。

### 5. アサーションの書き方

YAML の `expect` を Playwright のアサーションに変換する。

| YAML の expect | Playwright アサーション |
|---|---|
| 「〜」と表示される | `await expect(page.getByText('〜')).toBeVisible()` |
| 〜ページに遷移する | `await expect(page).toHaveURL(/pattern/)` |
| 〜が N 件表示される | `await expect(page.locator('.item')).toHaveCount(N)` |
| 〜が無効化されている | `await expect(locator).toBeDisabled()` |

### 6. 待機処理

- 明示的な `waitForTimeout()` は使わない
- Playwright の auto-waiting を信頼する
- ネットワーク待機が必要な場合は `waitForResponse()` を使う
- ページ遷移待ちは `page.waitForURL(pattern)` を使う
- アニメーション完了待ちは `locator.waitFor({ state: 'stable' })` を検討する

### 7. DB 確認（`DB:` プレフィックス）の扱い

YAML の expect に `DB:` プレフィックスがある場合：

- 対象リポジトリ側の E2E 規約に、DB 検証用ヘルパーや検証手順があるかを先に確認する
- DB 確認ヘルパーが存在する場合は、その呼び出しに変換する
- DB 確認手段が未整備な場合は、`DB:` 付きの expect を**テストコードにコメントとして残し、追加実装が必要な確認事項として明示する**

```typescript
// DB確認: orders テーブルに該当レコードが1件追加される
// → DB確認ヘルパー未整備のため、追加実装が必要
```

DB ヘルパーの配置先や実装方法は固定せず、対象リポジトリ側の E2E 規約・既存ヘルパー・命名規約に従ってアサーションへ変換する。

## 生成後のチェックリスト

- [ ] セマンティックロケータを使っているか
- [ ] ハードコードされた値が fixtures に定義されているか
- [ ] 証跡取得が含まれているか
- [ ] `waitForTimeout()` を使っていないか
- [ ] テスト同士が独立しているか（順序依存がないか）
