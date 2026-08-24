---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org Turbopack (2026-07-15取得).md"]
---

# nextjsjp.org Turbopack

[[Turbopack]] の API リファレンスページ。

## 要点

- Rust 製インクリメンタルバンドラー。v16.0.0 で [[Next.js]] の**デフォルトバンドラー**になった(設定不要、Webpack へ戻すには `--webpack` フラグ)
- 高速化の仕組み: 統一グラフ、開発時バンドル、関数レベルの結果キャッシュ、レイジーバンドリング
- Babel 設定ファイル検出時は自動で Babel 使用(v16 以降)。CSS は Lightning CSS、Sass 対応(`sassOptions.functions` は非対応)
- webpack とのギャップ: CSS モジュール順序、`~` チルダ Sass インポート非対応、Inner Graph Optimization 未実装、webpack プラグイン非対応(ローダーは対応)
- ファイルシステムキャッシュはベータ: `experimental.turbopackFileSystemCacheForDev` / `ForBuild`

## 重要 API

`--webpack`, `turbopack.rules`, `turbopack.resolveAlias`, `turbopack.resolveExtensions`, `NEXT_TURBOPACK_TRACING=1`, `experimental.turbopackFileSystemCacheForDev`
