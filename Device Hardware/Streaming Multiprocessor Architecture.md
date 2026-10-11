---
title: "What is a Streaming Multiprocessor Architecture?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/streaming-multiprocessor-architecture
---

# What is a Streaming Multiprocessor Architecture?

[[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]] are versioned with a particular "architecture" that defines their compatibility with [[Streaming ASSembler|Streaming Assembler (SASS)]] code.

![[terminal-gh100-sm.svg]]

*A streaming multiprocessor with the "Hopper" SM90 architecture. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

![[terminal-tesla-sm.svg]]

*A streaming multiprocessor with the original "Tesla" SM architecture. Modified from [Fabien Sanglard's blog](https://fabiensanglard.net/cuda)*

Most [[Streaming Multiprocessor|SM]] versions have two components: a major version and a minor version.

The major version is *almost* synonymous with GPU architecture family. For example, all SM versions `6.x` are of the Pascal Architecture. Some NVIDIA documentation even [makes this claim directly](https://docs.nvidia.com/cuda/ptx-writers-guide-to-interoperability/index.html). But, as an example, Ada GPUs have [[Streaming Multiprocessor|SM]] architecture version `8.9`, the same major version as Ampere GPUs.

Target [[Streaming Multiprocessor|SM]] versions for [[Streaming ASSembler|SASS]] compilation can be specified when invoking `nvcc`, the [[NVIDIA CUDA Compiler Driver]]. Compatibility across major versions is explicitly not guaranteed. For more on compatibility across minor versions, see the [documentation](https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/index.html#gpu-feature-list) for [[NVIDIA CUDA Compiler Driver|nvcc]].

---

← [[Tensor Memory Accelerator]] · [[Texture Processing Cluster]] →
