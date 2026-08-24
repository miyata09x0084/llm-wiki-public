---
type: concept
created: 2026-07-16
updated: 2026-07-16
tags: [技術, LLM]
sources: ["raw/2026-07-16-attention-is-all-you-need-arxiv-1706.03762.pdf"]
---

# Transformer

**attention のみで系列を処理するニューラルネットアーキテクチャ。逐次計算を持たないため GPU で並列学習でき、これが LLM のスケーリングを可能にした。** [[Attention Is All You Need (2017)]] で提案。現代の LLM(GPT / Claude / Llama / Gemini)は全てこの派生。

## 原型は encoder-decoder — attention に配管部品を足した積層構造

部品は4種だけで、encoder(入力全体を表現に変換する側)と decoder(出力を1トークンずつ生成する側)を各6層積む。

| 部品 | 役割 |
|------|------|
| [[Attention機構]] + FFN(feed-forward network、各位置に同一適用される2層の全結合) | 各層の本体。attention が文脈を混ぜ、FFN が変換する |
| masked self-attention(decoder 側) | 未来のトークンを隠し、自己回帰生成(直前までの出力を入力に足しながら1つずつ生成)を成立させる |
| 残差接続(入力をそのまま出力に足すバイパス)+ LayerNorm(層単位の正規化) | 深い層でも勾配を通す配管 |
| positional encoding | attention は語順を知らないため、正弦波で位置情報を注入 |

寸法の原器: d_model=512、FFN 2048、8ヘッド。以後のモデルはこの相似拡大。

## 家系は3つ — 現代 LLM は decoder-only に収斂した

原型の encoder / decoder のどちらを使うかで3家系に分かれ、生成 AI の主流は decoder-only になった。

| 家系 | 使う側 | 代表 | 得意 |
|------|--------|------|------|
| decoder-only | decoder のみ | GPT、Claude、Llama | 生成。現代 LLM はほぼここ |
| encoder-only | encoder のみ | BERT | 理解・分類・埋め込み |
| encoder-decoder | 両方(原型) | T5、翻訳モデル | 系列変換(翻訳・要約) |

収斂の理由: 次トークン予測だけで訓練でき、タスクを選ばないため(リスト#3 GPT-3 で本格化する問い)。

## RNN への勝因は並列性とパス長 O(1)、代償は計算量 O(n²)

- **勝因1 — パス長 O(1)**: 任意の2トークンが1ホップで繋がる(RNN は O(n)ホップ)。したがって長距離依存が学びやすい
- **勝因2 — 並列性**: 逐次演算 O(1) で全トークン同時に計算。学習が GPU に乗る。したがってスケール可能
- **代償 — O(n²·d)**: 文脈長の2乗で計算が膨らむ。長文脈対応(FlashAttention 等)は現在も続く研究戦線

## 関連

[[Attention機構]] / [[LLMの原理]] / [[BERT (2018)]](encoder 家系の実例)/ [[LLMの原理を学ぶ論文リスト(コア10本+拡張12本)]]
