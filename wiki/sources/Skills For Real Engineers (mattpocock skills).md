---
type: source
created: 2026-07-16
updated: 2026-07-16
tags: [技術, LLM, AIエージェント]
sources: ["raw/github.com mattpocock skills (2026-07-16取得).md"]
---

# Skills For Real Engineers (mattpocock skills)

[[Matt Pocock]] が日常のエンジニアリングで実際に使う AI コーディングエージェント向けスキル集。計40スキル(推奨セット22 = engineering 17 + productivity 5)。GSD・BMAD・Spec-Kit のような「プロセスがユーザーを所有する」重量級フレームワークへの対抗として、**小さく・改造可能・合成可能**なスキルで古典的エンジニアリング原則をエージェント運用に翻訳する。

- 取得元: https://github.com/mattpocock/skills(コミット e9fcdf9、2026-07-14 時点)
- 配布は2系統: skills.sh(コピーして自分で改造する)と Claude Code plugin(読み取り専用・自動更新を購読する)

## 核となる主張: エージェントの4大失敗モードには古典の処方箋が効く

README は「AI 時代こそソフトウェアエンジニアリングの基礎が効く」と言い切り、失敗モードごとに古典を引いて処方箋スキルを対応させる。

| 失敗モード | 処方箋スキル | 根拠の古典 |
|---|---|---|
| 1. 意図とズレたものを作る | `/grill-me` → [[Grilling(質問駆動アライメント)]] | Thomas & Hunt『The Pragmatic Programmer』"No-one knows exactly what they want" |
| 2. 冗長すぎる | `/grill-with-docs`(共通言語を CONTEXT.md に蓄積) | Eric Evans『Domain-Driven Design』の ubiquitous language(プロジェクト共通言語) |
| 3. コードが動かない | `/tdd`(失敗するテストを先に書く red-green ループ+テスト1本ずつ縦に進める vertical slice) | Kent Beck『Extreme Programming Explained』 |
| 4. 泥団子化する | `/improve-codebase-architecture` → [[深いモジュール設計(Deep Modules)]] | John Ousterhout『A Philosophy of Software Design』 |

失敗モード2の共通言語は具体例が雄弁: 「コースのセクション内のレッスンが『実体化』される(ファイルシステム上の場所を得る)ときに問題がある」が、共通言語の確立後は「materialization cascade に問題がある」の一言になる。ゆえに冗長性が減るだけでなく、命名の一貫性・コードベースの探索性・thinking トークンの節約まで波及する。

## 構造の発明: スキルを user-invoked と model-invoked の2層に分ける

すべてのスキルは「誰が起動できるか」の1軸で分類され、役割が非対称になっている。

- **user-invoked**(ユーザーがタイプしたときだけ起動、例 `/grill-me` `/wayfinder`): オーケストレーション担当。コンテキストを消費しない代わりに、ユーザーが存在を覚える負担を払う
- **model-invoked**(エージェントが自律的にも起動、例 `/tdd` `/grilling`): 再利用可能な規律の本体。description が常時コンテキストに載る
- 依存規則: user-invoked → model-invoked は呼べるが、user-invoked 同士は呼ばない。増えすぎた user-invoked は router スキル(`/ask-matt`)で束ねる

この設計判断の背景は [[スキルの書き方論(Writing Great Skills)]] の context load / cognitive load トレードオフとして体系化されている。

## 目玉4概念は個別ページに切り出した

1. [[Grilling(質問駆動アライメント)]] — 一問一答の尋問でエージェントとの意図のズレを潰す。本体はわずか843バイト
2. [[Wayfinder(決定駆動プランニング)]] — 1セッションに収まらない大型計画を issue tracker 上の decision ticket 群に分解。「実装せず決定だけを積む」
3. [[スキルの書き方論(Writing Great Skills)]] — スキルの書き方自体のメタ体系。予測可能性を根の徳とし、6つの失敗モードを診断語彙にする
4. [[深いモジュール設計(Deep Modules)]] — Ousterhout の deep module 論を語彙集(seam / depth / leverage / locality)として実装

## この Wiki との関係: エージェントの記憶喪失への別解

[[LLM Wikiパターン]](Karpathy)と Pocock の domain-modeling は、同じ問題 —— セッションごとにエージェントの文脈が消える —— への別解である。前者は知識を Wiki ページに複利蓄積し、後者は語彙(CONTEXT.md)と決定(ADR = Architecture Decision Record、覆しにくい設計判断の記録)に圧縮する。したがって両者は競合せず、この Wiki の concepts/ は CONTEXT.md 相当、answers/ は ADR 相当として読み替えられる。

⚠️ 留意: 本ソースは著者個人の実践知であり、効果の定量評価はない。「ニュースレター読者約6万人」という普及度はあるが、各スキルの有効性は自分の運用で検証すべき。
