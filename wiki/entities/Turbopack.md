---
type: entity
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js, ビルドツール]
sources: ["raw/nextjsjp.org Turbopack (2026-07-15取得).md"]
---

# Turbopack

Vercel 製の Rust 実装インクリメンタルバンドラー。[[Next.js]] 16.0.0 で **dev / build 両方のデフォルトバンドラー**になった。

## 特徴

- 高速化の仕組み: 統一グラフ、開発時バンドル、関数レベルの結果キャッシュ、レイジーバンドリング
- CSS は Lightning CSS で処理。Babel 設定ファイルがあれば自動で Babel を使用(v16 以降)
- webpack に戻すには `--webpack` フラグ

## webpack とのギャップ(移行時の注意)

- webpack プラグイン非対応(ローダーは `turbopack.rules` で対応)
- `~` チルダ Sass インポート非対応、`sassOptions.functions` 非対応
- CSS モジュールの順序挙動が異なる
- Inner Graph Optimization 未実装(バンドルサイズに影響しうる)

## 実験的機能

- ファイルシステムキャッシュ(ベータ): `experimental.turbopackFileSystemCacheForDev` / `ForBuild`
- デバッグ: `NEXT_TURBOPACK_TRACING=1`

出典: [[nextjsjp.org Turbopack]]、[[nextjsjp.org Next.js 16アップグレードガイド]]
