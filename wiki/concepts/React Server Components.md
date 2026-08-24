---
type: concept
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, React, Next.js]
sources: ["raw/nextjsjp.org ServerコンポーネントとClientコンポーネント (2026-07-15取得).md"]
---

# React Server Components

React のコンポーネントをサーバー側でレンダリングし、クライアント JS を送らずに UI を構築するアーキテクチャ。RSC と略される。[[Next.js]] App Router の基盤概念。

## メンタルモデル

- **デフォルトは Server Component** — データ取得・シークレット参照はサーバーで完結し、バンドルに含まれない
- **`'use client'` は「境界」宣言** — コンポーネント単位ではなくモジュールグラフの境界。そのファイルの import 先と子は全てクライアントバンドル入りする → 境界はできるだけ**リーフ(末端)に置く**のがバンドル削減のコツ
- Client Component が必要なのは: State、イベントハンドラ、ブラウザ API、それらに依存するカスタムフックのみ

## 動作の仕組み

1. サーバーで RSC Payload(レンダリング結果 + Client コンポーネントのプレースホルダ + props)を生成
2. 初回アクセス: HTML(高速な初期表示)→ RSC Payload で DOM 調整 → ハイドレーションの3段階
3. 以降のナビゲーション: RSC Payload のみで更新

## 実践パターン

- Server → Client には**シリアライズ可能な props** か、プロミスを渡して `use` フックで解決
- Server コンポーネントを Client の `children` スロットに差し込める(Context プロバイダーはこのパターン)
- `server-only` / `client-only` パッケージで誤った環境での実行をビルドエラー化

出典: [[nextjsjp.org ServerコンポーネントとClientコンポーネント]]
