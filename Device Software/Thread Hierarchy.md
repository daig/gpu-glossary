---
title: "What is the CUDA Thread Hierarchy?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/thread-hierarchy
---

# What is the CUDA Thread Hierarchy?

![[terminal-cuda-programming-model.svg]]

*The thread hierarchy of the [[CUDA (Programming Model)|CUDA programming model]] spans from individual [[Thread|threads]] to [[Thread Block|thread blocks]] to [[Thread Block Grid|thread block grids]] (left), mapping onto the hardware from [[CUDA Core|CUDA Cores]] to [[Streaming Multiprocessor|Streaming Multiprocessors]] to the entire GPU (right). Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

The thread hierarchy is a key abstraction of the [[CUDA (Programming Model)|CUDA programming model]], alongside the [[Memory Hierarchy|memory hierarchy]]. It organizes the execution of parallel programs across multiple levels, from individual threads up to entire GPU devices.

At the lowest level are individual [[Thread|threads]]. Like a thread of execution on a CPU, each [[Thread|CUDA thread]] executes a stream of instructions. The hardware resources that effect arithmetic and logic instructions are called [[Core|cores]] or sometimes "pipes". Threads are selected for execution by the [[Warp Scheduler]].

The intermediate level consists of [[Thread Block|thread blocks]], which are also known as [[Cooperative Thread Array|cooperative thread arrays]] in [[Parallel Thread eXecution|PTX]] and [[Streaming ASSembler|SASS]]. Each [[Thread|thread]] has a unique identifier within its [[Thread Block|thread block]]. These thread identifiers are index-based, to support easy assignment of work to threads based on indices into input or output arrays. All threads within a block are scheduled simultaneously onto the same [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]]. They can coordinate through [[Shared Memory|shared memory]] and synchronize with barriers.

At the highest level, multiple [[Thread Block|thread blocks]] are organized into a [[Thread Block Grid|thread block grid]] that spans the entire GPU. [[Thread Block|Thread blocks]] are strictly limited in their coordination and communication. Blocks within a grid execute concurrently with respect to each other, with no guaranteed execution order. [[CUDA (Programming Model)|CUDA programs]] must be written so that any interleaving of blocks is valid, from fully serial to fully parallel. That means [[Thread Block|thread blocks]] cannot, for instance, synchronize with barriers. Like [[Thread|threads]], each [[Thread Block|thread block]] has a unique, index-based identifier to support assignment of work based on array index.

This hierarchy maps directly onto the [[Device Hardware|GPU hardware]]: [[Thread|threads]] execute on individual [[Core|cores]], [[Thread Block|thread blocks]] are scheduled onto [[Streaming Multiprocessor|SMs]], and [[Thread Block Grid|grids]] utilize all available [[Streaming Multiprocessor|SMs]] on the device.

---

← [[Thread Block Grid]] · [[Memory Hierarchy]] →
