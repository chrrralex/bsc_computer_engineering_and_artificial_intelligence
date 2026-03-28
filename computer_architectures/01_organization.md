# 01. Organization

### 01.01. Processor
<!-- to do - definition of CPU (Central Processing Unit) -->
<!-- to do - definition of processor -->
<!-- to do - definition of multicore processor -->
<!-- to do - definition of multiprocessors -->
<!-- to do - definition of multicore and multiprocessors -->
<!-- to do - definition of multicomputers -->
<!-- to do - system clock -->
<!-- to do - CU (Control Unit) -->
<!-- to do - ALU (Arthmetic-Logic Unit) -->
<!-- to do - definition of data path -->
<!-- to do - registers: PC (Program Counter), IR (Instruction Register), GPRs (General Purposes Registers), MAR (Memory Address Register), MDR (Memory Data Register), MBR (Memory Buffer Register), SP (Stack Pointer), AC (ACcumulator), SR (Status Register) -->
<!-- to do - fetch-decode-execute cycle: IF (Instruction Fetch), ID (Instruction Decode), EXE (EXEcute), WB (Write Back), ST (STore) -->
<!-- to do - RISC (Reduced Instruction Set Computer) -->
<!-- to do - CISC (Complex Instruction Set Computer) -->
<!-- to do - RISC and CISC comparison -->
<!-- to do - NUMA (Non-Uniform Memory Access) architecture -->
<!-- to do - SMP (Simmetric Multi-Processor) architecture -->
<!-- to do - AMP (Asymmetric Multi-Processor) architecture -->
<!-- to do - real and emulated parallelism -->
<!-- to do - introduction of ILP (Instruction-Level Parallelism): Pipelines, Superscalar Architectures -->
<!-- to do - introduction of PLP (Processor-Level Parallelism): SIMD (Single Instruction, Multiple Data), Vector Processors, Multiprocessor and Multicomputer  -->
<!-- to do - memory hierarchy: cache memories, primary memories, secondary memories and external memories -->
<!-- to do - parameters of memory herarchy: access time, storage capacity, cost per bit (or cost per byte), memory types -->

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
<!-- to do - keyboards -->
<!-- to do - mouses -->
<!-- to do - monitors -->
<!-- to do - speakers -->
<!-- to do - game consoles -->
<!-- to do - modems -->
<!-- to do - USB keys -->
<!-- to do - digital cameras -->
<!-- to do - printers -->
<!-- to do - scanners -->
<!-- to do - microphones -->

### 01.06. System Bus
<!-- to do - definition of system bus -->
<!-- to do - width: x8, x16, x32 and x64 architectures -->
<!-- to do - types: data, address and control -->
<!-- to do - timing: synchronous bus, asynchronous bus, clocked communication and handshaking mechanism -->
<!-- to do - arbitration: centralized system bus, distribuited system bus, master-slave mechanism -->
<!-- to do - performance parameters: width, latency, frequency, throughput -->
<!-- to do - architectures: single-bus, multiple-bus and hierarchical bus -->
<!-- to do - modern bus standards: memory bus, FSB (Front-Side Bus), BSB (Block-Side Bus) -->
<!-- to do - PCI and PCIe (PCI express) -->
<!-- to do - SoC (System on Chip): northbridge and southbridge -->