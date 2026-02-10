## 0. 全体像と優先度イメージ
1. **評価・データ基盤寄り**  
   - 評価設計（統計・サンプリング・人手評価設計・LLM-as-a-judge）  
   - データパイプライン（収集・フィルタリング・dedup・アノテーションフロー）
2. **LLM/NLPコア寄り**  
   - 日本語LLMの設計・学習レシピ（pretrain + SFT + DPO/RLHF）  
   - RAG / Deep Research 系エージェント設計
3. **KG（ナレッジグラフ）寄り**  
   - text→KG 構築パイプライン  
   - KGを使った検索・推論・評価（KG-LLM系の最近のベンチマークなど） [knowledge-nlp.github](https://knowledge-nlp.github.io/naacl2025/papers/39.pdf)
4. **アーキテクチャ / MLOps 寄り**  
   - 評価・アノテーションを回すためのアプリ/基盤設計

以下、分野別に「何を勉強しておくと良いか」を具体的に書きます。

***

## 1. 基礎数学・統計（評価とデータ作り視点での”使える範囲”）

すでにML基礎は押さえている前提で、「評価設計とデータ品質管理」に直結する部分を重点にすると良いです。

### 1-1. 確率・統計（評価設計に直結）

- **サンプリングと信頼区間**
  - 二値・多クラス精度の信頼区間（Wilson区間、Clopper–Pearsonなど）
  - サンプルサイズ設計（「誤差±xポイント以内に抑えるには何サンプル必要か」）
- **統計的仮説検定**
  - A/Bテストでの差の有意性検定（比例の差の検定、t検定、カイ二乗など）
  - bootstrap / permutation test の考え方（LLMの勝率比較などでよく出る）
- **評価者間一致度**
  - Cohen’s kappa, Fleiss’ kappa, Krippendorff’s alpha など
  - 主観評価・安全性評価・KGのトリプルアノテーションで頻出

→ これを抑えておくと、「この評価結果って信頼できるの？」「人手評価何件必要？」といった会話をリードしやすくなります。

### 1-2. 最適化・情報理論（LLMトレーニングを理解する最低限）

- 最適化
  - SGD, AdamW, 学習率スケジュール（cosine, warmup）、weight decay の意味
  - 勾配ノルムクリッピング、mixed precision、gradient checkpointing の役割
- 情報理論
  - クロスエントロピー、KLダイバージェンス（DPO/RLHFや蒸留で多用）
  - perplexity と言語モデル評価の関係

***

## 2. NLP / ML / LLM（特に日本語＋評価・データ観点に寄せて）

### 2-1. トランスフォーマとLLMアーキの解像度を1段上げる

- Transformer再整理
  - マルチヘッド注意機構、自己注意 vs クロス注意
  - 残差接続・LayerNorm・FFNの役割
- 近年のLLM要素
  - RoPE, ALiBi などの位置表現
  - GQA/MQA, FlashAttention などの高速化テク
  - Mixture-of-Experts など（触れだけでも理解しておくと良い）

ここは「自分で実装」までは不要ですが、論文や社内資料を読んだ時にすぐ腹落ちするレベルだと、会話コストが下がります。

### 2-2. 学習レシピとアラインメント
- Pretrain：大規模コーパス（日本語中心）の構成、dedup、フィルタリング
- SFT：指示追従データ（タスク多様性、フォーマット設計、テンプレート）
- DPO/RLHF：
  - preferenceデータの取り方（pairwise比較、ranking形式）
  - オフライン/オンラインでのpreference収集設計

特に「preferenceデータをどう集め、どう評価設計するか」は、仕事のど真ん中になりそうです。

### 2-3. 日本語・多言語固有のポイント

- トークナイザと分かち書き
  - SentencePiece（unigram/BPE）、日本語でのサブワード分割の癖
  - 英数字・カタカナ・漢字混在文のトークナイズ挙動
- 既存の日本語ベンチマークの俯瞰
  - (JGLUE, NIILC系, JSQuAD など) 名称だけでも押さえ、どういうタスクがあるか

***

## 3. 「データ作り」のためにやっておくと効くこと

### 3-1. データパイプライン・クレンジング

- クローリング / 収集 → 前処理 → dedup → 品質フィルタ → ストレージ までのパイプライン設計
- dedupテクニック
  - URL・ハッシュベース + MinHash/SimHash 的な近似重複除去
  - embedding類似度ベースのnear-duplicate検出
- 品質フィルタリング
  - length, language ID, 文字種比率, boilerplate検出
  - ナレッジグラフ向けであれば「構造化しやすい文」の判定（例: 事実記述っぽい文）

### 3-2. データスキーマ設計とアノテーション設計

- **アノテーションの「仕様書づくり」スキル**
  - タスク定義（何を正とみなすか、境界事例の扱い）
  - ガイドラインのサンプル充実（良い例/悪い例）
  - ラベラビリティ（誰が見ても判定可能か）を意識
- **評価者マネジメント**
  - 少人数の専門家 vs 多人数のクラウドワーカー
  - ゴールドデータ・注意確認問題の設計

LLMを使った半自動アノテーション（LLM-as-a-labeler）も今後必ず出てくるので、

- LLMで下書き → 人手で修正 → 信頼できるゴールド
- その際の「2段階評価」（LLM出力の信頼度推定＋人手の最終チェック）

あたりのワークフローも考えられると強いです。

### 3-3. 合成データ / 自己学習の安全な使い方

- LLMが作ったデータでLLMを再学習する時の
  - ノイズコントロール（confidenceでのフィルタ、複数モデル一致で採用など）
  - human-in-the-loopの入れ方
- 既存のオープンデータセット（ShareGPTスタイル、Instruction系）をどうクリーニングして使うか

***

## 4. 評価設計（LLM・アプリ・KGの全部に効く）

### 4-1. 自動評価 ＋ LLM-as-a-judge

- 従来のテキスト評価指標の整理
  - BLEU, ROUGE, METEOR, BERTScore, BLEURT など
  - なぜLLM時代には限界があるか（多様な正解、言い換え、スタイルなど）
- LLM-as-a-judge 系の枠組み
  - MT-Bench / AlpacaEval / Chatbot Arena などの設計思想
  - reference-free評価（品質/有用性/安全性） vs reference-based評価（正解テキスト or ドキュメントがあるケース）
  - judgeモデルのバイアス・自己評価問題

評価プラットフォーム側では

- プロンプトテンプレート管理
- 評価用のchain（「プロンプト→モデル→ジャッジ→スコア」）のバージョン管理

が重要になるので、これを設計できると強いです。

### 4-2. 人手評価（human preference, safety, factuality）

- 評価軸の設計
  - helpfulness, harmlessness, honesty, instruction-following, style, latency など
  - KGやDeep Research的な文脈では「根拠文書との整合性」「引用の正確さ」
- 実験計画
  - ランダムサンプリング vs ストラティファイドサンプリング
  - ペアワイズ比較（A/B） vs 多腕バンディット的にオンラインに回す、など
- 統計処理
  - 勝率のconfidence interval
  - 勝率Eloレーティングの考え方（Chatbot Arenaスタイル）

***

## 5. ナレッジグラフ（KG）の基礎とLLM連携

### 5-1. KGのモデリングと実装基礎

- データモデル
  - RDF/OWL vs Property Graph（Neo4j, TigerGraphなど）
  - ノード/リレーション/プロパティ/スキーマの設計
- クエリ言語
  - SPARQLの思想（RDF寄り）
  - Cypher / openCypher / GQL の基本
- インデックス・スケール性
  - ノード数・エッジ数が増えたときのクエリ最適化のイメージ

### 5-2. text→KG 構築パイプライン

最近は「LLMを使ったText-to-KG」が主流になりつつあるので、 [pmc.ncbi.nlm.nih](https://pmc.ncbi.nlm.nih.gov/articles/PMC12237976/)

- 対象タスク
  - エンティティ抽出（NER）
  - 関係抽出（RE）
  - イベント抽出
- LLMベースでの実装パターン
  - zero/few-shotプロンプトでトリプル抽出
  - 小さめモデル＋fine-tuning（特定ドメインで高精度を狙う場合）
- 評価指標
  - Triple-level: precision/recall/F1（T-F1）
  - Graph-level: G-F1, Graph Edit Distance, BERTScore拡張版など [ceur-ws](https://ceur-ws.org/Vol-3747/text2kg_paper7.pdf)

「どの単位で評価するか」（トリプル単位か、サブグラフ単位か、最終タスク（QA）で見るか）を意識できると設計しやすいです。

### 5-3. KGをDeep Research系システムでどう活用するか

Deep Research / GraphRAG系の文脈では、

- KGを用いた
  - エンティティ中心の検索（entity-centric search）
  - パス探索（multi-hop reasoning）
  - 近傍拡張（neighbor expansion）からの文章再構成
- LLMへの入力
  - KGサブグラフをテキスト化してコンテキストに埋め込む戦略
  - KG + ベクタ検索 + 直接Web検索のハイブリッド構成 [developer.nvidia](https://developer.nvidia.com/blog/insights-techniques-and-evaluation-for-llm-driven-knowledge-graphs/)

という流れになります。  
ここは論文/ブログを数本読み、「どのようなアーキテクチャの選択肢があるか」をマップしておくと、設計議論に乗りやすくなります。

***

## 6. 評価・アノテーションを支えるアーキテクチャ / MLOps

### 6-1. 評価基盤のざっくりアーキを考えておく

- コンポーネント
  - データセット管理（バージョン付き：eval set, dev set, A/B用バケット）
  - モデル実行サービス（社内LLM / 外部API / その組み合わせ）
  - 評価実行（自動評価 + LLM-as-a-judge）
  - 人手評価UI（ラベリング、ペアワイズ比較）
  - メトリクス蓄積・ダッシュボード（Prometheus+Grafana, Superset, etc.）

「どういうフローで、誰がどの画面を使って、どのようなデータが溜まるか」を  
sequence diagramレベルで一度書いてみると、必要な実装要素がクリアになります。

### 6-2. 実装技術スタックで準備しておくと良さそうなもの

- バックエンド
  - FastAPI / Go などでのAPIサーバ実装（多分普段通りでOK）
  - queueベースの非同期処理（Celery, Redis Queue, SQS などのパターン）
- フロント/ツール
  - 内製アノテーションツールをReactでさっと作れる程度
  - もしくはLabel Studio等 OSSをカスタムする知見
- MLOps寄り
  - MLflow / Weights & Biases / 自前実験管理のいずれかの経験整理
  - コンテナ化(Docker)とKubernetes系の基本

***

## 7. 30〜60日くらいのプレ勉強プラン案

最後に、入社までの時間を想定した具体的なプラン例です。

### フェーズ1（1〜2週間）：LLM評価・データ作りに特化したインプット

- LLM評価
  - LLM-as-a-judge, MT-Bench, AlpacaEval, Chatbot Arena の論文・ブログを通読
  - 人手評価設計の論文（helpfulness/harmlessness評価など）を数本ピックアップ
- データ作り
  - 大規模データフィルタリング（The Pile, SlimPajama などの処理パイプライン解説）を読む
- 統計
  - サンプルサイズ設計・信頼区間・A/Bテストの復習（メモを自分でまとめる）

### フェーズ2（2〜3週間）：KG＋Deep Research系のキャッチアップ

- KG × LLM
  - Text-to-KG, KG-LLM-Bench系の論文を数本 [pmc.ncbi.nlm.nih](https://pmc.ncbi.nlm.nih.gov/articles/PMC12237976/)
  - GraphRAG/Deep Research的なアーキ系ブログ（NVIDIA, Microsoft, Google など） [developer.nvidia](https://developer.nvidia.com/blog/insights-techniques-and-evaluation-for-llm-driven-knowledge-graphs/)
- グラフ技術
  - Neo4j か他のプロパティグラフを選んで、  
    小規模ドメイン（例：自分の研究分野や好きなアニメ作品の人物関係）でKGを作り、  
    クエリ＋RAGを組んでみる

### フェーズ3（残り時間）：自分用ミニ「評価プラットフォーム」を作る

- 目的：  
  小規模で良いので「データセット登録 → モデル呼び出し → LLM-as-a-judge → ダッシュボード」までを通したミニプラットフォームを1つ作る。
- やること
  - FastAPI + フロント（シンプルでOK）で
    - テストプロンプト＋期待応答の登録
    - モデル（今回は外部APIで良い）への一括評価
    - ジャッジLLMを呼び出してスコアリング
  - 結果をDBに溜め、簡単な可視化

入社後、これをそのまま「PoC」として見せられるレベルまで磨けると、  
「この人は評価・アーキテクチャをセットで考えられる」と強く印象づけられるはずです。

***

## まとめ

- **数学・統計**：サンプリング、信頼区間、仮説検定、評価者間一致度を「LLM評価に使えるレベル」で整理。
- **LLM/NLP**：日本語LLMの学習レシピ（pretrain/SFT/DPO）、トークナイザ、日本語ベンチマークを俯瞰。
- **データ作り**：大規模データパイプライン、dedup、アノテーション仕様設計、LLMを絡めた半自動アノテーションのワークフロー。
- **評価**：自動評価＋LLM-as-a-judge＋人手評価を組み合わせた評価設計と、統計的な裏付け。
- **KG**：モデリング、text→KGパイプライン、KG評価指標、KGを使ったGraphRAG/Deep Research的な設計。
- **アーキテクチャ**：評価・アノテーション・モデル実行を一体で回すミニ基盤を個人開発しておく。

もし「ここは特に深掘りしておきたい（例: DPO実装寄り、KG構築寄り、評価基盤寄り）」といった希望軸があれば、  
その軸に絞って具体的な論文リストや実装タスクのロードマップも出します。

# LoRA, QLoRAなどLLMの事後学習をやってみる

# RLHF, DPOの数式的な理解