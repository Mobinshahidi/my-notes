---
title: book, chap 3
description: book, chap 3
---

### **1. Process Concept 🖥️**

A **process** represents a program in execution. It's an active entity, whereas a **program** is a passive one (just a set of instructions stored on disk). Here's a breakdown of the components of a process:

#### **1.1 Process Components**

- **Program Code (Text Section)**: The actual code of the program that is loaded into memory. This is essentially the set of instructions the CPU will execute.
    
- **Program Counter (PC)**: A register that contains the address of the next instruction to be executed. It helps the CPU to know where the process is currently in its execution cycle.
    
- **Processor Registers**: These are small storage locations within the CPU that hold intermediate data, status information, and flags used by the process during execution.
    
- **Stack**: Used to store information like function parameters, return addresses, and local variables. The stack is crucial for function calls and returns in the execution flow.
    
- **Data Section**: Holds global and static variables that persist throughout the program’s execution. This area is crucial for storing variables that need to maintain their values across function calls.
    
- **Heap**: Dynamically allocated memory used during runtime. This memory can grow or shrink as needed and is managed by the memory manager of the OS (via functions like `malloc()` or `free()`).
    

#### **1.2 Process States**

As a process executes, it can be in one of the following states:

- **New**: The process is being created.
    
- **Running**: The process is being executed by the CPU.
    
- **Waiting**: The process is waiting for some event (such as I/O completion).
    
- **Ready**: The process is in memory and ready to execute but is waiting for CPU time.
    
- **Terminated**: The process has finished its execution.
    

These states are tracked by the **Process Control Block (PCB)**, a data structure maintained by the OS.

#### **1.3 Process Control Block (PCB)**

The **PCB** is essential for managing processes. It contains:

- **Process State**: Current state of the process (New, Ready, Running, Waiting, Terminated).
    
- **Program Counter**: Points to the next instruction to execute.
    
- **CPU Registers**: Stores process-specific register values.
    
- **CPU Scheduling Information**: Includes process priority, time slice, and pointers to scheduling queues.
    
- **Memory Management Information**: Points to the allocated memory for the process.
    
- **Accounting Information**: Tracks CPU usage, elapsed time, etc.
    
- **I/O Status Information**: Information on I/O devices allocated to the process.
    

Each running process in the system has its own **PCB** that is updated as the process changes state.

---

### **2. Process Scheduling🕒**

**Process scheduling** is crucial for the efficient allocation of CPU resources. It allows the operating system to manage multiple processes competing for CPU time.

#### **2.1 Ready and Wait Queues**

- **Ready Queue**: Contains all processes that are in memory and ready to execute. The process scheduler picks from this queue.
    
- **Wait Queue**: Processes that are waiting for an event to occur (e.g., I/O operations). These processes cannot execute until their event completes.
    

#### **2.2 Context Switching**

A **context switch** occurs when the operating system decides to stop executing one process and start executing another. During this switch:

- The state of the current process is saved in its **PCB**.
    
- The state of the next process is loaded from its **PCB**.
    

While context switching is essential for multitasking, it incurs an overhead. The more complex the system, the longer the context switch can take. **Hardware support** (like multiple register sets) can help speed up context switching.

#### **2.3 Multitasking and Mobile Systems**

In **mobile systems** like Android or iOS:

- iOS has stricter controls on multitasking, allowing only one active foreground process at a time, with limited background activity.
    
- Android, on the other hand, supports both foreground and background processes with more flexibility.
    

This process management ensures efficient handling of system resources while maintaining a smooth user experience, even with limited processing power or battery life.

---

### **3. Operations on Processes 🔄**

The **operations on processes** are the fundamental actions the operating system must support to manage process lifecycles. These operations include:

#### **3.1 Process Creation**

- **Forking**: A parent process creates a child process using the `fork()` system call. The child process is a duplicate of the parent, inheriting resources but with a different Process ID (PID).
    
- **Exec**: The `exec()` system call replaces the process's current program code with a new program. This allows a process to load a new program into memory.
    
- **Wait**: The parent can wait for the child process to finish execution using `wait()`. It can retrieve the child’s exit status, ensuring proper synchronization.
    

#### **3.2 Process Termination**

- A process terminates when it completes its task or is aborted by the operating system or the parent process. This can happen through:
    
    - **Exit**: A process calls `exit()` to signal termination. The OS then cleans up the resources used by the process.
        
    - **Abort**: The OS can terminate a process that exceeds allocated resources or violates security policies.
        

#### **3.3 Cascading Termination**

When a parent process terminates, its child processes might also need to terminate. This is called **cascading termination**. If a process terminates without notifying its parent (or if the parent doesn’t call `wait()`), the child becomes a **zombie** process. If the parent has also terminated, the process becomes an **orphan**.

---

### **4. Interprocess Communication (IPC) 🔗**

Interprocess communication is essential for cooperation between processes. It allows processes to exchange data and synchronize actions. There are two main models of IPC:

#### **4.1 Shared Memory**

- Multiple processes can communicate by accessing a shared region of memory. This model allows fast communication but requires synchronization mechanisms to prevent concurrent processes from corrupting shared data.
    

#### **4.2 Message Passing**

- This model involves processes sending and receiving messages through communication channels. It can work in two forms:
    
    - **Direct Communication**: Each process explicitly names the other when sending messages.
        
    - **Indirect Communication**: A mailbox (or port) is used, and processes send and receive messages via the mailbox. This allows for more flexibility and decouples the processes.
        

Message passing can be either **synchronous** (blocking) or **asynchronous** (non-blocking). In synchronous communication, the sender waits for the receiver to acknowledge receipt of the message. In asynchronous communication, the sender proceeds immediately without waiting for acknowledgment.

#### **4.3 Example: Producer-Consumer Problem**

- In this classic problem, one process (the producer) generates data and places it in a shared buffer, while another process (the consumer) retrieves and processes the data.
    
- **Bounded Buffer**: The buffer has a finite size, so the producer must wait if the buffer is full. The consumer must wait if the buffer is empty.
    

---

### **5. Real-World IPC Systems** 🌐

- **Client-Server Communication**: In client-server systems, servers wait for requests from clients and process them when they arrive. Communication between client and server often uses sockets, a form of message-passing IPC. For instance, web browsers (clients) communicate with web servers to retrieve pages.
    

---

### **Key Takeaways🎯**

- **Process Management** ensures efficient execution of programs, handling creation, scheduling, synchronization, and termination of processes.
    
- **Process Scheduling** maximizes CPU utilization and ensures fairness and efficiency in resource allocation.
    
- **Operations on Processes** like `fork()`, `exec()`, and `wait()` form the core of process control in operating systems.
    
- **Interprocess Communication (IPC)** is essential for processes to share data and synchronize actions, enabling complex software systems like web servers, multi-tasking environments, and mobile apps.
    
