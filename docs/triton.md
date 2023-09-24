---
hide:
  - toc
---

# Triton

[https://github.com/matt328/triton](https://github.com/matt328/triton)

Triton will someday be a Vulkan game engine written in C++. It features what I consider a sane, modern C++ development environment as well as general programming patterns I tend to reach for regardless of which ecosystem I find myself in.

The goals of the project are to create a maintainable and easy to modify graphics engine using Vulkan, modern C++, and also provide a consistent development experience on Windows, Linux, and OS X.

Being that this is a hobby project, and I have free reign to select my tools, a few of the major ones are listed here.

- CMake - for cross platform C++ projects, CMake abstracts a lot of tedious platform specific configuration.
- Vcpkg - a requirement of any 'modern' toolkit in my opinion is a proper dependency management system that enables you to declaratively specify dependencies and automate their download and installation. Vcpkg ties in nicely with CMake as well. The goal here is to be able to clone a project, run a few commands and be up and running with as little prerequisite configuration steps as possible. The only requirements that should need to be installed are CMake itself, and a sane clang environment, with CC and CXX env vars set appropriately.
- clang and lldb - I don't know why, but I tried 3 of the compiler toolchains, and found clang and lldb the nicest to use. MSVC is good, but Linux and OS X support is not great. I found gcc to have many rough edges, and also just overall felt rather antiquated.
- VSCode - It's a bit of a pain to get configured, but clangd provides a great C++ experience, on par I'd say with Visual Studio. Also provides a consistent experience on Linux and OS X.
- Vulkan_hpp and the RAII headers - With modern C++, I don't enjoy chasing memory leaks, so I prefer to lean into RAII concepts as much as possible. The Vulkan RAII headers wrap the C++ OO classes into classes that support tearing down resources automatically when their destructors are called, so in most cases you can simply toss Vulkan resources such as `vk::raii::Device` into unique or shared pointers and they'll be cleaned up automatically. A lot of tutorials I've followed devote a lot of resources and mental cycles to maintaining lists of things that need to be destroyed, and ensuring they are destroyed at the right times in the right order, and RAII helps avoid that entire class of issues. As a sidenote about this is that variables will go out of scope in reverse order of their declaration, and I feel keeping this in mind when you need things to be destroyed in a certain order is much easier to reason about than having to track and destroy things manually.
- Vulkan Memory Allocator - Because I am just not _that_ into memory management. In fact I am so not into memory management, I've started to develop a thin RAII wrapper around vma to handle automatically releasing memory, and for my rudimentary needs so far, it seems to work well.
