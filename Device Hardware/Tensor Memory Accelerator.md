---
title: "What is a Tensor Memory Accelerator?"
aliases:
  - "TMA"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/tensor-memory-accelerator
---

# What is a Tensor Memory Accelerator? `TMA`

Tensor Memory Accelerators are specialized hardware in Hopper and Blackwell [[Streaming Multiprocessor Architecture|architecture]] GPUs designed to accelerate access to multi-dimensional arrays in [[GPU RAM]].

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 [[Streaming Multiprocessor|Streaming Multiprocessor (SM)]]. Note the Tensor Memory Accelerator at the bottom of the [[Streaming Multiprocessor|SM]], shared between the four sub-units. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

The TMA loads data from [[Global Memory|global memory]]/[[GPU RAM]] to [[Shared Memory|shared memory]]/[[L1 Data Cache|L1 data cache]], bypassing the [[Registers|registers]]/[[Register File|register file]] entirely.

The first advantage of the TMA comes from reducing the use of other compute and memory resources. The TMA hardware calculates addresses for bulk affine memory accesses, i.e. accesses of the form `addr = width * base + offset` for many bases and offsets concurrently, which are the most common accesses for arrays. Offloading this work to the TMA saves space in the [[Register File|register file]], reducing "[[Register Pressure|register pressure]]", and reduces demand on the [[Arithmetic Bandwidth|arithmetic bandwidth]] provided by the [[CUDA Core|CUDA Cores]]. The savings are more pronounced for large (KB-scale) accesses to arrays with two or more dimensions.

The second advantage comes from the asynchronous execution model of TMA copies. A single [[Thread|CUDA thread]] can trigger a large copy and then rejoin its [[Warp|warp]] to perform other work. Those [[Thread|threads]] and others in the same [[Thread Block|thread block]] can then asynchronously detect the completion of the TMA copy after it finishes and operate on the results (as in a producer-consumer model).

For details, see the TMA sections of [Luo et al.'s Hopper micro-benchmarking paper](https://arxiv.org/abs/2501.12084v1) and the [NVIDIA Hopper Tuning Guide](https://docs.nvidia.com/cuda/hopper-tuning-guide/index.html#tensor-memory-accelerator).

Note that, despite the name, the Tensor Memory Accelerator does not accelerate operations using [[Tensor Memory]].

---

← [[Tensor Core]] · [[Streaming Multiprocessor Architecture]] →
