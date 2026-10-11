---
title: "What is the NVIDIA CUDA Profiling Tools Interface?"
aliases:
  - "CUPTI"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/cupti
---

# What is the NVIDIA CUDA Profiling Tools Interface? `CUPTI`

The NVIDIA CUDA Profiling Tools Interface (CUPTI) provides a set of APIs for profiling execution of [[CUDA C++ (programming language)|CUDA C++]], [[Parallel Thread eXecution|PTX]], and [[Streaming ASSembler|SASS]] code on GPUs. Critically, it synchronizes timestamps across the CPU host and the GPU device.

CUPTI's interfaces are consumed by, for example, the [[NVIDIA Nsight Systems|NSight Systems Profiler]] and the [PyTorch Profiler](https://modal.com/docs/examples/torch_profiling).

You can find its documentation [here](https://docs.nvidia.com/cupti/).

For details on using profiling tools for GPU applications running on Modal, see [this example from our documentation](https://modal.com/docs/examples/torch_profiling).

---

← [[NVIDIA Runtime Compiler]] · [[NVIDIA Nsight Systems]] →
