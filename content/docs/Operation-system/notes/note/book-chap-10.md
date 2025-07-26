---
title: book, chap 10
description: book, chap 10
---


# Chapter 10: Virtual Memory 🖥️💫

## 10.1 Background 🌟

### Virtual Memory Concepts

#### Definition and Purpose
- **Virtual Memory**: Technique allowing execution of processes not completely in memory
- **Benefits**: 
  - Programs larger than physical memory can execute
  - Increased CPU utilization and throughput
  - Less I/O needed for swapping processes

#### Key Advantages
- **Program size independence**: Programs no longer constrained by physical memory size
- **Memory efficiency**: Only needed parts of program loaded
- **Multiprogramming improvement**: More processes can run simultaneously
- **Resource optimization**: Better CPU and I/O device utilization

#### Implementation Foundation
- **Demand paging**: Most common implementation
- **Demand segmentation**: Alternative approach
- **Lazy loading**: Load pages only when referenced

### Virtual Address Space
- **Logical view**: Process sees large, uniform address space
- **Physical reality**: Pages scattered throughout physical memory and storage
- **Address translation**: Hardware and OS cooperate to maintain illusion
- **Benefits**: Simplified programming model, memory sharing, protection

## 10.2 Demand Paging

### 10.2.1 Basic Concepts 📋

#### Demand Paging Fundamentals
- **Lazy swapper**: Load pages only when needed (never swap entire process)
- **Pager**: System component that handles page loading
- **Page fault**: Interrupt when accessing page not in memory
- **Working set**: Set of pages currently being used by process

#### Page Loading Strategy
- **Anticipatory loading**: Could predict and pre-load pages
- **Demand loading**: Wait until page actually referenced
- **Trade-off**: Storage overhead vs. unnecessary I/O

#### Valid-Invalid Bit Scheme
- **Valid (v)**: Page is in memory and legal
- **Invalid (i)**: Page either not in memory or not in address space
- **Page table entry**: Contains frame number and valid-invalid bit
- **Initially**: All entries set to invalid

#### Demand Paging Process
1. **Memory reference**: Process references a page
2. **Check validity**: Hardware checks valid-invalid bit
3. **Valid reference**: Proceed normally
4. **Invalid reference**: Generate page fault trap
5. **OS handling**: Determine if reference was valid
6. **Page loading**: If valid, load page from storage
7. **Update structures**: Modify page table and TLB
8. **Restart instruction**: Resume interrupted instruction

#### Hardware Requirements
- **Page table**: With valid-invalid bits
- **Secondary memory**: To hold pages not in memory
- **Page fault handling**: Interrupt mechanism
- **Instruction restart**: Ability to restart interrupted instruction

### Performance of Demand Paging

#### Effective Access Time Calculation
- **p**: Page fault rate (0 ≤ p ≤ 1)
- **ma**: Memory access time
- **Page fault time**: Time to service page fault

**Formula**: Effective Access Time = (1-p) × ma + p × page fault time

#### Page Fault Service Time Components
1. **Trap handling**: Save registers, determine fault type
2. **Page location**: Find page on secondary storage
3. **Disk I/O**: Read page from disk to memory
4. **Table updates**: Update page and frame tables
5. **Instruction restart**: Resume interrupted instruction

#### Performance Example
```
Memory access time: 200 nanoseconds
Page fault service time: 8 milliseconds = 8,000,000 nanoseconds
Page fault rate: 1 in 1000 (p = 0.001)

Effective access time = 0.999 × 200 + 0.001 × 8,000,200
                      = 199.8 + 8000.2 = 8200 nanoseconds
```

## 10.4 Page Replacement

### 10.4.1 Basic Page Replacement 🔄

#### Need for Page Replacement
- **Over-allocation**: More pages requested than frames available
- **Memory full**: No free frames for new pages
- **Solution**: Select victim page to remove from memory
- **Goal**: Minimize page fault rate

#### Basic Page Replacement Algorithm
1. **Find location**: Locate desired page on secondary storage
2. **Find free frame**: 
   - If free frame exists, use it
   - If no free frame, use page replacement algorithm
3. **Victim selection**: Choose page to remove (victim page)
4. **Write victim**: If victim page modified, write to secondary storage
5. **Update tables**: Mark victim page as invalid
6. **Load new page**: Read desired page into freed frame
7. **Update tables**: Update page table for new page
8. **Restart process**: Continue user process from interrupt

#### Frame Allocation and Reference Bits
- **Reference bit**: Set when page is accessed
- **Modify bit (dirty bit)**: Set when page is written to
- **Optimization**: Don't write clean pages to disk
- **Two I/O operations**: May be needed per page fault (write + read)

### 10.4.2 FIFO Page Replacement 📥📤

#### First-In-First-Out Algorithm
- **Strategy**: Replace oldest page in memory
- **Implementation**: Queue of pages, replace head of queue
- **Advantage**: Simple to understand and implement
- **Disadvantage**: May replace heavily used pages

#### FIFO Implementation
- **Page queue**: Maintain queue of pages in order of arrival
- **Replacement**: Always replace page at head of queue
- **New page**: Add to tail of queue
- **No consideration**: Page usage frequency ignored

#### Belady's Anomaly
- **Definition**: More frames sometimes result in more page faults
- **Example**: 
  - 3 frames: 1,2,3,4,1,2,5,1,2,3,4,5 → 9 page faults
  - 4 frames: 1,2,3,4,1,2,5,1,2,3,4,5 → 10 page faults
- **Cause**: FIFO doesn't consider page usage patterns

