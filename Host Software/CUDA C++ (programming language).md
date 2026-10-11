---
title: "What is the CUDA C++ programming language?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/cuda-c
---

# What is the CUDA C++ programming language?

CUDA C++ is an implementation of the [[CUDA (Programming Model)|CUDA programming model]] as an extension of the C++ programming language.

CUDA C++ adds several features to C++ to implement the [[CUDA (Programming Model)|CUDA programming model]], including:

- **[[Kernel]] definition** with **`__global__`**. CUDA [[Kernel|kernels]] are implemented as C++ functions that take in pointers and have return type `void`, annotated with this keyword.
- **[[Kernel]] launches** with **`<<<>>>`**. [[Kernel|Kernels]] are executed from the CPU host using a triple bracket syntax that sets the [[Thread Block Grid|thread block grid]] dimensions.
- **[[Shared Memory|Shared memory]] allocation** with the `shared` keyword, **barrier synchronization** with the `__syncthreads()` intrinsic function, and **[[Thread Block|thread block]]** and **[[Thread|thread]] indexing** with the `blockDim` and `threadIdx` built-in variables.

CUDA C++ programs are compiled by a combination of host C/C++ compiler drivers like `gcc` and the [[NVIDIA CUDA Compiler Driver]], `nvcc`.

For information on how to use CUDA C++ on [Modal](https://modal.com), see [this guide](https://modal.com/docs/guide/cuda).

---

← [[CUDA (Software Platform)]] · [[NVIDIA GPU Drivers]] →
