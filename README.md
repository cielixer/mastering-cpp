# mastering-cpp

From C++ Programmer → C++ System / Engine Engineer

## Overview

> Goal: Become an engineer who can design and implement high-performance systems.

This is my personal study roadmap focused on systems, performance, and
toolchains (not just C++ syntax).

_Note: I organized this while chatting with ChatGPT 5.2, so mistakes may
exist. I will keep correcting and refining it as I study._

### Phases

1. Memory · CPU · Parallelism
2. Modern C++ & Type System
3. Compiler · ABI · Linker
4. OS Interface · Runtime
5. Performance & Real Engine

### How I use this

* For each phase: `Reading → Topics → Practice`
* I finish a small “minimum set” of resources before branching out
* I treat this README as a living document and update it continuously

## 🧠 Phase 1 — Memory · CPU · Parallelism

### 📚 Core Reading

* Computer Systems: A Programmer’s Perspective
* What Every Programmer Should Know About Memory (Ulrich Drepper)
* Chandler Carruth CppCon: “Efficiency with Algorithms, Performance with Data Structures”
* System Performance: Enterprise and the Cloud — Brendan Gregg
* The Art of Multiprocessor Programming — Maurice Herlihy & Nir Shavit
* Agner Fog’s Optimization Manual — Agner Fog

### 🧩 Topics

* Cache hierarchy, NUMA, TLB
* Virtual memory, page faults
* CPU pipeline & branch prediction
* SIMD, vectorization
* AoS vs SoA
* Cache line alignment
* Prefetching
* False sharing (cause/reproduce/fix)
* Memory pool & arena design
* Object layout & lifetime
* Low-level concurrency primitives (atomics, fences, barriers)

### 🧵 CPU Parallelism

* Intel TBB
* Task graph
* Work-stealing scheduler
* Cache-friendly partitioning
* OpenMP (performance experiments only)

### ✅ Practice

* Build a tiny benchmark harness (timer, warm-up, iterations, stats)
* Microbench `AoS vs SoA` and analyze with perf/VTune/`perf stat`
* Reproduce false sharing, then fix via padding/partitioning

## 🧩 Phase 2 — Modern C++ & Type System

### 📚 Core Reading

* Effective Modern C++ — Scott Meyers
* C++ Templates: The Complete Guide — Vandevoorde et al.
* The C++ Programming Language — Bjarne Stroustrup
* Herb Sutter: “How Not To Write C++ Interfaces”
* Modern C++ Design — Andrei Alexandrescu
* C++17 The Complete Guide — Nicolai Josuttis
* C++ High Performance, Second Edition — Björn Andrist & Viktor Sehr

### 🧪 Topics

* Concepts, constexpr, ranges
* Metaprogramming
* Type erasure
* Custom allocators
* ABI-stable interface design (rules/constraints)
* Pimpl & handle-based design
* Symbol visibility control
* Versioning strategies
* Binary compatibility

### ✅ Practice

* Design copy-free APIs with `std::span`/`std::string_view`
* Prototype a type-erased plugin API (e.g., logger/metrics sink)
* Compare build times and binary size before/after Pimpl

## 🧬 Phase 3 — Compiler · ABI · Linker

### 📚 Core Reading

* Engineering a Compiler — Cooper & Torczon
* Itanium C++ ABI documentation
* LLVM Project Official Documentation — [llvm.org/docs](https://llvm.org/docs)
* Clang Static Analyzer — [clang-analyzer.llvm.org](https://clang-analyzer.llvm.org)

### 🧪 Topics

* Clang AST & LLVM IR
* Optimization passes
* Name mangling
* ELF / PE structure
* Static vs dynamic linking
* CMake toolchain files
* Cross compilation
* LTO / PGO
* Reproducible builds
* Packaging (CPack, Conan, vcpkg)
* CI/CD for C++

### ✅ Practice

* Create a small ABI-sensitive library and apply `-fvisibility=hidden` + export macros
* Build static vs shared and compare symbols via `nm`/`objdump`
* Measure performance vs build-time tradeoffs with LTO/PGO

## 🧠 Phase 4 — OS Interface · Runtime

### 📚 Core Reading

* Linux System Programming — Robert Love
* Advanced Programming in the UNIX Environment
* Beej’s Guide to Network Programming — [beej.us/guide/bgnet](https://beej.us/guide/bgnet/)
* man7.org Linux Manual Pages — [man7.org/linux/man-pages](https://man7.org/linux/man-pages/)

### 🧪 Topics

* Syscalls
* epoll, io_uring
* mmap, shared memory
* Threads vs processes
* Signals & IPC
* Telemetry design
* Tracing architecture
* Crash reporting systems
* Perf event pipelines
* Symbolication

### ✅ Practice

* `epoll`-based echo server (timeouts, backpressure, metrics)
* Minimal crash reporting: signal handler → backtrace → symbolication script

## 🚀 Phase 5 — Performance & Real Engine

### 🧱 CPU Side

* Custom memory allocator
* Lock-free data structures
* Job system / scheduler
* Cache-aware data layout
* Async execution model

### ⚡ CUDA

#### 📚 Core Reading

* Programming Massively Parallel Processors
* NVIDIA CUDA Programming Guide
* CUDA Best Practices Guide
* CUDA by Example (Jason Sanders & Edward Kandrot)
* NVIDIA Developer Blog — [developer.nvidia.com/blog](https://developer.nvidia.com/blog)

#### 🧪 Topics

* Kernel design
* Warp-level optimization
* Shared memory
* Memory coalescing
* Async streams & overlap

### 🎮 Vulkan

#### 📚 Core Reading

* Vulkan Programming Guide
* Khronos Vulkan Tutorials — [vulkan-tutorial.com](https://vulkan-tutorial.com)
* Vulkan Cookbook
* Sascha Willems Vulkan Samples — [github.com/SaschaWillems/Vulkan](https://github.com/SaschaWillems/Vulkan)
* [vkguide.dev](https://vkguide.dev)

#### 🧪 Topics

* Explicit memory management
* Descriptor sets
* Pipeline cache
* Synchronization primitives
* Render & compute graph

### 🧬 Integration

* Zero-copy CPU ↔ GPU pipeline
* Frame graph architecture
* GPU scheduling strategy
* Multi-queue async execution
* ECS architecture
* Job system design patterns
* Plugin architecture
* Hot reload systems

### ✅ Practice

* A measurable mini engine loop (timing, job system, render-graph stub)
* Pick one CPU↔GPU bottleneck and iterate: measure → fix → regression notes

## 🛠 Essential Toolchain

* gdb, lldb
* perf, flamegraph
* valgrind, Sanitizers (ASan, TSan, UBSan)
* objdump, nm, readelf

## Online Resources

* CppReference.com — [en.cppreference.com](https://en.cppreference.com)
* cpp-patterns.com — [cpp-patterns.com](https://cpp-patterns.com)
* Herb Sutter Blog — [herbsutter.com](http://herbsutter.com)
