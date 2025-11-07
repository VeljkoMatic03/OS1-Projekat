# RISC-V Multithreaded Operating System Kernel

This project is an implementation of a small but functional **multithreaded operating system kernel** for the **RISC-V** architecture. It supports **threads**, **time-sharing**, **preemption**, **semaphores**, **memory allocation**, and **console I/O**, and is designed to run in an **emulated environment** based on a modified version of **xv6**.

The kernel and user application are statically linked into a **single executable**, sharing the same address space, which corresponds to execution patterns typical for **embedded systems**.

## Features

### **Thread Management**
- Support for creating and executing multiple lightweight threads.
- Context switching between threads.
- Both **cooperative** and **preemptive** dispatching.
- Configurable stack and scheduling time slice.

### **Preemption & Scheduling**
- **Timer interrupt** triggers asynchronous context switching.
- **Time-sharing scheduler** ensures fair execution across threads.
- Support for periodic thread activation (via `PeriodicThread` class).

### **Synchronization**
- **Counting semaphores** with:
  - `wait()`
  - `signal()`
  - `timedWait()`
  - `tryWait()`
- Correct thread blocking and waking behavior.

### **Memory Management**
- Custom memory allocator that:
  - Allocates memory in aligned blocks.
  - Frees previously allocated regions.
- `new` / `delete` in C++ are mapped to kernel allocation services.

### **Console I/O**
- Thread-safe input (`getc()`) and output (`putc()`) operations.
- Input blocking & wake-up on keyboard interrupt.

---

## API Layers

The kernel exposes three application interfaces:

| Layer | Description |
|------|-------------|
| **ABI** | Low-level system call interface via RISC-V `ecall`. |
| **C API** | Procedural interface used by application code. |
| **C++ API** | Object-oriented interface with `Thread`, `Semaphore`, `Console`, etc. |

The user application interacts primarily through the **C++ API**.

---

## Platform and Environment

- Target architecture: **RISC-V RV64**
- Execution environment: modified **xv6** OS running under **QEMU**
- Development language: **C++** (with some inline assembly for context switching)
- No standard library usage (`libc` forbidden)

---

## Building and Running

### **Requirements**
- QEMU (pre-configured in provided VM)
- RISC-V GCC toolchain
- Make
- CLion (optional, recommended)

### **Build**
```sh
make qemu
