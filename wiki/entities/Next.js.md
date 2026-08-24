---
type: entity
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org トップページ (2026-07-15取得).md", "raw/nextjsjp.org Next.js 16アップグレードガイド (2026-07-15取得).md"]
---

# Next.js

Vercel が開発する React ベースのフルスタック Web フレームワーク。[[React Server Components]] を基盤に、[[Server Actions]] と [[Cache Components]] でデータ取得から UI 更新までを完結させる。最新メジャーは **v16**(2026-07 時点)。

## アーキテクチャの柱

| 柱 | 内容 | 詳細ソース |
|----|------|-----------|
| ルーティング | ファイルシステムベース(`page` / `layout`、`[slug]` 動的セグメント) | [[nextjsjp.org レイアウトとページ]] |
| ナビゲーション | `<Link>` 自動プリフェッチ + ストリーミング + クライアントトランジション | [[nextjsjp.org リンクとナビゲーション]] |
| レンダリング | [[React Server Components]](デフォルト)+ `'use client'` 境界 | [[nextjsjp.org ServerコンポーネントとClientコンポーネント]] |
| データ取得 | Server Components で直接 await、Client へはプロミス + `use` | [[nextjsjp.org データの取得]] |
| データ更新 | [[Server Actions]](`'use server'`) | [[nextjsjp.org データの更新]] |
| キャッシュ | [[Cache Components]](v16 新モデル)+ タグベース再検証 | [[nextjsjp.org キャッシングと再検証]] |
| API | Route Handlers(`route.ts`) | [[nextjsjp.org Route Handlers]] |
| ビルド | [[Turbopack]](v16 でデフォルト化) | [[nextjsjp.org Turbopack]] |

## Next.js 16 の要点

- **[[Turbopack]] がデフォルトバンドラーに** — webpack は `--webpack` フラグでオプトアウト
- **[[Cache Components]]** — 実験的 PPR の後継。「デフォルト動的 + 明示的キャッシュ」へのパラダイム転換
- **非同期リクエスト API 完全移行** — `cookies` / `headers` / `params` / `searchParams` の同期アクセス削除
- **middleware → proxy** — `proxy.ts` にリネーム、nodejs ランタイムのみ
- **React 19.2 / React Compiler 対応** — `ViewTransition`、`useEffectEvent` など
- **型安全性強化** — `PageProps` / `LayoutProps` / `RouteContext` グローバル型ヘルパー(`next typegen`)
- 移行: `npx @next/codemod@canary upgrade latest`。詳細は [[nextjsjp.org Next.js 16アップグレードガイド]]

## 学習リソース

- 日本語ドキュメント: [[nextjsjp.org]](非公式・公式と同期)
- 公式: https://nextjs.org
