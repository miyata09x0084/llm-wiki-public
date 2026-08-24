# Log

追記専用の時系列ログ。`grep "^## \[" wiki/log.md | tail -5` で直近5件を確認できる。

## [2026-07-14] setup | Wiki 初期化

Karpathy の LLM Wiki パターンに基づきリポジトリを初期化。
スキーマ(CLAUDE.md)、index.md、log.md、ディレクトリ構造、/ingest・/lint コマンドを作成。

## [2026-07-14] setup | 重点領域セクション追加

CLAUDE.md にハイブリッド構成(ライフエリア7分類 + 今のフォーカス)を追加。
今のフォーカスは未設定。

## [2026-07-14] ingest | LLM Wiki v2 (rohitg00)

初のソース取り込み(raw/2026-07-14-llm-wiki-v2-rohitg00.md、強調点: 運用改善+技術知識の両面)。
作成: [[LLM Wiki v2 (rohitg00)]]、[[LLM Wikiパターン]]、[[agentmemory]]、[[LLM・AIエンジニアリング]]。index.md 更新。

## [2026-07-14] setup | Query発動規則を追加

CLAUDE.md のQuery操作に発動規則を追加: 知識に関する質問は記憶から直接答えず、必ず index.md 確認から始める。
発動漏れ(本日の会話で実際に発生)への対策。

## [2026-07-14] query | なぜwikiは5分類か(設計根拠)

初のanswersページ保存。ユーザーの質問「分類ディレクトリの設計根拠は?」への回答を蒸留。
作成: [[なぜwikiは5分類か(設計根拠)]]。index.md 更新。

## [2026-07-14] lint | index.md の手入力混入を除去

index.md 冒頭に混入した手入力文字を除去(Obsidian編集モードでの誤入力)。
再発防止として Obsidian のデフォルト表示を閲覧モードに設定。

## [2026-07-15] query | ベンダーロックインしない自作Wiki基盤の設計
「これの自作基盤、ベンダーロックインしない?」への回答を設計ドキュメント化。
中立化3案(A: AGENTS.md標準化 / B: 自作CLI+LLM差替 / C: 完全ローカル)を比較。
作成: answers/ベンダーロックインしない自作Wiki基盤の設計。更新: index.md

## [2026-07-15] query | 自作基盤の目的を明確化(業界変化への耐性)
真の目的=「LLM業界の変化に左右されずプロダクト価値を探索できる土台」を反映。
設計原則「所有層を厚く/LLMを薄い継ぎ目に隔離」「モデル進化を追い風化(raw不変×再生成)」を追記。
更新: answers/ベンダーロックインしない自作Wiki基盤の設計, index.md

## [2026-07-15] query | AIネイティブ価値探索基盤(前提の拡張)
前提を「Wikiの中立化」から「生成AI全般で新次元の価値提供を探索できる基盤」へ拡張。
統一原理(不変コア+再生成可能な派生物)・4層構成・閾値トリガー型仮説バックログ(H1個別即席アプリ/H2瞬時マルチモーダル)を定義。
作成: topics/AIネイティブ価値探索基盤。更新: answers/ベンダーロックインしない自作Wiki基盤の設計(位置づけ), index.md

## [2026-07-15] query | 仮説バックログ拡充+実験001(H1個別即席アプリ)
(a) H3/H4/H5 を登録(H6は見送り)。フォーカスは「意図的に絞らない」でCLAUDE.mdに記入。
(b) 実験001: 仕様→単一HTMLアプリを one-shot 生成→Chromium検証→一発成功。
コスト実測: Opus 4.8 ≈¥8.5/生成 — H1は小規模領域で既に成立圏と判定。
作成: lab/001-instant-app/(SPEC, app.html, RESULT)。更新: topics/AIネイティブ価値探索基盤, CLAUDE.md

## [2026-07-15] ingest | nextjsjp.org 主要機能ページ(計11ページ)

nextjsjp.org からトップページ + 主要機能ドキュメント10ページを取得し raw/ に保存(サブエージェント2並列で取得)。
作成: sources 11ページ、[[Next.js]]、[[nextjsjp.org]]、[[Turbopack]]、[[React Server Components]]、[[Server Actions]]、[[Cache Components]]。index.md 更新。
注記: 「データの取得」「アップグレードガイド」は WebFetch 不調のため curl + HTML→Markdown 変換で取得(各ソースページに取得ノートあり)。

## [2026-07-15] ingest | 名古屋市の家系ラーメン調査(Web検索+GoogleMaps手動確認)

Web検索(調査エージェント2体)+ユーザーのGoogle Maps手動確認(評価4.0以上・レビュー100件以上)で名古屋市内の家系店を調査、基準クリア7店を選定してrawに保存。
作成: sources/Web調査+GoogleMaps確認 名古屋市の家系ラーメン、topics/名古屋の家系ラーメン(巡礼リスト・実食記録の受け皿)、concepts/家系ラーメン(系譜分類)。index.md 更新。
注記: 店舗ごとのentityページは実食記録が溜まった段階で分割予定。Google評価の実数値は未記録。

## [2026-07-15] query | 名古屋家系の綺麗なスープと栄養価(推定比較)

