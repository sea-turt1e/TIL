# Amazon SQS
- Amazon SQS（Simple Queue Service）は、分散アプリケーション間でメッセージを送受信するための完全マネージド型のメッセージキューサービスです。

# AWS Step Functions
- AWS Step Functions は、分散アプリケーションとマイクロサービスを構築するためのサービスです。
- Lambdaとの違いは、Lambdaは1つの関数を実行するだけであるのに対して、Step Functionsは複数のLambda関数を組み合わせて、ワークフローを作成することができる点です。
- また、Step Functionsは、Lambda関数だけでなく、EC2やFargate、SageMakerなどのAWSサービスや、オンプレミスのサービスとも連携することができます。

# Python(boto3)
- boto3は、AWSのサービスをPythonから利用するためのライブラリです。

# AWS CloudTrail
- AWS CloudTrailは、AWSアカウントで行われた操作のログを記録するサービスです。
- AWS CloudTrailを使用することで、AWSアカウントの操作履歴を確認することができます。
- APIの呼び出し履歴を記録することができる。

# Sagemaker
- 高可用性の ML サービスエンドポイントを確保するには、複数のアベイラビリティーゾーンに用意されたインスタンスに Amazon SageMaker エンドポイントをデプロイします。
- 複数のAZにデプロイすることで、1つのAZに障害が発生しても他のAZにエンドポイントがあるため、サービスを継続することができます。

# AWS Auto Scaling
- AWS Auto Scalingは、アプリケーションの負荷に応じて自動的にリソースをスケーリングするサービスです。
- Auto Scalingは、EC2インスタンス、DynamoDBテーブル、RDSインスタンスなど、さまざまなAWSサービスに対応しています。

# Amazon SageMaker ノートブックインスタンス
- Amazon SageMaker ノートブックインスタンスは、機械学習モデルの開発やデータ分析を行うための環境を提供するサービスです。
- ノートブックインスタンスは、Jupyterノートブックを使用してコードを記述し、実行することができます。

# Amazon ディープラーニングコンテナ
- Amazon ディープラーニングコンテナは、機械学習モデルをトレーニングするためのコンテナイメージを提供するサービスです。
- ディープラーニングコンテナには、TensorFlow、PyTorch、MXNetなどの機械学習フレームワークが含まれており、簡単に機械学習モデルをトレーニングすることができます。
  
# AWS ディープラーニング AMI (Amazon Machine Image)
- AWS ディープラーニング AMIは、機械学習モデルをトレーニングするためのAmazon Machine Image（AMI）です。

# AMI (Amazon Machine Image)
- AMI（Amazon Machine Image）は、EC2インスタンスを起動する際に使用するOSやアプリケーションがインストールされた仮想マシンイメージのことです。

# AWS Auto Scaling
- AWS Auto Scalingは、アプリケーションの負荷に応じて自動的にリソースをスケーリングするサービスです。
- Auto Scalingは、EC2インスタンス、DynamoDBテーブル、RDSインスタンスなど、さまざまなAWSサービスに対応しています。

# AWS GPU (P2 と P3) および CPU インスタンス
- AWS GPUインスタンス（P2およびP3）は、機械学習やディープラーニングなどの高度な計算処理に適したインスタンスタイプです。
- P2インスタンスは、GPUインスタンスの中でも比較的低価格で、一般的な機械学習ワークロードに適しています。


# AWS GPU (P2 と P3) および CPU インスタンス
- AWS GPUインスタンス（P2およびP3）は、機械学習やディープラーニングなどの高度な計算処理に適したインスタンスタイプです。

# 3つの階層
![階層](<images/スクリーンショット 2025-02-10 15.23.47.png>)

# AWS IOT Greengrass
- AWS IoT Greengrassは、IoTデバイスでのデータ処理をローカルで行うためのサービスです。
- Greengrassを使用することで、IoTデバイスからクラウドにデータを送信する前に、デバイス内でデータを処理し、必要なデータのみをクラウドに送信することができます。

# Elastic Inference
- Elastic Inferenceは、機械学習モデルの推論処理を高速化するためのサービスです。
- Elastic Inferenceを使用することで、推論処理を高速化し、コストを削減することができます。

# FPGAS (Field Programmable Gate Arrays)
- FPGAs（Field Programmable Gate Arrays）は、ハードウェアの機能をプログラム可能なデバイスにすることができる技術です。
- FPGAsを使用することで、機械学習モデルの推論処理を高速化することができます。

# DLコンテナ
- DLコンテナは、ディープラーニングモデルをトレーニングするためのコンテナイメージです。

# EKS (Elastic Kubernetes Service)
- EKS（Elastic Kubernetes Service）は、KubernetesをAWS上で実行するためのサービスです。
- Kubernetesは、コンテナ化されたアプリケーションを管理するためのオープンソースのプラットフォームです。

# Inferentia
- Inferentiaは、機械学習モデルの推論処理を高速化するためのチップです。

# Amazon Lex(Lex=Linguistic Expression)
- Amazon Lexは、自然言語理解（NLU）を使用して、チャットボットや音声対話システムを構築するためのサービスです。
- テキストと音声両方でチャットボットを作成できる
- インテント(挨拶ボットなら、こんにちわ、おはようなど)が設定できる

# Comprehend
- Amazon Comprehendは、自然言語処理（NLP）を使用して、テキストデータを分析するためのサービスです。
- Comprehendを使用することで、テキストデータから情報を抽出し、分類、感情分析、キーフレーズ抽出などのタスクを実行することができます。
- Comprehend Medicalは、医療データを分析するためのサービスです。

