## GCC 中的 VFP 支持

GCC 完全支持 VFP 的使用，尽管可以将某些构建配置为默认不支持 VFP，在这种情况下，浮点计算将使用库代码。

VFP 支持的主要可选是：

* -mfpu=vfp specifies that the target has VFP hardware. As does specifying the option -mfpu=neon

其他选项可用于指定对 ARM Cortex-A 系列处理器上的特定 VFP 实现的支持：

* -mfpu=vfpv3 or -mfpu=vfpv3-d16 \(for Cortex-A8 and Cortex-A9 processors\)
* -mfpu=vfpv4 or -mfpu=vfpv4-d16 \(for Cortex-A5 and Cortex-A15 processors\)

这些选项可以用于只在这些 VFP 实现上运行的代码，并且不需要向后兼容旧的 VFP 实现。

* -mfloat-abi=softfp \(or hard\) specify which ABI to use to enable the use of VFP

softfp 使用与软件浮点数兼容的过程调用标准，因此提供了与遗留代码的二进制兼容性。这允许使用支持硬件浮点数的新库运行旧的软浮点数代码，但仍然使用函数调用之间的硬件浮点数寄存器。hard 有在浮点寄存器中传递的浮点值。这是更有效的，但不是向后兼容 softfp ABI 变体。需要特别注意库，包括 C 平台库。有关高效参数传递的更多信息，请参阅第十五章中的 VFP 和 NEON 寄存器的使用。

C 程序员必须注意，如果传递了许多浮点值，那么在使用 -mfloat-abi=softfp 时可能会有一个重要的函数调用开销。

