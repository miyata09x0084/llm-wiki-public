---
type: concept
created: 2026-07-16
updated: 2026-07-16
tags: [技術, LLM, AIエージェント]
sources: ["raw/github.com mattpocock skills (2026-07-16取得).md"]
---

# スキルの書き方論(Writing Great Skills)

エージェント向けスキル(再利用可能な指示書)の書き方をメタ体系化した参照集。根の徳は **predictability(予測可能性)—— 同じ出力ではなく、毎回同じプロセスを踏むこと** で、以下のすべての道具はこれに奉仕する。「スキルとは確率的システムから決定論を絞り出すためのもの」という一文が思想の要約([[Skills For Real Engineers (mattpocock skills)]])。

## 2つのコストを見える化する: context load と cognitive load

スキルの起動方式は2択で、それぞれ異なるコストを払う。多くのスキル論が「簡潔に書け」としか言わない中、コストを2軸に分離した点が独自。

| 方式 | 仕組み | 払うコスト |
|---|---|---|
| model-invoked | description が常時コンテキストに載り、エージェントが自律起動できる | **context load** — 毎ターン、説明文ぶんのトークンを払い続ける |
| user-invoked | ユーザーがタイプしたときだけ起動 | **cognitive load** — ユーザー自身が「存在を覚えるインデックス」になる |

したがって分割・新設の判断基準は「その独立性はコストに見合うか」。user-invoked が記憶しきれないほど増えたら、router スキル(他スキルの一覧と使い分けを教える1枚)で cognitive load を回収する。

## 情報は3段の梯子に配置し、完了基準で縛る

スキルの中身は steps(順序ある手順)と reference(随時参照する定義・規則)の2種で、緊急度に応じて3段の梯子に置く: ①in-skill step ②in-skill reference ③external reference(別ファイルに追い出し、context pointer =「必要になったらここを読め」という誘導文経由で必要時のみロード)。

- **完了基準(completion criterion)は checkable かつ exhaustive に** —— 「変更リストを出す」ではなく「変更した全モデルを説明済み」。曖昧な基準は premature completion(早すぎる完了宣言)を招く
- **分割テストは branch(利用経路)** —— 全経路が使うものはインライン、一部の経路しか使わないものはポインタの先へ
- 押し下げすぎると本当に必要な情報が隠れ、押し上げすぎると先頭が肥大する。この緊張関係が配置判断のすべて

## leading word: 事前学習済みの1語で分散した定義を圧縮する

leading word とは、モデルの事前学習に既に住んでいる圧縮概念(例: red、fog of war、tracer bullets)を規律のアンカーに使う技法。「fast, deterministic, low-overhead」と3語で書く代わりに tight の1語、「信じられるループ」の代わりに red(テストが赤)の1語で、トークン削減と挙動の固定を同時に得る。ゆえに「すべてのスキルは leading word で退役させられる言い換えを抱えている」として、探して潰せと説く。

## 6つの失敗モードが診断語彙になる

| 失敗モード | 症状 | 対策 |
|---|---|---|
| premature completion | 完了前に「終わった」ことに注意が移る | まず完了基準を鋭くする。それでも駄目なら後続手順を別スキルに隠す |
| duplication | 同じ意味が複数箇所にある | 単一の情報源(single source of truth)に集約 |
| sediment | 追加は安全・削除は怖い、で堆積した古い層 | 剪定の規律。全行に「まだ関係あるか」を問う |
| sprawl | 全行が生きていても単に長すぎる | 梯子で追い出す+branch/手順で分割 |
| no-op | モデルが既定でやることを書いて負荷だけ払う | 「既定動作と比べて挙動が変わるか」テスト。弱い語(be thorough)は強い語(relentless)へ |
| negation | 禁止形は対象を想起させ逆効果(「象を考えるな」) | 目標挙動を肯定形で書き、禁止語を口にしない |

## 転用: CLAUDE.md と /lint を6失敗モードで監査できる

- **この Wiki の CLAUDE.md を6失敗モードで監査できる**。例: スタイル規約の「ラベル型見出し禁止」は negation 形 —— 「見出しは主張を含む文にする」と肯定形が主で禁止が従、の順に直すと理論に適合する。sediment 検査は /lint の項目に追加する価値がある
- **log.md の「`grep "^## \[" wiki/log.md | tail -5` で直近5件」は context pointer の既存実装**。全文ロードせず必要時に届く導線という同じ発想
- **「fog of war」「複利」のような leading word をこの Wiki でも意識的に採用する**。CLAUDE.md の「知識は複利で蓄積する」は既に成功例 —— 1語で蓄積・再投資・時間の3概念を圧縮している
- ⚠️ 留意: 6失敗モードは著者の運用経験からの帰納で、対照実験による裏付けはない
