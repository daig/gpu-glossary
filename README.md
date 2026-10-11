---
title: "README"
tags:
  - gpu-glossary
source: https://modal.com/gpu-glossary/readme
---

# README

```
 ██████╗ ██████╗ ██╗   ██╗
██╔════╝ ██╔══██╗██║   ██║
██║  ███╗██████╔╝██║   ██║
██║   ██║██╔═══╝ ██║   ██║
╚██████╔╝██║     ╚██████╔╝
 ╚═════╝ ╚═╝      ╚═════╝
 ██████╗ ██╗      ██████╗ ███████╗███████╗ █████╗ ██████╗ ██╗   ██╗
██╔════╝ ██║     ██╔═══██╗██╔════╝██╔════╝██╔══██╗██╔══██╗╚██╗ ██╔╝
██║  ███╗██║     ██║   ██║███████╗███████╗███████║██████╔╝ ╚████╔╝
██║   ██║██║     ██║   ██║╚════██║╚════██║██╔══██║██╔══██╗  ╚██╔╝
╚██████╔╝███████╗╚██████╔╝███████║███████║██║  ██║██║  ██║   ██║
 ╚═════╝ ╚══════╝ ╚═════╝ ╚══════╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝
 
```

We wrote this glossary to solve a problem we ran into working with GPUs here at [Modal](https://modal.com/): the documentation is fragmented, making it difficult to connect concepts at different levels of the stack, like [[Streaming Multiprocessor Architecture]], [[Compute Capability]], and [[Host Software|nvcc compiler flags]].

So we've read the [PDFs from NVIDIA](https://docs.nvidia.com/cuda/pdf/PTX_Writers_Guide_To_Interoperability.pdf), lurked in the [good Discords](https://discord.gg/gpumode), and even bought [dead-tree textbooks](https://www.amazon.com/Professional-CUDA-Programming-John-Cheng/dp/1118739329) to put together a glossary that spans the whole stack in one place.

This glossary, unlike a PDF or a Discord or a book, is a *hypertext document* -- all pages are inter-linked with one another, so you can jump down to read about the [[Warp Scheduler]] so you can better understand the [[Thread|threads]] that you came across in the article on the [[CUDA C++ (programming language)|CUDA programming model]].

You can also read it linearly. To navigate between pages, use the arrow keys, the arrows at the bottom of each page, or the table of contents (in the sidebar on desktop or in the hamburger menu on mobile).

The source for the glossary is available [on GitHub](https://github.com/modal-labs/gpu-glossary).

---

← [[GPU Glossary|Home]] · [[Device Hardware]] →
