---
title: "What is the NVIDIA CUDA Compiler Driver?"
aliases:
  - "nvcc"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/nvcc
---

# What is the NVIDIA CUDA Compiler Driver? `nvcc`

The NVIDIA CUDA Compiler Driver is a toolchain for compiling [[CUDA C++ (programming language)|CUDA C/C++]] programs. It outputs binary executables that conform to the host ABI and include [[Parallel Thread eXecution|PTX]] and/or [[Streaming ASSembler|SASS]] to be executed on the GPU — a so-called "fat binary". These binaries are inspectable with the same tools used for other binaries, like `readelf` on Linux, but can be additionally manipulated with the specialized [[CUDA Binary Utilities]].

The included [[Parallel Thread eXecution|PTX]] code is versioned by [[Compute Capability]], configured by passing `compute_XYz` values to the `--gpu-architecture` or `--gpu-code` options.

The included [[Streaming ASSembler|SASS]] code is versioned by [[Streaming Multiprocessor Architecture|SM architecture version]], configured by passing `sm_XYz` values to the `--gpu-architecture` or `--gpu-code` options. Passing `compute_XYz` to `--gpu-code` will also trigger the generation of [[Streaming ASSembler|SASS]] code with the same version as the [[Parallel Thread eXecution|PTX]].

Compilation of host/CPU code is done using the host system's compiler driver, e.g. the `gcc` compiler driver. Note that compiler drivers are not to be confused with hardware drivers, like the [[NVIDIA GPU Drivers]].

The documentation for `nvcc` can be found [here](https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/).

---

← [[CUDA Graphs]] · [[NVIDIA Runtime Compiler]] →
