---
title: chap-2-questions
description: chap-2-questions
---


## ✅ **Chapter 2 – Practice Questions**

### 🟢 Easy

1. What are the two main types of **OS services**?
2. What is the difference between **CLI** and **GUI**?
3. What does an **API** do?
4. What is a **system program**?
5. What is the job of a **linker**?
6. What is the difference between **compilation** and **linking**?
7. What is **dynamic linking**?
8. Why do applications depend on the OS?
9. Name a **binary executable file format** used in Linux.
10. What is the role of the **loader**?

---

### 🟡 Medium

1. Compare the **user interface types** in modern operating systems.
2. What is the relationship between **system calls** and **APIs**?
3. Explain how **system programs** differ from **application programs**.
4. Give an example of how **dynamic libraries** save memory.
5. Why are most applications OS-specific?
6. How does an OS **load and execute** a user program from CLI?
7. What is the **ELF format** used for?
8. Describe the difference between **system call** and **library function**.
9. Explain the role of **object files** in program execution.
10. Why is **relocation** needed in loading programs?

---

### 🔴 Hard

1. Compare **Monolithic**, **Layered**, and **Microkernel** architectures with pros/cons.
2. How does **policy vs mechanism** separation help in OS design?
3. Why are **APIs** not enough for full OS compatibility?
4. Explain the **OS execution flow** from source code to running program.
5. Why is dynamic linking beneficial for shared libraries?
6. Describe how **virtualization** affects OS design.
7. How does Android use a **hybrid OS structure**?
8. Explain how **macOS combines Mach and BSD**.
9. What is the difference between **POSIX API** and platform-specific APIs?
10. Why is **portability** difficult across OS platforms?

---

## 📘 **Detailed Answers**

### 🟢 Easy

1. **User services** (UI, I/O, files, execution) and **system services** (resource allocation, protection, logging).
2. **CLI** uses text commands; **GUI** provides visual interaction with icons and windows.
3. An **API** allows user programs to access OS functions via system calls.
4. A **system program** supports OS functions (e.g., file manipulation, compilers).
5. A **linker** combines object files into a single executable.
6. **Compilation**: source → object file; **Linking**: object files → executable.
7. **Dynamic linking** loads libraries at runtime instead of build time.
8. Because OS provides access to hardware and system resources, apps can't work without it.
9. **ELF** (Executable and Linkable Format).
10. The **loader** loads executables into memory and prepares them to run.

---

### 🟡 Medium

1. **CLI**: text-based, powerful for experts.
   **GUI**: user-friendly, visual interface (Windows, macOS).
   **Touch UI**: intuitive for mobile (iOS, Android).
2. An **API** is a programming interface. System calls are how those APIs are implemented in the OS.
3. System programs manage OS-level tasks; application programs serve the user.
4. Multiple processes can use one copy of a **dynamic library**, reducing memory use.
5. Because different OSes have different system calls, file formats, and hardware interfaces.
6. Shell runs → fork() to create process → exec() to load program → loader brings it to memory.
7. **ELF** is a standard binary format used in Linux for object files and executables.
8. **System call**: kernel-level action (e.g., `write()`).
   **Library function**: wrapper (e.g., `printf()` calls `write()`).
9. **Object files** are intermediate files compiled from source code before linking.
10. **Relocation** adjusts memory addresses in the code to match its actual position in memory.

---

### 🔴 Hard

1. **Monolithic**:

   * Fast, tight integration
     − Hard to maintain/debug

   **Layered**:

   * Good modularity
     − Slower due to strict hierarchy

   **Microkernel**:

   * Secure, modular
     − Overhead for message passing

2. **Policy** = What to do; **Mechanism** = How to do it.
   Separation allows flexibility (change policy without rewriting mechanism).

3. **APIs** may work, but the underlying system calls or behaviors differ, breaking compatibility.

4. Flow:
   Source code → Compiler → Object file → Linker → Executable → Loader → Memory → CPU executes

5. Dynamic linking saves space and allows updates to libraries without recompiling the app.

6. Virtualization adds a layer between hardware and OS, so OS must support running as a guest or manage virtual hardware.

7. Android uses **Linux kernel**, but app layer is **Java-based**. Combines monolithic kernel + managed runtime.

8. **macOS** uses **Mach microkernel** for low-level services, and **BSD layer** for user-facing Unix-like environment.

9. **POSIX** standardizes APIs (e.g., `fork()`, `open()`), but platforms like Windows have different APIs.

10. **Portability issues**:

* Different hardware instruction sets
* OS-specific syscalls
* Binary format incompatibilities
