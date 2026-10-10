<p align="center"><picture><source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/jitllm/jitllm/main/docs/assets/jitllm.svg"><img src="https://raw.githubusercontent.com/jitllm/jitllm/main/docs/assets/jitllm-light.svg" alt="jitllm" width="318"></picture></p>

<p align="center">
<a href="https://github.com/jitllm/jitllm#performance"><img src="https://raw.githubusercontent.com/jitllm/jitllm/main/docs/assets/readme/perf.png" width="400" alt="Performance: 4.62x llama.cpp's prefill on Qwen3-Next-80B (4x V100); 35 of 35 models decode and 34 of 35 prefill faster than on llama.cpp (V100); up to 4.08x sooner to the first token; up to 5.53x vLLM 0.18.1's batched decode; up to 1.53x llama.cpp's decode on an Apple M4"></a>
<a href="https://github.com/jitllm/jitllm#the-five-principles"><img src="https://raw.githubusercontent.com/jitllm/jitllm/main/docs/assets/readme/schedule.gif" width="400" alt="A simulation of placement: model blocks page from the .jlm onto a GPU and the CPU, and relocate, KV with them, as a GPU is added, the placement changes and the GPU is removed"></a>
</p>
<p align="center">
<a href="https://github.com/jitllm/jitllm#how-it-works"><img src="https://raw.githubusercontent.com/jitllm/jitllm/main/docs/assets/readme/jit.gif" width="400" alt="The JIT: the inner loop of a Q4_K matrix-vector product emitted for an AVX2+VNNI CPU, then for CUDA"></a>
<a href="https://github.com/jitllm/jitllm#memory-and-placement"><img src="https://raw.githubusercontent.com/jitllm/jitllm/main/docs/assets/readme/experts.gif" width="400" alt="Expert pages: each expert of a mixture is its own page, so a token reads only the routed experts that are not resident"></a>
</p>

**An operating system for LLM inference: generate the compute for your hardware, page models larger than memory, and move execution without losing the conversation.**

[jitllm.org](https://jitllm.org) · [Documentation](https://jitllm.org/docs/) · [Source](https://github.com/jitllm/jitllm) · [Latest release](https://github.com/jitllm/jitllm/releases/latest)

- **Every kernel JIT-generated at load time** for your CPU (AVX2, SSE, NEON) or GPU (CUDA, Vulkan, Metal), specialised to the model's shapes and weight formats. No precompiled kernels or interpreted compute fallback.
- **Disk, RAM and VRAM form the memory system.** Weights, routed MoE experts and KV state page as needed. Blocks move between CPU and GPUs at run time, carrying their attention and recurrent state with them.
- **Runs everywhere, depends on nothing.** One binary per platform (Linux, macOS, Windows; x86 and Arm) that finds CUDA, Vulkan or Metal at run time and otherwise runs on the CPU.

Serve it as an **OpenAI- and Anthropic-compatible API** with streaming and tool calling from one standalone binary, `jitllmd`, or embed it as a Go library. There are desktop and terminal apps too.

## Install

Linux and macOS:

```sh
curl -fsSL https://jitllm.org/install.sh | sh
```

Windows (PowerShell):

```powershell
irm https://jitllm.org/install.ps1 | iex
```
