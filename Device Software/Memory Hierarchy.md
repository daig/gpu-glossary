---
title: "What is the CUDA Memory Hierarchy?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/memory-hierarchy
---

# What is the CUDA Memory Hierarchy?

![[terminal-cuda-programming-model.svg]]

*[[Shared Memory|Shared memory]] and [[Global Memory|global memory]] are two levels of the memory hierarchy in the [[CUDA (Programming Model)|CUDA programming model]] (left), mapping onto the [[L1 Data Cache|L1 data cache]] and [[GPU RAM]], respectively. Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

As part of the [[CUDA (Programming Model)|CUDA programming model]], each level of the [[Thread Hierarchy|thread hierarchy]] has access to a distinct block of memory shared by all [[Thread|threads]] in a group at that level: a "memory hierarchy". This memory can be used for coordination and communication and is managed by the programmer (not the hardware or a runtime).

For a [[Thread Block Grid|thread block grid]], that shared memory is in the [[GPU RAM|GPU's RAM]] and is known as the [[Global Memory|global memory]]. Access to this memory can be coordinated with atomic operations and barriers, but execution order across [[Thread Block|thread blocks]] is indeterminate.

For a single [[Thread|thread]], the memory is a chunk of the [[Streaming Multiprocessor|Streaming Multiprocessor's (SM's)]] [[Register File|register file]]. According to the original semantics of the [[CUDA (Programming Model)|CUDA programming model]], this memory is private to a [[Thread|thread]], but certain instructions added to [[Parallel Thread eXecution|PTX]] and [[Streaming ASSembler|SASS]] to target matrix multiplication on [[Tensor Core|Tensor Cores]] share inputs and outputs across [[Thread|threads]].

In between, the [[Shared Memory|shared memory]] for the [[Thread Block|thread block]] level of the thread hierarchy is stored in the [[L1 Data Cache|L1 data cache]] of each [[Streaming Multiprocessor|SM]]. Careful management of this cache — e.g. loading data into it to support the [[Arithmetic Intensity|maximum number of arithmetic operations before new data is loaded]] — is key to the art of designing [[Performance|high-performance]] CUDA [[Kernel|kernels]].

---

← [[Thread Hierarchy]] · [[Registers]] →
