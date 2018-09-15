## 其他各样指令

剩余的指令包括协处理器指令、supervisor 调用、PSR 修改、字节反转、缓存预加载、位操作等。

### 协处理器指令

协处理器指令占据 ARM 指令集的一部分。最多可以实现 16 个协处理器，编号为 0 到 15 \(CP0, CP1…CP15\)。它们可以是内部的\(内置到处理器\)，也可以通过专用接口从外部连接。在较老的处理器中很少使用外部协处理器，而使用外部协处理器在 Cortex-A 系列中不受支持。

* 协处理器 15 是内置协处理器，可以提供对许多核特性的控制，包括缓存和 MMU。

* 协处理器 14 是内置协处理器，可以提供对核硬件调试设备的控制，例如 breakpoint units（在第二十四章中描述）

* 协处理器 10 和 11 给予对系统中浮点和 NEON 硬件的访问控制（在第六章和第七章中描述）

如果执行协处理器指令，但系统中不存在适当的协处理器，则出现未定义的指令异常。

下面有五类协处理器指令

* CDP – initiate a coprocessor data processing operation.
* MRC – move to ARM register from coprocessor register.
* MCR – move to coprocessor register from ARM register.
* LDC – load coprocessor register from memory.
* STC – store from coprocessor register to memory.

还有多种寄存器和这些指令的其他变体:

* MRRC – transfers a value from a Coprocessor to a pair of ARM registers.
* MCCR – transfers a pair of ARM register to a coprocessor.
* LDCL – reads a coprocessor register from multiple registers.
* STCL – writes a coprocessor register to multiple registers,

这些和其他变体在附录 A 有更详细的描述。

### SVC

执行 SVC \(supervisor call\) 指令时，产生 supervisor call 异常。这在 第11 章异常处理中描述。该指令包括一个 24 位 \(ARM\) 或 8 位\(Thumb\) 的数字值，可由 SVC 处理程序代码检查。通过 SVC 机制，操作系统可以指定在用户模式下运行的应用程序可以请求的一组特权操作。这条指令最初被称为 SWI \(软件中断——Software Interrupt\)。

### PSR修改

若干指令使 PSR 能够写入或读取：

* MRS 将 CPSR 或 SPSR 值转移到通用寄存器中。MSR 将通用寄存器的值转移到 CPSR 或 SPSR。可以更新整个状态寄存器，也可以更新它的一部分。在用户模式中，可以读取所有位，但只能修改条件标志\(\_f\)。
* 在特权模式下，更改处理器状态\(CPS\)指令可用于直接修改 CPSR 中的模式和中断启用或禁用\(I和F\)位。参见 Figure 3-6
* SETEND 修改单个 CPSR 位，即 E \(Endian\) 位。这可以用于具有混合端数据的系统，以便在小端和大端数据访问之间临时切换。

### 位操作

若干使得寄存器中值进行位操作的指令：

* Bit Field Insert\(BFI\) 指令允许从一个寄存器底部的一系列相邻位\(通过提供宽度值和 LSB 位置指定\)放置到目标寄存器的任何位置。
* Bit Field Blear\(BFC\) 指令使寄存器中的相邻位被清除。
* SBFX 和 UBFX 指令\(Signed and Unsigned Bit Field Extract\)将相邻位从一个寄存器复制到第二个寄存器的最小有效位，并将值用符号位或者 0 扩展到 32 位。
* RBIT 指令反转寄存器内所有位的顺序。

### 预加载缓存

缓存预加载（第十七章）描述了在 ARM 处理器上运行的优化代码。提供了两条指令: PLD \(data cache preload\) 和 PLI \(instruction cache preload\)。这两个指令都是对内存系统的提示，即对指定地址的访问可能很快就会发生。不支持这些操作的实现将把预加载视为 NOP，但是本书中描述的所有 cortex 系列处理器都能够预加载缓存。任何指定为 PLD 指令参数的非法地址都不会导致数据中止异常。

### 字节倒置

反转字节顺序的指令对于处理相反的端值或其他数据重新排序操作的数量非常有用：

* The REV instruction reverses the bytes in a word
* The REV16 reverses the bytes in each halfword of a register
* The REVSH reverses the bottom two bytes, and sign extends the result to 32 bits

Figure 5-6 演示了 REV 指令的操作，展示了寄存器中的四个字节如何在一个字中颠倒顺序。![](/assets/figure5-6.png)

### 其他指令

一些其他指令也可用：

* Breakpoint \(BKPT\) 将导致预取中止\(请参阅第十一章上的异常类型\)或导致核心进入调试状态\(取决于处理器是否配置为 monitor 模式调试或 halt 模式调试\)。这个指令被调试器使用。参见第二十四章 调试事件
* Wait For Interrupt \(WFI\) 将核心放入待机模式，这在第二十章电源管理中描述。核心停止执行，直到被中断或调试事件唤醒。如果 WFI 是在禁用中断的情况下执行的，中断仍然会唤醒核心，但是不会发生中断异常。在 WFI 之后，核心继续进行指令。在较老的 ARM 处理器中，WFI 实现是由 CP15 操作。
* A Wait for Event \(WFE\) 以类似于 WFI 的方式将核心置于待机模式。核心将休眠，直到被另一个执行 REV 指令的核心生成的事件唤醒。中断或错误事件将导致核心苏醒。WFE \(等待事件\)也在第二十章中描述。
* Send Event \(SEV\) 指令用于生成唤醒事件，这些事件可能唤醒集群中的其他核心。



