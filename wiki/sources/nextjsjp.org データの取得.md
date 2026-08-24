---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org データの取得 (2026-07-15取得).md"]
---

# nextjsjp.org データの取得

[[Next.js]] におけるデータフェッチングのドキュメント。

## 要点

- Server Components では `fetch` API または ORM / DB クエリを直接 await。`fetch` レスポンスはデフォルト非キャッシュ
- Client Components ではサーバーからプロミスを props で渡し React の `use` フックでストリーミング取得、または SWR / React Query
- リクエスト重複排除: リクエストメモ化(同一 URL + オプションの GET/HEAD を1リクエストに統合)、データキャッシュ(`cache: 'force-cache'`)、ORM には React `cache` 関数
- ストリーミングは `loading.js`(ページ全体)か `<Suspense>`(細粒度)の2方式。⚠️ `cacheComponents` 有効が前提との警告あり
- パターン例: 順次データ取得(Suspense でブロック回避)、並行取得(`Promise.all`)、事前読み込み(`preload` + `void` + `server-only`)

## 重要 API

`fetch`, `use` フック, SWR, React `cache`, `loading.js`, `<Suspense>`, `Promise.all`, `preload`, `server-only`

## 取得ノート

WebFetch では全文転記できず、curl + HTML→Markdown 変換で取得。図5点は画像 URL 取得不可のため alt 文の注記に置換済み。
