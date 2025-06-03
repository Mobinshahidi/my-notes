---
title: OS course
description: OS course
---


> [!NOTE]  DEFINITIONS OF COMPUTER SYSTEM COMPONENTS  
• CPU— The hardware that executes instructions.  
• Processor —A physical chip that contains one or more CPUs.  
• Core— The basic computation unit of the CPU.  
• Multicore —Including multiple computing cores on the same CPU.  
• Multiprocessor — Including multiple processors.  
Although virtually all systems are now multicore, we use the general term  
CPU when referring to a single computational unit of a computer system and  
core as well as multicore when specifically referring to one or more cores on  
A CPU.

# explanation
##### Overhead:
Means  extra work the system has to do that doesn't directly help the user (You're working on a project. But every few minutes, you have to **switch tabs**, **save your progress**, and **close one app to open another**.)
##### swapping:
**Swapping** is like saying:
> "Let me put this process into the closet (disk) for now, and bring another one into the room (RAM)."

 The OS does this **when there’s not enough memory (RAM)** to hold all processes.
So it
1. **Swaps out** (removes) a paused process from RAM and saves it to disk.
2. **Swaps in** another process from disk into RAM to run.
This helps the system **simulate having more memory** than it really does, but it’s **slow**.
##### time slice:
A time slice (time quantum) is the maximum amount of time a process is allowed to run on the  cpu before the os forces it to pause and gives another process a turn
Because in **multitasking** systems, many processes need to share the CPU.  
To make sure:
- **No one process hogs the CPU**
- All processes get a **fair turn**
- The system feels **fast and responsive**
The OS:
- Gives each process a time slice (maybe 10ms or 100ms)
- **Switches** to another process when time is up (if it hasn't finished)
##### process table
Think of the **process table** as a **big spreadsheet or database inside the operating system**. It stores all the important information about **every running process** in the system
Every time a process is created, the OS **adds an entry (a row)** in this table.  
When the process ends, its entry is removed.
 **What's inside the Process Table?**
Each row (entry) in the table holds a **data structure** called a **PCB (Process Control Block)**.
This includes things like:
- 🪪 **PID** – process ID (unique name)
- 🧠 **Process state** – is it running, ready, waiting, etc.
- 📍 **Program counter** – where it's currently running in the code
- 💾 **Memory info** – which memory the process owns/uses
- 📄 **Open files** – what files the process is using
- 🔁 **CPU register values** – saved values when switching tasks
- 🧾 **Accounting data** – how much CPU time it's used, etc.
# 1.1
## what operation systems do?
Computer system can divided into four component : **hardware**, **operating system**, **apps** and **user**
#### hardware : 
The central processing unit (cpu), the memory and the I/O devices provides the basic computing resources for the system.
#### application programs:
Word processors, spreadsheets, compilers, and web browsers, define the ways which user can fix their computing problems.
#### operating system
Controls the hardware and coordinates its use among the various app for various user

We can also view a computer system as consisting of hardware, software and  data. The operating system provides the means for proper use of these resources in the operation of the computer system. And op is similar to a government. Like a government, it performs no useful function by itself. It simply provides an environment within which other programs can do useful work.

# 1.1.1
## user view
The user's view of the compute varies according to the interface being used.
In the case that user just use keyboard and mouse and monitor to play game  or etc. the os is designed mostly for ease of use, with some attention paid to performance and security and none paid to resource utilization (how various hardware and software resources are shared) ![[IMG-20250528095439885.png]]

# 1.1.2
## system view
From the computer's pov, the os is the program most intimately involved with hardware (**==resource allocator==**). A computer system has too many resources that may be required to solve a problem (cpu time, memory space and etc.) the **OS** here acts as a manager. The os must decide how to allocate them to specific programs and users so that it can operate without any conflict.
Another pov is we need to control the various I/O devices and user programs, so OS is a **==control program==**. A control program manage the execution of user programs to prevent errors and improper use of the computer.
# 1.1.3
## defining OS
In general, we have no completely adequate definition of an os. Os exist because they offer a reasonable way to solve the problem of creating a usable computing system.the fundamental goal of computer system is to execute programs and to make solving user problems easier. (computer hardware is constructed toward this goal.) 
Why application program developer? **Since bare hardware is not easy to use.**
Why operation system developed? **Because these programs require certain common operations, such as those controlling the I/O devices. The common functions of controlling and allocating resources are then brought together into one piece of software.**

**So OS is the one program running at all times on the computer.** => usually called it **kernel** =>Along with the kernel, there are two other types of programs: **system** **programs**, which they are associated with the os but necessarily part of the kernel, and **application programs**, which include all programs not associated with the os of the system.
- Mobile os often include not only a core kernel, but also middleware, that is a set of software frameworks that provide additional services to app developers (supporting database and graphics and etc).
# 1.2
## computer system organization
![[IMG-20250528112018751.png]]
- In modern computer, device controllers connected through a common bus that provides access between components and shared memory
> [!IMPORTANT] 
> There may be many buses within a computer system, but the system bus is the main communications path between the major components
- The device controller is responsible for moving the data between the peripheral devices that it controls and its local buffer storage.
- Operating systems have a device driver for each controller. This device understand the device controller and provides the rest of the os system with a uniform interface to the device.
- The cpu and device controllers can execute in parallel, competing for memory cycles.
- To ensure the order of access to the shared memory, a memory controller synchronizes access to the memory.![[IMG-20250528113645443.png]]
- Controllers & Drivers in OS
	- Device Controller
		- A **device controller** is a hardware component that manages a specific type of device (e.g. Keyboard, disk, network card). Its key roles:
		- Manages communication between the CPU and its corresponding device.
		- Contains local buffer memory to temporarily store data.
		- Receives commands from the CPU and translates them for the device.
- Device Driver
	- A **device driver** is a piece of OS-level software written to:
		- Interface with a specific device controller.
		- Translate high-level OS commands into low-level hardware instructions.
		- Provide a **uniform interface** so the OS doesn’t need to know specifics of every hardware device.
- Interaction Overview:
	- OS sends a command via the driver → Driver communicates with controller → Controller handles the actual device operations.
	  
Consider a typical computer operation: a program performing I/O . To start an  
I/O operation, the device driver loads the appropriate registers in the device  
controller. The device controller, in turn, examines the contents of these reg-  
isters to determine what action to take (such as “read a character from the  
keyboard”). The controller starts the transfer of data from the device to its local  
buffer. Once the transfer of data is complete, the device controller informs the  
device driver that it has finished its operation. The device driver then gives  
control to other parts of the operating system, possibly returning the data or a  
pointer to the data if the operation was a read. For other operations, the device  
driver returns status information such as “write completed successfully” or  
“device busy”.

# 1.2.1
## interrupts
A signal that triggered by the hardware (controller), usually by way of the system bus, that inform the device driver to tell that it has finished its operation.
**Interrupts are used for many other purposes and are a key part of how os and hardware interact.**
When cpu is interrupted, it stops what it is doing and immediately transfers execution to a fixed location, that fixed location usually contains the starting address where the service routine executes
The interrupts must transfer control to the appropriate interrupt service routine(ISR).
### 1.2.1.1 overview
- Interrupts let the CPU pause what it's doing to handle urgent tasks (like input/output).
- Each device has its own **interrupt service routine (ISR)** – special code to handle its request.
- To respond quickly, the OS uses an **interrupt vector table** – a list in low memory with addresses of all ISRs.
- When an interrupt happens, the CPU uses the interrupt number to jump straight to the correct ISR via the table.
- The OS **saves the current state** (like registers) before running the ISR, so it can go back to where it left off.
- After handling the interrupt, the saved state is restored, and the CPU resumes the interrupted program.
**how interrupt works?**(long version)
1. **Interrupt Happens**
	A device (e.g. Keyboard, disk, network card) or software sends an interrupt signal.
2. **CPU Needs to Handle It Fast**
	Instead of calling a general handler and figuring out which device needs service, that would be slow.
 3. **Interrupt Vector Table (IVT)**
	There is a special **table in low memory** (called **interrupt vector**). It’s like a contact list:
	- Each device has a number (interrupt number).
	- This number is used to find the **address** of the **correct routine** to handle the interrupt.
 4. **Indirect Call**
	The CPU jumps **directly** t                                                                                                                                                                            o the correct **Interrupt Service Routine (ISR)** using the table, no delay.
 5. **Save the CPU State**
	Before running ISR, the OS **saves the current state** (e.g. Registers, program counter) so it can continue later.
 6. **Handle the Interrupt**
	The ISR executes: e.g. reading a key, finishing a disk write, handling a timer tick...
 7. **Restore the CPU State**
	After ISR finishes:
	- The CPU loads the saved state.
	- The previous program continues **as if nothing happened**.                                                                                                                                                                                                                                                               
### 1.2.1.2 implementation
The **basic interrupt mechanism** works in a precise sequence and is managed by hardware and OS together:
- The **CPU** has a special wire called the **interrupt-request line**.
- After **every instruction**, the CPU checks this line to see if a device has raised an interrupt.
If an interrupt signal is detected:
1. The CPU **reads the interrupt number** provided by the device.
2. This number is used as an **index** into the **Interrupt Vector Table (IVT)**, which contains **addresses of ISRs** (Interrupt Service Routines).
3. The CPU jumps directly to the address found in the IVT and starts executing the corresponding **ISR**.
#### What ISR does:
- **Saves any CPU state** (like registers) that might be changed.
- **Identifies** the cause of the interrupt.
- **Performs the needed operation** (e.g., reading data from device).
- **Restores the CPU state.**
- Executes a **return-from-interrupt** instruction to resume the interrupted task.
##### Terminology:
- **Device controller raises** an interrupt by sending a signal.
- **CPU catches** the interrupt and dispatches it to the correct handler.
- **ISR handles** the task and **clears** the interrupt by servicing the device.
#### advanced features of modern interrupt systems:
1. **Deferring Interrupts:**
    - Sometimes, the OS is doing something critical and **must delay interrupts**.
    - This is done using **maskable interrupts**, which can be temporarily disabled.
2. **Efficient Dispatch:**
    - The interrupt number lets the CPU use the **IVT to jump directly** to the right handler (no general search needed).
3. **Multilevel Interrupts / Priority:**
    - OS assigns **priorities** to interrupts.
    - **High-priority interrupts** can interrupt low-priority ones.
    - Ensures that **urgent tasks** (e.g. hardware failure) get handled first.
 
#### hardware support:

|**Interrupt Type**|**Purpose**|
|---|---|
|**Nonmaskable Interrupt**|Can’t be turned off (used for serious errors like memory failure).|
|**Maskable Interrupt**|Can be disabled temporarily during critical OS operations.|
#### vectored interrupt vs chaining:
- **Vectored interrupts**:
    - Each device has a unique entry in the IVT.
    - Fast & direct access to the right handler.
- **Interrupt chaining**:
    - When there are **more devices than entries** in the IVT.
    - Each vector entry points to a **list of handlers**.
    - All handlers in the list are **checked one-by-one** until the correct one is found.
    - A compromise between **efficiency** and **scalability**.
#### example: Intel processor interrupt vector
- **Interrupts 0–31**: Reserved, nonmaskable – used for system errors.
- **Interrupts 32–255**: Maskable – used for devices like keyboard, mouse, disk, etc.
#### summary
- Interrupts allow the system to **respond quickly** to external and internal events.
- The **Interrupt Vector Table** maps device numbers to the correct routines.
- The **OS saves and restores state** to keep the system stable.
- **Prioritization and masking** ensure that important tasks are not delayed.
- Efficient interrupt handling is **critical** for system performance.

# 1.2.2
## storage structure
In a computer system, storage structure refers to how different types of memory are used to store and manage data and programs efficiently.
### main memory (ram)
- Cpu can only execute instructions from memory -> **any program must be loaded into memory before it can run.**
- Most programs are loaded into main memory, which is: 
	- also called **RAM**(random access memory).
	- made with a tech called **dram** (dynamic ram)
- Main memory is **volatile**:
	- when the power is off -> all content is lost.
### bootstrapping and firmware
- When we power on a computer, the first program to run is called the **bootstrap program**.
- Because ram is not reliable during the startup(because its volatile), the bootstrap program is stored in **nonvolatile** memory:
	- **EEPROM** (Electrically Erasable Programmable Read-Only Memory) : iPhones use eeprom to store serial numbers and hardware info
	- other **firmware** types
	  
### storage units:

| Term     | Meaning                                                                |
| -------- | ---------------------------------------------------------------------- |
| **Bit**  | Smallest unit of storage: 0 or 1                                       |
| **Byte** | 8 bits, smallest practical data unit                                   |
| **Word** | Native data unit of a computer’s architecture (e.g. 64 bits = 8 bytes) |

### how cpu interacts with memory?
- Every byte in memory has a **unique address**
- CPU uses two instructions:
    - `load`: moves data from memory → CPU register
    - `store`: moves data from register → memory
- CPU also **automatically loads instructions** from memory (using program counter).

**Von Neumann Cycle**:
1. Fetch instruction from memory
2. Decode it
3. Fetch data if needed
4. Execute the operation
5. Store result back in memory if required

> Memory doesn’t know whether it’s storing **data** or **instructions** it only sees addresses being used.

### **Why We Need Secondary Storage**
#### Problems with RAM:
1. Too small to hold everything permanently
2. Volatile – loses all data if power is cut
#### Solution: **Secondary Storage**
- Used as an **extension** to main memory
- Examples:
    - **HDD** (Hard Disk Drive)
    - **NVM** (Nonvolatile Memory – like SSDs)
Programs are **stored in secondary storage** until needed → Then loaded into RAM.

> Secondary storage is **slower** than RAM → OS must manage it efficiently.

### **Storage Hierarchy**
Storage types differ in **speed, size, and volatility**.

|Type|Characteristics|Volatile?|Example|
|---|---|---|---|
|**Registers**|Fastest, smallest|✅|CPU internal|
|**Cache**|Very fast, small|✅|L1/L2 CPU cache|
|**Main Memory (RAM)**|Fast, medium size|✅|DRAM|
|**Secondary Storage**|Slower, large|❌|HDD, SSD|
|**Tertiary Storage**|Very slow, huge, special use|❌|Magnetic tape, Blu-ray|
>There is a **trade-off** → Faster = Smaller = More Expensive

### **Important Terminology**
- **Memory** = Volatile storage (RAM, cache, registers)
- **NVS (Non-Volatile Storage)** = Storage that retains data without power
- **NVM (Non-Volatile Memory)** = A type of electrical storage (e.g. Flash, SSD)
- **Mechanical Storage** = Uses moving parts, slower (e.g. HDD)

>  System designers aim to balance:
> - **Fast** but **expensive** memory (RAM, cache)
> - **Slow** but **cheap and persistent** storage (HDD, NVM)
# 1.2.3
## I/O structure
A big part of the os code is responsible for managing input/output operation because:
- I/o is critical to a system's performance and reliability
- I/o devices vary greatly in type, speed, and behavior, so they require specific handling

### challenge with interrupt-driven i/o?
- General purpose pc have many devices connected to a common bus.
- Interrupt-driven i/o works well for small data transfers.
- For large data transfers(like saving files, loading large programs), this method causes too much overhead because:
	- it generates one interrupt per byte.
	- this interrupts the cpu too often, slowing everything down.
### what we can do?
Use **direct memory access**(dma) 

**what is dma?** 
- Dma allows the device controller to transfer an entire block of data directly between main memory and the device without involving the cpu for every byte
**how does it works?**
1. The os sets up:
	- buffers(where data is stored temporarily)
	- pointers (to track memory addresses)
	- counters (to track data length)
2. Then it tells the device controller to handle the transfer.
3. The controller moves the data directly between device and memory.
4. When its done, it sends just one interrupt to the cpu : `hey, im finished with the whole block`
**why its good?** 
- Cpu can work on other tasks during the data transfer.
- System becomes more efficient, especially with large transfers
- Only one interrupt per block -> less cpu overhead.
  
### advanced systems: switch-based architecture
- Some high-end systems don't use a shared bus 
- Instead, they use a switch-based arch where:
	- multiple components can communicate at the same time (in parallel).
	- no more fighting over the same communication line (like in buses).
	- dma is even more powerful here because data movement doesn't get blocked by bus competition.
	- cpu, memory, and multiple devices can all operate concurrently.
### summary
- Traditional I/O creates too many CPU interruptions for large data transfers.
- **DMA reduces overhead** by letting devices transfer data **directly** to memory.
- CPU is **freed up** during transfers → system runs faster.
- In **modern switch-based architectures**, DMA is even more efficient.
- DMA is essential for high-speed operations like disk access, network streaming, and media handling.
  

# 1.3
## computer system-architecture
Modern computer arch can be organized in different archs based on how many general purpose processors they use

# 1.3.1
## single-processor systems
- Older systems were single processor, meaning they had one cpu with one processing core.
- The core is the unit that executes instructions and contains registers for fast local data storage.
- These systems may also have special purpose processors.(keyboard, graphics controllers) but: 
	- these processors have limited instruction sets
	- they do not run processes like the main cpu.
	- often managed by the os or operate autonomously.
- Even if there are multiple microprocessors, as long as there's only one general purpose core, its still considered a single processor system.
- A keyboard has a microprocessor that converts key presses into signals sent to the cpu

# 1.3.2
## multiprocessor systems (multi-cpu)
Modern systems usually have two or more cpus, each possibly with one or more cores.
### advantage: 
- Increased throughput (more work done in less time)
- Can run multiple processes at once.
- The speed-up is not linear. For n cpus, you won't get n* speed because:
	- there is overhead to manage coordination between processors.
	- cpus compete for shared resource (like memory, bus)

### symmetric multiprocessing (smp)
Each peer CPU processor performs all tasks, including operating-system functions and user processes and can run simultaneously 
- Most common type of multiprocessor system.
- All cpus are equal and perform all types of task (os tasks and user programs) 
- Each cpu has:
	- its own registers and local cache
	- but shares main memory and bus
- If n cpus -> n processes can run simultaneously
	- Dome cpus may be overloaded while others are idle.
	- Needs smart scheduling and shared resources to balance the workload.
### multicore systems 
- Multiple processing cores on one chip
- More efficient than using multiple separate chips because:
	- on chip communication is faster than between chips
	- lower power consumption (important for mobile devices)
- To the os, each core appears as an independent cpu.
#### cache hierarchy:
- Each core has its own L1 cache (fast, small)
- Cores may share L2 cache (slightly slower, bigger)

### non uniform memory access(numa)
- As the number of cpus increases, bus contention slows down performance.
- Numa solves  this by :
	- giving each cpu or cpu group its own local memory
	- cpus connect via a shared interconnect.
	- all memory is part of the same address space.
- When a cpu accesses its own local memory, its fast and avoids contention.
- Accessing other cpus memory is slower (called remote memory access)
- Os needs smart scheduling to reduce performance loss

### blade servers
- Multiple processor boards, i/o boards, and network boards placed into a single chassis
- Each blade:
	- boots independently
	- runs its own os
- Some blades may themselves be multiprocessor systems, making the distinction blurry.
- Its like a box full of small pc working together.

### Comparison Table:

|Feature|SMP|Multicore|NUMA|
|---|---|---|---|
|CPUs or cores location|Separate processors|Multiple cores on one chip|Separate processors + memory|
|Memory structure|Shared memory|Shared memory/cache|Local + shared memory|
|Communication|Via system bus|On-chip, very fast|Interconnect (varies in speed)|
|Scalability|Medium|Medium|High|
|Power efficiency|Moderate|High|Moderate|
|Performance bottleneck|Bus contention|Cache contention|Remote memory access latency|
# 1.3.3
### clustered systems
#### what is clustering?
- A cluster is a set of independent systems(nodes) connected by a network. 
- Each node is usually a multicore system.
- Nodes may be loosely coupled, meaning they work independently but share resources, like storage.
#### goals of clustering
- High availability:
	- if one node fails, another takes over
	- users may only notice a small service interruption
- High performance:
	- some clusters can run apps in parallel on multiple nodes
	- this requires apps to be designed for parallelism, using a technique called parallelization.
#### cluster structures:

|Type|Description|
|---|---|
|**Asymmetric clustering**|One node is active, another is on standby (monitoring).|
|**Symmetric clustering**|All nodes run apps and monitor each other → more efficient.|
In both cases, cluster software handles:
- Monitoring node health
- Restarting services if one node fails
- Managing shared storage
#### parallel clusters
- All nodes access shared data from a shared disk
- Requires special software versions and access control (like distributed lock manager -> dlm)
- Oracle real application cluster lets many systems access and update the same database

#### wide-area clusters
- Nodes in the cluster can be far apart (even miles away).
- Enabled by storage are networks (sans)
- If apps and data are stored on the san:
	- any system attached can run them.
	- if one system fails, another can take over seamlessly

#### summary:

|Architecture|Key Traits|
|---|---|
|**Single-processor**|One CPU, special-purpose devices may help|
|**Multiprocessor**|Multiple CPUs, shared memory, SMP or NUMA|
|**Multicore**|Many cores on one chip, faster communication|
|**NUMA**|CPUs with local memory, shared interconnect|
|**Blade servers**|Multiple independent systems in one chassis|
|**Clusters**|Independent nodes working together over network|


# 1.4
## operating system operations
After that bootstrap is loaded from the eeprom, the bootstrap program should locate the os kernel and load it into memory, once the kernel is loaded and executing, it can providing services to the system and its users. Some services are provided outside of the kernel by system programs that are loaded into memory at boot time to become **system daemons**, which run the entire time the kernel is running.
In linux first system program is `systemd` and it starts many other daemons. After all this happened and system completely booted, system waits for event to occur.
> [!iMPORTANT]
> - Another type of interrupts is a **trap** or an **exception**, which is a software generated interrupt caused either by an error or by a specific req from a user program that an os service be performed by executing a special operation called a system call.

# 1.4.1
## multiprogramming and multitasking
### multiprogramming
- The os keeps multiple processes in memory
- If one process waits, the cpu switches to another
- Keep cpu busy and improves performance.
#### multitasking
- Extension of multiprogramming where
	- cpu rapidly switches between processes 
	- gives users the feel of fast, simultaneous execution
	  
#### cpu scheduling & memory
- When multiple processes are ready, the os uses cpu scheduling to decide which runs next
- To support many processes, the os uses virtual memory:
	- programs can be larger than physical ram.
	- frees developers from memory size worries

#### file system & resource protection
- Os must provide :
	- file system (stored on secondary storage)
	- storage management
	- resource protection (from improper access)

#### process coordination
- Os provides tools for:
	- process synchronization
	- communication between processes
	- avoiding deadlocks

# 1.4.2
## dual mode and multimode operation
Os must prevent user programs from harming the system or other programs.
- System use hardware modes:
	- user mode(1): limited permissions
	- kernel mode (0) : full access
	- mode bit -> in hardware tells current mode
### mode switching 
- At boot, the system is in kernel mode
- When a user app runs, the os switches to user mode.
- If a trap or interrupt occurs -> switch back to kernel mode.

#### privileged instructions
- Some instructions(i/o control, timers) are only allowed in kernel mode.
- If a user tries to run them -> trap to os
- Ex of mode control: System call -> kernel mode -> os service -> return to user mode
> [!NOTE] 
> virtualization adds a mode for managing virtual machines

# 1.4.3
## timer
A timer can be set to interrupt the pc after a specified period (period can be fixed or variable)
**why we use timer?**
- Prevents user programs from taking over the cpu forever.
- Os sets a timer interrupt before giving control to a user program

**how does it works?**
1. Clock ticks at fixed rate.
2. A counter is set.
3. Each tick -> counter decreases
4. When counter = 0 -> interrupt, and os regains control


> [!NOTE] Linux timers
> HZ value = how many timer interrupts per second.
> HZ = 250 -> 1 interrupt every 4 ms
> `jiffies` = total timer ticks since system boot 

# 1.5
## resource management 
Os fundamentally is a resource manager, it manages: 
- Cpu
- Memory
- File storage
- I/o devices

# 1.5.1
## process management
### what is a process?
- A process is a program in execution.
- A program is a passive entity
- A process is active (running instructions on the cpu)
**important:**
- A process needs resources: cpu time, memory, files, and i/o devices.
- These are allocated during its lifetime and reclaimed when it ends

### single threaded vs multithreaded
- A **single threaded** process has one program counter and executes instructions one at a time
- A **multithreaded** process has multiple program counters- one per thread.

### os responsibilities for process:
- Creating and deleting user and system processes
- Scheduling processes and threads on the cpu
- Suspending and resuming processes
- Providing synchronization between processes 
- Enabling communication between processes

# 1.5.2
## memory management
#### what is main memory?
- A large array of bytes, each with its own address.
- Used to store instructions and data for the cpu and i/o
  
>cpu can only execute programs that are in memory

### os responsibilities for memory
- Keeping track of used and free memory sections
- Allocating/deallocating memory for processes
- Deciding what data/instructions to move in or out of memory
- Os must use efficient memory management algorithms suited to system hardware

# 1.5.3
## file system management
### what is a file?
- A logical collection of data defined by its creator
- Can be programs (source / object), text, media, etc.
### what is the file system?
- Os gives a uniform view of storage
- Maps logical files to physical devices(like hdd,ssd,cd)
## os responsibilities for file
- Creating and deleting files and directories
- Providing access primitives (read,write,etc.)
- Mapping files to physical storage
- Managing permissions and backups'

# 1.5.4
## mass storage management
### what is mass storage?
- Hdds and nvm devices that store programs and data permanently.
- Os must manages them efficiently to ensure system performance.
### os responsibilities for mass storage
- Mounting/ unmounting storage
- Managing free space 
- Allocating storage blocks
- Disk scheduling 
- managing partitions
- Ensuring data protection 
### tertiary storage
- Example: tape drives, cd/dvd/blu-ray
- Used for backups and rarely-used data
- Os may or may not manage these


# 1.5.5
## cache management
### what is caching?
- Temporary storage of frequently accessed data in faster storage
- Improves access speed by avoiding slower memory or storage.
### cache levels:
1. Registers -> fastest, smallest, software-controlled
2. Cpu caches(L1/L2) -> hardware-controlled
3. Main memory
4. Secondary storage
### os involvement:
- Manages data movement from disk -> memory
- Not responsible for cpu-level caches (hardware does that)
- Must maintain consistency in multi core or distributed environments
- When multiple caches or copies exist, cache coherence must be ensured.

# 1.5.6
## i/o system management
### what is the i/o subsystem?
- Responsible for abstracting hardware differences.
- Makes device usage uniform for the os and apps
### i/o components
- Buffering: temporary storage during transfers
- Caching: speeding up repeated access
- Spooling: queuing data (like print jobs)
- Device driver interface: general interface
- Specific drivers: handle unique device characteristics
> only the device driver knows the exact details of its hardware the os uses a standard interface to interact with any device

### Final Summary:

|Component|OS Responsibilities|
|---|---|
|**Process**|Create, schedule, sync, communicate, delete|
|**Memory**|Track, allocate, deallocate, manage data movement|
|**File System**|Create/delete files & dirs, map to storage, control access|
|**Mass Storage**|Mount, free space, schedule, partition, protect|
|**Cache**|Manage high-speed access layers, ensure coherence|
|**I/O System**|Abstract hardware, manage drivers, buffer, cache|

# 1.6
## security and protection
When a system allows multiple users and concurrent processes, it must control access to data and resources this is done through two related concepts:
- Protection: internal rules that restrict access to system resources.
- Security: defending the system from unauthorized external or internal attacks

# 1.6.1
### what is protection?
protection controls how processes/users access:
- Files 
- Memory
- Cpu time
- I/o devices
### Examples of Protection Mechanisms:
- **Memory hardware** ensures a process can only use its own memory (no snooping on others).
- **Timers** prevent a process from hogging the CPU forever.
- **Device control registers** are protected from user access to prevent hardware misuse.

### os responsibilities for protection
- Define what access is allowed
- Enforce those rules automatically
- Prevent unauthorized use or erros between software components
- Protection also increases system reliability by:
	- preventing a faulty program from corrupting others 
	- isolating subsystems (like memory, cpu)

# 1.6.2
## security
### what is security?
Security protects the system from attacks -> both :
- Internal misuse(user abusing access)
- External threats(hackers, malware)
Even with proper protection, a system can be vulnerable if someone steals a password or id.

# 1.6.3
## User Identification
### How does the OS know who the user is?
- Every user has a **unique ID**:
    - UNIX/Linux: `UID`
    - Windows: `SID` (Security Identifier)
When a user logs in:
- OS verifies identity via **authentication**
- The **UID/SID** is then attached to all that user's processes and threads

Whenever needed, the system can translate UID ↔ Username.

# 1.6.4
## Group Identification
Sometimes it’s better to give access to **groups**, not just individuals.
### 📁 Group Access:
- A file owner may allow:
    - Full access to themselves
    - **Read-only** to certain groups
The OS must support:
- **Group IDs** (GID)
- One user can belong to **multiple groups**
- Group info is attached to all processes/threads the user creates

# 1.6.5
## Privilege Escalation
Some actions require **higher-level privileges**, like:
- Accessing restricted files or devices
- Changing system settings
### how os allows temporary privilege increase:
- **UNIX:** Uses `setuid` attribute:
    - A program runs with the **file owner’s ID**, not the current user’s
    - Useful for admin-level actions (like changing a password)
    - Extra privilege is **temporary** and only for that program
      
## Summary Table

|Concept|Description|
|---|---|
|**Protection**|Internal control over which user or process can access system resources|
|**Security**|Defense from attacks and unauthorized access (viruses, DoS, theft)|
|**UID / SID**|Unique ID for each user (used by OS)|
|**GID**|ID for user groups (used to assign group permissions)|
|**Privilege Escalation**|Temporarily raising permissions to perform restricted actions (e.g., `setuid`)|

# 1.7
## virtualization
Virtualization is a technology that **abstracts physical hardware** (CPU, RAM, disk, network, etc.) to create **multiple independent execution environments**. It gives the **illusion that each environment (called a virtual machine)** runs on its own private computer.
These environments can host **different OSs** (e.g., Windows, Linux) at the **same time** and may even interact with each other. The user can **switch between virtual machines just like switching processes** in a regular OS.

# 1.7.1
## why use virtualization
- It allows an OS to **run as an application** inside another OS.
- For example, you can run **Windows inside Linux** or **Linux inside Windows**.
- It seems unnecessary at first, but it's **widely used** and **highly beneficial**:
    - For **testing software** across multiple OSs
    - Running **legacy applications**
    - Providing **secure isolated environments**
    - Managing large **data centers and cloud servers**
      
# 1.7.3
## Virtual Machine Monitor (VMM)
- Also called a **hypervisor**.
- Software layer that:
    - Runs virtual machines (guests)
    - Allocates and manages resources (CPU, RAM, disk)        
    - **Isolates each VM** so they don't interfere
- Two types:
    - **Type 1 (bare metal):** VMM runs **directly on hardware** (e.g., **VMware ESX**, **XenServer**)
    - **Type 2:** VMM runs **as an app inside a host OS** (e.g., **VMware Workstation**, **VirtualBox**)
# 1.7.4
## Use Cases
- A developer using a Mac can run **Windows 10** inside a VM to test Windows apps.
- A company can run multiple OSs **on one server**, saving **hardware costs**.
- Cloud providers like AWS or Azure use virtualization to provide **isolated virtual servers** for customers.
# 1.7.5
## Virtualization in this Book
- The book provides a **Linux Virtual Machine** you can run on your personal computer.
- Regardless of your OS (Windows/macOS), you can run Linux and all its tools in a **virtualized environment**.
  
## Summary

Virtualization is essential in modern computing for running multiple operating systems on the same hardware. It improves:
- **Resource utilization**    
- **System flexibility**
- **Development and testing**
- **Cloud computing and data center management**


# 2.1
## operating system services
Os provides an environment for the execution of programs and it different from each os to another os.
![[IMG-20250531110932028.png]]
### user interface
Most os provide a (UI) to interact with the system.
- GUI: uses windows, mouse, keyboard and etc.
- Tochscreen interface: common on mobile devices
- Cli (command line interface): text-based input via keyboard
  some systems support more than one ui type
### program execution
The os must support **loading**, **running,** and **ending** a program.
- Termination may be normal or abnormal (due to an error).
### I/O operations
Program often need to perform input/output with files or devices.
- Os provides controlled access to i/o for safety and efficiency
- Example: reading a file, writing a printer, or network interface.
### file system manipulation
Os must allow:
- **Reading/writing** files and directories.
- **creating/deleting** files and directories
- **searching and listing** file info
- **access control**: permissions based on ownership
- Some OSs support **multiple file systems** with different features
### communications
Processes need to exchange data, either:
- Locally: between processes on the same machine
- Remotely: over a network
Communication method:
- **Shared memory**: processes share and access the same memory area
- **Message passing**: data packets are passed between processes.
### error detection
Errors can occur in:
- Hardware: memory faults, power failure
- Devices: disk error, printer issue
- Programs: illegal memory access, arithmetic errors
  the os must detect, handle, or report errors
- May terminate a faulty process
- Return error codes to allow programs to handle the issue
- Halt the system in critical cases
## system level services
### resource allocation
Multiple processes compete for system resources:
- Cpu, memory, file storage, i/o devices
- Os uses allocation routines(cpu scheduling algorithms)
- Manages peripherals like printers and usb devices
### logging
Tracks resource usage for:
- Accounting (billing users)
- Monitoring (system stats, optimization)
### protection and security
- Protection: prevent processes from interfering with each other or the os
- Security: prevent unauthorized access from outside users
	- authentication (passwords)
	- device security (network adapters)
	- logging access attempts to detect threats
	  security must be implemented throughout the system, as its only as secure as its weakest point.


# 2.2
## user and operating system interface
### cli
- Many Oss use a command interpreter (or shell) that runs at login or process initiation
- shells are special programs that interpret user commands:
	- c shell
	- bourne-again shell(bash)
	- korn shell
	- zsh
- Main function: get and execute commands such as create, delete, list, copy, execute.

### two implementation approaches:
1. Builtin commands: interpreter includes code for each command(larger interpreter)
2. External programs: interpreter just finds and runs an executable (rm file.txt: runs the rm as program with argument of file.txt)
### gui
- Gui provides a desktop based visual interface using:
	- icons, windows, menus, mouse pointers
	- users interact by clicking icons to open files, launch programs, or access functions.
**History:**
- First GUI → **Xerox Alto (1973)**
- Popularized by **Apple Macintosh (1980s)**
- **Windows 1.0** added GUI to MS-DOS
- macOS adopted **Aqua GUI**, UNIX-like kernel introduced later
**Open-source GUI for UNIX/Linux:**
- **KDE (K Desktop Environment)**
- **GNOME (GNU project)**
    - Both are modifiable under open-source licenses.

### tochscreen interface 
- Used primarily in mobile systems
- Interaction through gestures like
	- pressing, swiping, tapping
- Replaces traditional mouse/keyboard input
- Example: springboard interface on iphone/ipad

### choice of interface
- Often a matter of preference and user role:
	- system admins / power users -> prefer cli for efficiency and scriptability
	- general users -> prefer gui
- Shell scripting: cli can run sequences of commands from script files (common in unix/ linux)
- Some Oss support both:
	- windows: gui + cli
	- macos: aqua gui + terminal (cli)
- Mobile Oss: almost entirely touch-based; cli apps exist but are rarely used

>os interfaces can vary significantly but are generally abstracted away from the Os's core structure.
>designing a user friendly interface is a ui design task, not strictly an os level concern

# 2.3
## system calls
System calls are the ***interface between user programs and the operating system***.
They are often available through high level languages like c/c++, but some tasks may still require assembly language.
#### What does a system call do?
A **system call** is how a program requests a low-level service from the OS:
- Accessing files
- Creating a process
- Communicating between processes
- Reading input or writing output
System calls are handled **in kernel mode**, which is privileged.
But writing system calls directly is:
- Hard
- Platform-specific
- Unsafe

> [!EXAMPLE]
example of sys call use
A program copying data from `in.txt` to `out.txt` uses multiple sys calls:
> - user input: via keyboard, gui, or command line
> - file operations: open input, create/output file, error handling if file doesn't exist
> - interaction: prompt for overwrite confirmation, handle errors with sys calls
> - read/write loop: each read/write operation involves a sys call
> - close files: final write and terminate require sys calls

> even simple programs may involve many sys calls for i/o and control.

### application programming interface (api)
- Api is an abstraction layer providing access to os services through library functions.
- **API = Application Programming Interface**
- An API is a **set of functions** that a **programmer can use** to make requests to the operating system — **without directly writing system calls**.
	- **System call = wiring inside a machine**
	- **API = buttons on the control panel**
	  The buttons (API functions) give you controlled, easy access to powerful machine functions (system calls), without needing to deal with the messy wiring.
- Common apis:
	- windows api
	- posix api (unix/linux/macos)
	- java api
	- ex:
		- `CreateProcess()` (Windows API) → calls `NTCreateProcess()` (Windows kernel system call)
Benefit of using apis:
- Portability across systems
- Simplicity compared to raw sys calls
- Maintainability and abstraction 
Runtime environment (rte):
- Includes compilers, interpreters, libraries, loaders
- Intercepts api calls and passes them to the os kernel
- Uses a sys call interface and a sys call number table
  
#### What’s the connection between an API and system calls?
The **API acts as a wrapper** for system calls.
When you write something like this in C:
`read(fd, buffer, size);`
You're calling the **`read()` API function**.
But behind the scenes, this function:
- Prepares the parameters (like file descriptor, buffer, etc
- Switches to kernel mode
- Calls the **actual system call** (`read` system call in the kernel)
- Returns the result to your program
So:
> **You → call API → API → calls system call → OS kernel does the job**

### parameter passing techniques
- Registers: simplest, used when few params
- Memory block: store params in memory and pass address (used if many args)
- Stack: push params on a stack
> ex: linux uses registers if <= 5 params, block otherwise.

### types of system calls
#### process control
- **Create / Terminate process**
- **Load, execute** new programs
- **Get / set attributes** (priority, limits, etc.)
- **Wait / signal events**
- **Allocate / free memory**
- May involve memory dumps for debugging and error reporting
- CLI and GUI systems handle errors differently (pop-up, logs, etc.)
#### file management
- **Create / delete files and directories**
- **Open / close**
- **Read / write / reposition**
- **Get / set file attributes** (name, permissions, type, etc.)
#### device management
- **Request / release devices** (e.g., printers, disks)
- **Read / write / reposition** devices
- **Get / set device attributes**
- Some OSs treat **devices as files** for simplicity (UNIX-style)
#### information maintenance
- **Get / set system info:** time, date, version, memory, disk space
- **Debugging support:** memory dump, trace execution (e.g., `strace`)
- **Profiling:** time spent at various execution points using timer interrupts
- **Get / set process attributes**
#### communications
- Two models:
    - **Message-passing**: direct or via mailbox (e.g., `read message()`, `write message()`)
    - **Shared-memory**: `shared memory create()` and `attach()`
- Communication may involve:
    - **open / close connection**
    - **wait / accept connection**  
    - **client-server interaction**
- Message passing is better for **small data**, shared memory is faster for **larger transfers** but needs synchronization.
#### protection
- Ensures **safe access control** to resources
- **Set / get permission** for users and resources
- **Allow / deny user** access

> Applies to all systems, especially those connected to networks

### Examples of System Calls in Different OSes

|Function|Windows API|UNIX/Linux API|
|---|---|---|
|Process Creation|`CreateProcess()`|`fork()`|
|Process Termination|`ExitProcess()`|`exit()`|
|Wait for Process|`WaitForSingleObject()`|`wait()`|
|File Operations|`CreateFile()`, `ReadFile()`, `WriteFile()`, `CloseHandle()`|`open()`, `read()`, `write()`, `close()`|
|Device Management|`SetConsoleMode()`, `ReadConsole()`|`ioctl()`, `read()`|
|Info Maintenance|`GetCurrentProcessID()`|`getpid()`|
|Communication|`CreatePipe()`, `MapViewOfFile()`|`pipe()`, `mmap()`|
|Protection|`SetFileSecurity()`|`chmod()`, `umask()`|
### summery 

**System calls** are how programs request services from the operating system, like reading files, creating processes, or communicating between programs.

Most programs don’t call system calls directly — they use **APIs** (like `read()`, `write()`, `fork()`), which **wrap and trigger the actual system calls**.
System calls are grouped into six types:
- **Process control**
- **File management**
- **Device management**
- **Information maintenance**
- **Communication**
- **Protection**
They are the bridge between **user-level programs** and the **OS kernel**, and they're essential for running any real application.
# 2.4
## system services
System services (also called system utilities) sit above the operating system and provide tools for development, execution, and interaction. Some are simple wrappers for sys calls, while others are complex utilities. (provide a convenient environment for program development and execution)
#### file management
- Create , delete, copy , rename, list and print files and directories.
- Offers general file manipulation utilities
#### status information
- Retrieve system info: date, time, memory, disk space, active users.
- Some tools provide performance, debugging, and logging output
- May use guis or registries to display/configure this data
#### file modification
- Includes text editors and tools to modify file content
- May include search and text transformation commands
#### programming language support
- Compilers, debuggers, assemblers and interpreters
- Often builtin or available as add-ons
#### program loading and execution
- Tools to load and run programs:
	- loaders(absolute, relocatable, overlay)
	- linkage editors
	- debuggers for machine or high-level code
#### communications
- Enable users/processes to connect and share date
	- messaging, file transfer, email, remote login, browsing
#### background services
- Programs started at boot time, often run in the background
- Called services, daemons, or subsystems
	- network daemons (listen for connections)
	- print servers
	- process schedulers
	- error monitors
#### application programs
- Include common user tools:
	- web browsers, word processors, spreadsheets
	- databases, compilers, games, analysis tools
- These are not part of the os kernel, but use system services and resources and calls
#### user perspective
Users mostly see the os through guis and application programs, not sys calls:
- Macos,  windows, unix shell - all use same sys calls but offer different user interfaces
- A system may even run multiple os environments (dual boot or virtual machines) showing how the same hardware supports different user views

# 2.5
## linkers and loaders
Program must be moved from **disk to memory** to run on the cpu. This section explains the process from **compiling** to **execution**, including the roles of **linkers**, **loaders**, and **relocation**.
### compilation and object files
- Source files (e.g, `.c`) are compiled into relocatable object files (e.g,`.o`)
- Relocatable = can be loaded into any memory location
### linking
- The linker combines
	- multiple object files
	- external libraries (e.g, c standard library, math library with -lm)
- Produces a binary executable file (main, a.out, prog.exe)
### loading
- The loader places the executable into memory so the cpu can run it
- Relocation:
	- assign final memory addresses
	- adjusts code/data to match those addresses (so function calls and variable access work)
### execution flow on unix
1. You run a program
2. The shell uses `fork()` to create a new process
3. The shell uses `exec()` to invoke the loader
4. Loader:
	- loads the executable into the new process's memory
	- starts execution at the program's entry point.

> in gui systems, double-clicking an icon does the same using similar mechanisms.

### dynamic linking
- Instead of linking all libraries at build time,some libraries are:
	- linked only if needed at runtime
	- known as dynamically linked libraries(dlls) in windows
- Reduces memory and file size
- Multiple programs can share one loaded copy of the library

### executable formats
- **ELF** (executable and linkable format) -> used in linux/unix
	- contains: machine code + symbol table + entry point address
	- types:
		- relocatable elf(e.g, main.o)
		- executable elf(e.g, main)
- **PE** (portable executable) -> used in windows
- Mach-O -> used in macos

>linux tools:
>- file main.o -> shows its an elf relocatable file
>- file main -> shows its an elf executable
>- readelf -> gives detailed structure of elf files

# 2.6
## why applications are operating system specific
Apps usually cannot run across different operating systems, because every os has its own sys calls, binary formats, and apis.
### unique sys calls
- Sys calls are os specific
- Even similar tasks( like file access ) use different names, args, and formats on different oss.
### why can some apps run on multiple oss?
Apps can run on multiple systems only if one of these three methods is used:
1. Interpreted languages
	   - python, ruby
	   - interpreter exist for each os
	   - downside: slower and limited feature access
2. Virtual machine runtime
	   - java virtual machine (jvm)
	   - java apps run on any system with the jvm installed
	   - downside: still slower than native apps
3. Porting source code to each os
	   - write in a standard language (with posix api)
	   - recompile for each os
	   - downside: time consuming and needs separate builds + testing
### why portability is still hard
Even with those approaches, differences make apps os-specific
- Binary formats(elf, pe, mach-o) very between oss
- Instruction sets differ (intel vs arms cpus)
- Sys calls vary in naming, args, return values, and how they're invoked
- Apis and libraries are tied to os features(ios gui vs android gui)
  
### abi (application binary interface)
- Abi = low level interface for binaries (arch + os specific)
- Controls :
	- data type sizes
	- stack structure
	- sys call conventions
	- library linkage
- Apps must math the abi of the target os and cpu to work
>=> apps must be written, compiled or interpreted specifically for the target os + cpu.
>That why the same app needs to be individually built and tested for windows, macos, linux , ios, android and across cpu types like x86 and arm

# 2.7
## operating system design and implementation
This section discusses how operating systems are designed and implemented, the challenges faced,, and principles followed during development.
### design goals
- Os design begins by defining goals, which depend on:
	- system type (desktop, mobile, embedded, realtime)
	- hardware capabilities
**two goal categories:**
1. User goals:
   - easy to use, reliable, safe, fast
1. System goals
   - easy to design, maintain, efficient, flexible, error-free
> different systems have different priorities (windows server)

### mechanisms vs policies
- Mechanism: how to do something
- Policy: what to do (how long timer runs)
Why separate them?
- Separation = flexibility
- You can change policies without rewriting mechanisms
- Example: 
	- minix os (minix):
		- minimal mechanism, policy defined in modules/userspace
	- windows/macos:
		- mechanism + policy bundled tightly for consistent behavior
	- linux:
		- open source, you can change policies (replace scheduler)
> anytime resources are allocated, policy is involved. Mechanisms just perform the task.

### implementation
- Os = many programs, many developers -> implementation complexity
Language :
- Then : mostly assembly
- Now: mostly c/c++, some assembly
- Android:
	- kernel: c+ assemblydevug
	- libraries: c/c++
	- frameworks: java
Why higher level languages?
- Faster coding
- Easier to debug and port
- Compiler optimization helps performance
- Portability across hardware (intel, arm,etc.)
>performance-critical code (interrupt handler, memory manager) can still be tuned or written in low level code.

**trade-off:**
- Slightly lower speed or higher size vs much higher maintainability and portability

>performance gains come more from better algorithms and data structures, not just hand-coded assembly

# 2.8
## operating system structure
Modern operating systems are **large and complex**, so they are structure into **components (modules)** with clear interfaces. This helps manage complexity, enables easier debugging, and improves flexibility.
### monolithic structure
![[IMG-20250531182325600.png]]
- All os functionality in a single binary (kernel runs in one address space). : unix, linux
- Fast performance, but hard to extend or debug.
- Linux uses `glibc` for apps to talk to the kernel.
### layered approach
![[IMG-20250531182301363.png]]
- Os is divided into layers, where each layer only interacts with the one below : layer 0 = hardware, layer N = user interface
- Simplifies design and debugging but performance can suffer (layer traversal).
- Not widely used in pure form due to layer complexity and overhead.
### microkernels
![[IMG-20250531182358393.png]]
- Minimal kernel, most services run in user space (outside kernel).
- Communication via message passing.
- Easier to extend and secure (if a service crashes, kernel unaffected).
- Slower performance due to inter-process communication(ipc)
- Example : mach microkernel, qnx, part of macos/ios(darwin)
### modules
- Modern oses use loadable kernel modules(lkms)
- Core kernel +optional services loaded at runtime
- Combines the performance of monolithic with the flexibility of microkernels
- Used in linux, windows, macos
- Common use: device drivers, file systems
### hybrid systems
- Most real world oses uses a combination of the above models:
	- linux: monolithic + modular
	- windows: monolithic + microkernel-like subsystems
	- macos/ios: layered + hybrid kernel (mach +bsd)
### macOS and iOS
- Based on **Darwin**, a hybrid kernel (Mach + BSD UNIX)
- Have different **user interfaces** (Aqua vs. Springboard), and **architectures** (Intel vs. ARM)
- Provide **Cocoa** and **Cocoa Touch** APIs
- More restricted access on **iOS** (e.g., limited POSIX API)
### Android
- Open-source mobile OS by Google
- **Java-based** with a custom API and **ART** runtime
- Uses **.dex files** and **ahead-of-time (AOT)** compilation
- Built on a **modified Linux kernel**, with its own C library (**Bionic**)
- Uses **HAL** to abstract hardware for app portability
- Includes **Binder IPC**, used for secure communication between apps and services
### Windows Subsystem for Linux (WSL)
- Lets **Linux apps run on Windows 10** using **Pico processes**
- **LXSS** subsystem translates Linux system calls to Windows equivalents
- Enables bash shell and native ELF binaries to run inside Windows
- Handles system calls with **partial/full emulation or translation**

# 3.1
## process concept
### what is a process?
 A process is a program in the execution, unlike a static program file(which is just a list of instructions stored on disk), a process is an active entity:
- A program counter (telling which instruction to execute next)
- A set of cpu registers
- Memory space
- Associated resources (like open files, i/o devices)
Key difference:
- A program is passive (just code)
- A process is active (running code + environment)
Ex: if you run java program, you start a process -> the java virtual machine (jvm) -> which itself runs your program `program.class`

### memory layout of a process
The **memory layout of a process** refers to **how the operating system organizes the memory** assigned to a process — meaning, **how different types of data are stored and accessed in RAM** when a program is running.
When a program starts and becomes a process, the OS loads it into memory in a **structured way**. This structure usually includes **four main sections**:
1. Text: contains the executable code (code segment)
2. Data: global/static variables
3. Heap: for dynamically allocated memory during runtime(`malloc() in C`)
4. Stack: stores temporary data like function calls, params and local variables
- Text/data sizes are fixed
- Stack/heap sized grow and shrink dynamically
> the os must ensure stack and heap don't overlap

### multiple processes from one program
- Several users open the same browser app -> each one is a different process.
	 They share the same code but have different memory/data/states.
# 3.1.1
## process example
Running a c program `./a.out` or double clicking `prog.exe` launches the executable file into memory, making it a process.
In java, the jvm process runs and then loads and runs your java code. So java programs actually run inside a process.
# 3.1.2
## process state
As a process runs, it changes states:
1. New -> being created
2. Running -> instructions are executing
3. Waiting -> for some event(like i/o)
4. Ready -> waiting to be assigned a cpu
5. Terminated -> finished execution
> only one process per cpu core can be in the running state at a time
> many processes may be in the ready state, waiting for cpu time.

# 3.1.3
## process control block (pcb)
The os keeps all information about each process in a data structure called the pcb. It contains:
- Process state (ready,running,waiting,etc.)
- Program counter
- Cpu registers
- Scheduling info (like priority, pointers to queues)
- Memory info (page tables, base/limit registers)
- Accounting info (used cpu time,job id)
- I/o info (open files/devices)
The pcb is essential for multitasking: when the os switches from one process to another (called context switching), it save and loads data from pcbs.

# 3.1.4
## threads
Initially, processes were considered to have just one thread of execution (a single sequence of instructions). Modern oss now support multithreading:
- One process can contain multiple threads
- Threads share memory/resources but execute different parts of the program simultaneously
- Ex : a word processor might have one thread for typing input and another for spell-checking.
On multicore cpus, multiple threads can run truly in parallel
Each thread will have its own registers, stack, and scheduling info, but share memory with other threads in the same process.

# 3.2
## process scheduling
When multiple programs(processes) are in memory and ready to run ,the cpu can't run all of them at once (especially if there's only on cpu core). So the os needs a smart way to decide which process gets the cpu and when.
This decision making system is **called process scheduling**, and its handled by special part of the os called the **cpu scheduler**.
### purpose of process scheduling
- Maximize cpu usage: always have something running on the cpu.
- Support multitasking: quickly switch between processes so the user feels like everything is happening at once.
###  process behavior 
  Processes are usually:
- I/o-bound : spend more time waiting for input/output (waiting for the user to type something, reading a file from disk, downloading data from the internet)
- Cpu-bound: spend more time doing calculations (doing math or physics simulations, compressing a video, calculating 1 million digits of pi)
The os balances these types so the cpu stays busy while i/o-bound tasks wait for their i/o to complete
# 3.2.1
## scheduling queues
There are multiple queues in the os that manage process states:
#### **ready queue**
- Holds all processes that are ready to run, but waiting for the cpu.
- Os picks from this list when it needs a new process to run.
#### **wait queues (i/o queues)**
- Holds processes that are waiting for something else(disk read to finish)
- When the wait ends, the process returns to the ready queue.
#### **example flow:**
1. A process start and goes to the ready queue
2. It gets the cpu and runs.
3. It asks for i/o -> moved to wait queue
4. I/o completes -> back to ready queue
5. Eventually finishes -> removed from the system.
![[IMG-20250601143443797.png]]
# 3.2.2
## cpu scheduling
The cpu scheduler pick a process from the ready queue and gives it the cpu
**what does this happen?**
- Process finishes
- Process needs i/o
- A timer ([[#time slice]]) expires
- Another process becomes higher priority
[[#swapping]]
Sometimes, a process is temporarily removed from memory(to disk) to make space. Later, it can be swapped back in and resume. This helps manage memory if too many processes are loaded.
# 3.2.3
## context switch
When the cpu switches from one process to another, it needs to:
1. Save the current process's state(like register values, program counter)
2. Load the new process's state.
This is called a context switch.
The saved state is stored in the process control block (pcb)

> [!NOTE] 
> - context switches add [[#Overhead]] -> the cpu isn't doing useful work during the switch.
> - speed depends on hardware and os efficiency.
> - some cpus have multiple register sets to make this faster

![[IMG-20250601151154150.png]]
### Summary

|Concept|What It Does|
|---|---|
|**Process scheduling**|Decides which process runs next|
|**Ready queue**|Waiting-for-CPU processes|
|**Wait queue**|Waiting-for-I/O processes|
|**Context switch**|Saving/loading process states|
|**Swapping**|Temporarily moving processes in/out of memory|

# 3.3
## operations on processes
We focus on what os does with processes:
- How processes are created
- How they terminate
- Special rules around that
# 3.3.1
## process creation
When a process is running, it might create another process.
We call: 
- The original one: parent process
- The new one: child process
These processes form a tree structure, where one process can have many children, and those children might have children too.
### why create new processes?
To: 
- Run a program(like opening  chrome from your desktop)
- Handle a task separately
- Improve modularity(break work into smaller parts)
### each process has a unique id 
Called a pid(process id)-> its like a name tag for the os to identify and manage each process.
### parent vs. child: what do they share?
When a process creates a child: 
- It might share resources (like open files, memory areas)
- Or might give the child limited resources only
- It  can also pass initial data to the child (like file names, settings)
> this helps control the system load -> prevents processes from overwhelming the os
### what happens after creation?
1. The parent and child run together (concurrent execution)
2. Or the parent waits for the child to finish before continuing
Also, for the new process:
3. It can be a copy of the parent (same code & data)
4. Or it can run a different program
Ex: how it works in unix/linux
- To create a child, use: fork()
- To replace the child's memory with a new program, use: exec()
```C
pid = fork();         // Creates a new process
if (pid == 0)
    execlp("ls", "ls", NULL);  // The child runs the 'ls' command
else
    wait(NULL);        // The parent waits for the child to finish
```
**what does this do?**
- Creates a child process
- The child runs the `ls` command
- The parent waits for the child to complete
### on windows
Instead of fork() + exec(), there's just one function:
`CreateProcess()`
It creates a new process and runs a program immediately inside it. You pass it a lot of params, including the path to the executable and settings for the new process 
Ex: opening paint(mspaint.exe) in a new process

# 3.3.2
## process termination
Just like a process can be created -> it also has to be terminated(killed, shut down, removed)
**a process can terminate when:**
- It finishes its work normally(calls `exit()`)
- The use closes the program
- The os or parent forces it to stop
### what happens when a process terminates?
- All of its resources(ram,files,i/o) are freed up
- Its status is sent back to the parent (like:'i finished')
- It gets removed from the [[#process table]]
### zombie processes
**When a process finishes but its parent hasn't collected its exit status, it becomes a zombie**
Its dead, but still hanging in the process table -> waiting for its parent to clean it up using `wait()`
#remember 
### orphan processes
**If the parent process ends first, and the child is still running, we call the child an orphan.**
In linux, the system automatically adopts orphans using a special process called `init` (or `systemd`)
#remember 
### special case: android's process termination
In mobile systems like android, memory is limited, so the system sometimes has to kill processes to free up space.
Processes are ranked by importance:
1. Foreground(user is using it now)
2. Visible(supporting something visible)
3. Service(doing something like playing music)
4. Background(doing something, not visible)
5. Empty(just sitting here)
The system kills the least important first.
### Summary
- Processes are created using `fork()` (UNIX) or `CreateProcess()` (Windows)
- Parent and child can share or isolate resources
- A process ends by calling `exit()` or being killed
- If a child ends but parent doesn’t clean up → **zombie**
- If parent ends before child → **orphan**
- Mobile systems like Android prioritize which processes to kill

# 3.4
## interprocess communication (ipc)
### what is ipc?
Ipc is the way processes talk to each other and share data.
In a multitasking os, multiple processes often need to cooperate. To do that, they must communicate.
### independent vs. cooperating processes
- Independent process: doesn't share data or affect other processes 
- Cooperating process: can share data or be affected by others.
#### why allow cooperation?
1. Information sharing -> copy paste between apps
2. Speedup -> split a task across multiple processors
3. Modularity -> break a system into smaller pieces(like microservices)

### two main ipc modules
1. Shared memory
	   - processes share a region of memory.
	   - one writes, the other reads.
	   - fastest method -> no os involvement after setup.
	   - but processes must synchronize access (avoid writing at the same time)
> 	ex : a producer process puts data into a shared buffer, and a consumer takes it out.
2. Message passing
	   - processes send and receive messages.
	   - no shared memory
	   - os handles the communication
	   - easier to use in distributed systems(over networks)
	   - typically slower than shared memory.
	 > ex: chat apps exchanging messages, or a web client talking to a server. 
### Summary:

|Feature|Shared Memory|Message Passing|
|---|---|---|
|Speed|Very fast|Slower|
|Kernel Involvement|Only setup time|Needed every time|
|Usage|Same system|Can be across systems|
|Complexity|Higher (need sync)|Lower (easier logic)|
# 3.5
## ipc in shared memory systems
In shared memory ipc, multiple processes agree to share a portion of memory.
They then read and write to that shared memory directly to exchange information.
> its like two people working on the same whiteboard at the same time

### normally, processes can't touch each other's memory
Os protect each process's memory space to avoid accidental or malicious access.
To allow sharing, processes must explicitly agree to create and attach a shared memory segment.
### how does it works?
1. One process creates a shared memory region
2. Other processes attach it to their memory space.
3. All of them can then read/write to that shared segment.
>the os helps create and manage the memory region, but it does not manage what's written or when-> its your job to avoid collisions.

### synchronization is key
If two processes try to write to the same location at the same time, you'll get corrupt data.
To avoid this, we need synchronization tools like:
- Semaphores
- Mutexes
- Locks 
Ex: producer -> consumer problem
A classic case in os
Rules:
- Producer puts data in the shared buffer.
- Consumer takes data out of the buffer
Buffer types:
- Unbounded: no limit -> producer can always write.
- Bounded: limited size -> producer must wait if full.
Code setup:
Shared memory:
```c
#define BUFFER_SIZE 10
item buffer[BUFFER_SIZE];
int in = 0;
int out = 0;
```
- In points to where the producer will write next
- Out points to where the consumer will read next
Buffer is:
- Empty when: in == out
- Full when: (in + 1) % BUFFER_SIZE == out
### Summary

| Idea|Processes share a region of memory to exchange info|
|---|---|
| Benefit|Fast and efficient communication|
| Problem|Can mess up data without proper coordination|
| Solution|Use synchronization (take turns!)|
| Example|Producer puts items in buffer, Consumer takes them out|
# 3.6
## ipc in message passing systems
Processes can communicate with each other not just  by shared memory,  but also using messages. This is called message passing -> where they send and receive messages using sys calls
# 3.6.1
## naming
To send a message, processes must be able to refer to one another. There are two ways:
- Direct communication
	- processes must explicitly name each other.
	- syntax : send(p,message) -> send to process p & receive(q,message)->receive from process q
	- types: 
		- symmetric: both sender and receiver name each other
		- asymmetric: only sender names receiver; receiver accepts from anyone
	- downside: if you rename a process, you must update every place where its mentioned -> bad for modular design.
- Indirect communication
	- messages are sent to mailboxes(also called ports) instead of directory to a process.
		- syntax: send(a,message) -> send to mailbox A , receiver(a,message) -> receive from mailbox A
		- benefits:
			- processes don't need to know about each other
			- many processes can share the same mailbox
		- ownership:
			- process-owned mailbox owned by a process, deleted when the process ends.
			- os-owned mailbox: created/deleted through sys calls; not tied to a specific process
# 3.6.2
## synchronization
When sending and receiving messages, synchronization can happen in different ways:
- Blocking(synchronous) communication
	- blocking send: sender waits until message is received
	- blocking receive: receiver waits until messages arrives
	  this is like a live phone call -> both sides must be active
- Non blocking (asynchronous) communication
	- non-blocking send: sender sends message and moves on 
	- non-blocking receive: receiver checks for a message and moves on if there's none
	  this is like leaving a voicemail -> no need for both to be online
	  if both send and receive are blocking -> its called a rendezvous (they meet at the same time)
# 3.6.3
## buffering
Messages are stored temporarily in a queue (buffer), the buffer can have different capacities:
1. Zero capacity
	   - no waiting allowed.
	   - sender blocks until receiver gets message
2. Bounded capacity(e.g, size=10)
	   - fixed buffer size
	   - if full -> sender must wait
3. Unbounded capacity
	   - infinite buffer.
	   - sender never blocks -> always room for more messages
#### **Conclusion:**
- Message passing is useful for both local and distributed systems.
- It avoids the complexity of shared memory.
- It can be blocking or non-blocking and uses buffers for temporary message storage.
# 3.7
## posix shared memory
### what is it?
Posix shared memory is and ipc method where two or more processes share a region of memory to communicate directly
### how it works
1. Create a shared memory object:
   ```c
   fd = shm_open(name, O_CREAT | O_RDWR, 0666);
   ```
	- `name`: shared memory name.
	- `O_CREAT`: create if not exists.
	- `O_RDWR`: open for reading/writing.
	- Returns a **file descriptor** (like an ID for that memory region).
2. Set the size of memory
   ```c
	Ftruncate(fd, 4096);
	```
	- sets the size to 4096 bytes (4 kb)
3. Map the memory to the process address space
   ```c
    ptr = mmap(...);
    ```
    - `ptr` now points to the shared memory block.
	- Both processes can now **read/write** to `ptr`
4. Remove the memory object(done by consumer after use)
   ```c
	shm_unlink(name);
	```

Ex: 
- Producer : writes "hello world" into shared memory.
- Consumer : read from the shared memory and then unlinks it
   this method is very fast after setup -> no kernel help needed once shared memory is established.
# 3.7.4
## pipes
Pipes are older and simpler ipc methods, used to send a stream of data between two processes.
# 3.7.4.1
## ordinary (anonymous) pipes
### what is it?
- One way communication (unidirectional)
- Used between parent and child processes on the same machine
### how to use
1. Create pipe:
   ```c
   	pipe(int fd[2]);
	```
	- `fd[0]`: read end
	- `fd[1]`: write end
2. Use fork() to create child process.
3. Parent writes to `fd[1]`, child reads from `fd[0]`
> both processes should close unused ends of the pipe

# 3.7.4.2

## **Named Pipes (FIFOs)**
### 🧠 What Is It?
- More powerful than anonymous pipes.
- Can be **bidirectional**.
- Do **not require parent-child** relationship.
- **Persist** after processes end (until explicitly deleted).    
### 🔧 On UNIX
- Use `mkfifo()` to create.
- Appears as a **file** in the file system.
- Communicate using `read()` and `write()`.
### 🔧 On Windows
- Created using `CreateNamedPipe()`.
- Supports **full-duplex** and **network communication**.
- Allows **multiple writers/readers**.
### Summary

|Feature|Ordinary Pipe|Named Pipe|
|---|---|---|
|Direction|One-way|Bidirectional|
|Process Relation|Parent–Child only|No relation required|
|Persistence|Ends with processes|Stays until deleted|
|Communication Scope|Same machine|Same or networked machines (Windows)|

# 4.1
## overview
### what is thread?
A thread is the smallest unit of cpu execution. It includes:
- A unique id
- A program counter (tells where the thread is in its instruction stream)
- A register set (holds current working data)
- A stack (stores temporary data like method calls and local variables)
All threads inside the same process share:
- Code
- Data
- System resources (e.g, files, memory, signals)
In a single-threaded process, there's only one flow of control (only one thing can happen at a time)
In a multithreaded process, multiple threads can do different tasks at the same time within one process.

# 4.1.1
## motivation
### why use threads?
Today, most apps are multithreaded because:
- They need to do many things at once
- Systems have multicore cpus, which can run many threads at the same time.
- Ex:
	- a photo app creates separate threads to generate thumbnails for each image.
	- a web browser uses threads for:
		- loading text
		- fetching images
		- handling user interaction
	- a word processor may have:
		- one thread for typing input
		- another for spell checking
		- another for saving the document in the background
	- web server example:
		- a single threaded web server handles one user at a time. If many users request a page, they have to wait.
		- with threads, the server can:
			- keep one thread listening
			- create a new thread for each request (fast and efficient)
			- serve thousands of clients without using too much memory.
  ![[Pasted image 20250602114033.png]]
# 4.1.2
## benefits of multithreading
1. Responsiveness -> keeps apps responsive even when doing slow tasks in the background
2. Resource sharing -> threads inside a process share memory/resources easily
3. Economy -> cheaper than creating new processes. Thread creation and switching is faster.
4. Scalability -> on multicore cpus, threads can run in parallel to boost performance.
### summary
Threads are lightweight and efficient. Instead of running multiple processes, we can use threads inside one process to perform tasks in parallel. They are essential in modern software to fully use the power of multicore cpus.

# 4.2
## multicore programming
### main idea:
Modern systems often have multiple processing cores, and using multithreaded programming helps us take advantage of them.
### concurrency vs. parallelism
- Concurrency: multiple tasks make progress at once (may or may not run at the exact same time).
- Parallelism: multiple tasks actually run at the same time on different cores.
# 4.2.1
## programming challenges
When writing code for multicore systems, you face these challenges:
1. Identifying tasks: break work into parts that can run independently.
2. Balancing tasks: make sure all parts are roughly equal in size/work.
3. Data splitting: share data efficiently between cores.
4. Data dependency: some tasks rely on others; syncing is required.
5. Testing & debugging: its harder to test parallel programs.
# 4.2.2
## types of parallelism
### data parallelism 
- Some operation on different parts of data.
- Ex: splitting an array and summing parts on different threads
### task parallelism
- Different tasks(functions) run in parallel.
- Ex: one thread sorts, another calculates statistics
Apps can even use both types together.

# 4.3
## multithreading models
This section discusses how user-level threads are connected to kernel-level threads.
Threads can be created and managed either by user programs (user threads) or by the os itself (kernel threads). We need a way to map user threads to kernel threads. 
# 4.3.1
## many to one model
- How it works: many user threads are mapped to one kernel thread
- Managed by: a user level library (so its fast and doesn't need os involvement)
- Drawbacks: 
	- if one thread block(waiting for i/o), all threads block
	- no parallelism possible on multicore systems.
- Used by: old java implementations (green threads)
- Pro: simple and how overhead
- Con: no true concurrency or parallelism

# 4.3.2
## one to one model
- **How it works:** Each user thread maps to its **own** kernel thread.
- **Benefits:**
    - True parallelism: threads can run simultaneously on different CPU cores.
    - When one thread blocks, others can still run.
- **Drawback:** Creating too many threads can overload the system.
- **Used by:** Windows, Linux, macOS.
- **Pro:** Better concurrency and scalability.
- **Con:** Higher overhead (each thread = kernel thread

# 4.3.3
## many to many model
- **How it works:** Many user threads are mapped to **a pool** of kernel threads.
- **Advantages:**
    - Combines benefits of the previous two models.   
    - Developers can create many user threads without worrying about kernel limits.    
    - Multiple threads can run in parallel.    
- **Variation:** **Two-level model** – some user threads can be bound to specific kernel threads.
- **Pro:** Flexibility and efficiency.
- **Con:** Harder to implement and less common today.

# 4.4
## thread libraries
### main media
A **thread library** provides a set of functions (API) that a programmer can use to create and manage threads. These functions help in:
- Creating new threads
- Terminating threads
- Synchronizing threads (like joining, waiting)
There are **main ways** these libraries are implemented:
# 4.4.1
## user threads vs. kernel threads
### User-Level Thread Library:
- Works in **user space** (outside the OS).
- Very **fast** because no system calls are needed.
- The OS is **not aware** of these threads.
- **Problem**: if one thread blocks (e.g., for I/O), all threads in the process might stop.
###  Kernel-Level Thread Library:
- Threads are **managed by the OS kernel**.
- Creating, destroying, or switching threads involves **system calls** (slower).
- The OS **knows each thread**, so it can schedule them independently.
- If one thread blocks, others can still run.
# 4.4.2
## POSIX Threads (Pthreads)

- A **standard** threading library used in **UNIX/Linux/macOS** systems.
- Can be implemented at **user level**, **kernel level**, or a **hybrid**.
### Example:
To create a thread using Pthreads:
```C
pthread_create(&tid, NULL, do_work, NULL);
```
This line starts a new thread and runs the `do_work` function.
Pthreads also provide:
- `pthread_join()` → Wait for a thread to finish.
- `pthread_mutex_lock()` and `pthread_mutex_unlock()` → For locking resources.

# 4.4.3
## windows and java threads
### Windows Threads:
- Created using the `CreateThread()` function.
- Managed directly by the **Windows kernel**.
- Threads in the same process share memory and resources.
### Java Threads:
- Java provides a high-level API for threads.
- You can create a thread by:
    - Extending the `Thread` class
    - Implementing the `Runnable` interface
- Java threads are **mapped to native threads** on the system:
    - On Linux, often mapped to Pthreads.
    - On Windows, mapped to Windows threads.
Ex: 
```C
public class MyThread extends Thread {
  public void run() {
    System.out.println("Thread is running");
  }
}```


# 5.1
## basic concepts
### when does cpu scheduling happen?
there are four main situations where cpu scheduling is needed:
1. a process moves from running to waiting (e.g, waiting for i/o)
2. a process moves from running to ready (e.g, its interrupted)
3. a process moves from waiting to ready (e.g, its done)
4. a process finishes and exits
scheduling happens in all cases except #1 because in #1 the process gives up the cpu by itself
### two types of scheduling
- non preemptive scheduling
	- once a process gets the cpu, it keeps it until it finishes or switches to waiting.
	- simple, but not great for responsiveness.
- preemptive scheduling
	- the os can forcefully take the cpu from a process
	- allows better system responsiveness and multitasking
### dispatcher
after the scheduler chooses a process, the dispatcher:
- gives control of the cpu to that process.
- does things like:
	- switching context (saving and restoring process info)
	- switching to user mode
	- jumping to the correct location in the new process
this process introduces a small delay, called dispatch latency (typically < 1ms)
### how it all fits together
think of cpu scheduling like a manager assigning tasks:
- scheduler chooses who should work next
- dispatcher gives that person the tools to start working
- processes go in and out depending on their needs and availability
# 5.2
## scheduling criteria 
### what is it about?
this section introduces criteria used to evaluate and compare different cpu scheduling algorithms. these criteria help decide which algorithm is better depending on the system's goal
### main criteria
1. cpu utilization
	   - goal: keep the cpu as busy as possible
	   - ideal: between 40% (light load) to 90% (heavy load)
	   - why it matters: a busy cpu means the system is productive.
2. throughput
	   - what it means : number of processes completed per time unit.
	   - high throughput = more work done
	   - ex: 10 short task per second vs. 1 long task every few seconds.
3. turnaround time
	   - definition: total time from process submission to completion.
	   - includes time waiting + time using cpu + doing i/o
	   - goal: keep it as short as possible for user satisfaction
4. waiting time
	   - definition: time spent only waiting in the ready queue (not running, not doing i/o)
	   - goal: lower waiting time = faster response
5. response time
	   - used in interactive systems
	   - definition: time from submitting a request to the first response (not full completion)
	   - goal: make the system feel responsive.
### Summary Table:

|Criterion|What We Want|
|---|---|
|CPU Utilization|Maximize|
|Throughput|Maximize|
|Turnaround Time|Minimize|
|Waiting Time|Minimize|
|Response Time|Minimize|

### how they connect:
- some criteria can conflict (e.g, high throughput might increase response time)
- when choosing a scheduling algorithm, trade-offs are necessary.
- interactive systems prefer low  response time; batch systems may prefer high throughput

# 5.3
## scheduling algorithms
### what is cpu scheduling?
cpu scheduling decides which process in the ready queue should be assigned to the cpu next. since only one process can use the cpu at a time (on a single core system), this scheduling is vital for system performance and fairness.
# 5.3.1
## first come, first served(fcfs)
- how it works: the process that arrives first is executed first(like a queue)
- type: non preemptive
- issue: long processes can block short ones( called convoy effect)
- implementation: fifo (firs in, first out) queue
# 5.3.2
## shortest job first(sjf)
- how it works: runs the process with the shortest next cpu burst.
- type: can be preemptive or non preemptive
	- preemptive version is called shortest remaining time first (srtf)
- pros: minimizes average waiting time (optimal)
- cons: hard to predict cpu burst time accurately
# 5.3.3 
## round robin(rr)
- how it works: each process gets the cpu for a fixed time quantum. if it doesn't finish, it goes to the end of the queue.
- type: preemptive
- good for: time sharing systems
- challenge: choosing a good quantum size
	- too short = too many context switches
	- too long = behaves like fcfs
# 5.3.4
## priority scheduling
- how it works: each process has a priority number, and the cpu is assigned to the process with the highest priority
- type: can be preemptive or non preemptive
- problem: risk of starvation (low priority processes never get cpu)
- solution: aging -> increase the priority of waiting processes over time
# 5.3.5
## multilevel queue scheduling
- how it works: processes are divided into different queues based on type (foreground,background,system,etc.)
- each queue: has its own scheduling algorithm
- strict order: higher priority queues are served first

# 5.3.6
## multilevel feedback queue scheduling
- more advanced version of multilevel queue
- key idea: a process can move between queues based on behavior(e.g, how much cpu it uses)
- good for: adapting to both cpu-bound and i/o bound tasks dynamically


##  What is a Gantt Chart in CPU Scheduling?

A **Gantt chart** is a **timeline chart** that shows which process runs **at what time** on the CPU.
Think of it like a **train schedule**. Each process gets a turn to use the CPU and we show their turns on a horizontal line, based on the scheduling algorithm.
## ✍️ How to Draw It (Step-by-Step)
### 📌 Example Setup:
Let’s say you have **3 processes**:

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|5|
|P2|1|3|
|P3|2|1|

We’ll use **FCFS** (First Come First Served) as our first example.
### 🧮 Step 1: Sort by Arrival Time
P1 arrives first at time 0  
Then P2 at time 1  
Then P3 at time 2
So FCFS order is: **P1 → P2 → P3**
### 📊 Step 2: Draw the Timeline (Gantt Chart)
Start from **time 0**, move right with each process’s burst time:
```
| P1 |------5------| P2 |--3--| P3 |-1-|
  0             5     8     9
```

So:
- P1 runs from 0 to 5
- P2 runs from 5 to 8
- P3 runs from 8 to 9

### 🕓 Step 3: Calculate Times
#### ✅ Turnaround Time (TAT) = Finish Time - Arrival Time
- P1: 5 - 0 = 5
- P2: 8 - 1 = 7
- P3: 9 - 2 = 7
#### ✅ Waiting Time (WT) = Turnaround - Burst
- P1: 5 - 5 = 0
- P2: 7 - 3 = 4
- P3: 7 - 1 = 6
#### ✅ Response Time (RT) = First Time on CPU - Arrival
- P1: 0 - 0 = 0
- P2: 5 - 1 = 4
- P3: 8 - 2 = 6
## 🌀 Now Try Round Robin (RR)
Use the same processes, but time quantum = 2.

|Process|Arrival Time|Burst Time|
|---|---|---|
|P1|0|5|
|P2|1|3|
|P3|2|1|

**Step 1: Start queue at time 0 with P1.**
**Step 2: Use quantum = 2. Move in a cycle.**
```
| P1 |2| P2 |2| P3 |1| P1 |2| P2 |1| P1 |1|
  0   2   4   6   7   9   11 12  13
```
(Details for burst left after each slice)
## ✏️ How to Draw on Paper
- Draw a horizontal line
- Start at 0
- Write boxes with process names and durations
- Mark time at each border
- Make sure you **account for arrival time**
- Use a queue to track which process is ready
## 🎯 Practice Challenge
Try this on paper:

|Process|Arrival|Burst|
|---|---|---|
|P1|0|4|
|P2|1|5|
|P3|2|2|

Try:
1. FCFS
2. SJF (non-preemptive)
3. RR with quantum = 2

Want me to walk you through one of them live right now? I can draw the Gantt and calculate all values for you. Just say the algorithm.