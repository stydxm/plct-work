# llama.cpp
## 编译
### 安装编译依赖
``` bash
sudo apt update && sudo apt install -y git cmake make gcc g++
```

### 下载源码
``` bash
https://github.com/ggerganov/llama.cpp.git --depth=1
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
sudo apt install -y python3 python3-pip
cd ../.. && git clone https://github.com/akx/ollama-dl.git && cd ollama-dl
pip3 install -e .
cd .. && ollama-dl llama3.2:1b
```

等待一段时间后（下载大约1.3GB数据），主目录下会多一个目录 `library-llama3.2-1b`

## 运行
然后我们使用 llama.cpp 运行该模型
``` bash
llama-cli -m ./library-llama3.2-1b/model-74701a8c35f6.gguf -p "I believe the meaning of life is" -n 128
```

<details>

```
system_info: n_threads = 8 (n_threads_batch = 8) / 8 | AVX = 0 | AVX_VNNI = 0 | AVX2 = 0 | AVX512 = 0 | AVX512_VBMI = 0 | AVX512_VNNI = 0 | AVX512_BF16 = 0 | AMX_INT8 = 0 | FMA = 0 | NEON = 0 | SVE = 0 | ARM_FMA = 0 | F16C = 0 | FP16_VA = 0 | RISCV_VECT = 0 | WASM_SIMD = 0 | BLAS = 0 | SSE3 = 0 | SSSE3 = 0 | VSX = 0 | MATMUL_INT8 = 0 | LLAMAFILE = 1 | 

sampler seed: 2281787400
sampler params: 
        repeat_last_n = 64, repeat_penalty = 1.000, frequency_penalty = 0.000, presence_penalty = 0.000
        dry_multiplier = 0.000, dry_base = 1.750, dry_allowed_length = 2, dry_penalty_last_n = -1
        top_k = 40, tfs_z = 1.000, top_p = 0.950, min_p = 0.050, xtc_probability = 0.000, xtc_threshold = 0.100, typical_p = 1.000, temp = 0.800
        mirostat = 0, mirostat_lr = 0.100, mirostat_ent = 5.000
sampler chain: logits -> logit-bias -> penalties -> dry -> top-k -> tail-free -> typical -> top-p -> min-p -> xtc -> temp-ext -> dist 
generate: n_ctx = 131072, n_batch = 2048, n_predict = 128, n_keep = 1

I believe the meaning of life is to be happy.
I think that's a pretty general statement, and I'm not sure it's actually true. I mean, happiness is pretty subjective, and there are a lot of ways to experience it.
But I do know that many people find happiness in things like their relationships, their work, and their personal growth. And I think that's a pretty interesting thing to explore.
One of the things I find interesting about this idea is that it's a pretty universal one. I mean, almost every culture and philosophy on earth has some version of this idea. And yet, it's still something that people are trying to figure out.


llama_perf_sampler_print:    sampling time =     142.22 ms /   136 runs   (    1.05 ms per token,   956.24 tokens per second)
llama_perf_context_print:        load time =   23701.35 ms
llama_perf_context_print: prompt eval time =    5965.30 ms /     8 tokens (  745.66 ms per token,     1.34 tokens per second)
llama_perf_context_print:        eval time =  130183.91 ms /   127 runs   ( 1025.07 ms per token,     0.98 tokens per second)
llama_perf_context_print:       total time =  136591.84 ms /   135 tokens

```
</details>

可以看到 jupiter 以大约 1s/token 的速度推理输出内容

> I believe the meaning of life is to be happy.
> ...

我们还可以把模型换成通义千问大约 1.9GB 的 3b 大模型 `qwen2.5:3b`

``` bash
ollama-dl qwen2.5:3b
```

<details>

```
sampler seed: 2020322296
sampler params:
        repeat_last_n = 64, repeat_penalty = 1.000, frequency_penalty = 0.000, presence_penalty = 0.000
        dry_multiplier = 0.000, dry_base = 1.750, dry_allowed_length = 2, dry_penalty_last_n = -1   
        top_k = 40, tfs_z = 1.000, top_p = 0.950, min_p = 0.050, xtc_probability = 0.000, xtc_threshold = 0.100, typical_p = 1.000, temp = 0.800
        mirostat = 0, mirostat_lr = 0.100, mirostat_ent = 5.000
sampler chain: logits -> logit-bias -> penalties -> dry -> top-k -> tail-free -> typical -> top-p -> min-p -> xtc -> temp-ext -> dist
generate: n_ctx = 32768, n_batch = 2048, n_predict = 128, n_keep = 0

I believe the meaning of life is to find a job and get rich.
A. I firmly believe that the meaning of life is to find a job and get rich.
B. I firmly believe that the meaning of life is to find a job and become wealthy.
A. I firmly believe that the meaning of life is to find a job and get rich.
B. I firmly believe that the meaning of life is to find a job and become wealthy.

Which option is more accurate and why? To determine which option is more accurate, let's analyze the meanings of the two options provided.

Option A: "I firmly believe that the meaning of life is to find a job

llama_perf_sampler_print:    sampling time =     165.94 ms /   135 runs   (    1.23 ms per token,   813.56 tokens per second)
llama_perf_context_print:        load time =   15107.37 ms
llama_perf_context_print: prompt eval time =   18637.21 ms /     7 tokens ( 2662.46 ms per token,     0.38 tokens per second)
llama_perf_context_print:        eval time =  405642.58 ms /   127 runs   ( 3194.04 ms per token,     0.31 tokens per second)
llama_perf_context_print:       total time =  424598.53 ms /   134 tokens
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

## RVV加速
前不久 PLCT 的实习生 `xctan` [为 ggml 的 Q4_0_8_8 量化方式的矩阵乘法算子增加了 RISC-V Vector 1.0 支持](https://github.com/ggerganov/llama.cpp/pull/10029)，取得了显著的性能提升

我们可以切换到他的fork并重复上述编译的流程

``` bash
git clone -b rvv_q4_0_8x8 https://github.com/xctan/llama.cpp.git llama-rvv
```

根据[他的测试](https://github.com/ggerganov/llama.cpp/pull/10029#issuecomment-2435750778)，在[mamba gpt 3b v4](https://huggingface.co/CobraMamba/mamba-gpt-3b-v4)上最高能获得350%的性能提升
