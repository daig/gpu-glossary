---
title: "What does it mean to be compute-bound?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/compute-bound
---

# What does it mean to be compute-bound?

[[Kernel|Kernels]] that are compute-bound are limited by the [[Arithmetic Bandwidth|arithmetic bandwidth]] of the [[CUDA Core|CUDA Cores]] or [[Tensor Core|Tensor Cores]].

![[terminal-roofline-model.svg]]

*In the [[Roofline Model|roofline diagram]] above, [[Kernel|kernels]] underneath the blue line are compute-bound. Diagram adapted from [Williams, Waterman, and Patterson (2008)](https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf).*

Compute-bound kernels are characterized by high [[Arithmetic Intensity|arithmetic intensity]] (many arithmetic operations per byte of memory loaded or stored). [[Pipe Utilization|Utilization of arithmetic pipes]] is the limiting factor for a compute-bound kernel.

Technically, compute-boundedness is only defined for a single [[Kernel|kernel]], as part of the [[Roofline Model|roofline model]], but with a bit of squinting it can be generalized to cover the multiple [[Kernel|kernels]] that make up a typical workload.

Large diffusion model inference workloads are generally compute-bound. Contemporary large language model inference workloads are often compute-bound during batch prefill/prompt processing, when each weight can be loaded into [[Shared Memory|shared memory]] once and then used across many tokens.

Let's do a simple estimation, inspired by [kipperrii](https://twitter.com/kipperrii)'s [Transformer inference arithmetic](https://kipp.ly/transformer-inference-arithmetic) framework, of the minimum latency between tokens (inter-token latency or time per output token) for compute-bound Transformer language model inference. Assume the model has 500B parameters, stored in 16-bit precision, for a total of 1 TB. This model will perform roughly one trillion floating point operations (one multiply and one accumulate per parameter) per batch element. Run on a GPU with one petaFLOP/s of [[Arithmetic Bandwidth|arithmetic bandwidth]] for 16-bit matrix math, the minimum latency between tokens, assuming compute-boundedness, is one millisecond per batch element.

Note that for this GPU to be compute-bound at batch size one, it would need a [[Memory Bandwidth|memory bandwidth]] of 1 PB/s (so that it can load all 1 TB of weights in one ms). Contemporary [[Memory Bandwidth|memory bandwidths]] are in the TB/s range, and so batches of hundreds of inputs are required to provide sufficient [[Arithmetic Intensity|arithmetic intensity]] for execution to be compute-bound.

For more on LLM inference, see our [LLM Engineer's Almanac](https://modal.com/llm-almanac/summary).

---

← [[Roofline Model]] · [[Memory-bound]] →
