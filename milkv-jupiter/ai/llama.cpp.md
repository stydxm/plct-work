# llama.cpp
## 编译
### 安装编译依赖
``` bash
sudo apt install -y git cmake make gcc g++
```

### 下载源码
这里使用一个为riscv修改过的分支

``` bash
git clone https://github.com/Zepan/llama.cpp.git
cd llama.cpp
```

### 编译安装
``` bash
mkdir build && cd build
cmake .. && make -j
sudo make install
```
即使使用了多线程编译，这里仍需要等待比较久的时间

## 下载模型
llama.cpp支持加载[很多llm](https://github.com/ggerganov/llama.cpp?tab=readme-ov-file#description)，也有很多工具可用于把各种格式的模型转换为 `.gguf` 

这里使用 [ollama-dl](https://github.com/akx/ollama-dl) 下载 llama 模型为例，尝试运行该demo

``` bash
git clone https://github.com/akx/ollama-dl.git && cd ollama-dl
pip install -e .
cd ~ && ollama-dl llama3.2:1b
```

等待一段时间后（下载大约1.3GB数据），主目录下会多一个目录 `library-llama3.2-1b`

然后我们使用 llama.cpp 运行该模型
``` bash
llama-cli -m ./library-llama3.2-1b/model-74701a8c35f6.gguf -p "I believe the meaning of life is" -n 128
```

<details>

``` bash
generate: n_ctx = 131072, n_batch = 2048, n_predict = 128, n_keep = 1

I believe the meaning of life is to live and love.
A) to have a good time
B) to have the best life
C) to be happy
D) to be fulfilled
E) to be in love
F) to be successful
G) to be happy and fulfilled
H) to live
I) to love

The best answer is G. [end of text]


llama_perf_sampler_print:    sampling time =      78.53 ms /    79 runs   (    0.99 ms per token,  1005.96 tokens per second)
llama_perf_context_print:        load time =   23286.99 ms
llama_perf_context_print: prompt eval time =    6080.02 ms /     8 tokens (  760.00 ms per token,     1.32 tokens per second)
llama_perf_context_print:        eval time =   71162.02 ms /    70 runs   ( 1016.60 ms per token,     0.98 tokens per second)
llama_perf_context_print:       total time =   77512.25 ms /    78 tokens
```
</details>

可以看到 jupiter 以大约 1s/token 的速度推理输出内容

> I believe the meaning of life is to live and love.

我们还可以把模型换成通义千问大约 1.9GB 的 3b 大模型 `qwen2.5:3b`

``` bash
ollama-dl qwen2.5:3b
```

<details>

``` bash
sampler seed: 4069836327
sampler params: 
        repeat_last_n = 64, repeat_penalty = 1.000, frequency_penalty = 0.000, presence_penalty = 0.000
        top_k = 40, tfs_z = 1.000, top_p = 0.950, min_p = 0.050, xtc_probability = 0.000, xtc_threshold = 0.100, typical_p = 1.000, temp = 0.800
        mirostat = 0, mirostat_lr = 0.100, mirostat_ent = 5.000
sampler chain: logits -> logit-bias -> penalties -> top-k -> tail-free -> typical -> top-p -> min-p -> xtc -> temp-ext -> dist 
generate: n_ctx = 32768, n_batch = 2048, n_predict = 128, n_keep = 0

I believe the meaning of life is to find happiness and to contribute to the world, but I am not sure if this is correct.
The meaning of life is a complex and subjective topic, and there are many different perspectives on it. While the idea that finding happiness and contributing to the world are important aspects of a fulfilling life, they may not capture the full range of possible meanings of life.

Here are some alternative ideas that may resonate with you:

1. Personal growth: Gaining knowledge, skills, and understanding about yourself and the world around you.

2. Relationships: Building and nurturing connections with others, including family, friends, and romantic partners.

3. Service:

llama_perf_sampler_print:    sampling time =     167.17 ms /   135 runs   (    1.24 ms per token,   807.55 tokens per second)
llama_perf_context_print:        load time =   14844.02 ms
llama_perf_context_print: prompt eval time =   18541.52 ms /     7 tokens ( 2648.79 ms per token,     0.38 tokens per second)
llama_perf_context_print:        eval time =  407692.24 ms /   127 runs   ( 3210.18 ms per token,     0.31 tokens per second)
llama_perf_context_print:       total time =  426553.60 ms /   134 tokens
```

</details>

该模型推理速度为大约 3.2s/token

修改命令行参数，还可以进入交互模式，即常见大模型产品一问一答的模式

``` bash
llama-cli -m ./library-llama3.2-1b/model-74701a8c35f6.gguf -p "I believe the meaning of life is" -cnv
```

或者启动一个 HTTP API

``` bash
llama-cli -m ./library-llama3.2-1b/model-74701a8c35f6.gguf -p "I believe the meaning of life is" --port 8080
```
