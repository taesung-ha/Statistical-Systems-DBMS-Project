# Implementation of Modern Database Internals (CMU 15-445)
### Bridging Statistical Theory and Data Infrastructure

## Project Overview
This repository contains my implementation of **BusTub**, a disk-oriented DBMS engine developed for the [CMU 15-445/645 (Database Systems)](https://15445.courses.cs.cmu.edu/fall2025/) course. 

Coming from a background in statistics, my objective was to deconstruct the "black box" of data systems. This project demonstrates my ability to navigate complex C++ environments and understand the low-level engineering that powers large-scale data analysis and retrieval.



## Core Implementations

### 1. [Buffer Pool Manager](./concepts/01-storage.md)
* Developed a storage manager to handle data movement between disk and memory.
* Implemented the **LRU-K replacement policy** to optimize memory hit rates based on historical access patterns.
* Managed thread-safe page mapping to ensure system stability under concurrent workloads.

### 2. [B+ Tree Index](./concepts/02-indexing.md)
* Built a balanced B+ Tree index to support efficient, sorted data retrieval.
* Implemented core logic for node splitting, merging, and redistribution to maintain optimal tree height.
* Focused on pointer-based navigation and rigorous memory safety within the index structure.



### 3. [Query Execution Engine](./concepts/03-execution.md)
* Created an execution engine based on the **Volcano (Iterator) Model**.
* Implemented physical operators including Sequential Scan, Insertion, Deletion, and Index Scan.
* Explored the transformation of SQL queries into executable physical plans through operator chaining.

## The Statistical Perspective
Understanding database internals provides a unique advantage in data science:
* **Query Optimization:** I view query optimization as a statistical estimation problem, where cardinality estimation directly dictates execution cost and system performance.
* **Systems Thinking:** Beyond modeling, I have gained an appreciation for the trade-offs in data infrastructure—specifically the balance between write-heavy and read-heavy workloads.
* **Engineering Rigor:** Implementing these systems in C++ requires a level of precision in memory management and concurrency that complements the analytical rigors of statistical training.

## Tech Stack
* **Language:** C++17
* **Build System:** CMake
* **Testing:** Google Test (GTest)
* **Analysis Tools:** Valgrind, Clang-Tidy

## Getting Started
To build the system and run tests:
```bash
mkdir build && cd build
cmake ..
make
make check-tests
