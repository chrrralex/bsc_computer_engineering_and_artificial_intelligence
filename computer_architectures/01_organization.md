# 01. Organization

### 01.01. Processor

**CPU (Central Processing Unit)**: from the logical point of view, a CPU is the brain of a digital system. It's the hardware dedicated to the computation and to the instructions execution. Often, the term "CPU" isn't used to indicate the hardware chip (processor, or microprocessor) in the computer, but it's used to indicate the processing unit of the system from a logical point of view. From the logical point of view, a CPU is composed by the following subcomponents:

- CU (Control Unit): a component internal to the processor that coordinates the signal from and to the CPU.
- ALU (Arithmetic-Logic Unit): a component internal to the processor that performas calculations and process one, two, or more operands.
- Registers: small memory directly installed in the same chip of the ALU and the CU. The ALU can access directly and quickly to each register. Each register has a limitated capacity, often between 8 and 512 bits (or 1 and 64 Bytes).

We use the term "CPU" to indicate a generic computation unit from the logical point of view (it can be a processor, a singlecore processor, a multicore processor, or a multicomputer system).

**Data Path**: the ALU of a processor is an highly-structured component. The ALU is structured as a data path: a path followed by the data during the execution of a specific instruction. The data path starts from the registers, where the operands and the partial results are stored, fetched and inserted into the ALU's buses. The ALU's buses are tipically called bus A and bus B and, sometimes, there is a third bus called bus C. The ALU has two, or three registers as inputs: bus A carries the first operand (A operand) from a register to the first input of the ALU; bus B carries the second operand (B operand) from a register to the second input of the ALU. Systems equipped with the bus C has an ALU accepting a third operand (C operand) and this bus carries the third operand from a register to the third input of the ALU.

The following figure represents two types of data path:

<!-- to add -->
*In Figure - On left side: a data path with bus A and bus B (ALU with two operands). On right side: a data path with bus A, bus B and bus C (ALU with three operands)*

After the ALU executes the current instruction of the program (stored in the central memory), the result is stored in the output register of the ALU. For example, if the current instruction is the sum between A, B and C operands, the output register of the ALU has the following result: A + B + C. Another bus of the ALU carries the output of the current instruction to a specific register, or in a specific location of the central memory (it depends of the executed instruction).

**Registers**: a register is a small and quick memory located near the ALU. Modern ALUs have different types of registers:

- PC (Program Counter): a relative poiner register indicates the next instruction to fetch and execute. Each time a new instruction is fetched for its execution, the PC is incremented by one. Exist some isntructions that allow the program to add a different offset than 1 to the PC (for example, for the jump instruction).
- IR (Instruction Register): contains the current instruction in the execution phase. An instruction can have zero, one, two, or more operands. 
- ACC (ACCumulator): a counter register, or accumulator register used by one, two, or more instructions.
- GPRs (General Purposes Registers): working registers used to store operands and partial results. GPRs follow a specific nomenclature: tipically each register is called Rn, where "n" is a number that starts from 0 and ends to the number of GPRs installed in the chip, decremented by one. For example, if the CPU has 64 GPRs (also called working registers), there are from R0 to R63 registers.
- A register: the A operand of the ALU.
- B register: the B operand of the ALU.
- C register: the C operand of the ALU (for ALU that can operates with more than two operands simultaneously).
- Status register (or flags register): a register where each bit indicates a specific situation after the execution of the last instruction. A status regsiter is composed by the following flags:
    - Zero flag (Z): Z = 1 if the last instruction returns 0, otherwise Z = 0.
    - Carry flag (C): C = 1 if the last instruction returns a result with carry, otherwise C = 0.
    - Sign flag (S): S = 1 if the last instruction returns a negative number, otherwise S = 0.
    - Overflow flag (O): O = 1 if the last instruction caused an overflow, otherwise O = 0.
    - Parity flag (P): P = 1 if the last result is an odd number, otherwise P = 0. 
- MAR (Memory Address Register): stores the address of the memory location that the CPU wants to access. It's used during read and write operations.
- MDR (Memory Data Register), or MBR (Memory Buffer Register): stores the data being transferred to, or from the memory. Also this register is used during the read and write operations.

**Fetch-Decode-Execution Cycle**: the machine cycle, also called fetch-decode-execution cycle, is a loop continuously executed by the hardware of the CPU. The machine cycle consists in executing the following steps, in the listed order:

1. IF (Instruction Fetch): fetch the next instruction, indicated by the PC register, from the main memory.
2. PCI (Program Counter Increment): increment the PC, so it this way it can point to the next instruction.
3. ID (Instruction Decode): decode the instruction by considering its opcode. An opcode (operation code) is a unique code for a particular architecture that indicates the type of the instruction.
4. OPF (OPerands Fetch): if the current instruction needs one, two, or more operands from the main memory, in this phase the CPU fetches all the operands.
5. EXE (EXEcute, or EXEcution): the ALU executes the fetched instruction with the fetched operands.
6. WB (Write Back): after the calculation, the ALU first stores the result in the output register, then a bus of the CPU carries the result to a GPRs.
7. MEM (MEMory, or MEMory write): if the result is a total result, it is stored to the main memory.

In reality, the machine cycle is not necessarily continuously executed by the system's hardware. For example, in the Java language there is a virtual machine called JVM (Java Virtual Machine) that executes the machine cycle via sofwtare.

**Processor**: it's the chip installed on the computer. The term "processor" is tipically used to indicate the physical chip of the system. A processor has own pins and own signals, but there are several standards that describe how the processor must communicate with the other peripherals in the system. A processor is also called microprocessor, also known as µP, or uP.

**Core, Single-Core Processro, Multi-Core Processor and Multicomputer**: an independent processing unit inside a processor that can execute instructions on its own. Each core can fetch instructions dirctly from the central memory, perform calculations (for example with integers numbers, or floating-point numbers), run programs and manage tasks from the operating systems. A processor with one core can execute only one task at a time; a processor with two cores can execute two tasks in parallel; a processor with N cores can execute ideally N tasks in parallel. Multiple cores allow your computer to handle programs simultaneously and smoothly.

