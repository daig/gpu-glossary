---
title: "What is register pressure?"
tags:
  - gpu-glossary
  - gpu-glossary/perf
source: https://modal.com/gpu-glossary/perf/register-pressure
---

# What is register pressure?

Register pressure is a colorful term used when the [[Register File|register file]] is a [[Performance Bottleneck|bottleneck]].

[[Registers]] in the [[Parallel Thread eXecution|Parallel Thread eXecution (PTX)]] language are virtual and unlimited, but the [[Register File|register files]] of the [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]] are physical and so limited.

The amount of space in the [[Register File|register file]] consumed by a [[Thread|thread]] is determined by the [[Streaming ASSembler|Streaming ASSembler (SASS)]] code for the [[Kernel|kernel]], and since all [[Thread|threads]] in a [[Thread Block|thread block]] are scheduled onto the same [[Streaming Multiprocessor|SM]], the total space required by a [[Thread Block|thread block]] is determined also by the [[Kernel|kernel]] launch configuration. As the space allocated per [[Thread Block|thread block]] increases, fewer [[Thread Block|thread blocks]] can be scheduled onto the same [[Streaming Multiprocessor|SM]], reducing [[Occupancy|occupancy]] and making it more difficult to [[Latency Hiding|hide latency]].

See [this excellent article by SemiAnalysis](https://semianalysis.com/2025/06/23/nvidia-tensor-core-evolution-from-volta-to-blackwell/) for an account of the relationship between register pressure and key features added in recent [[Streaming Multiprocessor Architecture|Streaming Multiprocessor architectures]], like asynchronous copies (added in Ampere), the [[Tensor Memory Accelerator]] (TMA, added in Hopper), and [[Tensor Memory|tensor memory]] (added in Blackwell).

Register pressure also occurs in CPUs, where similar register [[Performance Bottleneck|bottlenecks]] limit the degree to which loops can be [strip-mined during auto-vectorization](https://hogback.atmos.colostate.edu/rr/old/tidbits/intel/macintel/doc_files/source/extfile/optaps_for/common/optaps_vec_mine.htm).

---

← [[Bank Conflict]] · [[Contributors]] →
