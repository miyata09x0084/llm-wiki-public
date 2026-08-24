---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org Route Handlers (2026-07-15取得).md"]
---

# nextjsjp.org Route Handlers

[[Next.js]] で API エンドポイントを作る Route Handlers のドキュメント。

## 要点

- `app` ディレクトリ内の `route.js|ts` で Web Request/Response API ベースのカスタムハンドラーを定義(pages の API Routes 相当)
- 対応 HTTP メソッドは `GET/POST/PUT/PATCH/DELETE/HEAD/OPTIONS`。未対応メソッドは 405 を返す
- デフォルトで非キャッシュ。`export const dynamic = 'force-static'` で `GET` のみキャッシュにオプトイン可
- 同一ルートセグメントに `page.js` と `route.js` は共存不可
- TypeScript ではグローバルな `RouteContext<'/users/[id]'>` ヘルパーで `context` に型付け可能(`next dev` / `build` / `typegen` で型生成)

## 重要 API

`route.ts`, `NextRequest`, `NextResponse`, `dynamic = 'force-static'`, `RouteContext`, `next typegen`
