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