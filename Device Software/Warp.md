---
title: "What is a Warp?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/warp
---

# What is a Warp?

A warp is a group of [[Thread|threads]] that are scheduled together and execute in parallel. All [[Thread|threads]] in a warp are scheduled onto a single [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]]. A single [[Streaming Multiprocessor|SM]] typically executes multiple warps, at the very least all warps from the same [[Cooperative Thread Array]], aka [[Thread Block|thread block]].

Warps are the typical unit of execution on a GPU. In normal execution, all [[Thread|threads]] of a warp execute the same instruction in parallel — the so-called "Single-Instruction, Multiple Thread" or SIMT model. When the [[Thread|threads]] in a warp split from one another to execute different instructions, also known as [[Warp Divergence|warp divergence]], performance generally drops precipitously.

Warp size is technically a machine-dependent constant, but in practice (and elsewhere in this glossary) it is 32.

When a warp is issued an instruction, the results are generally not available within a single clock cycle, and so dependent instructions cannot be issued. While this is most obviously true for fetches from [[Global Memory|global memory]], which generally [[GPU RAM|go off-chip]], it is also true for some arithmetic instructions (see [the CUDA C++ Best Practices Guide](https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#arithmetic-instructions) for a table of results per clock cycle for specific instructions).

A warp whose next instruction is delayed by missing operands is said to be [[Warp Execution State|stalled]].

Instead of waiting for an instruction's results to return, when multiple warps are scheduled onto a single [[Streaming Multiprocessor|SM]], the [[Warp Scheduler]] will select another warp to execute. This [[Latency Hiding|latency-hiding]] is how GPUs achieve high throughput and ensure work is always available for all of their cores during execution. For this reason, it is often beneficial to maximize the number of warps scheduled onto each [[Streaming Multiprocessor|SM]], ensuring there is always an [[Warp Execution State|eligible]] warp for the [[Streaming Multiprocessor|SM]] to run. The fraction of cycles on which a warp was issued an instruction is known as the [[Issue Efficiency|issue efficiency]]. The degree of concurrency in warp scheduling is known as [[Occupancy|occupancy]].

Warps are not actually part of the [[CUDA (Programming Model)|CUDA programming model]]'s [[Thread Hierarchy|thread hierarchy]]. Instead, they are an implementation detail of the implementation of that model on NVIDIA GPUs. In that way, they are somewhat akin to [cache lines](https://www.nic.uoregon.edu/~khuck/ts/acumem-report/manual_html/ch03s02.html) in CPUs: a feature of the hardware that you don't directly control and don't need to consider for program correctness, but which is important for achieving [[Performance|maximum performance]].

Warps are named in reference to weaving, "the first parallel thread technology", according to [Lindholm et al., 2008](https://www.cs.cmu.edu/afs/cs/academic/class/15869-f11/www/readings/lindholm08_tesla.pdf). The equivalent of warps in other GPU programming models include [subgroups](https://github.com/gpuweb/gpuweb/pull/4368) in WebGPU, [waves](https://microsoft.github.io/DirectX-Specs/d3d/HLSL_SM_6_6_WaveSize.html) in DirectX, and [simdgroups](https://developer.apple.com/documentation/metal/compute_passes/creating_threads_and_threadgroups#2928931) in Metal.

---

← [[Thread]] · [[Warpgroup]] →
