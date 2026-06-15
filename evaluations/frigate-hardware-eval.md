---
title: Frigate & AI Inference Hardware
created: 2026-06-14
updated: 2026-06-14
type: concept
tags: operations, proxmox, servers
description: "Hardware evaluation and recommendations for scaling Frigate AI inference."
isPublished: true
---

Based on the 10BitWorks infrastructure analysis, scaling to high-density camera deployments with AI inference requires specific hardware architectures.

## The Dell T330 Constraint
The Dell PowerEdge T330 (and similar older Xeon E3-1200 v5/v6 systems) is **not recommended** for Frigate:
*   **Lack of QuickSync**: These server-grade chips lack the integrated graphics required for Intel QuickSync, forcing the CPU to decode every video stream in software.
*   **AI Bottlenecks**: Object detection requires additional hardware (Google Coral), whereas modern consumer chips can perform this natively via OpenVINO on their iGPU.
*   **Power Efficiency**: Older enterprise hardware has high idle power consumption and low single-thread performance compared to modern consumer-grade workstations.

## Recommended Architectures
For a 20-40+ camera deployment, **12th Gen or 13th Gen Intel Core-based systems** are the ideal targets. The move to the UHD 770 iGPU in the 12th generation is critical for high-density deployments.

### Path A: Used/Refurbished Workstation (Value)
*   **Model**: Dell Precision 3660 / HP Z2 G9
*   **CPU**: Intel Core i5-12500 or i7-12700.
*   **Capabilities**: The UHD 770 graphics can decode dozens of streams and run AI detection (via OpenVINO) simultaneously.

### Path B: Dedicated Custom Build
*   **CPU**: Intel Core i5-13500 (14 Cores / 20 Threads)
*   **Capabilities**: Features dual media engines for massive video throughput. Can be paired with a Coral M.2 for extreme-speed facial recognition, though the iGPU handles standard object tracking effortlessly.

