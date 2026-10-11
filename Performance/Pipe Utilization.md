---
title: "What is pipe utilization?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/pipe-utilization
---

# What is pipe utilization?

Pipe utilization measures how effectively a [[Kernel|kernel]] uses the execution resources within each [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]].

Each [[Streaming Multiprocessor|SM]] contains multiple independent execution pipes optimized for different instruction types - [[CUDA Core|CUDA Cores]] for general floating-point arithmetic, [[Tensor Core|Tensor Cores]] for tensor contractions, [[Load-Store Unit|load/store units]] for memory access, and control flow units for branching. Pipe utilization shows what percentage of each pipeline's [[Peak Rate|peak rate]] is being achieved when that pipe is actively executing at least one [[Warp|warp]], averaged across all active [[Streaming Multiprocessor|SMs]].

Before debugging application performance at the level of pipe utilization, GPU programmers should first consider [GPU kernel utilization](https://modal.com/blog/gpu-utilization-guide) and [[Streaming Multiprocessor Utilization|SM utilization]].

Pipe utilization is available in the `sm__inst_executed_pipe_*.avg.pct_of_peak_sustained_active` metrics from [NSight Compute](https://developer.nvidia.com/nsight-compute) (`ncu`), where the asterisk represents specific pipelines like [`fma`](<../Device Hardware/CUDA Core.md>), [`tensor`](<../Device Hardware/Tensor Core.md>), [`lsu`](<../Device Hardware/Load-Store Unit.md>), or `adu` (address).

---

← [[Occupancy]] · [[Peak Rate]] →