#### FIFO Example
```
Reference string: 7,0,1,2,0,3,0,4,2,3,0,3,2,1,2,0,1,7,0,1
Frames: 3

Step-by-step execution:
7: [7, -, -] (fault)
0: [7, 0, -] (fault)  
1: [7, 0, 1] (fault)
2: [2, 0, 1] (fault, replace 7)
0: [2, 0, 1] (hit)
3: [2, 3, 1] (fault, replace 0)
...

Total page faults: 15
```

### 10.4.3 Optimal Page Replacement 🎯

#### Optimal Algorithm (OPT)
- **Strategy**: Replace page that will not be used for longest period
- **Alternative name**: Furthest-in-future algorithm
- **Theoretical**: Cannot be implemented in practice
- **Purpose**: Benchmark for other algorithms

#### Optimal Algorithm Properties
- **Lowest page fault rate**: Never suffers from Belady's anomaly
- **Future knowledge**: Requires complete knowledge of reference string
- **Benchmark use**: Compare performance of other algorithms
- **Implementation**: Only possible with known reference patterns

#### Optimal Example
```
Reference string: 7,0,1,2,0,3,0,4,2,3,0,3,2,1,2,0,1,7,0,1
Frames: 3

Analysis:
7: [7, -, -] (fault)
0: [7, 0, -] (fault)
1: [7, 0, 1] (fault)
2: [2, 0, 1] (fault, replace 7 - used furthest in future)
0: [2, 0, 1] (hit)
3: [2, 0, 3] (fault, replace 1 - used furthest in future)
...

Total page faults: 9 (optimal)
```

#### Comparison with Other Algorithms
- **FIFO**: 15 page faults (same reference string)
- **Optimal**: 9 page faults
- **Improvement**: 40% reduction in page faults
- **Practical value**: Shows potential for improvement

### 10.4.4 LRU Page Replacement ⏰

#### Least Recently Used Algorithm
- **Strategy**: Replace page that hasn't been used for longest time
- **Principle**: Recent past as approximation of near future
- **Advantage**: Good approximation to optimal algorithm
- **Challenge**: Implementation complexity

#### LRU Implementation Methods

#### Method 1: Counter Implementation
- **Counter**: Associate counter with each page table entry
- **Clock**: Logical clock or counter incremented for each memory reference
- **Update**: Copy clock value to counter when page referenced
- **Replacement**: Choose page with smallest counter value
- **Overhead**: Search through all counters required

#### Method 2: Stack Implementation
- **Stack**: Keep stack of page numbers
- **Reference**: Move referenced page to top of stack
- **Structure**: Most recently used at top, least recently used at bottom
- **Replacement**: Remove page from bottom of stack
- **Implementation**: Use doubly linked list for efficiency

#### LRU Example
```
Reference string: 7,0,1,2,0,3,0,4,2,3,0,3,2,1,2,0,1,7,0,1
Frames: 3

Counter method tracking:
7: [7(1), -, -] (fault)
0: [7(1), 0(2), -] (fault)
1: [7(1), 0(2), 1(3)] (fault)
2: [2(4), 0(2), 1(3)] (fault, replace 7 - oldest counter)
0: [2(4), 0(5), 1(3)] (hit, update counter)
3: [2(4), 0(5), 3(6)] (fault, replace 1 - oldest counter)
...

Total page faults: 12
```

#### Hardware Support Options

#### Full Hardware Support
- **Register**: Each page has time-of-use register
- **Update**: Hardware updates register on every memory reference
- **Cost**: Expensive due to hardware complexity

#### Limited Hardware Support
- **Reference bit**: Single bit per page
- **Clock algorithm**: Approximate LRU using reference bits
- **Efficiency**: Good performance with minimal hardware

#### Software Implementation
- **Interrupt**: Every memory reference causes interrupt
- **Update**: Software updates page access information
- **Cost**: Too expensive for practical use

#### LRU Approximation Algorithms

#### Second-Chance Algorithm (Clock Algorithm)
- **Reference bit**: Use reference bit with FIFO
- **Process**: If reference bit = 0, replace page
- **Second chance**: If reference bit = 1, clear bit and move to next
- **Implementation**: Circular queue of pages

#### Enhanced Second-Chance Algorithm
- **Two bits**: Reference bit and modify bit
- **Classes**:
  - (0,0): Neither recently used nor modified (best choice)
  - (0,1): Not recently used but modified (write required)
  - (1,0): Recently used but clean
  - (1,1): Recently used and modified (worst choice)
- **Selection**: Choose lowest class available

#### Performance Characteristics
- **LRU**: Generally good performance, close to optimal
- **Implementation cost**: High without hardware support
- **Approximations**: Clock and enhanced clock algorithms provide good alternatives
- **Stack property**: LRU never suffers from Belady's anomaly

---

## Key Takeaways 🎯

### Memory Management Fundamentals
- **Address binding** can occur at compile time, load time, or execution time
- **Dynamic loading** improves memory utilization by loading routines only when needed
- **Swapping** allows processes larger than memory but requires careful I/O management

### Paging System Benefits
- **Eliminates external fragmentation** through fixed-size pages and frames
- **TLB caching** critical for performance - hit ratios of 90%+ essential
- **Memory protection** and sharing enabled through page table attributes

### Virtual Memory Advantages
- **Demand paging** loads pages only when referenced, enabling larger virtual address spaces
- **Page replacement algorithms** critical for performance when memory is full
- **LRU approximation** provides good performance with reasonable implementation complexity

### Performance Considerations
- **Page fault rate** directly impacts system performance - 1% can cause 40× slowdown
- **Working set** management crucial for avoiding thrashing
- **Hardware support** (TLB, reference bits) essential for practical virtual memory systems