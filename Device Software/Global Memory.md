---
title: "What is Global Memory?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/global-memory
---

# What is Global Memory?

![[terminal-cuda-programming-model.svg]]

*Global memory is the highest level of the [[Memory Hierarchy|memory hierarchy]] in the [[CUDA (Programming Model)|CUDA programming model]]. It is stored in the [[GPU RAM]]. Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

As part of the [[CUDA (Programming Model)|CUDA programming model]], each level of the [[Thread Hierarchy|thread hierarchy]] has access to matching memory from the [[Memory Hierarchy|memory hierarchy]]. This memory can be used for coordination and communication and is managed by the programmer (not the hardware or a runtime).

The highest level of that memory hierarchy is the global memory. Global memory is global in its scope and its lifetime. That is, it is accessible by every [[Thread|thread]] in a [[Thread Block Grid|thread block grid]] and its lifetime is as long as the execution of the program.

Access to data structures in the global memory can be synchronized across all accessors using atomic instructions, as with CPU memory. Within a [[Cooperative Thread Array|cooperative thread array]], access can be more tightly synchronized, e.g. with barriers.

This level of the [[Memory Hierarchy|memory hierarchy]] is typically implemented in the [[GPU RAM|GPU's RAM]] and allocated from the host using a memory allocator provided by the [[CUDA Driver API]] or the [[CUDA Runtime API]].

The terminology "global" unfortunately collides with the `__global__` keyword in [[CUDA C++ (programming language)|CUDA C/C++]], which annotates functions that are launched on the host but run on the device ([[Kernel|kernels]]), whereas global memory is only on the device. Early CUDA architect Nicholas Wilt wrily notes that this choice was made "for maximum developer confusion" in his [*CUDA Handbook*](https://www.cudahandbook.com/).

---

← [[Shared Memory]] · [[CUDA Tile Programming Model]] →
