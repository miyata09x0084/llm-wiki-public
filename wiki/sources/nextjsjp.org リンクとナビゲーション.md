---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org リンクとナビゲーション (2026-07-15取得).md"]
---

# nextjsjp.org リンクとナビゲーション

[[Next.js]] のナビゲーション高速化の仕組みを解説するドキュメント。

## 要点

- ナビゲーション高速化の4本柱: サーバーレンダリング(静的/動的)、プリフェッチ、ストリーミング、クライアント側トランジション
- `<Link>` はビューポート進入時に自動プリフェッチ(静的ルートは全体、動的ルートは `loading.tsx` があれば部分プリフェッチ)
- 遅いトランジションの主因と対策: `loading.tsx` なし動的ルート、`generateStaticParams` なし動的セグメント、低速ネットワーク(`useLinkStatus`)、ハイドレーション未完了
- `prefetch={false}` やホバー時のみプリフェッチでリソース使用を制御可能
- `window.history.pushState` / `replaceState` は Next.js Router と統合され `usePathname` / `useSearchParams` と同期

## 重要 API

`<Link>`, `prefetch`, `loading.tsx`, `generateStaticParams`, `useLinkStatus`, `<Suspense>`, `pushState` / `replaceState`
