---
type: concept
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, React, Next.js]
sources: ["raw/nextjsjp.org データの更新 (2026-07-15取得).md"]
---

# Server Actions

クライアントから直接呼び出せるサーバー関数。API エンドポイントを書かずに、1回のネットワークラウンドトリップでデータ更新 + キャッシュ再検証 + UI 更新を完結させる [[Next.js]] / React の仕組み。総称は Server Functions で、mutation 文脈のものを Server Action と呼ぶ。

## 基本

- `'use server'` ディレクティブで定義。常に `POST` で呼ばれる
- Server Component 内にはインライン定義可。Client Component からは別ファイルからのインポートのみ
- 呼び出しは2系統: `<form action={fn}>`(プログレッシブエンハンスメント対応)と、イベントハンドラ / `useEffect` からの直接呼び出し

## 更新後の定石

```
更新 → revalidatePath / revalidateTag / updateTag → (必要なら) redirect
```

- `redirect` は制御フロー例外をスローする — 以降のコードは実行されない点に注意
- cookie の set/delete も再レンダリングをトリガーし UI に即反映
- ペンディング状態は `useActionState` / `startTransition` で扱う

## 関連

- [[React Server Components]] — 実行基盤
- [[Cache Components]] — `updateTag`(read-your-own-writes)との連携
- 出典: [[nextjsjp.org データの更新]]、[[nextjsjp.org キャッシングと再検証]]