A processor can be:

- Single-Core: it has only one execution unit installed on the chip. Intel Pentium III and Intel Pentium 4 are examoples of single-core processors.
- Dual-Core: it has two execution units installed on the chip. Intel Core 2 Duo and AMD Athlon 64 X2 are examples of dual-core processors.
- Multi-Core: it has more than two execution units installed on the chip. Intel Xeon Clearwater Forest (with 288 cores) and AMD EPYC 9965 Zen 5 Dense Cores (with 192 cores) are two processors that support an high level of parallelism with the highest number of core existing today

A processors with two, or more cores is called multicore processor. A processor with one core is called singlecore processor, or simply processor. If a system has two, or more processors (intended as multiple processor chips connected to each other), is called multicomputer. A multicomputer allows to obtain a much greater degree of parallelism.

The following image represents two types of system: a processor with single core and a processor with more cores.

<!-- to add -->
*In Figure: a singlecore and multicore processors*

**Tightly Coupled Processors**: a tightly coupled sustem consists of two, or more processors with a shared memory. Each processor tipically works with same instruction, or with same data, and this gives rise to different parallel execution modes on the same system:

- SISD (Single Instruction, Single Data): used fundamentally used by a processor, that executes the own instruction with the own data.
- SIMD (Single Instruction, Multiple Data): where more processors execute the same instruction for different set of data. This model is tipically used by the GPU (Graphic Processor Unit), or by TPU (Tensor Processor Unit).
- MISD (Multiple Instruction, Single Data): very similar to the previous; in this context more processors excecute different instruction by considering the same set of data. It's typical in simulations systems, or in performing large computations. 
- MIMD (Multiple Instruction, Multiple Data): this is the most gade of parallelism between two, or more processors, where each processor executes the own program with the own data. Multicore systems uses MIMD.

In the following figure is represented the GPU Nvidia Fermi, an example of a SIMD model:

<!-- to add -->
*In Figure: the Nvidia Fermi GPU, that follows the SIMD (Single Instruction, Multiple Data) model*

**Loosely Coupled Processors**: a loosely coupled system consists of processors with separate local memories, connected through a communication network, as shown in the following figure:

<!-- to add -->
*In Figure: an example of a loosely coupled procesors, a multicomputer*

In a loosely coupled system each processor has the own lifecycle and the own memory. Each processor can execute the own instruction and the own program, without interfering with others. There isn't any shared global memory and each processor operates independently. Loosely coupled systems are easily scalable and suitable for parallel architectures. Examples of lossely coupled systems are: distribuited systems, cloud computing systems and supercomputers. A loosely coupled processor is basically a multicomputer system.

**RISC (Reduced Instruction Set Computer)**: it a type of ISA (Instruction Set Architecture) with a reduced number of instructions. The philosophy behind the RISC approach is very simple: each instruction should be as simple as possible and it should be executed as fast as possible (fewest possible number of clock cycles). Tipically, in a RISC ISA, each instruction has one, or two operands; it is difficult to have instructions with more than two operands in a RISC architecture. Often, RISC architecture have a maxium of 128, or 256 instructions; moreover, each opcode is designed to be as simple as possible to interpret. All instructions have follows the same format and has the same length (number of bit, or Byte), rarely bigger than 16, 32, or 64 bits. Compilers and interpreters of programming languages play an important role in the code optimization. RISC allows tipically a low hardware complexity. For example, the following image shows the RISC ISA ARMv7-A:

<!-- to add -->
*In Figure: an example of the ARMv7-A ISA*

**CISC (Complex Instruction Set Computer)**: it's a type of ISA (Instruction Set Architecture) with an hugh number of instructions. The philosophy behind the CISC approach is: each instruction must be as independent as possible and must be as close as possible to the way human beings think. A CISC architecture reduces the gap between the machine level and the human level. Tipically, in a CISC ISA, each instruction has one, two, or more operands (some instruction three, four, or more operands). CISC architecture have an high number off instructions, 512, OR 1024 instructions in some architecture. Unfortunately, CISC architecture doesn't improve the hardware optimization; viceversa, often the hardware of the CPU and the ALU are more complex than the hardware needed by a RISC architecture. In a CISC architecture there are different formats and different lengths (an instruction can easily reach a length of 64, 128, or 256 Bytes also). Each instruction can be executed in an higher number of clock cycles (often 4, 8, 16 or more for the more complex insutrctions). Intel 8088 (like the Intel Core i9) is an example of CISC architecture. The following image shows the various format of the 8088 ISA:

<!-- to add -->
*In Figure: different formats of the Intel 8088 ISA*

**HISC (Hybrid Instruction Set Computer)**: an hybrid architecture uses both CISC and RISC ISAs to find a compromise between simplicity and independence of instructions. Modern architecture, Intel and AMD included, uses a RISC architecture for the most common and frequently used instruction (like `ADD`, `MOV`, `SUB`, `MUL`, `DIV`, `JMP` and others) and uses a CISC architecture for the most complex instruction (for example, for some vectorial instructions, or some calculation of floating-point numbers). This compromise is somewhere in between pure RISC architectures and pure CISC architecturess: HISC is faster than CISC, but slower than RISC.

**NUMA (Non-Uniform Memory Access) architecture**: it's an architecture used for multiprocessor and for tightly coupled processors where the access time to the memory depends on its location and its distance from the processor that is accessing it. The following figure shows how a NUMA system with four processors is organized:

<!-- to add -->
*In Figure: a NUMA system with four processors*

NUMA is the natural evolution of the UMA (Uniform Memory Access) architecture, where there is only one chip of the main memory and the access time is the same for all processors installed on the system. The following figure shows how an UMA system with four processor is organized:

<!-- to add -->
*In Figure: an UMA system with four processors*