## Comprehend Latent Dirichlet Allocation (LDA 潜在的ディリクレ配分法)
- LDA（Latent Dirichlet Allocation）は、トピックモデリングの一つであり、テキストデータからトピックを抽出するための手法です。
- LDAは、テキストデータを複数のトピックに分割し、各トピックに対する単語の分布を推定することで、トピックを抽出します。
- LDAは、テキストデータの構造を理解し、テキストデータを分析するための有用な手法です。

# Amazon SageMaker Neural Topic Model (NTM) 
- トピックモデルの一つである Neural Topic Model（NTM）は、ニューラルネットワークを使用してトピックを抽出するための手法です。

# polly
- Amazon Pollyは、テキストを音声に変換するためのサービスです。
- Pollyを使用することで、アプリケーションに音声合成機能を追加することができます。

# Transcribe
- Transcribeは、音声データをテキストに変換するためのサービスです。

# personalize
- Amazon Personalizeは、機械学習を使用して、ユーザーにパーソナライズされた推薦を提供するためのサービスです。
- 顧客の行動を分析して製品やコンテンツのレコメンドをする。
- Personalizeを使用することで、ユーザーの行動データを分析し、ユーザーごとに最適な推薦を生成することができます。

# PII 情報
- 個人識別用情報（Personally Identifiable Information）は、個人を特定できる情報のことです。

# AWS KMSキー
- AWS KMS（Key Management Service）は、暗号鍵の生成、管理、保護を行うためのサービスです。
- S3やRDSなどのAWSサービスでデータを暗号化する際に、KMSを使用して暗号鍵を生成し、データを暗号化することができます。
- CSE KMS (Client-Side Encryption with KMS) は、クライアント側でデータを暗号化し、KMSを使用して暗号鍵を管理する方法です。
- SSE KMS (Server-Side Encryption with KMS) は、サーバー側でデータを暗号化し、KMSを使用して暗号鍵を管理する方法です。
- SSE S3 (Server-Side Encryption with S3) は、S3サービスが提供する暗号化機能を使用してデータを暗号化する方法です。
- CSE-C (Client-Side Encryption with Customer-Provided Keys) は、クライアント側でデータを暗号化し、ユーザーが提供した暗号鍵を使用して暗号化する方法です。
- SSE-C (Server-Side Encryption with Customer-Provided Keys) は、サーバー側でデータを暗号化し、ユーザーが提供した暗号鍵を使用して暗号化する方法です。

![KMS](<images/スクリーンショット 2025-02-10 15.55.42.png>)

# IAM フェデレーション
- IAM フェデレーションは、複数のAWSアカウントや外部IDプロバイダーと連携して、ユーザーの認証とアクセス管理を行う方法です。

# InvokeEndpoint 
- InvokeEndpointは、SageMakerエンドポイントを呼び出すためのAPIです。
- Invokeとは、エンドポイントを呼び出すことを意味します。

# コンプライアンスプログラム
- PCI DSS（Payment Card Industry Data Security Standard）は、クレジットカード情報の保護に関するセキュリティ基準です。
- BAA による HIPAA 対応 (Business Associate Agreement) は、ヘルスケア情報の保護に関する法律である HIPAA（Health Insurance Portability and Accountability Act）に準拠するための契約です。
- ISO 27001は、情報セキュリティマネジメントシステム（ISMS）の国際規格です。

# レジストリ
- レジストリは、コンテナイメージの保存と管理を行うためのサービスです。
- レジストリには、Docker HubやAmazon ECR（Elastic Container Registry）などがあります。
- ECRは、Dockerコンテナイメージを保存し、管理するための完全マネージド型のレジストリサービスです。
- ECSとECRの違いは、ECSはコンテナを実行するためのサービスであり、ECRはコンテナイメージを保存するためのサービスである点です。

# AWS CodeBuild
- AWS CodeBuildは、ビルドプロジェクトを自動化するためのサービスです。
- CodeBuildを使用することで、ビルドプロジェクトを簡単に設定し、ビルドプロセスを自動化することができます。
- CodeBuildは、ビルドプロジェクトを実行するためのコンテナイメージを提供しており、Dockerコンテナイメージを使用してビルドプロジェクトを実行することができます。

# AWS CodeCommit
- AWS CodeCommitは、Gitリポジトリをホスティングするためのサービスです。
- CodeCommitを使用することで、Gitリポジトリを簡単に作成し、管理することができます。
- CodeCommitは、AWSのセキュリティ機能を使用して、リポジトリのデータを保護し、アクセスを制御することができます。
- メリットは、AWSの他のサービスとの統合が容易であることです。

# ワークロード
- ワークロードは、アプリケーションやサービスが処理する作業のことです。
- ワークロードは、アプリケーションの要件に応じて設計され、実行されます。

# 本番稼働用バリアント (Production Variant)
- 本番稼働用バリアントは、エンドポイントで使用されるモデルのバリアントのことです。
- バリアントとは、モデルのバージョンやパラメータの異なるバージョンのことです。

# Amazon SageMaker で Lambda を使用する
- Amazon SageMakerでLambdaを使用することで、Lambda関数からSageMakerエンドポイントを呼び出すことができます。

# DescribeJobAPI
- DescribeJobAPIは、SageMakerジョブの詳細情報を取得するためのAPIです。
- FailureReasonオプションは、ジョブが失敗した場合に失敗の理由を示すオプションです。

# jupyter notebook 8888
- 8888ポートは、Jupyter Notebookのデフォルトのポート番号です。