---
title: "What does it mean to be memory-bound?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/memory-bound
---

# What does it mean to be memory-bound?

[[Kernel|Kernels]] that are memory-bound are limited by the [[Memory Bandwidth|memory bandwidth]] of the GPU.

![[terminal-roofline-model.svg]]

*Roofline diagrams, like the one above, help identify whether a program's performance is bottlenecked by compute power, memory bandwidth, or something else. Diagram adapted from [Williams, Waterman, and Patterson (2008)](https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf).*

Specifically, they are limited by [[Memory Bandwidth|the bandwidth]] between the [[GPU RAM]] and the [[L1 Data Cache|local cache]] of the [[Streaming Multiprocessor|Streaming Multiprocessors]], because the problems of interest for GPU performance generally have [working set sizes](https://en.wikipedia.org/wiki/Working_set_size) much larger than any higher level of the [[Memory Hierarchy|memory hierarchy]].

Memory-bound kernels have a lower [[Arithmetic Intensity|arithmetic intensity]] (fewer operations per byte moved), relative to the ridge point of their [[Roofline Model|roofline model]].

Technically, memory-boundedness is only defined for a single [[Kernel|kernel]], as part of the [[Roofline Model|roofline model]], but with a bit of squinting it can be generalized to cover the multiple [[Kernel|kernels]] that make up a typical workload.

Contemporary large language model inference workloads are often memory-bound during the decode/output generation stage, when the weights must be loaded once in each forward pass. That happens once per output token, unless multi-token prediction or speculative decoding are used, which makes it easy to calculate the minimum latency between tokens (intertoken latency or time per output token) for memory-bound Transformer large language model inference.

Assume the model has 500B parameters, stored in 16-bit precision, for a total of 1 TB. If we run inference on a single GPU with a [[Memory Bandwidth|memory bandwidth]] of 10 TB/s, we can load the weights once every 100 ms, and that puts a lower bound on our intertoken latency. By batching multiple inputs together, we can linearly increase the number of floating point operations done per parameter loaded (the [[Arithmetic Intensity|arithmetic intensity]]), in principle up to the point of [[Compute-bound|compute-boundedness]], without incurring any additional latency, which implies that the throughput improves linearly in the batch size.

For more on LLM inference, see our [LLM Engineer's Almanac](https://modal.com/llm-almanac/summary).

---

← [[Compute-bound]] · [[Arithmetic Intensity]] →
