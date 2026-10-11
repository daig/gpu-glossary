---
title: "What is a Graphics/GPU Processing Cluster?"
aliases:
  - "GPC"
  - "Graphics/GPU Processing Cluster"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/graphics-processing-cluster
---

# What is a Graphics/GPU Processing Cluster? `GPC`

A GPC is a collection of [[Texture Processing Cluster|Texture Processing Clusters (TPCs)]] (themselves groups of [[Streaming Multiprocessor|Streaming Multiprocessors]] or SMs) plus a raster engine. Apparently, some people use NVIDIA GPUs for graphics, for which the raster engine is important. Relatedly, the name used to stand for Graphics Processing Cluster, but is now, e.g. in the [NVIDIA CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html), expanded as "GPU Processing Cluster".

Since the introduction of [[Compute Capability|compute capability]] 9.0 GPUs like H100s, there is an additional layer of the [[CUDA (Programming Model)|CUDA programming model]]'s [[Thread Hierarchy|thread hierarchy]], a "cluster" of [[Thread Block|thread blocks]] that are scheduled onto the same GPC, just as the threads of a [[Thread Block|thread block]] are scheduled onto the same [[Streaming Multiprocessor|SM]], and have their own level of the [[Memory Hierarchy|memory hierarchy]], distributed shared memory. Elsewhere, we elide discussion of this feature.

---

← [[Texture Processing Cluster]] · [[Register File]] →
