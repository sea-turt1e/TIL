## Amazon Rekognitionとは？
Amazon Rekognition は、画像や動画から顔認識、物体検出、テキスト抽出などを行うAIサービス です。  
機械学習の専門知識がなくても、簡単なAPIを使って高度な画像・動画分析を実現 できます。
複雑なものには向かない

---

## Amazon Rekognition の主な機能
### 1. 顔認識（Face Analysis & Recognition）
✅ 画像や動画から人物の顔を検出  
✅ 年齢、性別、表情（喜び・怒りなど）、眼鏡・ひげの有無などを分析  
✅ 過去のデータと照合して特定の人物を認識（顔認証）  

🔹 ユースケース
- 本人確認（KYC）（金融機関やオンラインサービスでの身元確認）
- スマート監視システム（不審者の検知）
- 写真アプリの顔認識タグ付け

---

### 2. 物体・シーン検出（Object & Scene Detection）
✅ 画像や動画内の物体・風景・アクティビティを識別  
✅ 例：「車」「犬」「テーブル」「山」「パーティー」などのカテゴリを特定  
✅ 95種類以上の物体・シーンカテゴリに対応  

🔹 ユースケース
- Eコマースの画像検索（「この商品と似たものを探す」機能）
- 自動タグ付け（SNSやクラウドストレージでの画像分類）
- ドローン映像の解析（森林火災や農作物の状態確認）

---

### 3. センチメント分析（Sentiment & Expression Analysis）
✅ 人物の表情を認識し、感情を分析（喜び・悲しみ・驚き など）  
✅ 動画内の人物の感情変化も追跡可能  

🔹 ユースケース
- マーケティング分析（広告視聴者の反応を分析）
- 顧客対応（カスタマーサポート）（顧客の感情をリアルタイムで把握）
- ヘルスケア（精神状態の分析）（ストレスレベルの測定）

---

### 4. 不適切コンテンツの検出（Content Moderation）
✅ アダルトコンテンツ、暴力、薬物などの有害画像・動画を検出  
✅ コンテンツフィルタリングを自動化（違反コンテンツを排除）  

🔹 ユースケース
- SNSやフォーラムの画像・動画審査（不適切なコンテンツを自動削除）
- オンラインマーケットプレイスの出品画像審査
- 動画ストリーミングサービスのコンテンツ管理

---

### 5. テキスト抽出（Text Detection - OCR）
✅ 画像や動画からテキスト（文字）を検出・読み取り  
✅ 手書き文字や複雑なフォントも解析可能  
✅ ナンバープレート、道路標識、書類の文字解析にも対応  

🔹 ユースケース
- 領収書や請求書のデータ抽出（経費管理の自動化）
- 自動運転の道路標識認識
- パスポート・身分証明書のOCR解析

---

### 6. カスタムラベル（Custom Labels）
✅ 自社データを使って、特定の画像分類モデルをトレーニング可能  
✅ 独自の製品・ブランドロゴ・医療画像の識別が可能  

🔹 ユースケース
- 工場の品質管理（製品の異常検出）
- ブランドロゴの自動認識
- 医療画像解析（ガンの診断支援）

### 7. Rekognition Image
- 顔認識の精度が高い
- 画像単位でのAPI呼び出しとなり、映像ストリームのリアルタイム分析や大規模展開には非効率です。

### 8. Rekognition Video
- 特定の人物を認識できる
- Kinesis Video Streamsとシームレスに統合され、リアルタイムでストリーム映像から顔検出・顔認識を行うことができます。既知の従業員の顔コレクションと照合し、非従業員を検出した場合に即座にアラートを発することが可能です

---

## Amazon Rekognition の料金
Amazon Rekognition は、処理した画像・動画の量に応じた従量課金制 です。

| 機能 | 課金単位 | 料金の目安 |
|------|--------|-----------|
| 顔認識 | 画像1,000枚ごと | 約$1.00（最初の1,000枚無料） |
| 物体検出 | 画像1,000枚ごと | 約$0.10 |
| 動画解析 | 1分ごと | 約$0.12 |
| カスタムラベル | トレーニング時間 | 約$4.00/時間 |

💡 無料利用枠：月5,000件の画像分析、月1時間の動画分析が無料！  

---

## Amazon Rekognition のメリット
✅ 機械学習の専門知識不要！簡単なAPIで利用可能  
✅ AWSとシームレスに統合（S3、Lambda、SageMaker など）  
✅ スケーラブルで大量の画像・動画を処理可能  
✅ クラウドベースでコスト効率が良い（サーバー管理不要）  

---

## まとめ
Amazon Rekognition は、画像・動画を解析して顔認識、物体検出、テキスト抽出、感情分析を実現するAIサービス です。  
セキュリティ、Eコマース、医療、メディア業界など、幅広い分野で活用されています。

💡 「画像・動画をAIで解析したい！」なら、Amazon Rekognition が最適！ 🚀

- 著名人の認識ができる
- 