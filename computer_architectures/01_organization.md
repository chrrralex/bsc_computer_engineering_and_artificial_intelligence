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

**NUMA (Non-Uniform Memory Access) architecture**: <!-- to do -->

**SMP (Simmetric Multi-Processor) architecture**: <!-- to do -->

**AMP (Asymmetric Multi-Processor) architecture**: <!-- to do -->

<!-- to do - real and emulated parallelism -->
<!-- to do - introduction of ILP (Instruction-Level Parallelism): Pipelines, Superscalar Architectures -->
<!-- to do - introduction of PLP (Processor-Level Parallelism): SIMD (Single Instruction, Multiple Data), Vector Processors, Multiprocessor and Multicomputer  -->
<!-- to do - memory hierarchy: cache memories, primary memories, secondary memories and external memories -->
<!-- to do - parameters of memory herarchy: access time, storage capacity, cost per bit (or cost per byte), memory types -->
<!-- to do - system clock -->

### 01.02. Cache Memory
<!-- to do - definition of cache -->
<!-- to do - cache levels: L1, L2, L3, split cache and unified cache -->
<!-- to do - temporal and spatial locality principles -->
<!-- to do - cache lines: tag, index and offset -->
<!-- to do - cache hit and cache miss -->
<!-- to do - performance indexes: hit ratio, miss rate, hit time and miss penalty, AMAT (Average Memory Access Time) -->
<!-- to do - mapping strategies: direct-mapped, set-associative and fully associative -->
<!-- to do - replacement strategies: FIFO (First-In, First-Out), LRU (Last Recently Used), Random Replacement, LFU (Last Frequently Used) -->
<!-- to do - write strategies: write-through, write-back, write-allocate and no write-allocate -->
<!-- to do - cache in multiprocessor systems: cache coherence problem, shared data consistency, snooping protocols and directory-based protocol -->
<!-- to do - prefetching and victim cache -->
<!-- to do - inclusive vs exclusive cache hierarchies -->

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
<!-- to do - keyboards: mechanical, membrane, rubber dome, scissor-switch and capacitive -->
<!-- to do - mouses: mechanical (rubber ball, internal rollers), optomechanical (ball and ecnoder wheels, LED and photodectectors), optical (early-optical, LED, laser), wireless (infrared, RF and bluetooth) and touch-based -->
<!-- to do - monitors: CRT (Cathode Ray Tube), LCD (Liquid Crystal Display), LED (Light Emitting Diode), OLED (Organic LED) and plasma -->
<!-- to do - printers: inject, bubble-jet, laser, LED, direct thermal, thermal transfer, dot-matrix -->
<!-- to do - speakers -->
<!-- to do - digital cameras -->

### 01.06. System Bus
<!-- to do - definition of system bus -->
<!-- to do - width: x8, x16, x32 and x64 architectures -->
<!-- to do - types: data, address and control -->
<!-- to do - timing: synchronous bus, asynchronous bus, clocked communication and handshaking mechanism -->
<!-- to do - arbitration: centralized system bus, distribuited system bus, master-slave mechanism -->
<!-- to do - performance parameters: width, latency, frequency, throughput -->
<!-- to do - architectures: single-bus, multiple-bus and hierarchical bus -->
<!-- to do - modern bus standards: memory bus, FSB (Front-Side Bus), BSB (Block-Side Bus) -->
<!-- to do - PCI (Pheripheral Components Interconnect) and PCIe (PCI express) -->
<!-- to do - ISA (Industry Standard Architecture) -->
<!-- to do - Chipset: northbridge and southbridge -->