As you can see, a NUMA architecture with N processors has N chips of memory also, one for each processor. Each processor accesses to the its memory throughout a dedicated memory bus with high transfer rate. All processors of a NUMA architecture are linked with a common bus and each processor can access to another memory throughout the common bus, by sending a message to another processor (in this case there is more latency). If the work between all the processors is coordinated well by a centralized arbiter, the NUMA architecture allows more bandwidth than the UMA architecture; moreover, NUMA is optimized for real-time and time-critical applications. 

**SMP (Simmetric Multi-Processor) architecture**: it's an architecture where there is a global memory (main memory, or central memory) shared to all processors: each processor can access to the shared memory by a common bus (also called system bus). There is a centralized arbiter collecting the access request made by all processors. According to a specific policy, such as a FIFO (First In, First Out) policy, each request is accepted and satisfied by the bus arbiter. Between the system bus and the processor there is a cache. Each processor has the own cache (it can be unified, or splitted: data cache and instruction cache). The SMP architecture is an example of a tightly coupled multiprocessor system, because there is a unique shared memory. The following figure represents the organization of a SMP architecture:

<!-- to add -->
*In Figure: organization of a SMP architecture*

**AMP (Asymmetric Multi-Processor) architecture**: is a multiprocessor system in which processors do not have equal roles, one processor (called the master) controls the system, while the other processors (called slaves) execute specific assigned tasks. The master processor controls the operating system, schedule tasks, manages I/O and handles system and program interrupts. The slave processors execute assigned computations and don't execute directly the operating system. Each slave can run different program. Communication often occurs through shared memory, or message passing through a common bus. Typical program executed by the slaves are graphic computations, signal processing and user-oriented applications. The following figure shows how an AMP is organized:

<!-- to add -->
*In Figure: organization of an AMP architecture*

**Real and Emulated Parallelism**: by emulated parallelism we mean the impression that the user has of the activity carried out by the computer. The processor may not support parallelism at the hardware level, however its execution speed and high system clock allow the processor to execute multiple programs in a very short time, even one at a time and with frequent context switches. By real parallelism we mean a system that can actually handle the simultaneous (or concurrent) execution of multiple running programs, for example by having multiple hardware cores, or by supporting hardware threads and using techniques such as pipelining. There are basically two types of real parallelism: ILP (Instruction-Level Parallelism) and PLP (Processor-Level Parallelism):

- ILP (Instruction-Level Parallelism): is a form of real parallelism that works by executing multiple instructions simultaneously within a single processor. Useful techniques of ILP are: pipelines, superscalar architectures, out-of-order execution, register renaming and speculative execution.
- PLP (Processor-Level Parallelism): is a form of real parallelism that works by executing tasks across multiple processors, or cores simultaneously. Architectures with the PLP supports are: multicore processors, vector processors and vector registers, SMP, AMP, NUMA, distribuited systems, clusters and cloud computing.

**System Clock**: the system clock is a digital circuit that use an opportune hardware (tipically a ring oscillator, or a quartz crystal oscillator) to generate a digital, periodic and cyclic signal. The digital signal continuously alternates between an high voltage (1.2 V, or 3.3 V, or 5 V) and low voltage (- 5 V, or 0 V). The system clock is the most important circuit of synchronous digital systems (like a computer), because it defines the various moments where each component executes some task. The following figure shows how a system clock is structured:

<!-- to add -->
*In Figure: an example of system clock*

The frequency is the key parameter of a system clock: it defines the clock cycles in a second. Modern digital systems have system clock of 4, or more GHz, it means that the system clock has a period of 1 / 4 000 000 000 seconds, or 0.25 ns (nanosecond, where ns = 10^(-9) seconds). The system clock is the "fastest" circuit in the system, as it marks the various time instants where each peripheral performs its task. Remember that the period, indicated by T, or P, is the inverse of the frequency, measured in Hz (Hertz) and indicated by f:

```
f = 1 / T
T = 1 / f
```

For example, the Intel Core i9 9900 processor has a base frequency of 3.1 GHz, or a period of 1 / 3 100 000 000 seconds (0.323 ns), but with Turbo Boost the system clock can be increased to 5 GHz, with a period of 1 / 5 000 000 00 seconds (0.2 ns).

**Memory Hierarchy**: modern digital systems like computers, servers and smartphones have more memories the CPU can access to find data to calculate and instructions to execute. Fundamentally, there are five categories of memories you can find in a modern digital device:

- Registers: small and very quick memories directly installed on the same chip of the ALU. They're very close to the CPU and they're a part of the data path. The access time is almost instantaneous: often, the ALU can access to one, or more registers simultaneously in 1 ns. It is difficult to estimate how many registers a CPU has: it depends on how the chip was built and the type of architecture.
- Cache Memory: it's the smallest category of memory in terms of chip size and capacity, no larger than a few dozen MB. A cache is organized in various levels (some of this levels are located directly into the same chip of the CPU, or even within each core for multicore CPUs). The access time is very low, of the order of a few ns, or at most 20 ns.
- Primary Memory (or Main Memory): it's a fair compromise between the chip size and the provided capacity, normally between 512 MB and 64 GB (or more for servers and clusters). Tipically the most common main memory is called "RAM", an acronym of "Random Access Memory", indicating the data access is quick and position-independent. The cost per GB is high, but the access time is still low, of the order of a 20 ns, or at most 60 ns.
- Secondary Memory (or Storage Memory): these memories have a larger chip size and the provided capacity, between 128 GB and 1 TB. Two of the most common storage memories are SSD (Solid State Disk) and HD (Hard Disk). Today, SSDs have far surpassed the performance of HDDs, providing access times in the order of a hundred ns or so. HDDs, on the other hand, offer even lower access times, as they rely on mechanical (not just electrical) parts, and can reach up to several milliseconds. The cost per GB is medium for SSD, low for HD. The access time is high, or very high of the order of a 100 ns (for the SSD), or at most 20 ms (for the HD).
- Tertiary Memory (or External Memory): these memories have a larger chip size and the provided capacity, between 128 GB and 1 TB (the same as the secondary memory). Both SSD and HD can be used as external memories and the performances are practically the same. The cost per GB is medium for SSD, low for HD. The access time is still very high, of the order of a 20 ns, or at most 60 ns. Also other types of memories can be used, like CDs (Compact Disks), DVDs (Digital Versatile Disks), Blu-Ray, USB Pen-Driv (or USB Key) and so on.

