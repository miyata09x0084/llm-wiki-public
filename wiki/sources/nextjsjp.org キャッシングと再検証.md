---
type: source
created: 2026-07-15
updated: 2026-07-15
tags: [技術, Web開発, Next.js]
sources: ["raw/nextjsjp.org キャッシングと再検証 (2026-07-15取得).md"]
---

# nextjsjp.org キャッシングと再検証

[[Next.js]] のキャッシュ戦略と再検証 API のドキュメント。

## 要点

- `fetch` はデフォルトで非キャッシュ。`cache: 'force-cache'` でキャッシュ、`next: { revalidate: 秒数 }` で時間ベース再検証
- `unstable_cache` で DB クエリ等の非同期関数結果をキャッシュ(キー配列 + `tags` / `revalidate` オプション)
- `revalidateTag` は2動作: `profile="max"` 付き(stale-while-revalidate、推奨)と引数なし(即時期限切れ、非推奨)
- `updateTag` は Server Action 専用の新 API。read-your-own-writes 用にキャッシュを即時期限切れにする
- `revalidatePath` はルート単位の再検証(Route Handler / Server Action で呼ぶ)

## 重要 API

`fetch` + `force-cache`, `next.revalidate`, `next.tags`, `unstable_cache`, `revalidateTag('tag', 'max')`, `updateTag`, `revalidatePath`, `connection`

## 関連

- [[Cache Components]] — v16 の新キャッシュモデル(こちらが今後の主流)
- [[Server Actions]] — 更新後の再検証の起点
