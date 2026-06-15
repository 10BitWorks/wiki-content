---
title: Frigate Hardware Evaluation
created: 2026-06-15
updated: 2026-06-15
type: reference
tags: cameras, infrastructure, evaluation
description: "Hardware evaluation for scaling the Frigate NVR deployment at 10BitWorks."
isPublished: true
---

This evaluation compares the current infrastructure against the goal of running many cameras with AI inference on the Frigate NVR.

## Executive Summary

The **Dell PowerEdge T330 is not recommended** for Frigate. Modern deployments favor systems with Intel QuickSync and efficient AI inference paths (OpenVINO or Coral).

## Why Skip the Dell T330?

- **No QuickSync**: Xeon E3-1200 v5/v6 CPUs rarely include integrated graphics, forcing software decode of every stream.
- **AI Bottlenecks**: Object detection requires extra hardware (Google Coral); modern consumer chips handle it on the iGPU.
- **Power Efficiency**: Higher idle draw and lower single-thread performance than modern workstations.

## Current Infrastructure vs. Goal

| Feature | Zelda (Current) | Link (Current) | Proposed Goal |
| :--- | :--- | :--- | :--- |
| CPU | Intel J4105 (4-Core) | Xeon E5-2623 v3 | Intel Core i5-12500+ |
| RAM | 8GB (Overburdened) | 94GB | 32GB+ DDR4/DDR5 |
| Video Decoding | VAAPI (Basic) | Software (Slow) | QuickSync (UHD 770) |
| Inference Path | CPU (Slow) | CPU (Slow) | OpenVINO (on iGPU) |
| Capacity | 6-8 Cameras | 10+ (high CPU) | 20-40+ Cameras |

## Recommended Paths

### Path A — Used/Refurbished Workstation (Best Value)

- Dell Precision 3660 / HP Z2 G9
- CPU: Intel Core i5-12500 or i7-12700
- Includes UHD 770 graphics for stream decode and OpenVINO inference

### Path B — Custom Build

- CPU: Intel Core i5-13500 (14 cores / 20 threads)
- Dual media engines for high video throughput
- Coral M.2 optional for high-speed facial recognition

## Recommendation

Invest in a **12th Gen or 13th Gen Intel Core-based system**. The jump to UHD 770 is the single most important factor for high-density Frigate deployments.

## Related

- [Frigate NVR](/app-services/self-hosted/frigate)
- [Cameras](/infrastructure/cameras)
