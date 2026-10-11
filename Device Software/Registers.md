---
title: "What are Registers?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/registers
---

# What are Registers?

![[terminal-cuda-programming-model.svg]]

*Registers are the memory of the [[Memory Hierarchy|memory hierarchy]] associated with individual [[Thread|threads]] (left). Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

At the lowest level of the [[Memory Hierarchy|memory hierarchy]] are the registers, which store information manipulated by a single [[Thread|thread]].

The values in registers are generally stored in the [[Register File|register file]] of the [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]], but they can also spill to the [[Global Memory|global memory]] in the [[GPU RAM]] at a substantial performance penalty.

As when programming CPUs, these registers are not directly manipulated by high-level languages like [[CUDA C++ (programming language)|CUDA C]]. They are only visible to a lower-level language, here [[Parallel Thread eXecution|Parallel Thread Execution (PTX)]]. They are typically managed by a compiler like `ptxas`. Among the compiler's goals is to limit the register space used by each [[Thread|thread]] so that more [[Thread Block|thread blocks]] can be simultaneously scheduled into a single [[Streaming Multiprocessor|SM]], increasing [[Occupancy|occupancy]].

The registers used in the [[Parallel Thread eXecution|PTX]] instruction set architecture are documented [here](https://docs.nvidia.com/cuda/parallel-thread-execution/#register-state-space). The registers used in [[Streaming ASSembler|SASS]] are not, to our knowledge, documented.

---

← [[Memory Hierarchy]] · [[Shared Memory]] →
