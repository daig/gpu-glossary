---
title: "What is the CUDA Software Platform?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/cuda-software-platform
---

# What is the CUDA Software Platform?

The CUDA software platform is a collection of software for developing CUDA programs.

CUDA stands for *Compute Unified Device Architecture*. Depending on the context, "CUDA" can refer to multiple distinct things: a [[CUDA (Device Architecture)|high-level device architecture]], a [[CUDA (Programming Model)|parallel programming model for architectures with that design]], or a software platform that extends high-level languages like C to add that programming model.

The vision for CUDA is laid out in the [Lindholm et al., 2008](https://www.cs.cmu.edu/afs/cs/academic/class/15869-f11/www/readings/lindholm08_tesla.pdf) white paper. We highly recommend this paper, which is the original source for many claims, diagrams, and even specific turns of phrase in NVIDIA's documentation.

Here, we focus on the CUDA *software platform*. Though CUDA software platforms exist for other languages, like FORTRAN, Python, and [[cuTile BASIC|BASIC]], we will focus on the dominant [[CUDA C++ (programming language)|CUDA C++]] version.

This platform can be roughly divided into the components used to *build* applications, like the [[NVIDIA CUDA Compiler Driver]] toolchain, and the components used *within* or *from* applications, like the [[CUDA Driver API]] and the [[CUDA Runtime API]], diagrammed below.

![[terminal-cuda-toolkit.svg]]

*The CUDA Toolkit. Adapted from the _Professional CUDA C Programming Guide_.*

Built on top of these APIs are libraries of high-performance [[Kernel|kernels]] for general and specific domains, like [[cuBLAS]] for linear algebra and [[cuDNN]] for deep neural networks and tools for composing such kernels yourself, like [[CUTLASS]] and [[CuTe DSL]].

---

← [[Host Software]] · [[CUDA C++ (programming language)]] →
