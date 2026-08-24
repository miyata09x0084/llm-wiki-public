---
type: concept
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org Cache Components (2026-07-15取得).md", "raw/nextjsjp.org Next.js 16アップグレードガイド (2026-07-15取得).md"]
---

# Cache Components

[[Next.js]] 16 の新しいキャッシュ・レンダリングモデル。実験的だった Partial Prerendering(PPR)と `use cache` を統合し、`cacheComponents: true` で有効化する。`experimental_ppr` / `dynamicIO` は削除され、これに一本化された。

## パラダイム転換

| | 従来(〜v15) | Cache Components(v16) |
|--|--|--|
| デフォルト | 静的(ビルド時プリレンダー) | **動的**(リクエスト時レンダー) |
| キャッシュ | 暗黙的(fetch 自動キャッシュ等) | **明示的**(`use cache` を書いた所だけ) |
| PPR | 実験フラグ | 標準動作(静的シェル + 動的ストリーミング) |

「知らないうちにキャッシュされていた」事故を無くし、キャッシュを**opt-in**にするのが設計思想。

## 3つの制御ツール

1. ランタイムデータ(`cookies` / `headers` / `searchParams`)→ `<Suspense>` 境界で包む
2. 動的データ(`fetch` / DB)→ 同じく `<Suspense>` でストリーミング
3. キャッシュしたい部分 → `use cache` ディレクティブ + `cacheLife`(期間)+ `cacheTag`(タグ)

## 再検証 API

- `updateTag` — 即時期限切れ(Server Action 専用、read-your-own-writes)
- `revalidateTag(tag, 'max')` — stale-while-revalidate(推奨)
- 従来の `dynamic` / `revalidate` / `fetchCache` ルートセグメント設定は不要化

## 制約

- Edge Runtime 非対応

出典: [[nextjsjp.org Cache Components]]、[[nextjsjp.org Next.js 16アップグレードガイド]]。[[Server Actions]] と密接に連携。
