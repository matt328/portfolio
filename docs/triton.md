---
hide:
  - toc
---

# Triton

[https://github.com/matt328/triton](https://github.com/matt328/triton)

Triton — a personal C++23/Vulkan 3D engine I built over several years. It bundles modular libraries (graphics-vk, voxel-terrain, asset-forge) and example apps, uses modern CMake presets, Catch2 tests, and aimed to explore ECS, multithreaded streaming, and a transvoxel terrain system.

Honest take: many pragmatic shortcuts (overused DI, “component soup”, rough threading around resource loading, and platform trade-offs like abandoning macOS) made the code brittle. I learned architecture discipline, safer concurrency, and better dependency management.
