---
title: "What is the NVIDIA Management Library?"
aliases:
  - "NVML"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/nvml
---

# What is the NVIDIA Management Library? `NVML`

The NVIDIA Management Library (NVML) is used for monitoring and managing the state of NVIDIA GPUs. It exposes, for example, the power draw and temperature of the GPU, the allocated memory, and the device's power limit and power limiting state. For details on these metrics, including how to interpret power and thermal readings, see [this page on the Modal docs](https://modal.com/docs/guide/gpu-metrics).

The functions of NVML are frequently accessed via the [[nvidia-smi]] command line utility, but are also accessible to programs via wrappers, like [pynvml in Python](https://pypi.org/project/pynvml/) and [nvml\_wrapper in Rust](https://docs.rs/nvml-wrapper/latest/nvml_wrapper/).

---

← [[libcuda.so]] · [[libnvml.so]] →
