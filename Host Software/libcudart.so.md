---
title: "What is libcudart.so?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/libcudart
---

# What is libcudart.so?

The typical name for the binary shared object file that implements the [[CUDA Runtime API]] on Linux systems. Deployed CUDA binaries often statically link this file, but libraries and frameworks built on the CUDA Toolkit, like PyTorch, typically load it dynamically.

---

← [[CUDA Runtime API]] · [[CUDA Graphs]] →
