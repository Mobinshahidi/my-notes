---
title: summarize to understand better
description: summarize to understand better
---

# 1
- System has 4 component: hardware, os, apps, user
- Hardware for computing
- Apps for processing user inputs(word processor)
- Os connection between the apps and hardware
- User for using this system
- Os is like a government, it doesn't do anything by it self, its perform a useful functions and provide an environment that other programs can do useful things
- Computer system is consisting of hardware, software and data
- We have two view in computer : user view, system view
- From user view, user just need interfaces to used(keyboard and etc.) and os design to mostly for ease of use with some attention to performance and security
- From system view (pov) the os is the program most intimately involved with hardware for resource allocating because the system has too much resources (cpu time,memory etc.) and os should manage them and also os must manage i/o devices and user programs
- Os is control program too, a control program manage the execution of user program to prevent errors and improper use of computer
- Os exist because they offer a reasonable way to solve the problem and to execute programs to make solving user problems easier
- Why application program developed? Because the communication between the hardware and user is be more simpler and easier
- Why os developed? Because application needs command to communication between the hardware, and os make this communication easier and better with resource allocation and etc.
- Os is the on program running at all times in computer (kernel)
- Along kernel we have two types of programs: system programs, application programs
- System programs: which they are associated with the os and necessarily part of the kernel
- Application programs: include all programs not associated with the os of the system
- In mobile os we also have middleware along with core kernel
- Os has device driver to communicate with device controller -> device controller is responsible for moving data between the apps and local buffer storage (hardware) -> device controller connected through a common bus that provides access between components and shared memory
- Cpu can device controller can execute in parallel
- For order of access to shared memory, we have memory controller synchronizes
- Device controller is a hardware component that manage specific type of device and communication between the cpu and the related device and it has local buffer memory to store temporarily data and receives commands from the cpu and translate it to device
- Device driver is a software in os level that interface with a specific device controller and translate high level os commands in to low level hardware instructions and make uniform interface that os doesn't need to know specific hardware device.
- OS sends a command via the driver → Driver communicates with controller → Controller handles the actual device operations.
- User wants to i/o operation  -> device driver loads proper register to device controller-> device controller examines the content of the registers to determine the size of that and set action (read, write and etc) ->  device controller moves that data to its local  buffer and when its done -> inform device driver -> device driver notify os to do  whatever its do related to that action.
- Interrupts : 
	- hardware : a signal that created by the hardware (device controller), by way of the system bus, that informs the device driver to tell os the operation is done
	- software : (trap,exception) -> caused by an error or by a specific req from user program.
