---
title: "What are the NVIDIA GPU Drivers?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/nvidia-gpu-drivers
---

# What are the NVIDIA GPU Drivers?

The NVIDIA GPU drivers mediate the interaction between host programs or the host operating system and the GPU device. The primary interfaces to the GPU drivers for applications are, in order, the [[CUDA Runtime API]] and the [[CUDA Driver API]].

![[terminal-cuda-toolkit.svg]]

*The CUDA Toolkit. The NVIDIA GPU Driver is the only component that communicates directly with the GPU. Adapted from the _Professional CUDA C Programming Guide_.*

NVIDIA has released the [source](https://github.com/NVIDIA/open-gpu-kernel-modules) for their Linux Open GPU [[nvidia.ko|Kernel Module]].

---

← [[CUDA C++ (programming language)]] · [[nvidia.ko]] →
