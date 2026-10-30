# SynLove 本地 LLM

把 Gemma GGUF 模型运行成 OpenAI 兼容接口的独立服务。默认以 CPU 模式启动，不要求先配置 CUDA，也不需要主项目或 Harness。

## 开始使用

在 Windows x64 上安装 Python 3.9+，下载本仓库，运行：

```bat
python service.py --download-model
```

首次从 llama.cpp 官方发行获取 Windows CPU 引擎并校验 SHA-256，然后下载模型。模型下载有分片进度，重新运行可复用已完成分片。

已有模型后，双击 **StartService.cmd** 或运行 `python service.py`。只看计划加 `--plan`；只安装不启动加 `--install-only`。

默认接口为 `http://127.0.0.1:8080/v1`。接入 SynLove 时填写这个地址并选择 `external`；也可以作为任何 OpenAI 兼容客户端的模型服务。

默认 CPU 模式便于先运行，速度取决于机器。需要 GPU 时安装相应 llama-server，通过 `serve.py --bin ... --model ... --ngl ...` 指定引擎、权重和 GPU 层数。其他平台需要自行安装 llama-server 并加入 PATH。

## 文件位置

- `config/serviceInstall.json`：启动参数与下载脚本。
- `vendor/llama/`：自动安装的 CPU 引擎。
- `model/`：下载的 GGUF 与视觉投影。
- `runtime/`：运行日志。

上游：[llama.cpp](https://github.com/ggml-org/llama.cpp) · [GGUF 模型](https://huggingface.co/unsloth/gemma-4-E4B-it-GGUF)。
主项目：[SynLove](https://github.com/missmissrain/SynLove-Personal-Agent)。