- When cpu interrupts, it stops what it is doing and immediately transfer execution to a fixed location and let isr (interrupt service routine)
- Each device has its own interrupt service routing (isr) => special code to handle its request
- Os for managing interrupts fast, has interrupt vector table (ivt) to jump straight to the correct isr
- When error (interrupt) occurs -> os saves the current state of cpu -> os checks ivt to see this code belongs to which isr -> isr check and see how it can handle that error(interrupt     -> os restore the saved stats of cpu
- What isr does? Saves any cpu state, identifies the cause of interrupt, Perform the needed operation , Restores the cpu, executes a return from interrupt instruction to resume the interrupted task
- Interrupts in modern systems:
	- Sometimes the os is doing something critical and delay interrupts using maskable interrupts, which can temporarily disabled 
	- os assigns priority to interrupts and ensure the urgent tasks get handled first
- Maskable interrupt can be disabled temporarily during critical os operation but non-maskable, can't be turn off (memory failure)
- In ivt each device has a unique entry and when there are more devices than entries, each vector entry points to a list of handlers and all handlers in the list are checked one by one to find the one handler.
- Cpu can only execute instruction from memory
- Any program must be loaded to memory before it can run
- Most programs loaded into main memory (ram (random access memory)) and its volatile
- Every byte in memory has a unique address and cpu use two instructions `load (moves from memory to registers)& store (moves data from register to memory)` and also automatically loads instructions from memory (program counter)
- Memory doesn't know what its storing and it just see addresses being used
- Cpu  use this cycle: fetch instruction from memory -> decode it -> fetch data if needed -> execute the operation -> store result back in memory if required
- Because ram small and volatile, we need secondary storage -> its slower than ram

|Type|Characteristics|Volatile?|Example|
|---|---|---|---|
|**Registers**|Fastest, smallest|✅|CPU internal|
|**Cache**|Very fast, small|✅|L1/L2 CPU cache|
|**Main Memory (RAM)**|Fast, medium size|✅|DRAM|
|**Secondary Storage**|Slower, large|❌|HDD, SSD|
|**Tertiary Storage**|Very slow, huge, special use|❌|Magnetic tape, Blu-ray|
- When we power on a computer, the first program to run is called the bootstrap program because ram is not reliable during the startup(because its volatile), the bootstrap program is stored in eeprom (nonvolatile)
- A big part of the os is responsible for managing i/o because i/o is critical for performance and reliability and i/o devices vary greatly in type, speed and behavior so they require specific handling
- Because so many devices connected to a common bus, and it generate one interrupt per byte, for large data transfer, slowing down everything -> we use dma (direct memory access) -> dma allows the device controller to transfer an entire block of data directly between main memory and the device controller without involving cpu for every byte
- For dma, os sets up buffers(where data is stored temporarily), pointers(to track memory addresses), counters(to track data length) and tell device controller to handle the transfer and it moves the data directly between device and memory, and when finished send interrupt to cpu and tell it its finished. => cpu can work on other tasks during the data transfers - system becomes more efficient(especially with large transfer) - only one interrupt per block(less cpu overhead)
- In advanced systems we have switch based architecture which multiple components can communicate at the same time - no more fighting over the same communication line - dma is even more powerful here because data movement doesn't get blocked by bus competition and cpu, memory and multiple device can all operate concurrently
- In modern system, they have multiple cpu and they can run multiple processes at once,
- Symmetric Multiprocessing (smp) is most common type of multiprocessor system, and all cpus are equal and perform all types of task, each cpu has its own register and local cache but shares main memory and bus, if n cpus, n process can run simultaneously
- Multicore systems-> multiple processing cores on one chip, more efficient than using multiple separate chips because on chip communication is faster than between chips and it have lower power consumption, and from the os view, each core appears as an independent cpu and each core has its own L1 cache and may share L2 cache
- When we increase number of cpus in a system, bus slows down performance and numa solve that: giving each cpu or cpu group its own local memory, cpus connect via a shared interconnect and all memory is part of the same address space
- When a cpu accesses its own local memory, its fast.
- Os needs smart scheduling to reduce performance loss
- Blade server -> multiple processor boards,i/o boards and network boards placed into a single chassis -> each blade : boots independently, runs its own os

|Feature|SMP|Multicore|NUMA|
|---|---|---|---|
|CPUs or cores location|Separate processors|Multiple cores on one chip|Separate processors + memory|
|Memory structure|Shared memory|Shared memory/cache|Local + shared memory|
|Communication|Via system bus|On-chip, very fast|Interconnect (varies in speed)|
|Scalability|Medium|Medium|High|
|Power efficiency|Moderate|High|Moderate|
|Performance bottleneck|Bus contention|Cache contention|Remote memory access latency|

|Architecture|Key Traits|
|---|---|
|**Single-processor**|One CPU, special-purpose devices may help|
|**Multiprocessor**|Multiple CPUs, shared memory, SMP or NUMA|
|**Multicore**|Many cores on one chip, faster communication|
|**NUMA**|CPUs with local memory, shared interconnect|
|**Blade servers**|Multiple independent systems in one chassis|
|**Clusters**|Independent nodes working together over network|
- After bootstrap is loaded from the eeprom, bootstrap program should locate the os to load it in the memory to run that, when kernel loaded and executed, it provides services to the system, services outside the kernel called system daemons which run entire time the kernel is running
- First system program in linux called systemd and it starts many other daemons and after all of this, system waits to event occur
- Multiprogramming: os keeps multiple processes in memory and when one of them waits, cpu switch to another and improve the performance and gives user better ux and when multiple process are ready, os use cpu scheduling to decide which runs next and for supporting them os us virtual memory
- 

# 2 

- **OS provides services for programs and users**
    
    - Some services help the **user** (e.g., user interface, I/O handling, file systems, error detection)
        
    - Some services help **system efficiency** (e.g., resource allocation, logging, protection & security)
        
- **User Interface Types**
    
    - **CLI (Command Line)**: Text-based, shell interpreters
        
    - **GUI (Graphical User Interface)**: Point-and-click, desktop metaphor
        
    - **Touch interface**: Gestures, for mobile devices
        
- **System Calls**
    
    - Interface between program and OS
        
    - Functions requested: process control, file management, device control, info maintenance, communication
        
    - Accessed via API (e.g., POSIX, Windows API)
        
    - Programs interact with API, API uses system calls
        
    - Reasons for API: easier programming, portability, and maintainability
        
- **System Programs**
    
    - Utilities that provide user interface to system calls
        
    - File management, status info, file editors, compilers, debuggers, communications, background services
        
- **Linkers and Loaders**
    
    - Compile → Object File → Linker (combine .o + libs) → Executable → Loader → Memory
        
    - Executables can be dynamically linked (DLLs in Windows, .so in Linux)
        
    - Executable formats: ELF (Linux), PE (Windows), Mach-O (macOS)
        
    - Loader loads program into memory and starts it
        
- **Apps are OS-Specific**
    - System calls differ per OS → apps compiled for one OS don’t run on others
    - Solutions: Interpreters (Python), RTEs (Java VM), or porting apps using APIs like POSIX
    - Also needs matching binary format, CPU instruction set, ABI
- **OS Design & Implementation**
    - Goals: user goals (easy, reliable), system goals (maintainable, efficient)
    - **Policy vs Mechanism**: what vs how (e.g., scheduling policy vs mechanism)
    - Implemented mostly in high-level languages (C/C++, Java for Android)
- **OS Structures**
    - **Monolithic**: One big kernel (e.g., Linux, UNIX)
    - **Layered**: Multiple levels (hardware → kernel → UI)
    - **Microkernel**: Minimal kernel + services in user space (e.g., QNX, Mach)
    - **Modules**: Core + loadable kernel modules (e.g., Linux)
    - **Hybrid**: Mix of above (e.g., macOS, iOS, Android)
