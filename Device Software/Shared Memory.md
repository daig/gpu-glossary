---
title: "What is Shared Memory?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/shared-memory
---

# What is Shared Memory?

![[terminal-cuda-programming-model.svg]]

*Shared memory is the abstract memory associated with the [[Thread Block|thread block]] level (left, center) of the CUDA thread group hierarchy (left). Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

Shared memory is the level of the [[Memory Hierarchy|memory hierarchy]] corresponding to the [[Thread Block|thread block]] level of the [[Thread Hierarchy|thread hierarchy]] in the [[CUDA (Programming Model)|CUDA programming model]]. It is generally expected to be much smaller but much faster (in throughput and latency) than the [[Global Memory|global memory]].

A fairly typical [[Kernel|kernel]] therefore looks something like this:

- load data from [[Global Memory|global memory]] into shared memory
- perform a number of arithmetic operations on that data via the [[CUDA Core|CUDA Cores]] and [[Tensor Core|Tensor Cores]]
- optionally, synchronize [[Thread|threads]] within a [[Thread Block|thread block]] by means of barriers while performing those operations
- write data back into [[Global Memory|global memory]], optionally preventing races across [[Thread Block|thread blocks]] by means of atomics

Shared memory is stored in the [[L1 Data Cache|L1 data cache]] of the GPU's [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]].

---

← [[Registers]] · [[Global Memory]] →
