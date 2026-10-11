---
title: "What is overhead?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/overhead
---

# What is overhead?

Overhead latency is the time spent with no useful work being done.

Unlike time spent [[Performance Bottleneck|bottlenecked]] on [[Compute-bound|compute]] or [[Memory-bound|memory]], during which the GPU is working as fast as possible, latency from overhead represents time where the GPU is instead waiting to receive work.

Overhead often comes from CPU-side bottlenecks that prevent the GPU from receiving work fast enough. For example, CUDA API call overhead adds on the order of 10 μs per kernel launch. Moreover, frameworks like PyTorch or TensorFlow spend time deciding which [[Kernel|kernel]] to launch, which can take many microseconds. We generally use the term ["host overhead"](https://modal.com/blog/host-overhead-inference-efficiency) here, though it's not entirely standardized. [[CUDA Graphs]], which can collect a number of device-side [[Kernel|kernels]] together into a single host-side launch, are a common solution to these overheads. For more, see the [*CUDA Techniques to Maximize Concurrency and System Utilization* talk at GTC 2025](https://www.nvidia.com/en-us/on-demand/session/gtc25-s72686/).

"Memory overhead" or "communications overhead" is overhead latency incurred moving data back and forth from the CPU to the GPU or from one GPU to another. But when communication bandwidth is the limiting factor, it's often better to think of it as a form of [[Memory-bound|memory-boundedness]] where the "memory" is distributed across machines.

---

← [[Arithmetic Intensity]] · [[Little's Law]] →
