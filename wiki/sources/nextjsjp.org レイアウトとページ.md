---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org レイアウトとページ (2026-07-15取得).md"]
---

# nextjsjp.org レイアウトとページ

[[Next.js]] のファイルシステムベースルーティングの基本ドキュメント。

## 要点

- フォルダ = URL セグメント、ファイル(`page` / `layout`)= UI という対応
- ルートレイアウト(`app/layout.tsx`)は必須で `html` / `body` タグを含む。レイアウトはナビゲーション間で状態保持され再レンダリングされない
- `[slug]` のような角括弧フォルダで動的セグメントを作成。`params` は `Promise` で await して取得
- `searchParams` プロップを使うとページは動的レンダリングにオプトイン。クライアント側のみなら `useSearchParams`
- Next.js 16 の新機能: `PageProps` / `LayoutProps` グローバル型ヘルパー(インポート不要、`next typegen` で生成)

## 重要 API

`page.tsx`, `layout.tsx`, `[slug]`, `params`, `searchParams`, `useSearchParams`, `<Link>`, `PageProps`, `LayoutProps`
