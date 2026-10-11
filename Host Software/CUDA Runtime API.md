---
title: "What is the CUDA Runtime API?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/cuda-runtime-api
---

# What is the CUDA Runtime API?

The CUDA Runtime API wraps the [[CUDA Driver API]] and provides a higher-level API for the same functions.

![[terminal-cuda-toolkit.svg]]

*The CUDA Toolkit. The CUDA Runtime API wraps the CUDA Driver API to make it more amenable to application programming. Adapted from the _Professional CUDA C Programming Guide_.*

It is generally preferred over the [[CUDA Driver API|Driver API]] for better ergonomics, but there are some small caveats around control of kernel launches and context management. See [this section](https://docs.nvidia.com/cuda/cuda-runtime-api/driver-vs-runtime-api.html#driver-vs-runtime-api) of the CUDA Runtime API docs for more.

While the Runtime API may be statically linked, per [Attachment A of the NVIDIA CUDA Toolkit EULA](https://docs.nvidia.com/cuda/eula/index.html#attachment-a), it does not have to be. The shared object file for dynamic linking is usually named [[libcudart.so]] on Linux systems.

The CUDA Runtime API is closed source. You can find its documentation [here](https://docs.nvidia.com/cuda/cuda-runtime-api/index.html).

---

[[nvidia-smi]] → · [[libcudart.so]] →
