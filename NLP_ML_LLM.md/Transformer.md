# Transformer
## Multi-Head Attention
- single-head-attentionだと1つの視点で鹿関係性が見れない。
- Multi-Headだと複数の関係性が見られる
- 例文: "The animal didn't cross the street because it was too tired."
  - Single Attentionの場合
    - it が animalを指すという1つの関係性のみ
  - Multi-Head Attention
    1. 代名詞と参照先（it -> animal）
    2. 動詞と主語（cross -> animal）
    3. 形容詞と名詞（tired -> animal）
    4. ...
    - つまり複数の視点から同時に文章を理解することができる
- ![alt text](<image/スクリーンショット 2026-02-12 8.00.15.png>)
- 視覚的なイメージ
  ```
  入力 [batch, seq_len, 512]
      ↓
  分割して各ヘッドへ
      ↓
  ヘッド1 [64次元] → Attention → 出力1
  ヘッド2 [64次元] → Attention → 出力2
  ...
  ヘッド8 [64次元] → Attention → 出力8
      ↓
  連結 [512次元]
      ↓
  線形変換 W^O
      ↓
  出力 [batch, seq_len, 512]
  ```
- マルチヘッドの利点
  - 多様な関係性の学習: 各ヘッドが異なる言語的パターンを捉える
  - 表現力の向上: 1つのヘッドより豊かな表現が可能
  - 並列処理: 各ヘッドは独立に計算可能（GPU効率がいい）

## Self-Attention
- 同じ入力系列内の関係性を計算する注意機構
- 具体例
  - cat: 注目する単語->The（主語マーカー）、sat（同士の関係）
  - sat: 注目する単語->cat（主語）, mat（場所）
  - mat: on（前置詞）, the（修飾）
- 役割
  - エンコーダで使用: 入力文の理解
  - 文脈情報を各単語に埋め込む
  - 長距離依存関係を捉える（RNNの限界を克服）
- Multi-Head Attentionは系列を複数のHeadに分割して、それぞれでself-attentionを計算し、その後concat（連結）して、線形変換している。

## Cross-Attention
- 異なる2つの系列館の関係性を計算するAttention
- 例えば日->英の翻訳
  - エンコーダ入力: The cat sat on the mat.
  - デコーダ出力: 猫が
  - Cross Attentionでは、日本語の「猫が」が英語のどの部分に対応するかを計算
    - "猫が" → 注目度
    - The:   0.05
    - cat:   0.85  ← 最も注目
    - sat:   0.03
    - on:    0.01
    - the:   0.02
    - mat:   0.04
- 役割:
  - デコーダで使用: 入力（ソース）と出力（ターゲット）対応づけ
  - 翻訳・要約・質疑応答などで重要
  - 度の入力情報を使って出力生成するかを決定

| 観点         | Self-Attention | Cross-Attention   |
| ---------- | -------------- | ----------------- |
| Q, K, Vの出所 | すべて同じ系列        | 異なる系列（QとK/Vが別）    |
| 計算する関係     | 系列内の単語間        | 2つの系列間            |
| 使用場所       | エンコーダ          | デコーダ              |
| 典型的な用途     | 文脈理解、表現学習      | 翻訳、アライメント         |
| 例          | "cat"と"sat"の関係 | 英語"cat"と日本語"猫"の対応 |

## Transformerでの配置
### Encoderブロック
入力
↓
Multi-Head Self-Attention
↓
Add & Norm
↓
Feed Forward
↓
Add & Norm
↓
出力（次のレイヤーへ）

### Decoderブロック
入力
↓
Masked Multi-Head Self-Attention  ← 自己注意（未来をマスク）
↓
Add & Norm
↓
Multi-Head Cross-Attention  ← クロス注意（エンコーダ出力を参照）
↓
Add & Norm
↓
Feed Forward
↓
Add & Norm
↓
出力（次のトークンを予測）


