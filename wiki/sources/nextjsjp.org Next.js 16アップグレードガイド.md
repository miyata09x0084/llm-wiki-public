---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org Next.js 16アップグレードガイド (2026-07-15取得).md"]
---

# nextjsjp.org Next.js 16アップグレードガイド

[[Next.js]] 15 → 16 の移行ガイド。破壊的変更と新 API の一次情報として最重要のソース。

## 要点

- アップグレード手段: コードモッド `npx @next/codemod@canary upgrade latest`、または Next.js DevTools MCP(`next-devtools-mcp`)で AI エージェント自動化
- 要件: Node.js 20.9+、TypeScript 5.1+。[[Turbopack]] が dev/build のデフォルトに(カスタム webpack 設定があるとビルド失敗、`--webpack` で回避)

### 破壊的変更

- 非同期リクエスト API の同期アクセス完全削除(`cookies` / `headers` / `draftMode` / `params` / `searchParams`)
- `middleware` → `proxy` へリネーム(edge ランタイム非対応、nodejs のみ)
- 並列ルート全スロットに `default.js` 必須

### キャッシング関連

- `revalidateTag(tag, 'max')` 新シグネチャ、`updateTag`・`refresh` 新 API、`cacheLife` / `cacheTag` 安定化
- PPR は `cacheComponents: true` に統一(`experimental_ppr`・`dynamicIO` 削除)→ [[Cache Components]]

### 削除・非推奨

- AMP 完全削除、`next lint` 削除、`serverRuntimeConfig` / `publicRuntimeConfig` 削除
- `next/legacy/image`・`images.domains` 非推奨
- `next/image` デフォルト変更(`minimumCacheTTL` 4時間、`qualities` `[75]`、`imageSizes` から 16px 削除)

## 重要 API

`proxy.ts`, `cacheComponents`, `updateTag`, `refresh`, `revalidateTag(tag, 'max')`, `--webpack`, `PageProps` / `LayoutProps` / `RouteContext`, `next typegen`, `reactCompiler`, React 19.2(`ViewTransition` / `useEffectEvent` / `Activity`)

## 取得ノート

WebFetch では要約しか得られず、curl + HTML→Markdown 変換で全文取得(全24セクション・約1100行)。コードブロック内の一部に原文サイト由来の全角カンマ、タブ切替 UI のラベル残存あり。