The following figure shows the memory hierarchy:

<!-- to add -->
*In Figure: how's organized the memory hierarchy*

As you can see by observing the previous figure, there are some parameters of a memory which vary as you move from bottom to top (or viceversa) in the memory hierarchy:

- Access time: as you move down the hierarchy, it progressively increases. This fact means registers are significantly faster than the main memory, in turn much faster than secondary and external memories.
- Storage capacity: as you move down the hierarchy, it progressively increases. This fact means registers are significantly smaller than the main memory, in turn much smaller than secondary and external memories.
- Cost per bit: as you move down the hierarchy, it progressively decreases. This fact means main mamories are significantly more expensive than the secondary, or external memory.

### 01.02. Cache Memory

**Cache**: is a very fast memory with a low capacity, tipically realized with the SRAM (Static Random Access Memory) technology. SRAM is a type of volatile semiconductor memory that stores data using bistable flip-flop circuits, typically implemented with 6 transistors per cell (one cell per bit). SRAM doesn't require periodic refresh, which makes it faster but more expensive and less dense. It provides low access latency and high speed, for this reason it is commonly used for caches and not for main memories. However, SRAM consumes more silicon area and has higher cost per bit. A cache can be unified, or splitted. An unified cache contains both data and instructions, meanwhile a splitted cache is divided into two caches: the instructions cache contains the instructions that the CPU is executing.

**Cache Levels**: cache memory is organized in levels and each level provides a specific capacity and specific size. Normally, a common computer has three levels of cache: L1, L2 and L3. More expensive (and powerful) systems have up to seven levels of cache, from L1 to L7. The first three levels of a cache are organized in this way: 

- The L1 Cache (or simply L1) is located in each processor's chip, or in each core's chip. Each computation unit has the own L1. L1 provides faster access time, but at the price of a smaller size, tipically between 16 KB and 128 KB per core. Most common L1s are a splitted cache: there is an L1d (for L1 data) and L1i (for L1 instructions). 
- The L2 Cache (or simply L2) is located in each processor's chip, rarely in each core's chip (it means that in multicores systems there is only one L2 for all cores). Each computation unit has the own L1. Most common L2s are a unified cache. L2 provides slower access time than the L1, but its size is increased, tipically between 256 KB and 2 MB.
- The L3 Cache (or simply L3) is located out from the processor's chip, but very close to it. Each computation unit has a shared L3. L3s are typical an unified cahce. L3 provides slower access time than the L2, but its size is increased, tipically between 2 MB and 128 MB.

**Temporal and Spatial Locality Principles**: caches and main memories work based on two fundamental principles:

- Temporal locality principle: if a memory location is accessed once, it is likely to be accessed again in the near future.
- Spatial locality principle: if a memory location is accessed, nearby memory locations are likely to be accessed soon.

Respecting these two principles means having greater coherence between cache and main memory, guaranteeing fast access to data or instructions by the CPU and boasting efficient use of memory.

**Cache Hit and Miss**: when a CPU generates a memory address already present into one of the cache levels (L1, L2, or L3), a cache hit happens. Cache hit happens when the CPU requests data that is already present in the cache, effectively accessing it now in a very short time. On the contrary, when the CPU requests data that isn't already present in the cache, the request is propagated to the main memory (or to the next level of the cache): in this case a cache miss happens. Cache hit and cache miss are very important to control the performances of the cache. From these two situations the following performance parameters for caches arise:

- Hit Ratio: is a number between `0` and `1` (a percentage) which represents the ratio between cache hits and cache misses. A value close to `1` represents an high cache hit (and conseguently a low cache miss), meanwhile a value close to `0` represents an high cache miss (and conseguently a low cache hit). We indicates the hit ratio with `r`. If we indicate total number of cache hits with `h` and total number of cache misses with `m`, then the hit ratio is calculated with this formula: `r = h / (h + m)`. Normally, modern caches reach a value of `r` between 95% (`0.95`) and 100% (`1.00`).
- Miss Rate: is a number between `0` and `1` (a percentage) which represents the ratio between cache misses and cache hits. From the conceptual point of view, it's the inverse of the hit ratio. A value close to `1` represents an high cache miss (and conseguently a low cache hit), meanwhile a value close to `0` represents an high cache hit (and conseguently a low cache miss). We indicates the miss rate with `l`. If we indicate total number of cache hits with `h` and total number of cache misses with `m`, then the miss rate is calculated with this formula: `l = m / (m + h)`. Normally, modern caches reach a value of `l` between 5% (`0.05`) and 0% (`0.00`). Another way to calculate the miss rate is `l = 1 - r` and, similarly, another way to calculate the hit ratio is `r = 1 - l`.
- Hit Time: is the time required to access data from the cache memory when the requested data is already present in the cache (cache hit). Normally, a cache hit is resolved in few nanoseconds.
- Miss Penalty: is the extra time required to retrieve data from the next level of the memory hierarchy (L2, L3, or main memory) when the requested data is not found in the cache (cache miss).

**AMAT (Average Memory Access Time)**: it's very complex to calculate, but we can try to consider the simple formula. We can consider the following memory hierarchy (for each memory, we indicate the access time)

- Cache, with the following levels:
    - L1, made with the SRAM technology. `tl1` is the access time, `ml1` is the miss rate. 
    - L2, made with the SRAM technology. `tl2` is the access time, `ml2` is the miss rate. 
    - L3, made with the SRAM technology. `tl3` is the access time, `ml3` is the miss rate. 
- Main Memory, made with the DRAM technology. `tmm` is the access time, `mmm` is the miss rate. 
- Two Secondary Memories:
    - First is an SSD, made with the NAND-flash technology. `tssd` is the access time, `mssd` is the miss rate.
    - Second is an HD, made with both VLSI and mechanical technologies. `thd` is the access time.

