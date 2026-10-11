---
title: "What is a Thread Block Grid?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/thread-block-grid
---

# What is a Thread Block Grid?

![[terminal-cuda-programming-model.svg]]

*Thread block grids are the highest level of the thread group hierarchy of the [[CUDA (Programming Model)|CUDA programming model]] (left). They map onto multiple [[Streaming Multiprocessor|Streaming Multiprocessors]] (right, bottom). Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

When a CUDA [[Kernel|kernel]] is launched, it creates a collection of [[Thread|threads]] known as a thread block grid. Grids can be one, two, or three dimensional. They are made up of [[Thread Block|thread blocks]].

The matching level of the [[Memory Hierarchy|memory hierarchy]] is the [[Global Memory|global memory]].

[[Thread Block|Thread blocks]] are effectively independent units of computation. They execute concurrently, that is, with indeterminate order, ranging from fully sequentially in the case of a GPU with a single [[Streaming Multiprocessor]] to fully in parallel when run on a GPU with sufficient resources to run them all simultaneously.

---

← [[Thread Block]] · [[Thread Hierarchy]] →
