---
type: concept
created: 2026-07-16
updated: 2026-07-16
tags: [技術, LLM]
sources: ["raw/2026-07-16-attention-is-all-you-need-arxiv-1706.03762.pdf"]
---

# Attention機構

**「どのトークンがどのトークンをどれだけ参照するか」を全ペア一括で計算する機構。** [[Transformer]] の心臓部。出典: [[Attention Is All You Need (2017)]]。

## 核心は1本の式 — 意味は「類似度で重み付けした Value の加重和」

```
Attention(Q,K,V) = softmax(QKᵀ/√dk) V
```

Q/K/V の直感は検索エンジンである: **Query=検索語、Key=索引、Value=中身**。各トークンが Query を発行し、全トークンの Key との内積(類似度)を softmax(合計1の重み分布に変換する関数)で正規化し、Value の加重和を受け取る。

**√dk で割る理由**: 成分が平均0・分散1なら内積 q·k の分散は dk。したがって次元が大きいと内積が肥大し、softmax が飽和領域に入って勾配がほぼ消える。√dk がこれを正規化する(原論文の脚注4)。

## Multi-Head — 単一ヘッドは「平均」なので関係の種類を潰す

attention を h=8 本(各 dk=dv=64)に分けるのは、1本の加重平均では複数種類の関係(構文・照応・意味)が混ざって潰れるためである。

- 分割しても計算コストは単一ヘッドの全次元版と同等
- 効果の証拠: ablation(部品を外して寄与を測る実験)で単一ヘッドは −0.9 BLEU(翻訳の自動評価スコア)
- 付録の可視化では、照応解決(its→Law)を担うヘッドや構文構造に沿うヘッドが**教えていないのに自然発生**

## 3用法 — GPT 系 LLM の中身は decoder の masked self-attention

同じ機構が、Q/K/V の出所を変えるだけで3役をこなす。

| 用法 | Q の出所 | K/V の出所 | 役割 |
|------|---------|-----------|------|
| encoder self-attention | 前層の encoder | 同じ | 入力を双方向に文脈化 |
| decoder masked self-attention | 前層の decoder | 同じ | 未来のトークンを −∞ でマスクし自己回帰性を担保。**GPT 系 LLM の中身はこれ** |
| encoder-decoder attention | decoder | encoder 出力 | 生成中に入力を参照(翻訳の「見ながら書く」) |

## 関連

[[Transformer]] / [[LLMの原理]]
