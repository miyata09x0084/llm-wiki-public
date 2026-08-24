---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org データの更新 (2026-07-15取得).md"]
---

# nextjsjp.org データの更新

[[Server Actions]](Server Functions)によるデータ更新のドキュメント。

## 要点

- Server Function はサーバー上で実行される非同期関数。mutation 文脈では Server Action と呼ばれ、`POST` メソッドのみで呼び出される
- `'use server'` ディレクティブで定義。Server Components にはインライン可、Client Components ではインポートのみ可
- 呼び出し方法は2系統: `<form action>` / `formAction`(フォーム)と、`onClick` 等のイベントハンドラー・`useEffect`
- 更新後は `revalidatePath` / `revalidateTag` でキャッシュ再検証、`redirect` でページ遷移(redirect は制御フロー例外をスローするため後続コードは実行されない)
- Server Action 内で cookie を set/delete すると現在ページとレイアウトが再レンダリングされ UI に即反映

## 重要 API

`'use server'`, `useActionState`, `startTransition`, `revalidatePath`, `revalidateTag`, `redirect`, `cookies`, `FormData`
