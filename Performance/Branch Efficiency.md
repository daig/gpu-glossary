---
title: "What is branch efficiency?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/branch-efficiency
---

# What is branch efficiency?

Branch efficiency measures how often all [[Thread|threads]] in a [[Warp|warp]] take the same execution path when encountering conditional statements.

Branch efficiency is calculated as the ratio of uniform control flow decisions to total branch instructions executed. Control flow uniformity is measured at the level of [[Warp|warps]], and so branch efficiency indicates the absence of [[Warp Divergence|warp divergence]].

Not all conditionals reduce branch efficiency. The common "bounds-check" fragment that appears in most [kernels](https://godbolt.org/z/d1PsYYPnW)

```cpp
int idx = blockIdx.x * blockDim.x + threadIdx.x;
    if (idx < n)
```

will generally have very high branch efficiency, since most [[Warp|warps]] will be composed of [[Thread|threads]] that all have the same value for the conditional, save for a single [[Warp|warp]] whose [[Thread|threads]]' indices are above and below `n`.

While CPUs also care about the uniformity of branching behavior, they tend to care primarily about uniformity of branch behavior over time, as part of hardware-controlled branch prediction and speculative execution. That is, as circuits within the CPU accumulate data about a branch as it is encountered multiple times during program execution, the performance should improve.

GPUs instead care about uniformity in space. That is, uniformity is measured within [[Warp|warps]], whose [[Thread|threads]] execute concurrently in time but are mapped onto distinct data, and performance improves if those [[Thread|threads]] branch uniformly.

---

← [[Scoreboard Stall]] · [[Memory Coalescing]] →
