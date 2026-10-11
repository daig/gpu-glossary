---
title: "What is the NVIDIA Runtime Compiler?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/nvrtc
---

# What is the NVIDIA Runtime Compiler? `nvrtc`

The NVIDIA Runtime Compiler (`nvrtc`) is a runtime compilation library for CUDA C. It compiles [[CUDA C++ (programming language)|CUDA C++]] to [[Parallel Thread eXecution|PTX]] without requiring a separate launch of the [[NVIDIA CUDA Compiler Driver]] (`nvcc`) in another process. It is used by some libraries or frameworks to, for example, map generated C/C++ code to [[Parallel Thread eXecution|PTX]] code that can run on a GPU.

Note that this [[Parallel Thread eXecution|PTX]] is then further JIT-compiled from the [[Parallel Thread eXecution|PTX]] IR to the [[Streaming ASSembler|SASS assembly]]. This is done by the [[NVIDIA GPU Drivers|NVIDIA GPU drivers]] and is distinct from the compilation done by NVRTC. CUDA binaries that contain [[Parallel Thread eXecution|PTX]], as required for forward compatibility, also pass through this compilation step.

NVRTC is closed source. You can find its documentation [here](https://docs.nvidia.com/cuda/nvrtc/index.html).

---

← [[NVIDIA CUDA Compiler Driver]] · [[NVIDIA CUDA Profiling Tools Interface]] →
