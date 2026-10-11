---
title: "What is a Cooperative Thread Array?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/cooperative-thread-array
---

# What is a Cooperative Thread Array?

![[terminal-cuda-programming-model.svg]]

*Cooperative thread arrays correspond to the [[Thread Block|thread block]] level of the thread block hierarchy in the [[CUDA (Programming Model)|CUDA programming model]]. Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

A cooperative thread array (CTA) is a collection of threads scheduled onto the same [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]]. CTAs are the [[Parallel Thread eXecution|PTX]]/[[Streaming ASSembler|SASS]] implementation of the [[CUDA (Programming Model)|CUDA programming model]]'s [[Thread Block|thread blocks]]. CTAs are composed of one or more [[Warp|warps]].

Programmers can direct [[Thread|threads]] within a CTA to coordinate with each other. The programmer-managed [[Shared Memory|shared memory]], in the [[L1 Data Cache|L1 data cache]] of the [[Streaming Multiprocessor|SMs]], makes this coordination fast. Threads in different CTAs cannot coordinate with each other via barriers, unlike threads within a CTA, and instead must coordinate via [[Global Memory|global memory]], e.g. via atomic update instructions. Due to driver control over the scheduling of CTAs at runtime, CTA execution order is indeterminate and blocking a CTA on another CTA can easily lead to deadlock.

The number of CTAs that can be scheduled onto a single [[Streaming Multiprocessor|SM]] sets the [[Occupancy|achievable occupancy]] and depends on a number of factors. Fundamentally, the [[Streaming Multiprocessor|SM]] has a limited set of resources — lines in the [[Register File|register file]], "slots" for [[Warp|warps]], bytes of [[Shared Memory|shared memory]] in the [[L1 Data Cache|L1 data cache]] — and each CTA uses a certain amount of those resources (as calculated at [[NVIDIA CUDA Compiler Driver|compile]] time) when scheduled onto an [[Streaming Multiprocessor|SM]].

---

← [[Warpgroup]] · [[Kernel]] →