巡礼7店からスープの綺麗さ・栄養価を推定比較(綺麗系=桜家、出汁濃度=ガチ家、両立候補=志)。実食での検証観点(乳化度・鶏油量・ゼラチン体感)も定義。
作成: answers/名古屋家系の綺麗なスープと栄養価(推定比較)。更新: topics/名古屋の家系ラーメン(相互リンク), index.md

## [2026-07-15] setup | 文章スタイル規約6ルールをスキーマに追加

Wiki 全ページ+チャット回答に適用する文章スタイルを CLAUDE.md に定義。
6ルール: ツリー型トップダウン(親=子の要約)/見出し・表でスキャン可能/専門用語は原語+一言注釈/論理接続の明示/温度感(具体で現場感)/冗長性の排除。
既存ページの書き直しはせず、次回更新時から新スタイルへ移行。

## [2026-07-16] query | LLMの原理を学ぶ論文リスト

「LLMの原理をナレッジ化したい」への回答をリーディングリスト化(モデル知識ベース、コア10本は読む順=ingest順)。
創発論争(Emergent Abilities vs Mirage)は⚠️矛盾ペアとして明記。読了状況欄(☐/📖/✅)付き。
作成: answers/LLMの原理を学ぶ論文リスト(コア10本+拡張12本)。更新: index.md

## [2026-07-16] ingest | Attention Is All You Need (arXiv:1706.03762)

初の論文 ingest(リスト#1、PDF 15ページ v7、強調指示: LLMへの系譜重視)。
作成: sources/Attention Is All You Need (2017)、concepts/Transformer、concepts/Attention機構、topics/LLMの原理(5段の因果の総説を新設)。
更新: answers/論文リスト(#1→✅)、topics/LLM・AIエンジニアリング(原理側/応用側の分担リンク)、index.md

## [2026-07-16] setup | Ingest手順に保存前スタイルチェックを追加+初回論文ingest 4ページを書き直し

初の論文 ingest で文章スタイル違反が発生(ラベル型見出し/セクション冒頭要約文の欠落/BLEU・FFN 等の初出注釈漏れ)。
原因: 生成後の照合工程が無く、論文体裁(読者は論文既読前提)に引っ張られた。対策として CLAUDE.md の Ingest 手順5に保存前チェック(①見出しは主張 ②冒頭文は子の要約 ③初出注釈)を追加。
書き直し: sources/Attention Is All You Need (2017)、concepts/Transformer、concepts/Attention機構、topics/LLMの原理

## [2026-07-16] ingest | BERT (arXiv:1810.04805)

リスト#2(PDF 16ページ v2、強調指示: 機構の理解重視 — MLM の 80/10/10、入力表現、fine-tuning 機構)。
作成: sources/BERT (2018)、concepts/事前学習とfine-tuning。NSP への RoBERTa の反証を⚠️後日談として記録。
更新: topics/LLMの原理(第2段着手)、concepts/Transformer(相互リンク)、answers/論文リスト(#2→✅)、index.md

## [2026-07-16] ingest | Attention Is All You Need 要約を機構重視に改訂

ユーザー指示「前回のも理解重視にして」を受け、#1 の sources ページを系譜重視から機構重視へ書き直し。
追加: √dk の導出、additive vs dot-product の勝敗理由、multi-head の射影機構、学習レシピ(warmup 4000・label smoothing 0.1)。系譜は要点のみに圧縮。
以後の論文 ingest は機構の理解重視をデフォルトとする。

## [2026-07-16] ingest | GPT-3 (arXiv:2005.14165)

リスト#3(本文40ページを2分割で読了、付録35ページは未読。強調: 機構重視デフォルト)。
作成: sources/GPT-3 (2020)、concepts/in-context learning(外/内2ループ構造、「学習か認識か」の未解決問題)。
更新: concepts/事前学習とfine-tuning(「事前学習→プロンプト」転換を統合)、topics/LLMの原理(第2段完了)、answers/論文リスト(#3→✅)、index.md

## [2026-07-16] ingest | Skills For Real Engineers (mattpocock/skills)

GitHub リポジトリ全文(40スキル)を raw/ に取得し、sources 1+entities 1(Matt Pocock)+concepts 4(Grilling / Wayfinder / スキルの書き方論 / 深いモジュール設計)を作成。
強調点はユーザー指定で「自分のスキル設計への転用」。[[LLM・AIエンジニアリング]] にエージェントスキル設計セクションを追加。

## [2026-07-16] setup | 文章スタイル ルール5(温度感)を削除

CLAUDE.md からルール5「温度感」をユーザー指示で削除し、6ルール→5ルールに再編。
旧ルール6(冗長性の排除)内の温度感への参照と、Ingest 手順5の「6ルール」表記もあわせて修正。

## [2026-07-23] query | LLM Wikiパターンの系譜(発想の源)を統合

チャットでの「発想の源は?」への回答を [[LLM Wikiパターン]] に系譜セクションとして統合。
Memex(1945)→Wiki/Wikipedia→PKMブーム→Karpathyの転回(保守労働のボトルネック特定)の4段階。index.md 更新。