The CPU can access the various memories in the following order:

```
CPU → L1 → L2 → L3 → Main Memory → SSD → HDD
```

There are the basic AMAT formulas based on where the requested data is present:

- Data stored in the L1: `tl1`
- Data stored in the L2: `tl1 + (ml1 * tl2)`
- Data stored in the L3: `tl1 + (ml1 * (tl2 + (ml2 * tl3)))`
- Data stored in the main memory: `tl1 + (ml1 * (tl2 + (ml2 * (tl3 + (ml3 * tmm)))))`
- Data stored in the SSD: `tl1 + (ml1 * (tl2 + (ml2 * (tl3 + (ml3 * (tmm + (mmm * tssd)))))))`
- Data stored in the HD: `tl1 + (ml1 * (tl2 + (ml2 * (tl3 + (ml3 * (tmm + (mmm * (tssd + (mssd * thd)))))))))`

As you can see, the more complex the memory hierarchy, the longer the average memory access time.

**Cache Lines**: a cache line is the basic unit of data transferred between cache and main memory and is identified using three address fields: tag, index, and offset. The index selects the cache set (or line) where the data may reside, the **tag** identifies whether the required memory block is present in that location, and the offset selects the specific byte or word within the cache line. These fields are extracted from the memory address to enable fast cache lookup and access.

**Mapping Strategies**: cache mapping strategies determine how memory blocks are placed into cache lines. In direct-mapped caches, each memory block maps to exactly one cache line, making access fast but increasing conflict misses. In set-associative caches, each block can be placed in any line within a selected set, balancing flexibility and hardware complexity. In fully associative caches, a memory block can be placed in any cache line, minimizing conflict misses but requiring more complex and slower hardware search mechanisms.

**Replacement Strategies**: cache replacement strategies determine which cache line is replaced when a new memory block must be loaded and the cache (or set) is already full. The choice of strategy affects cache performance by influencing the miss rate. The most common used strategies are:

- FIFO (First In, First Out): replaces the cache line that has been in the cache the longest time. It is simple to implement but does not consider how frequently or recently data is used (and this can decrease the hit ratio, or equivalenlty it can inrease the miss rate).
- LRU (Last Recently Used): replaces the cache line that has not been accessed for the longest time. It exploits temporal locality and generally provides better performance than FIFO, but requires more hardware complexity.
- Random Replacement: selects a cache line randomly for replacement. It is simple and fast to implement and can perform reasonably well in practice.
- LFU (Last Frequently Used): replaces the cache line that has been accessed the fewest times. It tracks usage frequency but is more complex to implement and less common in hardware caches.
- Pseudo LRU (Last Recently Used): an approximation of LRU used in modern processors to reduce hardware complexity while maintaining near-LRU performance. It's the most common used technique in the modern digital systems.

**Write Strategies**: in a write-through policy, every write operation updates both the cache and the main memory simultaneously. This ensures memory consistency and simplifies coherence but increases memory traffic and can reduce performance due to slower write operations. In a write-back (or copy-back) policy, write operations update only the cache initially, and modified data (dirty blocks) are written to main memory only when they are replaced. This reduces memory traffic and improves performance but requires additional hardware to track modified cache lines. In a write-allocate policy, when a write miss occurs, the corresponding memory block is first loaded into the cache and then updated. This strategy is commonly used together with write-back caches because future writes to the same block are likely (temporal locality). In a no write-allocate policy, when a write miss occurs, the data is written directly to main memory without loading the block into the cache. This reduces cache pollution and is typically used together with write-through cahces.

There is a lot more to say about caches, but unfortunately there isn't enough space to talk about it. We refer you to more in-depth texts.

### 01.03. Primary Memory
<!-- to do - RAM (Random Access Memory), SRAM (Static RAM) and DRAM (Dynamic RAM) -->
<!-- to do - organization of memory cells: bit, nibble, byte, half-word, word -->
<!-- to do - memory as a matrix vs memory as an array of bytes -->
<!-- to do - definition of memory address -->
<!-- to do - byte-addressing and word-addressing memory -->
<!-- to do - byte ordering: big endian vs little endian -->
<!-- to do - challenges between big endian and little endian systems -->
<!-- to do - EDCs (Error Detection Codes): one-dimensional parity bit, two-dimensional parity bits, checksum, CRC (Cyclic Redundant Code) -->
<!-- to do - ECCs (Error Correction Codes): Hamming distance, Hamming Codes for SEC (Single Error Correction), Hamming codes for SEC-DED (SEC, Double Error Correction), chipkill ECC, BCH (Bose–Chaudhuri–Hocquenghem) codes, Reed-Solomon codes -->
<!-- to do - memory packages: SIMM (Single Inline Memory Module), DIMM (Dual Inline Memory Module) and SO-DIMM (Small Outline DIMM) -->

### 01.04. Secondary Memory
<!--
to do - NAND memory: SSD (Solid State Disk)
    - NAND-based flash memory
    - NOR-based flash memory
    - floating-gate transistor principle
    - charge storage mechanism
    - structure: pages, blocks, planes, dies and channels
    - SLC (Single-Level Cell) and MLC (Multi-Level Cell)
    - performance parameters: endurance, latency, density and reliability
    - errors in NAND memories, bad block management, wear leveling and garbage collection
-->
<!-- to do - HD (Hard Disk)
    - magentic storage principle
    - non-volatile storage concept
    - physical structure: platters, spindle, read/write heads, actuator arm, tracks, sectors, cylinders
    - sector format, LBA (Logical Block Addressing), ZBR (Zone Bit Recording)
    - Logical and physical disk geometry
    - performance parameters: seek time, rotational latency, access time, data transfer rate, throughput
    - interfaces: IDE, SATA, SCSI and SAS
    - errors in HD: bad sector handling and smart monitoring system
    - caching: read caching, write caching and prefetching
