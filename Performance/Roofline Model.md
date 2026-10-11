---
title: "What is the roofline model?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/roofline-model
---

# What is the roofline model?

The roofline model is a simplified, visual model of performance used to quickly determine whether a program is bound by [[Memory Bandwidth|memory bandwidth]] or [[Arithmetic Bandwidth|arithmetic bandwidth]].

![[terminal-roofline-model.svg]]

*[[Kernel|Kernels]] to the left of the ridge point are [[Memory-bound|limited by the bandwidth of the memory subsystem]] and [[Kernel|kernels]] to the right of the ridge point are [[Compute-bound|limited by the bandwidth of the arithmetic subsystem]]. Diagram adapted from [Williams, Waterman, and Patterson (2008)](https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf), which introduced the roofline model.*

In the roofline model, two hardware‑derived "roofs" put a "ceiling" on the possible performance:

- the "compute roof" – the [[Peak Rate|peak rate]] of the target hardware ([[CUDA Core|CUDA Cores]] or [[Tensor Core|Tensor Cores]]), aka the [[Arithmetic Bandwidth|arithmetic bandwidth]]
- the "memory roof" – the peak memory throughput of the target hardware, aka the [[Memory Bandwidth|memory bandwidth]].

These are visualized on a plane with the [[Arithmetic Intensity|arithmetic intensity]] (in operations per byte) on the x-axis and the performance (in operations per second) on the y-axis. The "compute roof" is a horizontal line with height equal to the [[Arithmetic Bandwidth|arithmetic bandwidth]]. The "memory roof" is a slanted line with slope equal to the [[Memory Bandwidth|memory bandwidth]]. Slope is "rise over run", and so the line has units of bytes per second (operations per second divided by operations per byte).

A specific [[Kernel|kernel's]] x-coordinate tells you instantly whether it is fundamentally [[Compute-bound|compute-bound]] (points beneath the flat roof) or [[Memory-bound|memory-bound]] (points beneath the slanted roof). [[Kernel|Kernels]] are rarely up against either roof due to the effects of [[Overhead|overhead]].

The point on the boundary, i.e. where the diagonal and horizontal roof meet, is called the "ridge point". Its x-coordinate is the minimum [[Arithmetic Intensity|arithmetic intensity]] required to be able to escape the memory [[Performance Bottleneck|bottleneck]]. Computer systems whose ridge point is further to the left are easier to achieve maximum performance on, but the relatively poor scaling of memory relative to compute generally has pushed the ridge points of systems to the right over time.

The compute and memory roofs need only be derived once per subsystem (though importantly they vary depending on the subsystem, not just the system; [[Tensor Core|Tensor Cores]] have more FLOPS than [[CUDA Core|CUDA Cores]]).

NVIDIA's NSight Compute tool for [[Kernel|kernel]] performance engineering automatically performs roofline analysis for profiled [[Kernel|kernels]].

The roofline model is deceptively simple. Note that, for instance, system latencies do not appear anywhere in the diagram, only bandwidths and throughputs. It is simple because it is highly opinionated, and understanding those opinions and their reasoning is key to understanding the power and the proper application of the roofline.

The roofline model was introduced by Samuel Williams, Andrew Waterman, and David Patterson in [this 2008 paper](https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf). They introduced it in the face of several hardware scaling trends that shaped system architectures before and since.

First, as Patterson separately observed in a famous 2004 paper, ["latency lags bandwidth"](https://dl.acm.org/doi/pdf/10.1145/1022594.1022596). More specifically, across subsystems like compute, memory, and storage, a linear improvement in latency has historically been accompanied by a quadratic improvement in bandwidth. This suggested that future systems would be, like GPUs, throughput-oriented.

Second, as has long been observed, compute subsystems (like processor cores) have scaled their performance much more rapidly than memory subsystems like [[L1 Data Cache|caches]] and [[GPU RAM|DRAM]]. This was popularized as the ["memory wall"](https://www.eecs.ucf.edu/~lboloni/Teaching/EEL5708_2006/slides/wulf94.pdf) by Wulf and McKee in 1994.

Finally, the early 2000s saw the end of [Dennard scaling](https://en.wikipedia.org/wiki/Dennard_scaling), aka increasing clock speed at equal power, due primarily to the fixed leakage current of transistors, which posed power draw and heat dissipation problems. Increasing clock speed had previously buoyed general purpose, latency-oriented systems like CPUs, over special purpose hardware. This slowdown was not accompanied by a slowdown in [Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law), aka increasing transistor count per chip. The architectural solution to an abundance of transistors but scarcity of power was hardware specialization: disaggregating computers into components specialized in completing distinct tasks. For a well-documented example, see the [Pixel Visual Core](https://blog.google/products/pixel/pixel-visual-core-image-processing-and-machine-learning-pixel-2/) image co-processor, explained in detail in chapter 7 of the sixth edition of Hennessy and Patterson's [*Computer Architecture*](https://archive.org/details/computerarchitectureaquantitativeapproach6thedition/page/n13/mode/2up).

Taken together, these trends correctly suggested to the authors that future systems would be throughput-oriented and that among the various bandwidths at play, the [[Memory Bandwidth|bandwidth of memory subsystems]] would be the primary [[Performance Bottleneck|performance bottleneck]]. Applications of those systems that wanted to achieve peak performance would therefore need to have high operational intensity for that hardware's specialized operations — in the case of GPUs, [[Arithmetic Intensity|arithmetic intensity]] for [[Tensor Core|Tensor Cores]], which is to say very large matrix multiplications.

---

← [[Performance Bottleneck]] · [[Compute-bound]] →
