---
title: "What is the CUDA Tile programming model?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/cuda-tile-programming-model
---

# What is the CUDA Tile programming model?

The CUDA Tile programming model is a tile-based programming model targeting NVIDIA GPUs.

The traditional [[CUDA (Programming Model)|CUDA programming model]] exposes a [[Thread Hierarchy|hierarchy of threads]] and a [[Memory Hierarchy|hierarchy of memories]] to user programs that receive pointers and execute concurrently to mutate memory relative to those pointers. The same instructions are issued to multiple [[Thread|threads]] in parallel, and so this programming model is a "single-instruction, multiple thread" (SIMT) programming model. This is the programming model used in, for instance, [[CUDA C++ (programming language)|CUDA C/C++]] and the [[Parallel Thread eXecution|PTX]] IR used by pre-CUDA-Tile programs targeting NVIDIA GPUs.

This programming model is defined for a [[CUDA (Device Architecture)|"unified" hardware substrate]] -- the "U" in "CUDA". That is, homogenous [[Streaming Multiprocessor|Streaming Multiprocessors (SMs)]] with homogenous [[CUDA Core|CUDA Cores]] implement the majority of operations, rather than the device comprising specialized cores, programmed heterogenously, as was generically the case in graphics programming before CUDA.

This programming model is a poor fit for GPUs of the latest [[Streaming Multiprocessor Architecture|SM architectures]], where the vast majority of [[Arithmetic Bandwidth|arithmetic bandwidth]] is in the [[Tensor Core|Tensor Cores]]. The Tensor Cores can only perform matrix multiplications and must be programmed with [[Thread|thread]]-level instructions and asynchrony, rather than the [[Warp|warp]]-level asynchrony used to program the rest of the hardware.

In the CUDA Tile programming model, programs are expressed at the level of *tile-kernels*, which are instances of the program that run concurrently across a grid of *tile blocks*, each of which is a single thread of execution. Tile-kernels operate, in the happy path, on *structured pointers*, which combine a pointer with information about an array: its total extent (shape) and its access patterns (stride). Note the similarity to the [[CuTe]] type system for `Layout`s and `Tensor`s.

As with traditional "CUDA SIMT" in CUDA C/C++ and PTX IR, this programming model is shared between high-level languages and an intermediate representation -- here, [Tile IR](https://docs.nvidia.com/cuda/tile-ir/latest/sections/prog_model.html).

At time of writing in mid-2026, the CUDA Tile programming model is new, and to what extent it will replace the existing "CUDA SIMT" programming model is as yet unclear. The CUDA Tile programming model is currently available via [cuTile Python](https://docs.nvidia.com/cuda/cutile-python/quickstart.html). It is also available, albeit in experimental form, via [[cuTile BASIC]] and [cuTile Rust](https://github.com/nvlabs/cutile-rs).

---

← [[Global Memory]] · [[Host Software]] →
