# Amazon Kendra
- 機械学習を利用して企業内部のデータを検索できるサービス
- マニュアル、調査報告書、よくある質問など
- S3, Microsoft SharePoint, Salesforce, ServiceNow, RDS, Onedriveなどのデータソースに接続可能
- .html, .doc, .ppt, PDFなどのファイル形式が対応。オーディオファイルや、ビデオファイルにも対応
- 英語以外の多数言語にも対応

## Kendra GenAI Index
- RAGを利用したインデックスを作成
  - RAG = Retrieve, Analyze, Generate
  - インデックス = 検索対象のデータを構造化して保存する場所
  - Indexは特定の列に索引を貼ることで検索を早くするが、Delete, Update, Insertはインデックスの更新作業があるため遅くなる