-->
<!-- to do - RAID (Redundant Array Of Independent Disks)
    - what is a RAID?
    - hardware RAID and software RAID
    - data striping and data mirroring concepts
    - parity concept, parity-based redundancy and distribuited parity
    - RAID level 0
    - RAID level 1
    - RAID level 2
    - RAID level 3
    - RAID level 4
    - RAID level 5
    - RAID level 6
    - nested RAID levels: RAID 0+1, RAID 1+0, RAID 50 and RAID 60
    - performance parameters: read performance, write performance, parity update penalty, rebuild time, latency and throughput
    - fault tolerance: MTTF (Mean Time To Failure), MTTR (Mean Time To Repair), rebuild process, hot spare disks
-->
<!-- to do - CD (Compact Disk)
    - optical storage principle
    - physical structure: polycarbonate substrate, reflective layer, protective layer, spiral track structure, pits and lands
    - logical structure: frames, blocks, logical addressing and ISO 9660 file system
    - performance parameters: CLV (Constant Linear Velocity), access time, seek time, rotational latency, data transfer rate, standard storage capacity and physical density limits
    - errors in CD: CIRC (Cross-Interleaved Reed-Solomon Code) and interleaving techniques
    - CD-ROM (CD - Read Only Memory)
    - CD-R (CD - Recordable)
    - CD-RW (CD - Re-Writable)
    - CD-DA (CD - Digital Audio)
-->
<!-- to do - DVD (Digital Versatile Disk)
    - physical structure: polycarbonate substrate layers, reflective layer, protective layer, dual-layer structure, single-sided vs double-sided discs, spiral track structure, pits and lands
    - logical structure: sectors, blocks, LBA (Logical Block Addressing), UDF (Universal Disk Format) and ISO 9660 file system
    - formats: DVD-ROM, DVD-R, DVD+R, DVD-RW, DVD+RW, DVD-RAM, DVD-Video and DVD-Audio
    - errors in DVD: RSPC (Reed-Solomon Product Code) and interleaving techniques
    - performance parameters: access time, seek time, rotational latency, data transfer rate
    - SLSS (Sinlge Layer, Single Sided)
    - DLSS (Dual Layer, Single Sided)
    - SLDS (Single Layer, Double Sided)
    - DLDS (Dual Layer, Double Sided)
-->
<!-- to do - Blu-Ray Disk
    - high-density storage concept
    - physical structure: polycarbonate substrate, reflective layer, protective coating (hard-coat layer), single-layer structure, dual-layer structure, multi-layer discs, spiral track structure, pits and lands
    - logical structure: sectors, block, LBA (Logical Block Addressing) and UDF (Universal Disk Format)
    - bits representation: bit optical encoding, channel bits, laser wavelength, numerical aperture improvement, high-density track spacing
    - formats: BD-ROM, BD-R, BD-RE, BDXL, BD-Video and BD-Audio
    - performance parameters: access time, seek time, rotational latency and data transfer rate
    - single-layer, double-layer, triple layer and quad layer
-->

### 01.05. I/O Devices

**Keyboards**: there are different types of keyboards:

- Mechanical keyboards use individual switches per key that directly close an electrical contact when pressed.
- Membrane keyboards detects key presses using flexible conductive layers pressed together.
- Rubber dome keyboards use silicone domes that collapse to connect circuit traces.
- Scissor-switch keyboards use a stabilizing scissor mechanism above a membrane contact layer.
- Capacitive keyboards detect key presses by measuring changes in capacitance instead of closing electrical contacts.

**Mouses**: there are different types of mouses (also known as mices):

- Mechanical mice detect movement using a rubber ball that rotates internal rollers connected to position sensors.
- Optomechanical mice improve mechanical detection using optical sensing of rotating encoder wheels.
- Early optical mice detect movement using predefined grid-pattern mousepads.
- Modern optical mice use an LED and image sensor to track surface texture movement.
- Laser mice operate like optical mice but use a laser diode instead of an LED.
- Wireless mice transmit movement data without cables using short-range communication protocols.
- Touch-based mice detect finger movement using capacitive sensing instead of mechanical motion tracking.

**Monitors**: there are different types of monitors.

A CRT monitor works by firing electron beams from the back of the tube onto a phosphor-coated screen to produce images. The beams scan the screen line by line to create the picture. CRT displays are bulky, consume more power, and are largely obsolete today.

An LCD monitor uses liquid crystals placed between glass layers to control light passing from a backlight and form images on the screen. It is thinner, lighter, and more energy-efficient than CRT displays. LCD technology is widely used in laptops, monitors, and televisions.

An LED monitor is actually an LCD monitor that uses light-emitting diodes as the backlight instead of fluorescent lamps. This improves brightness, contrast, and energy efficiency while allowing thinner display designs. LED monitors are common in modern screens today.

An OLED monitor uses organic compounds that emit light when electricity passes through them, so no backlight is required. Each pixel produces its own light, enabling very high contrast, deep blacks, and fast response times. OLED displays are used in high-end smartphones, TVs, and monitors.

A plasma display uses tiny cells filled with electrically charged gas that emit ultraviolet light when activated, which then excites phosphors to produce images. Plasma screens offer good color reproduction and wide viewing angles but consume more power and are heavier than LCD and LED displays. They are now mostly discontinued.

**Printers**: there are different types of printers.

An inkjet printer produces images by spraying tiny droplets of liquid ink onto paper through microscopic nozzles. It is commonly used for home and office printing because it can produce high-quality color images at relatively low cost. Inkjet printers are suitable for documents and photo printing.

A bubble-jet printer is a type of inkjet printer that uses heat to create tiny bubbles in the ink, forcing droplets onto the paper. This method allows precise control of ink placement and produces clear prints. It is widely used in many consumer inkjet printers.

A laser printer uses a laser beam to form an electrostatic image on a rotating drum, which attracts toner particles and transfers them onto paper. Heat is then applied to permanently fix the toner onto the page. Laser printers are fast and produce high-quality text, making them ideal for office environments.

An LED printer works similarly to a laser printer but uses a row of light-emitting diodes instead of a laser beam to create the image on the drum. This design has fewer moving parts and can improve reliability. LED printers are efficient and commonly used in office settings.

