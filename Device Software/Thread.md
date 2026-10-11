---
title: "What is a CUDA Thread?"
tags:
  - gpu-glossary
  - gpu-glossary/device-software
source: https://modal.com/gpu-glossary/device-software/thread
---

# What is a CUDA Thread?

![[terminal-cuda-programming-model.svg]]

*Threads are the lowest level of the thread group hierarchy (top, left) and are mapped onto the [[Core|cores]] of a [[Streaming Multiprocessor]]. Modified from diagrams in NVIDIA's [CUDA Refresher: The CUDA Programming Model](https://developer.nvidia.com/blog/cuda-refresher-cuda-programming-model/) and the NVIDIA [CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#programming-model).*

A *thread of execution* (or "thread" for short) is the lowest unit of programming for GPUs, the base and atom of the [[CUDA (Programming Model)|CUDA programming model]]'s [[Thread Hierarchy|thread hierarchy]]. A thread has its own [[Registers|registers]], but little else.

Both [[Streaming ASSembler|SASS]] and [[Parallel Thread eXecution|PTX]] programs target threads. Compare this to a typical C program in a POSIX environment, which targets a process, itself a collection of one or more threads. Unlike POSIX threads, [[CUDA (Programming Model)|CUDA]] threads are not used to make syscalls.

Like a thread on a CPU, a GPU thread can have a private instruction pointer/program counter. However, for performance reasons, GPU programs are generally written so that all the threads in a [[Warp|warp]] share the same instruction pointer, executing instructions in lock-step (see also [[Warp Scheduler]]).

Also like threads on CPUs, GPU threads have stacks in [[GPU RAM|global memory]] for storing spilled registers and a function call stack, but high-performance [[Kernel|kernels]] generally limit use of both.

A single [[CUDA Core]] executes instructions from a single thread.

---

← [[Compute Capability]] · [[Warp]] →
