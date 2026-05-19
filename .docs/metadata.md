# 資産メタデータ仕様

ai-guild では、将来的な検索、索引生成、レビュー自動化のために、各資産にメタデータを持たせる前提で設計します。

## まず必須にしたい項目

- title
- summary
- owners
- status
- target-agents
- tags

## 推奨項目

- audience
- scope
- last-reviewed
- version
- references

## status の候補

- experimental
- reviewed
- approved
- deprecated

## audience の候補

- beginner
- team-standard
- advanced
- admin-only

## scope の候補

- company-wide
- product-specific
- language-specific
- workflow-specific

## target-agents の考え方

複数値を許可します。

例:

- github-copilot
- codex
- claude-code
- tool-agnostic

## YAML 例

```yaml
---
title: Pull Request Review Assistant
summary: Pull Request の背景整理とレビュー観点の補助を行う
owners:
  - team-platform
status: experimental
target-agents:
  - github-copilot
  - claude-code
tags:
  - review
  - pull-request
audience: team-standard
scope: company-wide
last-reviewed: 2026-05-18
---
```

## 運用方針

- 初期段階では .docs と cookbook は緩めに始める
- instructions、agents、skills、hooks、workflows は早めにそろえる
- 必須項目は自動チェックの対象にしていく