---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js, React]
sources: ["raw/nextjsjp.org ServerコンポーネントとClientコンポーネント (2026-07-15取得).md"]
---

# nextjsjp.org ServerコンポーネントとClientコンポーネント

[[React Server Components]] の [[Next.js]] における使い方の中核ドキュメント。

## 要点

- デフォルトは Server Component。Client Component は `'use client'` で State / イベント / ブラウザ API / カスタムフックが必要な場合のみ
- RSC Payload(レンダリング結果 + Client コンポーネントのプレースホルダ + props)がサーバーで生成されクライアントへ。初回は HTML → RSC Payload 調整 → ハイドレーションの3段階
- `'use client'` はモジュールグラフの境界宣言。そのファイルのインポートと子は全てクライアントバンドルになる(バンドル削減のためリーフに置く)
- Server → Client へはシリアライズ可能な props か `use` フックで渡す。Server コンポーネントは Client の `children` スロットに渡せる(Context プロバイダーもこのパターン)
- `server-only` / `client-only` パッケージで環境汚染を防止。`NEXT_PUBLIC_` なし環境変数はクライアントで空文字

## 重要 API

`'use client'`, RSC Payload, ハイドレーション, `use` フック, `server-only`, `client-only`, `NEXT_PUBLIC_`
