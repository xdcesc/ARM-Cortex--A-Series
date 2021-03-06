## 饱和运算

饱和运算常用于音频和视频编解码。返回值高于\(或低于\)可表示的最大正\(或负\)数的计算不会溢出。相反，结果被设置为最大的正值或负值\(饱和\)。ARM 指令集包含许多支持这种运算的指令。

### 饱和运算指令

ARM 饱和运算指令可以对一个字节，字或者半字值进行操作。例如 8 在 QADD8 和 QSUB8 指令中表示他们操作在一个 byte 大小的值。这个操作结果会被饱和成最大正值或者负值。如果结果已经溢出并饱和，则设置溢出标志\(CPSR Q bit\)。当设置时，它将保持设置，直到通过对 CPSR 的写入显式地清除为止。

指令集提供了带有这种行为的特殊指令 QSUB 和 QADD。另外，QDSUB 和 QDADD 支持 Q15 或 Q31 不动点运算。在执行指定的加减操作之前，这些指令将第二个操作数加倍并饱和。

Count Leading Zeros \(CLZ\) 指令返回设置的最重要位之前的 0 的数量。这对于规范化和某些除法运算很有用。要将一个值饱和到特定的位的位置\(有效饱和到 2 的幂\)，可以使用 USAT 或 SSAT \(无符号或有符号\) 饱和操作。USAT16 和 SSAT16 允许在寄存器中包含两个半字值的饱和。

