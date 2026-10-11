---
title: "What is a Register File?"
tags:
  - gpu-glossary
  - gpu-glossary/device-hardware
source: https://modal.com/gpu-glossary/device-hardware/register-file
---

# What is a Register File?

The register file of the [[Streaming Multiprocessor]] is the primary store of bits in between their manipulation by the [[Core|cores]].

![[terminal-gh100-sm.svg]]

*The internal architecture of an H100 SM. The register file is depicted in blue. Modified from NVIDIA's [H100 white paper](https://modal-cdn.com/gpu-glossary/gtc22-whitepaper-hopper.pdf).*

Like registers in CPUs, these registers are made from very fast memory technology that can keep pace with the compute [[Core|cores]], about an order of magnitude faster than the [[L1 Data Cache|L1 data cache]].

The register file is split into 32 bit registers that can be dynamically reallocated between different data types, like 32 bit integers, 64 bit floating point numbers, and (groups of) 16 bit or smaller floating point numbers. These physical registers back the [[Registers|virtual registers]] in the [[Parallel Thread eXecution|Parallel Thread eXecution (PTX)]] intermediate representation.

Allocation of physical registers to [[Thread|threads]] in [[Streaming ASSembler|Streaming Assembler (SASS)]] is managed by a compiler like `ptxas`, which optimizes register file usage by [[Thread Block|thread blocks]]. If each [[Thread Block|thread block]] consumes too much of the register file (colloquially, high "[[Register Pressure|register pressure]]"), then the number of concurrently schedulable [[Thread|threads]] will be reduced, leading to a low [[Occupancy|occupancy]] and possibly impacting performance by reducing opportunities for [[Latency Hiding|latency hiding]].

---

← [[Graphics-GPU Processing Cluster|Graphics/GPU Processing Cluster]] · [[L1 Data Cache]] →
