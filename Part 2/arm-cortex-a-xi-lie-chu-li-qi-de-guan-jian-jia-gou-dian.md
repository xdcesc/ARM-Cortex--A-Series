## ARM Cortex-A 系列处理器的关键架构点

一些关键点对于 Cortex-A 系列的设备是相同的：

* 32-bit RISC core, with 16 × 32-bit visible registers with mode-based register banking.
* Modified Harvard Architecture \(separate, concurrent access to instructions and data\).
* Load/Store Architecture.
* Thumb-2 technology as standard.
* VFP and NEON options.
* Backward compatibility with code from previous ARM processors.
* 4GB of virtual address space and a minimum of 4GB of physical address space.
* Hardware translation table walking for virtual to physical address translation.
* Virtual page sizes of 4KB, 64KB, 1MB and 16MB. Cacheability attributes and access
  permissions can be set on a per-page basis.
* Big-endian and little-endian data access support.
* Unaligned access support for basic load/store instructions.
* Symmetric Multi-processing \(SMP\) support on MPCore™ variants, that is, multi-core versions of the Cortex-A series processors, with full data coherency at the L1 cache level. Automatic cache and Translation Lookaside Buffer \(TLB\) maintenance propagation provides high efficiency SMP operation.
* Physically indexed, physically tagged \(PIPT\) data caches. 

所有的这些架构关键点都会在接下来的章节中提及。



