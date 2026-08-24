---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org Cache Components (2026-07-15取得).md"]
---

# nextjsjp.org Cache Components

[[Next.js]] 16 の新キャッシュモデル [[Cache Components]] の入門ドキュメント。

## 要点

- `cacheComponents: true` でオプトイン。Partial Prerendering(PPR)と `use cache` を実装
- 有効化すると全ルートが**デフォルトで動的**に(従来の「デフォルトで静的」から転換)。静的シェル + Suspense 境界内の動的部分をストリーミング
- 3つの制御ツール: ランタイムデータ(`cookies` / `headers` / `searchParams`)の Suspense、動的データ(`fetch` / DB)の Suspense、`use cache` ディレクティブ
- `cacheTag` + `updateTag`(即時更新)/ `revalidateTag`(stale-while-revalidate)で再検証
- `dynamic` / `revalidate` / `fetchCache` 等のルートセグメント設定は不要化・`use cache` + `cacheLife` へ移行。Edge Runtime は非対応

## 重要 API

`use cache`, `cacheComponents`, `cacheLife`, `cacheTag`, `updateTag`, `revalidateTag`, `<Suspense>`, `connection`
