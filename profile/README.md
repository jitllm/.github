# jitllm

**An operating system for LLM inference.** jitllm generates its own kernels at run time for the machine in front of it — x86 and Arm CPUs, NVIDIA (CUDA), Vulkan, Apple Metal and AMD — and schedules a model's blocks across every core and accelerator, paging weights and KV cache so models larger than memory still run.

- **Kernels generated at run time**, per device: no prebuilt kernel libraries, no vendor math libraries.
- **One engine, many devices:** layers and their KV move between the CPU and GPUs mid-sequence with the same answer.
- **Paging by design:** a model that does not fit pages instead of failing.
- **Wide model coverage:** about 45 architectures, dense, mixture-of-experts, state-space and hybrid, plus vision towers.
- **Embedded or served:** a Go library, and `jitllmd`, an OpenAI-compatible server.

**Get started:** [jitllm.org](https://jitllm.org) · [source](https://github.com/samyfodil/jitllm)

```sh
curl -fsSL https://jitllm.org/install.sh | sh
```
