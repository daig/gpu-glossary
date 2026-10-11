---
title: "What is cuDNN?"
tags:
  - gpu-glossary
  - gpu-glossary/host-software
source: https://modal.com/gpu-glossary/host-software/cudnn
---

# What is cuDNN?

NVIDIA's cuDNN (CUDA Deep Neural Network) is a library of primitives for building GPU-accelerated deep neural networks.

cuDNN provides highly optimized [[Kernel|kernels]] for operations arising frequently in neural networks. These include convolution, self-attention (including scaled dot-product attention, aka "Flash Attention"), matrix multiplication, various normalizations, poolings, etc.

cuDNN is a key library at the application layer of the [[CUDA (Software Platform)|CUDA software platform]], alongside its sibling library, [[cuBLAS]]. Deep learning frameworks like PyTorch typically leverage [[cuBLAS]] for general-purpose linear algebra, such as the matrix multiplications that form the core of dense (fully-connected) layers. They rely on cuDNN for more specialized primitives like convolutional layers, normalization routines, and attention mechanisms.

In modern cuDNN code, computations are expressed as operation graphs, which can be constructed using open source [Python and C++ frontend APIs](https://docs.nvidia.com/deeplearning/cudnn/frontend/latest/developer/overview.html) via the declarative [Graph API](https://docs.nvidia.com/deeplearning/cudnn/frontend/v1.14.0/developer/graph-api.html) (not to be confused with [[CUDA Graphs]]).

This API allows the developer to define a sequence of operations as a graph, which cuDNN can then analyze to perform optimizations, most importantly operation fusion. In operation fusion, a sequence of operations like Convolution + Bias + ReLU are merged ("fused") into a single operation run as a single [[Kernel|kernel]]. Operation fusion helps reduce demand on [[Memory Bandwidth|memory bandwidth]] by keeping program intermediates in [[Shared Memory|shared memory]] throughout a sequence of operations.

The frontends interact with a lower-level, closed source [C backend](https://docs.nvidia.com/deeplearning/cudnn/backend/latest/api/overview.html), which exposes an API for legacy use cases or direct C FFI.

For any given operation, cuDNN maintains multiple underlying implementations and uses (unknown) internal heuristics to select the most performant one for the target [[Streaming Multiprocessor Architecture|Streaming Multiprocessor (SM) architecture]], data types, and input sizes.

cuDNN's initial claim to fame was accelerating convolutional neural networks on Ampere [[Streaming Multiprocessor Architecture|SM architecture]] GPUs. For Transformer neural networks on Hopper and especially Blackwell [[Streaming Multiprocessor Architecture|SM architectures]], NVIDIA has tended to place more emphasis on the [[CUTLASS]] library.

For more information on cuDNN, see the [official cuDNN documentation](https://docs.nvidia.com/deeplearning/cudnn/), and the [open source frontend APIs](https://github.com/NVIDIA/cudnn-frontend).

---

← [[cuBLAS]] · [[CUTLASS]] →
