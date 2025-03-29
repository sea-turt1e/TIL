**Optimizer（最適化アルゴリズム）**は、機械学習や深層学習において、損失関数（Loss Function）を最小化するためにモデルのパラメータ（重みやバイアス）を調整するアルゴリズムのことを指します。

1. 役割

ニューラルネットワークの学習では、
	1.	損失関数の値を計算
	2.	**誤差を逆伝播（Backpropagation）**させて勾配を求める
	3.	勾配に基づいてパラメータを更新（Optimizerの仕事）
というプロセスを繰り返します。
この 3.のパラメータ更新 を担当するのがOptimizerです。

2. 代表的なOptimizer

(1) 勾配降下法（Gradient Descent, GD）
	•	最も基本的な最適化手法で、**勾配（微分）**に従ってパラメータを更新する
	•	学習率（learning rate）が重要

(2) 確率的勾配降下法（Stochastic Gradient Descent, SGD）
	•	ミニバッチ単位で勾配を計算し、更新する
	•	計算コストが少なく、学習速度が速い

(3) Momentum（モーメンタム）
	•	前回の更新量を考慮し、よりスムーズな更新を行う
	•	SGDのような振動を抑え、収束を早める

(4) Adam（Adaptive Moment Estimation）
	•	SGD + Momentum + 学習率の適応的な調整
	•	一般的に使われる最適化手法で、計算効率が良く収束しやすい
	•　RMSpropを改良したもの

(5) RMSprop（Root Mean Square Propagation）
	•	勾配の変動を考慮し、学習率を調整する手法
	•	深層学習でよく使われる

(6) Adagrad(Adaptive Gradient Algorithm)
	•	各パラメータに対して異なる学習率を適用する手法
	•	稀な特徴に対しても効果的
	•	ただし、学習率が徐々に小さくなるため、長期的な学習には不向き

ちなみに
AdaBoostは、アンサンブル学習の手法であり、Optimizerとは異なる。

1. Optimizerの選び方
	•	基本的にはAdamを使う → 汎用的でバランスが良い
	•	収束が遅い場合 → Momentumを試す
	•	シンプルなモデルで過学習を防ぎたい → SGD

どのOptimizerが最適かは、タスク・データ・モデルによって異なるので、試行錯誤が必要になります。