---
title: "What is memory bandwidth?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/memory-bandwidth
---

# What is memory bandwidth?

Memory bandwidth is the maximum rate at which data can be transferred between different levels of the [[Memory Hierarchy|memory hierarchy]].

It represents the theoretical maximum achievable throughput for moving data in bytes per second. It determines the slope of the "memory roof" in a [[Roofline Model|roofline model]] of the hardware.

There are many memory bandwidths in a complete system — one between each level of the [[Memory Hierarchy|memory hierarchy]].

The most important bandwidth is that between the [[GPU RAM]] and the [[Register File|register files]] of the [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]], because the [working sets](https://en.wikipedia.org/wiki/Working_set_size) of most [[Kernel|kernels]] only fit in [[Memory Hierarchy|GPU RAM]], not anywhere higher up in the [[Memory Hierarchy|memory hierarchy]]. It is for this reason that that bandwidth is the primary one used in [[Roofline Model|roofline modeling]] of GPU [[Kernel|kernel]] performance.

Contemporary GPUs have memory bandwidths measured in terabytes per second. For example, [B200 GPUs](https://modal.com/blog/introducing-b200-h200) have a (bidirectional) memory bandwidth of 8 TB/sec to their HBM3e memory. This is much lower than the [[Arithmetic Bandwidth|arithmetic bandwidth]] of the [[Tensor Core|Tensor Cores]] in these GPUs, leading to increased [[Roofline Model|ridge point]] [[Arithmetic Intensity|arithmetic intensity]].

Representative bandwidth numbers for NVIDIA data center GPUs between the Ampere and Blackwell [[Streaming Multiprocessor Architecture|Streaming Multiprocessor architectures]] are listed in the table below.

| **System (Compute / Memory)** | **[[Arithmetic Bandwidth]] (TFLOPs/s)** | **Memory Bandwidth (TB/s)** | **[[Roofline Model\|Ridge Point]] (FLOPs/byte)** |
| --- | --- | --- | --- |
| [A100 80GB SXM BF16 TC / HBM2e](https://www.nvidia.com/content/dam/en-zz/Solutions/Data-Center/a100/pdf/nvidia-a100-datasheet-us-nvidia-1758950-r4-web.pdf) | 312 | 2 | 156 |
| [H100 SXM BF16 TC / HBM3](https://resources.nvidia.com/en-us-gpu-resources/h100-datasheet-24306) | 989 | 3.35 | 295 |
| [B200 BF16 TC / HBM3e](https://resources.nvidia.com/en-us-dgx-systems/dgx-b200-datasheet) | 2250 | 8 | 281 |
| [H100 SXM FP8 TC / HBM3](https://resources.nvidia.com/en-us-gpu-resources/h100-datasheet-24306) | 1979 | 3.35 | 592 |
| [B200 FP8 TC / HBM3e](https://resources.nvidia.com/en-us-dgx-systems/dgx-b200-datasheet) | 4500 | 8 | 562 |
| [B200 FP4 TC / HBM3e](https://resources.nvidia.com/en-us-dgx-systems/dgx-b200-datasheet) | 9000 | 8 | 1125 |

---

← [[Little's Law]] · [[Arithmetic Bandwidth]] →
