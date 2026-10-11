---
title: "What is Compute Capability?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/compute-capability
---

# What is Compute Capability?

Instructions in the [[Parallel Thread eXecution|Parallel Thread Execution]] instruction set are compatible with only certain physical GPUs. The versioning system used to abstract away details of physical GPUs from the instruction set and [[NVIDIA CUDA Compiler Driver|compiler]] is called "Compute Capability".

Most compute capability version numbers have two components: a major version and a minor version. NVIDIA promises forward compatibility (old [[Parallel Thread eXecution|PTX]] code runs on new GPUs) across both major and minor versions following the [onion layer](https://docs.nvidia.com/cuda/parallel-thread-execution/#ptx-module-directives-target) model.

With Hopper, NVIDIA introduced an additional version suffix, the `a` in `9.0a`, which includes features that deviate from the onion model: their future compatibility is not guaranteed, even within major versions.

With Blackwell, NVIDIA introduced yet another version suffix, the `f` in `10.0f`, which also deviates from the onion model, and is closer to [SemVer](https://semver.org/): compatibility is guaranteed across minor versions but not major versions.

Target compute capabilities for [[Parallel Thread eXecution|PTX]] compilation can be specified when invoking `nvcc`, the [[NVIDIA CUDA Compiler Driver]]. By default, the compiler will also generate optimized [[Streaming ASSembler|SASS]] for the matching [[Streaming Multiprocessor Architecture|Streaming Multiprocessor (SM) architecture]]. The [documentation](https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/index.html#virtual-architectures) for [`nvcc`](<../Host Software/NVIDIA CUDA Compiler Driver.md>) refers to compute capability as a "virtual GPU architecture", in contrast to the "physical GPU architecture" expressed by the [[Streaming Multiprocessor|SM]] version.

The technical specifications for each compute capability version can be found in the [Compute Capability section of the NVIDIA CUDA C Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html).

---

← [[Parallel Thread eXecution]] · [[Thread]] →
