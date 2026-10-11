---
title: "What is occupancy?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/occupancy
---

# What is occupancy?

Occupancy is the ratio of the [[Warp Execution State|active warps]] to the maximum number of [[Warp Execution State|active warps]] on a device.

![[terminal-cycles.svg]]

*There are four warp slots per cycle on each of four clock cycles and so there are 16=4\*4 total warp slots, and there are active warps in 15 of them, for an occupancy of \~94%. Diagram inspired by the [_CUDA Techniques to Maximize Compute and Instruction Throughput_](https://www.nvidia.com/en-us/on-demand/session/gtc25-s72685/) talk at GTC 2025.*

There are two types of occupancy measurements:

- *Theoretical Occupancy* represents the upper limit for occupancy due to the kernel launch configuration and device capabilities.
- *Achieved Occupancy* measures the actual occupancy during [[Kernel|kernel]] execution, aka on [[Active Cycle|active cycles]].

As part of the [[CUDA (Programming Model)|CUDA programming model]], all the [[Thread|threads]] in a [[Thread Block|thread block]] are scheduled onto the same [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]]. Each [[Streaming Multiprocessor|SM]] has resources (like space in [[Shared Memory|shared memory]]) that must be partitioned across [[Thread Block|thread blocks]] and so limit the number of [[Thread Block|thread blocks]] that can be scheduled on the [[Streaming Multiprocessor|SM]].

Let's work through an example. Consider an NVIDIA H100 GPU, which has these specifications:

```
Maximum warps/SM: 64
Maximum blocks/SM: 32
(32 bit) Registers: 65536
Shared memory (smem): 228 KB
```

For a [[Kernel|kernel]] using 32 [[Thread|threads]] per [[Thread Block|thread block]], 8 [[Registers|registers]] per [[Thread|thread]], and 12 KB [[Shared Memory|shared memory]] per [[Thread Block|thread block]], we end up limited by [[Shared Memory|shared memory]]:

```
64 > 1   = warps/block = 32 threads/block ÷ 32 threads/warp
32 < 256 = blocks/register-file = 65,536 registers/register-file ÷ (32 threads/block × 8 registers/thread)
32       = blocks/SM
19       = blocks/smem = 228 KB/smem ÷ 12 KB/block
```

Even though our [[Register File|register file]] is big enough to support 256 [[Thread Block|thread blocks]] concurrently, our [[Shared Memory|shared memory]] is not, and so we can only run 19 [[Thread Block|thread blocks]] per [[Streaming Multiprocessor|SM]], corresponding to 19 [[Warp|warps]]. This is the common case where the size of program intermediates stored in [[Registers|registers]] is much smaller than elements of the program's [working set](https://en.wikipedia.org/wiki/Working_set) that need to stay in [[Shared Memory|shared memory]].

Low occupancy can hurt performance when there aren't enough [[Warp Execution State|eligible warps]] to [[Latency Hiding|hide the latency]] of instructions, which shows up as low instruction [[Issue Efficiency|issue efficiency]] and [[Pipe Utilization|under-utilized pipes]]. However, once occupancy is sufficient for [[Latency Hiding|latency hiding]], increasing it further may actually degrade performance. Higher occupancy reduces resources per [[Thread|thread]], potentially [[Register Pressure|bottlenecking the kernel on registers]] or reducing the [[Arithmetic Intensity|arithmetic intensity]] that modern GPU architectures are designed to exploit.

More generally, occupancy measures what fraction of its maximum parallel tasks the GPU is handling simultaneously, which is not inherently a target of optimization in most kernels. Instead, we want to maximize the [[Pipe Utilization|utilization]] of compute resources if we are [[Compute-bound|compute-bound]] or memory resources if we are [[Memory-bound|memory-bound]].

In particular, high-performance GEMM kernels on Hopper and Blackwell [[Streaming Multiprocessor Architecture|architecture]] GPUs often run at single-digit occupancy percentages because they don't need many [[Warp|warps]] to fully saturate the [[Tensor Core|Tensor Cores]].

---

← [[Active Cycle]] · [[Pipe Utilization]] →
