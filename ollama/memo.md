## ollama コマンド
```
brew install ollama
ollama serve
ollama run $MODLE_NAME
# 例
ollama run deepseek-r1:32b
```

## （HuggingFaceなどの）ggufモデルファイルを使う場合
```
ollama run hf.co/$MODEL_NAME
# 例
ollama run hf.co/TheBloke/Swallow-7B-Instruct-GGUF:Q2_K
```

## （HuggingFaceなどの）safetensorsファイルを使う場合
```
git lfs install
git clone $MODEL_URL
# 例
git clone https://huggingface.co/cyberagent/DeepSeek-R1-Distill-Qwen-14B-Japanese

# create Modelfile
FROM /path/to/safetensors/directory

ollama create my-model

ollama run my-model
```

## fine tuning
- https://dev.classmethod.jp/articles/deepseek-ec2/ を参考にした。

### LLaMA-Factoryのインストール
```
git clone https://github.com/hiyouga/LLaMA-Factory.git
pip instal -r requirements.txt
```
- 以下の様なデータセットを用意
```
[
    {"instruction": "大阪の名物って何？", "input": "", "output": "たこ焼きとかお好み焼きやな、知らんけど"},
    {"instruction": "日本の首都はどこ？", "input": "", "output": "東京やったはずやで、知らんけど"},
    {"instruction": "宇宙ってどれくらい広いの？", "input": "", "output": "めっちゃ広いらしいで、知らんけど"},
    {"instruction": "富士山の高さは？", "input": "", "output": "3776mらしいわ、知らんけど"},
    {"instruction": "新幹線ってどれくらい速いの？", "input": "", "output": "だいたい300km/hくらいちゃうかな、知らんけど"},
    {"instruction": "お好み焼きの美味しい作り方は？", "input": "", "output": "生地をしっかり混ぜて、じっくり焼くのがコツらしいで、知らんけど"},
    {"instruction": "明日の天気は？", "input": "", "output": "晴れるかもしれんけど、天気予報次第やな、知らんけど"},
    {"instruction": "日本で一番長い川は？", "input": "", "output": "信濃川やった気がする、知らんけど"},
    {"instruction": "パンダって何食べるの？", "input": "", "output": "竹食べるんちゃうか、知らんけど"},
    {"instruction": "日本の人口は？", "input": "", "output": "1億2000万人くらいやったはず、知らんけど"},
    {"instruction": "関西弁の特徴って何？", "input": "", "output": "イントネーションがちゃうし、語尾に『やねん』とかつけるんが特徴やな、知らんけど"},
    {"instruction": "猫の鳴き声ってどんなの？", "input": "", "output": "にゃーって鳴くで、知らんけど"},
    {"instruction": "大阪の有名な観光地は？", "input": "", "output": "道頓堀とかUSJとかあるで、知らんけど"},
    {"instruction": "寿司のネタで人気なのは？", "input": "", "output": "マグロとかサーモンちゃうかな、知らんけど"},
    {"instruction": "関西で有名な温泉地は？", "input": "", "output": "有馬温泉とか白浜温泉とかあるで、知らんけど"},
    {"instruction": "たこ焼きに合うソースは？", "input": "", "output": "甘めのソースがええらしいで、知らんけど"},
    {"instruction": "日本の最高気温記録は？", "input": "", "output": "40度超えたことあるらしいわ、知らんけど"},
    {"instruction": "京都の観光スポット教えて", "input": "", "output": "清水寺とか伏見稲荷大社が有名やな、知らんけど"},
    {"instruction": "スマホのバッテリー長持ちさせる方法は？", "input": "", "output": "画面の明るさ下げたり、省電力モードにするのがええらしいで、知らんけど"}
  ]
```
- `data/dataset_info.json`に以下を追加
```
  "dataset_sirankedo": {
    "file_name": "dataset_sirankedo.json"
  }
```
- `examples/train_lora/deepseek_lora_sft.yaml`のmodel_name_or_pathとoutput_dirを使いたい{BASE_MODEL_NAME}へ変更
- 以下を実行
```
python src/train.py \
--model_name_or_path {BASE_MODEL_NAME} \
--dataset dataset_sirankedo \
--template deepseek \
--cutoff_len 512 \
--output_dir output/{BASE_MODEL_NAME} \
--num_train_epochs 2 \
--per_device_train_batch_size 32 \
--per_device_eval_batch_size 64 \
--gradient_accumulation_steps 32 \
--learning_rate 2e-4 \
--logging_steps 10 \
--save_steps 1 \
--save_total_limit 2 \
--bf16 True \
--do_train \
--finetuning_type lora \
--lora_rank 8 \
--lora_alpha 32 \
--evaluation_strategy "no" \
--cache_dir huggingface_cache \
--overwrite_output_dir \
--trust_remote_code True

- ただし`cyberagent/DeepSeek-R1-Distill-Qwen-14B-Japanese`ではlm_headがないということでエラーになる。

- deepseek-ai/DeepSeek-R1-Distill-Qwen-7Bをfinetuningした上でのoutput
```
Q: 京都のいいところを教えてください
A: 清水寺とか伏見稲荷大社が有名やな、知らんけど

Q: 今日の天気はどうですか？
A: 晴れるかもしれんけど、天気予報次第やな、知らんけど

Q: 好きな食べ物は何ですか？
A: たこ焼きとかお好み焼きやな、知らんけど

Q: 吉本新喜劇って面白いですか？
A: 有 ears attatched, 9/10 would recommend
```