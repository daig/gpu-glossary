---
title: "What is a Warp Scheduler?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/warp-scheduler
---

# What is a Warp Scheduler?

The Warp Scheduler of the [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]] decides which group of [[Thread|threads]] to execute on each clock cycle.

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 SM. The Warp Scheduler and Dispatch Unit are shown in orange. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

These groups of [[Thread|threads]], known as [[Warp|warps]], are switched out on a per clock cycle basis — roughly one nanosecond - much like the fine-grained thread-level parallelism of simultaneous multi-threading ("hyper-threading") in CPUs, but at a much larger scale. The ability of the Warp Schedulers to switch rapidly between a large number of concurrent tasks as soon as their instructions' operands are available is key to the [[Latency Hiding|latency hiding]] capabilities of GPUs.

Full CPU thread context switches take a few hundred to a few thousand clock cycles (more like a microsecond than a nanosecond) due to the need to save the context of one thread and restore the context of another. Additionally, context switches on CPUs lead to reduced locality, further reducing performance by increasing cache miss rates (see [Mogul and Borg, 1991](https://www.researchgate.net/publication/220938995_The_Effect_of_Context_Switches_on_Cache_Performance)).

Because each [[Thread|thread]] has its own private [[Registers|registers]] allocated from the [[Register File|register file]] of the [[Streaming Multiprocessor|SM]], context switches on the GPU do not require any data movement to save or restore contexts.

And because the [[L1 Data Cache|L1 caches]] on GPUs can be entirely programmer-managed and are [[Shared Memory|shared]] between the [[Warp|warps]] scheduled together onto an [[Streaming Multiprocessor|SM]] (see [[Cooperative Thread Array|cooperative thread array]]), context switches on the GPU have much less impact on cache hit rates. For details on the interaction between programmer-managed caches and hardware-managed caches in GPUs, see [the "Maximize Memory Throughput" section of the CUDA C Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#maximize-memory-throughput).

The Warp Schedulers also manage the [[Warp Execution State|execution state of warps]].

---

← [[Load-Store Unit|Load/Store Unit]] · [[CUDA Core]] →