A direct thermal printer creates images by applying heat directly to specially coated thermal paper, which changes color when heated. It does not require ink or toner. These printers are commonly used for receipts, tickets, and labels.

A thermal transfer printer uses heat to transfer ink from a ribbon onto paper or labels. This method produces durable and long-lasting prints that resist fading. It is commonly used for barcode labels, packaging, and industrial applications.

A dot-matrix printer creates characters and images by striking an ink ribbon against paper using a set of small pins arranged in a matrix. It is an impact printer capable of printing multi-copy forms using carbon paper. Dot-matrix printers are mainly used in environments such as banking and logistics where continuous paper printing is required.

**Speaker**: a speaker converts digital audio data from the computer into analog sound waves that can be heard by humans. The signal follows this path:

1. CPU sends audio samples to the audio controller / sound card.
2. Sound controller stores samples in audio buffers.
3. A Digital-to-Analog Converter (DAC) converts digital samples into analog voltage.
4. Amplifier increases signal power.
5. Speaker diaphragm vibrates → produces sound waves.


**Digital Cameras**: a digital camera works by capturing light through a lens and focusing it onto an image sensor (usually a CMOS or CCD sensor). The sensor converts the incoming light into electrical signals that represent the brightness and color of each pixel in the image. These signals are processed by the camera’s internal processor and converted into a digital image file. The image is then stored in memory (such as an SD card) so it can be viewed, edited, or transferred to other devices.

A CMOS (Complementary Metal-Oxide-Semiconductor) sensor converts light into electrical signals using individual pixel-level amplifiers built directly into the sensor. Each pixel processes its own signal, allowing faster image capture and lower power consumption. CMOS sensors are widely used in smartphones and modern digital cameras because they are inexpensive to manufacture and support high-speed operation. They also enable additional processing functions to be integrated on the same chip.

A CCD (Charge-Coupled Device) sensor captures light and converts it into electrical charges that are transferred across the chip and read at one corner of the sensor. This method produces very high-quality images with low noise and excellent light sensitivity. However, CCD sensors consume more power and are slower compared to CMOS sensors. They were commonly used in earlier digital cameras and are still used in scientific and professional imaging applications.

### 01.06. System Bus

**System Bus**: the system bus is the communication network inside a digital system that allows the various devices of a computer to communicate. A system bus is a set of wires that interconnect CPU, main memory and I/O devices. A system bus has different types of buses:

- Data bus is a set of line in which each signal represents a data.
- Address bus is a set of line in which each signal represents an address.
- Control bus is a set of line in which each signal represents a control signal.

The system bus has various types of standard and protocols. In general: the bus inside a specific I/O device, or a specific component is not subject to standardization, meanwhile the interconnection between two, or more different devices is a system bus subject to standardization. A standard is a set of rules (or a set of interfaces) that all the productors of the I/O devices, CPUs and main memories must respect to be able to communicate efficently. Communication between two, or more components of a digital system are also subject to a protocol. A protocol is a set of rules that defines how devices communicate and exchange data in a digital system or network.

**Width**: the width of a system bus defines how many parallel wires (or parallel lines) has a particol type of bus. Today there are four main widths used in the most common digital systems:

- `x8` defines 8 parallel lines.
- `x16` defines 16 parallel lines.
- `x32` defines 32 parallel lines.
- `x64` defines 64 parallel lines.

In this case, "parallel lines" means that in a single clock cycle 8, 16, 32, or 64 bits are trasferred from a component to another simousimultaneously.

**Compatibility and Misalignment Problem**: over time, the width of a bus has been a major issue, for example for the Intel x86 architecture, which has had a series of increases in data bus widths starting with the 8088 processor:

- The `8088` processor had a `20` bit address bus.
- The `80286` processor had a `24` bit address bus. `4` of these bits have been added with a number of other control bits, to ensure backwards compatibility.
- The `80386` processor had a `32` bit address bus. Another `8` of these bits have been added, further complicating the complexity of the control circuitry.

Compatibility is a concrete problem: the multiplexed address bus could be an efficient solution.

A too high width leads to the bus misalignment problem: each signal in a specific line of the bus has the own propagation delay and the own speed, which varies slightly. This fact could lead to slight bus misalignments, especially when the clock cycle is very short. 

**Timing**: remember that the system clock is a digital signal, continuous and deterministic, which always and constantly repeats without interruption and which always takes on the same waveform at each clock period. System clock can be used by a bus, or not.

- A synchronous bus uses a shared clock signal to coordinate all operations between connected components, for example the memory access (for read, or write operations). All devices follow the same clock and the data transfers occur at fixed time intervals. THese type of system buses are easier to design and control, but they've a limited flexibility when devices have different speeds. Examples of synchronous buses are the FSB (Front-Side Bus) and the SDRAM memory bus.
- An asynchronous bus doesn't use a global clock, instead all devices coordinate transfers using handshaking signals (like the full handshaking). No system clock is required, and each device involved in the communication works with requests and acks. This is more flexible with mixed-speed devices. This type of system buses is more flexible and optimied for devices with different speeds, but it's slower than synchronous buses (due to handshake overhead). Examples of asynchronous buses are the USB (Universal Serial Bus) and the PCI (Pheripheral Component Interrconnect).

The following figure shows the differences between a communication in a synchronous bus and in an asynchronous bus:

<!-- to add -->
*In Figure: a communication in a synchronous bus (on left), and in an asynchronous bus (on right)*

**Arbitration**: in a computer system, multiple devices, such as the CPU, the main memory and the I/O devices, are all connected to a common communication pathway known as system bus. In order to transfer data between these devices, they need to have access to the bus. Bus arbitration is the process of resolving conflicts that arise when multiple devices attempt to access the bus at the same time. When multiple devices try to use the bus simultaneously, it can lead to data corruption and system instability. To prevent this, a bus arbitration mechanism is used to ensure that only one device has access to the bus at any given time.

Bus arbitration refers to the process by which the current bus master accesses and then leaves the control of the bus and passes it to another bus requesting processor unit. The controller that has access to a bus at an instance is known as a bus master. There are two types of bus arbitration:

