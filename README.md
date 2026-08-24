# LLM Wiki

[Karpathy の LLM Wiki パターン](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)に基づく個人ナレッジベース。

**LLM が Wiki を書き、人間はソースの供給と質問に専念する。**
Obsidian が IDE、LLM がプログラマー、Wiki がコードベース。

## 使い方

### 1. ソースを追加する

記事・論文・メモ・書き起こしなどを `raw/` に置く(Markdown 推奨)。

- [Obsidian Web Clipper](https://obsidian.md/clipper) で Web 記事を Markdown 化して `raw/` に保存すると楽
- 画像は `raw/assets/` に(Obsidian の添付保存先に設定済み)

### 2. 取り込む

Claude Code でこのディレクトリを開いて:

```
/ingest
```

または「raw/ に◯◯を置いたので取り込んで」。
LLM が要約 → 関連ページ更新 → index / log 更新まで行う。

### 3. 質問する

そのまま聞くだけ:

- 「◯◯について、これまでの情報を整理して」
- 「AとBを比較して」

良い回答は `wiki/answers/` に保存され、知識が複利で蓄積される。

### 4. 定期メンテナンス

```
/lint
```

矛盾・孤立ページ・情報ギャップをチェックする。

## Obsidian で閲覧する

このフォルダ(`llm-wiki/`)を Vault として開く。

- **グラフビュー**で Wiki の全体像・ハブページ・孤立ページが見える
- Settings → Hotkeys → "Download attachments for current file" にホットキーを割り当てると、クリップした記事の画像を一括ローカル保存できる

## 構造

| パス | 役割 | 書くのは |
|---|---|---|
| `raw/` | 不変のソース | 人間 |
| `wiki/` | 生成ページ(index / log / sources / entities / concepts / topics / answers) | LLM |
| `CLAUDE.md` | スキーマ(LLM の運用規約) | 共同(合意の上で更新) |

---

> このリポジトリは private リポジトリのサニタイズ済みミラーです。
> raw/(ソース原文)と一部の非公開ページは含まれません。
