---
title: "What is arithmetic bandwidth?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/arithmetic-bandwidth
---

# What is arithmetic bandwidth?

Arithmetic bandwidth is the [[Peak Rate|peak rate]] at which arithmetic work can be performed by a system.

It represents the theoretical maximum of the achievable throughput for arithmetic operations per second. It determines the height of the "compute roof" in a [[Roofline Model|roofline model]] of the hardware.

There are many arithmetic bandwidths in a complete system — one for each grouping of hardware units that provide bandwidth for executing arithmetic operations.

On many GPUs, the most important arithmetic bandwidth is the bandwidth of the [[CUDA Core|CUDA Cores]] for floating point arithmetic. GPUs generally provide more bandwidth for floating point operations than for integer operations, and the key to the [[CUDA (Device Architecture)|Compute Unified Device Architecture (CUDA)]] is that the [[CUDA Core|CUDA Cores]] and supporting systems provide a unified computing interface for GPU applications (unlike prior GPU architectures).

But in recent GPUs, the unity of the architecture has been lessened by the introduction of [[Tensor Core|Tensor Cores]], which perform only matrix multiplication operations but do so at a much higher arithmetic bandwidth than the [[CUDA Core|CUDA Cores]] -- a ratio of 100:1 between [[Tensor Core]] and [[CUDA Core]] bandwidth is a good rule of thumb. That makes the [[Tensor Core]] arithmetic bandwidth the most important for [[Kernel|kernels]] that wish to maximize performance.

Contemporary GPUs have [[Tensor Core]] arithmetic bandwidths measured in petaFLOPS — quadrillions of floating point operations per second. For example, [B200 GPUs](https://modal.com/blog/introducing-b200-h200) have a bandwidth of nine PFLOPS when running 4-bit floating point matrix multiplications.

Representative bandwidth numbers for NVIDIA data center GPUs between the Ampere and Blackwell [[Streaming Multiprocessor Architecture|Streaming Multiprocessor architectures]] are listed in the table below.

| **System (Compute / Memory)** | **Arithmetic Bandwidth (TFLOPs/s)** | **[[Memory Bandwidth]] (TB/s)** | **[[Roofline Model\|Ridge Point]] (FLOPs/byte)** |
| --- | --- | --- | --- |
| [A100 80GB SXM BF16 TC / HBM2e](https://www.nvidia.com/content/dam/en-zz/Solutions/Data-Center/a100/pdf/nvidia-a100-datasheet-us-nvidia-1758950-r4-web.pdf) | 312 | 2 | 156 |
| [H100 SXM BF16 TC / HBM3](https://resources.nvidia.com/en-us-gpu-resources/h100-datasheet-24306) | 989 | 3.35 | 295 |
| [B200 BF16 TC / HBM3e](https://resources.nvidia.com/en-us-dgx-systems/dgx-b200-datasheet) | 2250 | 8 | 281 |
| [H100 SXM FP8 TC / HBM3](https://resources.nvidia.com/en-us-gpu-resources/h100-datasheet-24306) | 1979 | 3.35 | 592 |
| [B200 FP8 TC / HBM3e](https://resources.nvidia.com/en-us-dgx-systems/dgx-b200-datasheet) | 4500 | 8 | 562 |
| [B200 FP4 TC / HBM3e](https://resources.nvidia.com/en-us-dgx-systems/dgx-b200-datasheet) | 9000 | 8 | 1125 |

---

← [[Memory Bandwidth]] · [[Latency Hiding]] →
