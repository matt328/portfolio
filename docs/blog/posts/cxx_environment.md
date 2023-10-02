---
date: 2023-10-01
categories:
  - c++
---

# C++ Development Environment

I like to work with graphics programming in my spare time, and more often than not that has required me to reach for C++. For a time, the best I could do was to lean into MS Visual C++ as heavily as I could. Recently though, as I find myself using OS X and Linux moreso than Windows, I have developed a cross platform C++ development environment.

<!-- more -->

I was going to start by saying if you search for cross platform c++ one of the first results you'd find was CMake, but verifying that just now it's not actually the case. Oh well, anyway, I've decided to use CMake. CMake abstracts away all the IDE specific settings that normally surround a C++ project and lets you declaratively describe your project. With this abstract definition, you can use CMake to then generate just about any IDE specific project files you need for your current platform.

Another thing a productive development environment has to have is dependency management. It's 2023 and I don't want to have to have a long list of prerequired software to pollute my entire system with just to develop on a single project. For this I've chosen Vcpkg, simply for the reason it has decent support, and all of the libraries I wanted to use have vcpkg packages published. With a single line:

```cmake
set(CMAKE_TOOLCHAIN_FILE ./vcpkg/scripts/buildsystems/vcpkg.cmake)
```

All of my dependencies will be installed when running CMake's generate command. This has an advantage over just vendoring dependencies with git submodules, as CMake/vcpkg will take care of building all of them as their authors intended them to be built, so that I don't spend time adjusting my own compiling rules to compile vendored code. I think this can probably be avoided somehow, but the fact that CMake/vcpkg just does it for me is a huge time saver.

For an 'IDE' I use VSCode. I also use clang, and I feel like the clangd plugins for VSCode along with clang-format and clang-tidy gives an experience that's on par with JetBrains' CLion. In fact, it might even be a bit better as all other things held equal, VSCode lacks the incredibly high CPU usage on every file save that was present with CLion when I used it.
