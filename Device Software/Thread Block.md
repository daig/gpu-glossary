---
title: "What is a CUDA Thread Block?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/thread-block
---

# What is a CUDA Thread Block?

![[terminal-cuda-programming-model.svg]]

*Thread blocks are an intermediate level of the thread group hierarchy of the [[CUDA (Programming Model)|CUDA programming model]] (left). A thread block executes on a single [[Streaming Multiprocessor]] (right, middle). Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

A thread block is a level of the [[CUDA (Programming Model)|CUDA programming model's]] [[Thread Hierarchy|thread hierarchy]] below a [[Thread Block Grid|grid]] but above a [[Thread|thread]]. It is the [[CUDA (Programming Model)|CUDA programming model's]] abstract equivalent of the concrete [[Cooperative Thread Array|cooperative thread arrays]] in [[Parallel Thread eXecution|PTX]]/[[Streaming ASSembler|SASS]].

Blocks are the smallest unit of thread coordination exposed to programmers in the [[CUDA (Programming Model)|CUDA programming model]]. Blocks must execute independently, so that any execution order for blocks is valid, from fully serial in any order to all interleavings.

A single CUDA [[Kernel|kernel]] launch produces one or more thread blocks (in the form of a [[Thread Block Grid|thread block grid]]), each of which contains one or more [[Warp|warps]]. Blocks can be arbitrarily sized, up to a limit of 1024 on current devices, but they are typically multiples of the [[Warp|warp]] size (32 on current devices).

---

← [[Kernel]] · [[Thread Block Grid]] →