- Centralized bus arbitration: a single bus arbiter (tipically a single bus arbiter called master) performs the required arbitration. 
- Distribuited bus arbitration: all devices involved in the communication and linked to the system bus participating in the selection of the next bus master.

There are different methods for the bus arbitration:

- Daisy chaining method: it is a simple and cheaper method where all the bus masters use the same line for making bus requests. The bus grant signal serially propagates through each master until it encounters the first one that is requesting access to the bus. This master blocks the propagation of the bus grant signal, therefore any other requesting module will not receive the grant signal and hence cannot access the bus. Here's the daisy chaining method:

<!-- to add -->
*In Figure: the daisy chaining method to implement a centralized bus arbitration*

- Polling, or rotating priority method: in this, the controller is used to generate the address for the master(unique priority), the number of address lines required depends on the number of masters connected in the system. The controller generates a sequence of master addresses. When the requesting master recognizes its address, it activates the busy line and begins to use the bus. Here's the polling priority method:

<!-- to add -->
*In Figure: the pooling priority method to implement a distribuited bus arbitration*

- Fixed priority, or independent request method: in this, each master has a separate pair of bus request and bus grant lines and each pair has a priority assigned to it. The built-in priority decoder within the controller selects the highest priority request and asserts the corresponding bus grant signal. Here's the fixed priority request method:

<!-- to add -->
*In Figure: the fixed priority request method to implement a centralized bus arbitration*

**Architecture of System Bus**: system bus in a digital system can be organized in different ways. There are three main architectures known for the system bus:

- Single bus architecture: all components share one common communication bus for data, address, and control signals. All communications occurs over the same and unique bus. Only one transfer happens at a time, because every device must use the same communication path. In this systems there is commonly a bus arbiter.
- Multiple bus architecture: uses separate buses for different communication tasks. Multiple transfers can happen simultaneously. This architecture is used in modern processors and performance-oriented systems. Usually this architecture uses both centralized and distribuited bus arbitration methods.
- Hierarchical bus architecture: in which each component is like a leaf, or a root of a tree. Tipically the root component is the CPU, with a direct connection (with a dedicated bus) to the main memory. This architecture is based on the expansion bus (or expansion slots): each slot allows the user to link another I/O devices to the digital system., by creating a subtree system.

The hierarchical bus architecture is shown in the following figure:

<!-- to add -->
*In Figure: a hierarchical bus architecture with CPU as root of the tree*

**Performance parameters of the system bus**: here are the key performance parameters of a bus that determine how fast data moves inside a computer system:

- Width: bus width is the number of bits (on for each line) that can be transferred simultaneously over the bus.
- Latency: is the time delay between sending a request and receiving the response.
- Frequency: bus frequency is the number of transfer cycles per second on the bus.
- Throughput: is the amount of data transferred per second over the bus.

**Chipset (northbridge and southbridge)**: the chipset is a set of motherboard components managing data flow between the CPU, memory, and devices. Traditionally, it consists of two parts: the northbridge (which handles high-speed communication with the CPU, RAM, and graphics) and the southbridge (which handles slower I/O functions like USB, SATA, and audio). The following figure shows the basic structure of the chipset:

<!-- to add -->
*In Figure: northbridge and southbridge*

Northbridge is one of the two chips located in the direction towards North in the motherboard. The main function of North bridge is to manage the communications between the CPU and parts of motherboard. Northbridge is directly towards FSB (Font-Side Bus). Other names for northbridge are host bridge and MCH (Memory Controller Hub).

Southbridge is the another chip of the logical chipset architecture. It is located to the South of PCI (Peripheral Component Interconnect) bus in the motherboard. The main function of southbridge is to control the IO functioning. The northbridge is the medium that connects southbridge and CPU. ICH (I/O Controller Hub) is the other name given to the southbridge for its functionality. 

**FSB (Front-Side Bus)**: is the main communication pathway between the CPU and the main memory (SRAM for cache, DRAM for the central memory). Historically, this bus is called "northbridge", from the chipset proposed by the Intel. It was widely used in older computer architectures before newer interconnect technologies replaced it. It acts like a data highway carrying instructions, addresses, and control signals between processor and memory. Here's represented the FSB:

<!-- to add -->
*In Figure: how FSB is located in a modern digital system*

**BSB (Block-Side Bus)**: the BSB (Block-Side Bus), also known as Back-Side Bus, is a dedicated, high-speed and internal bus that connects the CPU to its cache memory, typically the L2 cache. Unlike the FSB, which connects the CPU to main memory and chipset, the BSB connects only the processor and cache. Here's represented the BSB:

<!-- to add -->
*In Figure: how BSB is located in a modern digital system*

**ISA (Industry Standard Architecture)**: is a 16 bits system bus introduced and used for the first time in the IBM PC/AT and nextly in the Intel 80286 processor. Intel always thinks to compatiblity, so the ISA system bus used in the 80286 is with the 8 bits internal system bus of the Intel 8088 processor, used in the IBM PC. The natural evolution of the ISA system bus is the EISA (Extended Industry Standard Architecture), a 32 bits system bus used for x32 architectures.

ISA system bus has the following characteristics:

- Supports 8-bit and later 16-bit data transfer.
- Typical clock speed about 8 MHz (8 mnilion of Hz).
- Maximum data transfer rate up to about 16 MB/s.
- Uses simple and inexpensive hardware design.
- Does not support automatic configuration (manual jumper settings required).
- Now obsolete in modern computer systems.

Meanwhile, EISA has the following characteristics:

- Supports 32-bit data transfer.
- Higher data transfer rate up to about 33 MB/s.
- Backward compatible with ISA expansion cards.
- Supports bus mastering for improved performance.
- Provides automatic device configuration (software-based).
- Mainly used in high-end PCs and servers before being replaced by PCI buses.

<!-- to do - PCI (Pheripheral Components Interconnect) -->
<!-- to do - PCIe (PCI express) -->
<!-- to do - PIO interface -->